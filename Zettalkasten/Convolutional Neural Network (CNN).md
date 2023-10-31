202310200344
Meta Tags: #definition 
Tags: [[AI]] [[computer vision]]

# Convolutional Neural Networks (CNNs)
![colorful image](/Files/cnn1.jpg)
What I see when I look at this image are colors and shapes. However, a computer sees this as a grid of tiny dots, or [[pixel|pixels]], that each have a specific [[color value]]. 

If I want a computer to have "vision" in the same way that I do, CNNs are the way to go with [[layer|layers]] designed to process visual information and recognize patterns from them.

## [[network architecture|Network Architecture]]:
![[3l6n5hl2.bmp]]
### 1. Input Layer
- Where the [[neural network]] receives input data; for a CNN, this would be an image.
### 2. Convolutional Layer
- These are made up of combinations of [[filter|filters]], which are basically tiny windows that "slide over" the image and find patterns.
- Outputs [[feature map|feature maps]], which are basically maps of detected patterns.
### 3. Pooling Layer
- CNNs use [[pooling]] to "compress" the feature maps from Convolutional Layers into smaller dimensions while still retaining important information.
### 4. Flatten Layer
- Used to convert multi-dimensional data into a one-dimensional [[vector]], which is necessary when transitioning from Convolutional Layers to FC Layers.
### 5. [[Fully Connected (FC) Layer|Fully Connected (FC) Layers]]
- Processes the flattened [[feature map|feature maps]], learning high-level associations. Every [[neuron]] in each of these layers are connected to every neuron in previous layers. 
### 6. Output Layer
- Outputs the result of the processing, and usually has as many [[neuron|neurons]] as the amount of [[class|classes]] you are trying to quantify.

```ad-seealso
title: Other Layers
collapse: open

There are 3 other layers which are commonly used in CNNs but are not 100% essential, even though it would be stupid not to have them.

---
### 1. Batch Normalization Layer
- Usually after FC or Convolutional layers, [[normalization|normalizes]] [[activations]] before sending them to the activation layer, improving training stability and speed.

### 2. Activation Layer
- Usually after Batch Normalization layers, but also can take direct input from FC or Convolutional layers. Introduces [[non-linearity]] to the network.

### 3. Dropout Layer
- Usually after Activation layers. They randomly get rid of a fraction of the [[neurons]] during training, which helps prevent [[overfitting]].

```
```ad-example
title: Example Architecture
collapse: open

This is an example architecture:

1. **Input Layer**
	1. Receives an input image
2. **Convolutional Layer 1**
	1. Applies a combination of [[filter|filters]] to extract patterns
3. **Pooling Layer 1**
	1. Compresses patterns
4. **Convolutional Layer 2**
	1. Applies another combination of [[filter|filters]] for more complex features
5. **Pooling Layer 2**
	1. Further compresses patterns
6. **Flatten Layer 1**
	1. Converts multi-dimensional data into a one-dimensional [[vector]]
7. **FC Layer 1**
	1. Applies [[weight|weights]] for further extraction
8. **FC Layer 2**
	1. Further processes data to make a final decision
9. **Output Layer**
	1. Produces the final result, which might be something like a [[probability distribution]] over different [[class|classes]]

```

## Training a CNN

Training a CNN involves teaching it to recognizes patterns in an image using a process called [[supervised learning]]. Here is the specific implementation in this context:
### 1. Data Collection
- Gather a large, relevant dataset; if you are training the CNN to recognize people, get lots of pictures of people.
### 2. Data Preprocessing
- Training time increases with image size. As such, images are usually resized to be relatively small, and [[pixel]] values are [[normalization|normalized]] to a range between 0 and 1.
### 3. Model Architecture
- Design the structure of the CNN; choose the amount of [[layer|layers]], [[filter|filters]] per [[layer]], and how they are connected to one another. This is like an outline for how the CNN will detect patterns.
### 4. Initialization
- Initially, the [[filter|filters]] in the CNN have random values. As the network sees more images, it will adjust these values to learn the best features for the task at hand.
### 5. Forward Pass
- The CNN takes an image and runs it through the layers, looking for progressively more complex patterns.
### 6. Loss Calculation
- After the forward pass, the network compares its prediction with the actual label of the image. The goal is to minimize this error, or "loss".
### 7. [[backpropogation|Backpropagation]]
- The network learns from its mistakes by working back through the layers from the end and adjusting the values of the filters/weights.
### 8. Optimization
- A special algorithm is used to update the filter values to fine-tune the CNN.
### 9. Iterations
- Steps 5-8 are repeated many times using different images from the dataset. Each pass through the entire data set is an "[[epoch]]".
### 10. Validation
- After each [[epoch]], the network is tested on a separate dataset to check if it actually works.
### - Stopping Criterion
- Training continues until a certain condition is met, like when the improvement in accuracy levels off or starts to decrease on the validation set.
### - Testing
- Once training is complete, the final model is evaluated on a completely new set of images to see how well it performs.

---
# *References*
```ad-info
title: Types of Layers
collapse: open
<iframe src="https://chat.openai.com/share/b4e4e274-2a51-49e3-9fd8-cbb40385dd2a" width="650" height="600"></iframe>
```


