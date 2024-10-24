202410161849
Meta Tags: #class
Tags:

# Picamera

## Camera Hardware

- Uses rolling shutter to capture images

>[!info] rolling shutter
>A method of image capture in which a still picture (in a still camera) or each frame of a video (in a video camera) is captured not by taking a snapshot of the entire scene at a single instant in time but rather by scanning across the scene rapidly, vertically, horizontally or rotationally. 
>
>In other words, not all parts of the image of the scene are recorded at exactly the same instant. (Though, during playback, the entire image of the scene is displayed at once, as if it represents a single instant in time.) This produces predictable distortions of fast-moving objects or rapid flashes of light. 
>
>This is in contrast with "**global shutter**" in which the entire frame is captured at the same instant.

1. Open shutter
2. Let sensor "view" the scene
3. Close the shutter
4. Read out each line from the sensor

- The camera is not effectively idle until we tell it to capture a frame. 

As soon as it is initialized, it is constantly streaming frames (or rather rows of frames) down the ribbon cable to the Pi for processing. 

While the script may be sleeping or doing nothing, numerous tasks like automatic gain control, exposure time, white balance, and others are going on.  

So when we request the camera to "capture a frame" the camera gives us the next complete frame 

- The camera sensor detects photon counts; the more photons that hit the sensor elements, the more those elements increment their counters. 

The camera has no physical shutter, so we can't prevent light falling on the elements and incrementing the counts. **In fact, we can only perform two operations on the sensor: reset a row of elements, or read a row of elements.**

So, exposure time of a frame can be controlled by varying the delay between resetting a line and reading it.

There are limits to the minimum exposure time, as reading out a line of elements must take a certain minimum time. Maximum framerate is determined by the minimum exposure time, the reciprocal to be exact.

- The other important factor influencing sensor element counts, aside from line read-out time, is the sensor's **gain**. 

Specifically, the gain given by the analog_gain attribute.

The sensor elements are not simple digital counters but are in fact analog components that build up charge as more photons hit them. The analog gain influences how this charge is built-up. 

Analog gain cannot be directly controlled in picamera, but various attributes can be used to 'influence' it.

- Division of labor. Lines are not actively 'read' from the sensor; rather, the sensor is configured (via its registers) with a time per line and a number of lines to read. The camera doesn't send these lines to the CPU; it sends them to the Pi's GPU (VideoCore IV) which its running its own RTOS (VCOS, ThreadX).

1. The camera’s sensor has been configured and is continually streaming frame lines over the CSI-2 interface to the GPU.
2. The GPU is assembling complete frame buffers from these lines and performing post-processing on these buffers (we’ll go into further detail about this part in the next section).
3. Meanwhile, over on the CPU, `myscript.py` makes a `capture` call using picamera.
4. The picamera library in turn uses the MMAL API to enact this request (actually there’s quite a lot of MMAL calls that go on here but for the sake of simplicity we represent all this with a single arrow).
5. The MMAL API sends a message over VCHI requesting a frame capture (again, in reality there’s a lot more activity than a single message).
6. In response, the GPU initiates a [DMA](https://en.wikipedia.org/wiki/Direct_memory_access) transfer of the next complete frame from its portion of RAM to the CPU’s portion.
7. Finally, the GPU sends a message back over VCHI that the capture is complete.
8. This causes an MMAL thread to fire a callback in the picamera library, which in turn retrieves the frame (in reality, this requires more MMAL and VCHI activity).
9. Finally, picamera calls `write` on the output object provided by `myscript.py`.

![[Pasted image 20241016191238.png]]

1. Starting at the camera module, some minor processing happens. Specifically, flips (horizontal and vertical), line skipping, and pixel [binning](http://www.andor.com/learning-academy/ccd-binning-what-does-binning-mean) are configured on the sensor’s registers. Pixel binning actually happens on the sensor itself, prior to the ADC to improve signal-to-noise ratios. See [`hflip`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.hflip "picamera.PiCamera.hflip"), [`vflip`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.vflip "picamera.PiCamera.vflip"), and [`sensor_mode`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.sensor_mode "picamera.PiCamera.sensor_mode").
2. As described previously, frame lines are streamed over the CSI-2 interface to the GPU. There, it is received by the Unicam component which writes the line data into RAM.
3. Next the GPU’s [image signal processor](https://en.wikipedia.org/wiki/Image_processor) (ISP) performs several post-processing steps on the frame data. These include (in order):

> - **Transposition**: If any rotation has been requested, the input is transposed to rotate the image (rotation is always implemented by some combination of transposition and flips).
> - **Black level compensation**: Use the non-light sensing elements (typically in a covered border) to determine what level of charge represents “optically black”.
> - **Lens shading**: The camera firmware includes a table that corrects for chromatic distortion from the standard module’s lens. This is one reason why third party modules incorporating different lenses may show non-uniform color across a frame.
> - **White balance**: The red and blue gains are applied to correct the [color balance](https://en.wikipedia.org/wiki/Color_balance). See [`awb_gains`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.awb_gains "picamera.PiCamera.awb_gains") and [`awb_mode`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.awb_mode "picamera.PiCamera.awb_mode").
> - **Digital gain**: As mentioned above, this is a straight-forward post-processing step that applies a gain to the [Bayer values](https://en.wikipedia.org/wiki/Bayer_filter). See [`digital_gain`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.digital_gain "picamera.PiCamera.digital_gain").
> - **Bayer de-noise**: This is a noise reduction algorithm run on the frame data while it is still in Bayer format.
> - **De-mosaic:** The frame data is converted from Bayer format to [YUV420](https://en.wikipedia.org/wiki/YUV#Y.E2.80.B2UV420p_.28and_Y.E2.80.B2V12_or_YV12.29_to_RGB888_conversion) which is the format used by the remainder of the pipeline.
> - **YUV de-noise**: Another noise reduction algorithm, this time with the frame in YUV420 format. See [`image_denoise`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.image_denoise "picamera.PiCamera.image_denoise") and [`video_denoise`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.video_denoise "picamera.PiCamera.video_denoise").
> - **Sharpening**: An algorithm to enhance edges in the image. See [`sharpness`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.sharpness "picamera.PiCamera.sharpness").
> - **Color processing**: The [`brightness`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.brightness "picamera.PiCamera.brightness"), [`contrast`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.contrast "picamera.PiCamera.contrast"), and [`saturation`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.saturation "picamera.PiCamera.saturation") adjustments are implemented.
> - **Distortion**: The distortion introduced by the camera’s lens is corrected. At present this stage does nothing as the stock lens isn’t a [fish-eye lens](https://en.wikipedia.org/wiki/Fisheye_lens); it exists as an option should a future sensor require it.
> - **Resizing**: At this point, the frame is resized to the requested output resolution (all prior stages have been performed on “full” frame data at whatever resolution the sensor is configured to produce). See [`resolution`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.resolution "picamera.PiCamera.resolution").


Some of these steps can be controlled directly (e.g. brightness, noise reduction), others can only be influenced (e.g. analog and digital gain), and the remainder are not user-configurable at all (e.g. demosaic and lens shading).

At this point the frame is effectively “complete”.

4. If you are producing “unencoded” output (YUV, RGB, etc.) the pipeline ends at this point, with the frame data getting copied over to the CPU via [DMA](https://en.wikipedia.org/wiki/Direct_memory_access). The ISP might be used to convert to RGB, but that’s all.
5. If you are producing encoded output (H264, MJPEG, MPEG2, etc.) the next step is one of the encoding blocks, the H264 block in this case. The encoding blocks are specialized hardware designed specifically to produce particular encodings. For example, the JPEG block will include hardware for performing lots of parallel [discrete cosine transforms](https://en.wikipedia.org/wiki/Discrete_cosine_transform) (DCTs), while the H264 block will include hardware for performing [motion estimation](https://en.wikipedia.org/wiki/Motion_estimation).
6. Once encoded, the output is copied to the CPU via [DMA](https://en.wikipedia.org/wiki/Direct_memory_access).
7. Coordinating these components is the VPU, the general purpose component in the GPU running VCOS (ThreadX). The VPU configures and controls the other components in response to messages from VCHI. Currently the most complete documentation of the VPU is available from the [videocoreiv repository](https://github.com/hermanhermitage/videocoreiv).

![[Pasted image 20241016191700.png]]

### MMAL

Provides a greatly simplified interface to the camera firmware running on the GPU. Conceptually, it presents the camera with three "ports": the still port, video port, and preview port.

#### Still Port

Whenever used to capture images, it (briefly) forces the camera's mode to one of the two supported still modes so that images are captured using the full area of the sensor. It also uses a strong noise reduction algorithm on captured images so that they appear higher quality.

#### Video Port

Never changes the camera's mode. Images captured from the video port tend to have a "grainy" appearance, much more akin to a video frame than the images captured by the still port.

### Preview Port

Operates more or less identically to the video port. It is always connected to some form of output to ensure that the auto-gain algorithm can run. 

#### Pipelines

Encoders are connected directly to the still port. For example, when capturing a picture using the still port, the camera's state conceptually moves through these states:

![[Pasted image 20241016192235.png]]

The video port is more complex. In order to permit simultaneous video recording and image capture via the video port, a "splitter" component is permanently connected to the video port by picamera, and encoders are in turn attached to one of its four output ports.

![[Pasted image 20241016192336.png]]

![[Pasted image 20241016192346.png]]

when the resize parameter is passed to one of the aforementioned methods, a resizer component is placed between the camera's ports and the encoder.

![[Pasted image 20241016192428.png]]

## API - The PiCamera Class

### PiCamera

```
class picamera.PiCamera(camera_num=0, stereo_mode='none', stereo_decimate=False, resolution=None, framerate=None, sensor_mode=0, led_pin=None, clock_mode='reset', framerate_range=None)
```

Pure Python interface to the Pi's camera module.

When finished with the camera, you should ensure you call the close() method to release the camera resources.

The class supports the context manager protocol to make this easy with the `with` statement.

```
add_overlay(source, size=None, format=None, **options)
```

Allows you to add a static overlay to the camera's preview output. The overlay will be rendered on top of the preview but will not be included in any captures or video recordings. Multiple overlays can be added, and each call to `add_overlay` returns a `PiOverlayRenderer` instance representing the new overlay.

>[!warning]
>If too many overlays are added, the display output will be disabled and a reboot will generally be required to restore the display. Overlays are composited “on the fly”. Hence, a real-time constraint exists wherein for each horizontal line of HDMI output, the content of all source layers must be fetched, resized, converted, and blended to produce the output pixels.
>
>If enough overlays exist (where “enough” is a number dependent on overlay size, display resolution, bus frequency, and several other factors making it unrealistic to calculate in advance), this process breaks down and video output fails. One solution is to add `dispmanx_offline=1` to `/boot/config.txt` to force the use of an off-screen buffer. Be aware that this requires more GPU memory and may reduce the update rate.

```
capture(output, format=None, use_video_port=False, resize=None, splitter_port=0, bayer=False, **options)
```

Capture an image from the camera, storing it in *output*.

If _output_ is a string, it will be treated as a filename for a new file which the image will be written to. If _output_ is not a string, but is an object with a `write` method, it is assumed to be a file-like object and the image data is appended to it (the implementation only assumes the object has a `write` method - no other methods are required but `flush` will be called at the end of capture if it is present). If _output_ is not a string, and has no `write` method it is assumed to be a writeable object implementing the buffer protocol. In this case, the image data will be written directly to the underlying buffer (which must be large enough to accept the image data).

>[!warning]
>If _resize_ is specified, or _use_video_port_ is `True`, Exif metadata will **not** be included in JPEG output. This is due to an underlying firmware limitation.

This means that if Exif metadata is used for location, timestamps, or other identifying info, it may not be included in the captured images.

Additionally, the `capture()` function supports writing the image data directly to a writable buffer object. If the buffer is not properly validated/sanitized, it could allow an attacker to write arbitrary data to memory.

```
capture_continuous(output, format=None, use_video_port=False, resize=None, splitter_port=0, burst=False, bayer=False, **options)
```

Capture images continuously from the camera as an infinite iterator.

This method returns an infinite iterator of images captured continuously from the camera. If _output_ is a string, each captured image is stored in a file named after _output_ after substitution of two values with the [`format()`](https://docs.python.org/3.4/library/stdtypes.html#str.format "(in Python v3.4)") method. Those two values are:

- `{counter}` - a simple incrementor that starts at 1 and increases by 1 for each image taken
- `{timestamp}` - a [`datetime`](https://docs.python.org/3.4/library/datetime.html#datetime.datetime "(in Python v3.4)") instance

The table below contains several example values of _output_ and the sequence of filenames those values could produce:

|_output_ Value|Filenames|Notes|
|---|---|---|
|`'image{counter}.jpg'`|image1.jpg, image2.jpg, image3.jpg, …||
|`'image{counter:02d}.jpg'`|image01.jpg, image02.jpg, image03.jpg, …||
|`'image{timestamp}.jpg'`|image2013-10-05 12:07:12.346743.jpg, image2013-10-05 12:07:32.498539, …||
|`'image{timestamp:%H-%M-%S-%f}.jpg'`|image12-10-02-561527.jpg, image12-10-14-905398.jpg||
|`'{timestamp:%H%M%S}-{counter:03d}.jpg'`|121002-001.jpg, 121013-002.jpg, 121014-003.jpg, …||

1. Note that because timestamp’s default output includes colons (:), the resulting filenames are not suitable for use on Windows. For this reason (and the fact the default contains spaces) it is strongly recommended you always specify a format when using `{timestamp}`.
2. You can use both `{timestamp}` and `{counter}` in a single format string (multiple times too!) although this tends to be redundant.

If _output_ is not a string, but has a `write` method, it is assumed to be a file-like object and each image is simply written to this object sequentially. In this case you will likely either want to write something to the object between the images to distinguish them, or clear the object between iterations. If _output_ is not a string, and has no `write` method, it is assumed to be a writeable object supporting the buffer protocol; each image is simply written to the buffer sequentially.

The _format_, _use_video_port_, _splitter_port_, _resize_, and _options_ parameters are the same as in [`capture()`](https://picamera.readthedocs.io/en/release-1.13/api_camera.html#picamera.PiCamera.capture "picamera.PiCamera.capture").

If _use_video_port_ is `False` (the default), the _burst_ parameter can be used to make still port captures faster. Specifically, this prevents the preview from switching resolutions between captures which significantly speeds up consecutive captures from the still port. The downside is that this mode is currently has several bugs; the major issue is that if captures are performed too quickly some frames will come back severely underexposed. It is recommended that users avoid the _burst_ parameter unless they absolutely require it and are prepared to work around such issues.

The `burst` parameter can be exploited to capture low-quality or corrupted images through under-exposed frames. 

```
capture_sequence(outputs, format='jpeg', use_video_port=False, resize=None, splitter_port=0, burst=False, bayer=False, **options)
```

Same problems as capture_continuous().

```
close()
```

Must be called to prevent GPU memory leaks

```
record_sequence(outputs, format='h264', resize=None, splitter_port=1, **options)
```

Same buffer problem.



---
# *References*