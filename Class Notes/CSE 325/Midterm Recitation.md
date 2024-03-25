## Embedded Systems Introduction

- What is an [[embedded systems|Embedded System]]?
	- Designed for a specific purpose/task; part of a larger system with a more general purpose; "Applied Computer System"; Not designed to be programmed by the end user
- Characteristics of an Embedded System
	- Dedicated to a single task, Cost-sensitive, Low Resources, Power constraints, Low tolerance for failure, **No OS or [[RTOS]]**, Must meet [[real-time computing]] constraints, must be rugged for certain physical conditions (weather, environment, forces)
- Embedded System vs. Real-time Operating System
	- Purpose of [[OS]]? -> Manage multitasking and resources; Embedded systems have few tasks, if not only one; They only require simple multitasking most of the time: [[RTOS]]s are designed to react to soft and hard real-time constraints

| Embedded System                                        | OS                                              | RTOS                                           |
| ------------------------------------------------------ | ----------------------------------------------- | ---------------------------------------------- |
| - Hardware + Software designed for a specific function | - Software for scheduling, multitasking,etc.    | - OS with deadlines for real-time applications |
| - Examples: Camera, calculator, watches, applicances   | - Examples: iOS, Windows, macOS, Android, Linux | - Examples: Pacemaker, Robot, Airline reservation system                                               |
## Schematics and Datasheets

- Physical Characteristics - port connections, pinouts; Electrical Characteristics - power, voltage, current; Logical Characteristics - timing, ISA; Schematic/Diagram
- Identifying Components
	- Passive: capacitors, resistors, inductors, diodes; Active: transistors, integrated circuits
	- Identifier - Resistor -> R*n*, Capacitor -> C*n*, Inductors -> L*n*, Diodes -> D*n*  like variable name; Value - Resistor -> 10K, variable value
	- dot is pin 1 on ICs, schematic usually not ordered, but logically efficient or part number (1N4001 is part number for diode) because complicated
- Wires, Busses and Signals
	- Wire = "Node", shares same voltage; Buses = bundle of "nodes", named at entry and exit; Signals = Named nodes, same name = connected (5V, GND)
- Pinouts and Electrical Characteristics: Application Information

## Low-Level C Programming

```
int a = 5; int *p; p = &a; //p = 0x1234,*p = 5 
```

`ptr = (int*) malloc(100*sizeof(int));`
`malloc` returns a void pointer that is casted into a pointer of any type; above allocates 400 bytes of memory
`free(ptr)` needs to be used to deallocate memory allocated by `malloc` and `calloc`.

|Data Type|Size (bytes)|Range|Format Specifier|
|---|---|---|---|
|short int |2|-32,768 to 32,767|%hd|
|unsigned short int |2|0 to 65,535|%hu|
|unsigned int |4|0 to 4,294,967,295|%u|
|int |4|-2,147,483,648 to 2,147,483,647|%d|
|long int |4|-2,147,483,648 to 2,147,483,647|%ld|
|unsigned long int |4|0 to 4,294,967,295|%lu|
|long long int |8|-(2^63) to (2^63)-1|%lld|
|unsigned long long int |8|0 to 18,446,744,073,709,551,615|%llu|
|signed char |1|-128 to 127|%c|
|unsigned char |1|0 to 255|%c|
|float |4|1.2E-38 to 3.4E+38|%f|
|double |8|1.7E-308 to 1.7E+308|%lf|
|long double |16|3.4E-4932 to 1.1E+4932|%Lf|
& - AND, | - OR, ^ - XOR, << - LS, >> - RS, ~ - NOT, for in place just add = after operator, i.e. &=
- Big Endian -> MSB at base address/lowest address; Little Endian -> LSB instead
- Last element address, last byte address
	- `type arr[n];LE at base+(n-1)*sizeof(type), LB at base+n*sizeof(type)-1`
- Set - make 1, Clear - make 0; Masks: &= to extract a subset of bits, |= to set a subset of bits, ^= to toggle a subset of bits, just have all 1s on the bits you want to affect
- Signed left shift has undefined behavior, signed right shift pads with sign-extension bit
- Write Little Endian Given Big Endian and vice-versa
```
swapped = ((num>>24)&0xff) | // move byte 3 to byte 0
((num<<8)&0xff0000) | // move byte 1 to byte 2
((num>>8)&0xff00) | // move byte 2 to byte 1
((num<<24)&0xff000000); // byte 0 to byte 3
```

## Power Supplies and Batteries

- Why care? Holistic design (do the most with least possible), System Limitations, Run-Time, Minimizing Cost
- $V = IR; \ P = VI$ Watts; Voltage - potential difference between two points,  "pressure"; Current - rate of flow of charge; Resistance/**load** - opposition to flow of charge
- Power Supplies: AC & **DC** (needed for digital systems); AC -> DC: transformer, rectifier, smoothing. Current ratings are maximums, Voltage ratings are constant when current under rating. Power rating = Current rating times Voltage rating. 
- Batteries: voltage source, run time = capacity/current draw (**WATCH UNITS**), *n*C -> discharge rate = *n* times capacity, assume 95% of capacity is real. 
- Voltage dividers are inefficient, dropout voltage is minimum difference between regulator I/O, quiescent current = how much current is converted to heat energy; Treat LEDs as resistors for the exam. Linear < price than Switching regulators

## Digital Input/Output

- Digital Output - LEDs (**CHECK ACTIVE HIGH VS. ACTIVE LOW**)
	1. Turn on clock gating for port `SIM->SCGCn |= (1<<m);`
	2. Setup PTxn as GPIO using PCR `PORTx->PCRn &= ~(0x700); PORTx->PCRn |= (1 << 8);`
	3. Setup pin PTxn as output `GPIOx->PDDR |= (1<<n);`
- Digital Input - Switches: same 1 as LEDs but: remember to clear and set pull select and enable and remember active low is usual: `GPIOx_PDIR & (1<<n)` should be **off** state. Plus set up of GPIO input for switches.
- Pull up and pull down resistors: for active low and active high respectively; fixes floating issue (uncertain value between logic high and logic low)  
- Switch debouncing - Software vs. Hardware
	- Software: Counter that checks if value has been the same for a  period of time; Hardware: Capacitors
- PDDR (Port Data Direction Register), PDOR (PD Output Register), PDIR (PD Input Register), PTOR (Port Toggle OR), PSOR (Port Set OR), PCOR (Port Clear OR)

## Timers and PWM

- Periodic Timers
	- Chained T flip-flops
	- Reference Register -> automatically generate a signal when counter register becomes greater than the reference value. This signal goes to both to the reference match bit and, it it is enabled, the reset counter bit.
	- Up-counting - increment and reset counter to 0 after greater than MOD. TOF is set on posedge of first overflow. Up-down counting - after reaching MOD on the counter, start decrementing down to 0. TOF is set on posedge of first decrement.

1. Enable Clock Gating for TPMn `SIM->SCGC6 |= (1 << 24)`
2. Set clock source to OSCERCLK `SIM->SOPT2 |= (0x2 << 24)`
3. Configure using TPMx->CONF `TPM0->CONF |= (1 << 17)`
4. Calculate PS: 1. Set MOD to max value (65335), Find true PS through equation, find closest PS greater than true PS, calculate true MOD using new PS. 
5. Set true prescalar and reset TOF `TPM0->SC |= (1<<7) | (0x7)`
PS is first three bits of SC, value is 2^(the 3 bits in binary).
6. Set true MOD `TPM0->MOD = true_MOD_value`
7. Start counter `TPM0->SC |= (1<<3)`
$$T = \frac{MOD+1}{f_{clk}/PS}$$
OSCERCLK -> 8 MHz

- Pulse Width Modulation
	- Duty cycle (D) = time on/period or cycle time. TOF/MOD of TPM decides the period length, while CnV decides the compare match time.
	- $V_{avg} = D\cdot V_{max} + (1-D) \cdot V_{min}$ 
	1. Go through steps 1 - 6 of TPM set up
	2. Setup PWM clock gating (if needed) `SIM->SCGC6 |= (1<<24)`
	3. Setup PWM clock source (if needed) `SIM->SOPT2 |= (0x2<<24)`
	4. Enable pin as PWM (**CHECK FOR PINS THAT CAN DO CHANNELS ON SCHEMATIC**) `SIM->SCGC5 |= (1<<n); PORTx->PCR[n1] &= ~(0x700); PORTx->PCR[n1] |= 0x400`
	5. Setup Channel *n* `TPMy->CONTROLS[n].CnSC |= (0x2<<2) | (0x2<<4); TPMy->CONTROLS[n].CnV = match value`
	6. start the clock, see 7 of TPM

## Analog Input/Output

Digital Sensors: buttons, car detectors, tripwires; Analog sensors: temperature, humidity
- Analog to Digital Converter - partition ranges into different bit values, 2^n partitions means n-bit quantization. Sample rate is also important for accuracy, needs both. **Nyquist Limit**: to capture signal of frequency B we must sample at frequency 2B.
	- voltage divider gives analog voltage; comparators output to digital signal. Or binary search using successive approximation tactic
	1. enable I/O ports `SIM->SCGC5 |= (3<<12)`
	2. enable ADC Module `SIM->SCGC6 |= (1<<27)`
	3. Setup port as Analog Input (**SEE 172-175**)
	4. Setup ADC clock `ADC0->CFG1 = 0;`
	5. Calibration:
		1. Enable Maximum Hardware Averaging `ADC0->SC3 = 0x07`; Start `ADC0->SC3 |= 0x80`
		2. Wait for COCO to become 1 `while(!(ADC0->SC1[0] & 0x80)){}`
		3. Write calibration registers `unsigned short cal_v = ADC0->CLP0 + ADC0->CLP1 + ADC0->CLP2 + ADC0->CLP3 + ADC0->CLP4 +  ADC0->CLPS; cal_v = cal_v >> 1 | 0x8000;  = ADC0->PG = cal_v; cal_v = 0; cal_v = ADC0->CLM0 + ADC0->CLM1 + ADC0->CLM2 + ADC0->CLM3 + ADC0->CLM4 + ADC0->CLMS; cal_v = cal_v >> 1 | 0x8000; ADC0->MG = cal_v;`
		4. Set Channel, start conversion `ADC0->SC1[0] = 0x03 //selects channel DAD3`
		5. wait for conversion to finish  `while(!(ADC0->SC1[0] & 0x80)){}`
		6. declare variable equal to value of result register corresponding to SC1n register `unsigned char light_val = ADC0->R[0]`. This resets Conversion flag, so go back to 4 and repeat for more conversions
- Digital to Analog converter - binary value -> voltage; binary value is the **level**; level/max level \* voltage is output; Voltage ladder using voltage dividers; 
	- The 12-bit DAC module can select one of the two reference inputs—DACREF_1 and DACREF_2 as the DAC reference voltage, Vin by C0[DACRFS]. See the module introduction for information on the source for DACREF_1 and DACREF_2. When the DAC is enabled, it converts the data in DACDAT0[11:0] or the data from the DAC data buffer to a stepped analog output voltage. The output voltage range is from Vin to Vin∕4096, and the step is Vin∕4096.
	1. Enable clock gating for DAC and DAC0_Out port (PTE30) `SIM->SCGC5 |= (1<<13); SIM->SCGC6 |= (1<<31);`
	2. Set up port as DAC_OUT through GPIO method in LED section
	3. Use default settings for DAC_C0, C1, and C2. Only need C1 for enabling the module later.
	4. Decide on 12-bit level according to equation above, and then set DAC0_DAT[0]H to four most MSBs, and DAT[0]L to the rest. `DAC0->DAT[0]H = (level>>8); DAC0->DAT[0]L = (0xff & level);`
	5. Enable the DAC `DAC0->C0 |= (1<<7);`

## Motors and Encoders

- Types of motors
	- DC: Brushed - Coils on the inner rotor, Inexpensive, simple construction, simple control, low power to weight ratio; Brushless - permanent magnet on the inner rotor, expensive, complex control (firing coils), high power to weight ratio, precise. Stepper motors -> type of brushless motor that is expensive, has precise position control, high power usage, and specialized controls. Brushed -> wheels, pumps, appliances. Brushless -> PC fans, drones. Stepper motors -> 3D printing, precise machining.
- Motor Circuits
	- Motors require a lot of current, higher voltages, and are electrically noisy. No limit. Use transistor to have on-off motor control
	- Back EMF
		- Noise caused by Back-EMF, which is caused by the stored magnetic energy within the magnetic field resisting the change in magnetic flux within the coils with an emf. magnetic field collapses.
		- Add EMF diodes going from GND to 12V, dissipating the back emf. 
	- Managing noise
		- put a capacitor parallel to the motor to smooth out the bumps.
- Types of encoders - ways to judge displacement, speed, absolute position
	- Rotary encoders - LED through disk with slots, photo sensor on other end that detects frequency of light pulses
	- Quadrature encoder - type of rotary encoder that uses 2 photo sensors that are slightly offset from each other to see cw vs. ccw rotation
	- Absolute encoder - rotary encoder with n-layers (n-bits) of slots, array of light sensors placed on each level, combined bits make the "angle level" of the encoder
	- Optical encoder - not precise, but cheap
	- Hall effect - more reliable in dirty environments, sense passage of magnets, very inexpensive, not much resolution
	- Capacitive - expensive, but lots of resolution, tolerant to environmental conditions
- Servos - combination of motor, control circuit, and encoder - limited range of rotation, but very precise. Take PWM signal that adjusts the position of the servo.
