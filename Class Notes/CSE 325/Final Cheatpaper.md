>PORTX->PCR\[1-0\] - Pull Enable; Pull Select(1-pullup, 0-pulldown)
>SIM->SCGC5 (9-13 = PORTA-PORTE); SCGC4 (23-22 = SPI1-0), (12-10 = UART2-0), (7-6 = I2C1-0); SCGC6 (31 = DAC0), (27 = ADC0), (26-24 = TPM2-0), (23 = PIT); SOPT2 (27-26 = UART0SRC), (25-24 = TPMSRC)

---
- What is an [[embedded systems|Embedded System]] - Designed for a **specific purpose/task**; part of a larger system with a more general purpose; "Applied Computer System"; Not designed to be programmed by the end user
- Characteristics of an Embedded System: Dedicated to a single task, Cost-sensitive, Low Resources, Power constraints, Low tolerance for failure, **No OS or [[RTOS]]**, Must meet [[real-time computing]] constraints, must be rugged for certain physical conditions (weather, environment, forces)
- Embedded System vs. Real-time Operating System: Purpose of [[OS]]? -> Manage multitasking and resources; Embedded systems have few tasks, if not only one; They only require simple multitasking most of the time: [[RTOS]]s are designed to react to soft and hard real-time constraints

| Embedded System                                        | OS                                              | RTOS                                           |
| ------------------------------------------------------ | ----------------------------------------------- | ---------------------------------------------- |
| - Hardware + Software designed for a specific function | - Software for scheduling, multitasking,etc.    | - OS with deadlines for real-time applications |
| - Examples: Camera, calculator, watches, applicances   | - Examples: iOS, Windows, macOS, Android, Linux | - Examples: Pacemaker, Robot, Airline reservation system                                               |

- **Schematics and Datasheets:** Physical Characteristics - port connections, pinouts; Electrical Characteristics - power, voltage, current; Logical Characteristics - timing, ISA; Schematic/Diagram
- Identifying Components - Passive: capacitors, resistors, inductors, diodes; Active: transistors, integrated circuits
	- Identifier - Resistor -> R*n*, Capacitor -> C*n*, Inductors -> L*n*, Diodes -> D*n*  like variable name, ICs -> IC*n*; Value - Resistor -> 10K, variable value
	- dot is pin 1 on ICs, schematic usually not ordered, but logically efficient or part number (1N4001 is part number for diode) because complicated
- Wires, Busses and Signals
	- Wire = "Node", shares same voltage; Buses = bundle of "nodes", named at entry and exit; Signals = Named nodes, same name = connected (5V, GND)
- C language: Systems language, fundamental data types, no memory management | C++/Java: application language, abstracted datatypes, built-in memory management

```
int a = 5; int *p; p = &a; //p = 0x1234,*p = 5 
```

`ptr = (int*) malloc(100*sizeof(int));`
`malloc` returns a void pointer that is casted into a pointer of any type; above allocates 400 bytes of memory `free(ptr)` needs to be used to deallocate memory allocated by `malloc` and `calloc`.

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
- Big Endian -> MSB at base address/lowest address; Little Endian -> LSB instead; Last element address, last byte address: `type arr[n];LE at base+(n-1)*sizeof(type), LB at base+n*sizeof(type)-1`
- Set - make 1, Clear - make 0; Masks: &= to extract a subset of bits, |= to set a subset of bits, ^= to toggle a subset of bits, just have all 1s on the bits you want to affect; Signed left shift has undefined behavior, signed right shift pads with sign-extension bit; Write Little Endian Given Big Endian and vice-versa:
```
swapped = ((num>>24)&0xff) | // move byte 3 to byte 0
((num<<8)&0xff0000) | // move byte 1 to byte 2
((num>>8)&0xff00) | // move byte 2 to byte 1
((num<<24)&0xff000000); // byte 0 to byte 3
```

- **POWER SUPPLY and BATTERIES**: Why care? Holistic design (do the most with least possible), System Limitations, Run-Time, Minimizing Cost
- $V = IR; \ P = VI$ Watts; Voltage - potential difference between two points,  "pressure"; Current - rate of flow of charge; Resistance/**load** - opposition to flow of charge
- Power Supplies: AC & **DC** (needed for digital systems); AC -> DC: transformer, rectifier, smoothing. Current ratings are maximums, Voltage ratings are constant when current under rating. Power rating = Current rating times Voltage rating. 
- Batteries: voltage source, run time = capacity div by current draw (**WATCH UNITS**), *n*C -> discharge rate = *n* times capacity, assume 95% of capacity is real. 
- Voltage dividers are inefficient, dropout voltage is minimum difference between regulator I/O, quiescent current = how much current is converted to heat energy; Treat LEDs as resistors for the exam. Linear < price than Switching regulators
- **Digital Output** - LEDs (**PTE29 is RED, PTD5 is GREEN**) (**CHECK ACTIVE HIGH VS. ACTIVE LOW**): **1**. Turn on clock gating for port `SIM->SCGCn |= (1<<m);` **2**. Setup PTxn as GPIO using PCR `PORTx->PCRn &= ~(0x700); PORTx->PCRn |= (1 << 8);` **3**. Setup pin PTxn as output `GPIOx->PDDR |= (1<<n);`
- **Digital Input** - Switches (**SW1 is PTC3, SW2 is PTC12**): same 1 as LEDs but: remember to clear and set pull select and enable and remember active low is usual: `GPIOx_PDIR & (1<<n)` should be **off** state. Plus set up of GPIO input for switches.
- Pull up and pull down resistors: for active low and active high respectively; fixes floating issue (uncertain value between logic high and logic low)  
- Switch debouncing - Software vs. Hardware: Software: Counter that checks if value has been the same for a  period of time; Hardware: Capacitors
- PDDR (Port Data Direction Register), PDOR (PD Output Register), PDIR (PD Input Register), PTOR (Port Toggle OR), PSOR (Port Set OR), PCOR (Port Clear OR)
- **Timers and PWM**: Reference Register -> automatically generate a signal when counter register becomes greater than the reference value. This signal goes to both to the reference match bit and, it it is enabled, the reset counter bit.
- Up-counting - increment and reset counter to 0 after greater than MOD. TOF is set on posedge of first overflow. Up-down counting - after reaching MOD on the counter, start decrementing down to 0. TOF is set on posedge of first decrement.
- **1**. Enable Clock Gating for TPMn `SIM->SCGC6 |= (1 << 24)` **2**. Set clock source to OSCERCLK `SIM->SOPT2 |= (0x2 << 24)` **3**. Configure using TPMx->CONF `TPM0->CONF |= (1 << 17)` **4**. Calculate PS: Set MOD to max value (65335), Find true PS through equation, find closest PS greater than true PS, calculate true MOD using new PS. **5**. Set true prescalar and reset TOF `TPM0->SC |= (1<<7) | (0x7)` *PS is first three bits of SC, value is 2^(the 3 bits in binary)*. **6**. Set true MOD `TPM0->MOD = true_MOD_value` **7**. Start counter `TPM0->SC |= (1<<3)`
$$T = \frac{MOD+1}{f_{clk}/PS}$$
- **Pulse Width Modulation**: Duty cycle (D) = time on/period or cycle time. TOF/MOD of TPM decides the period length, while CnV decides the compare match time. OSCERCLK -> 8 MHz: $V_{avg} = D\cdot V_{max} + (1-D) \cdot V_{min}$ 
- **1**. Go through steps 1 - 6 of TPM set up. **2**. Setup PWM clock gating (if needed) `SIM->SCGC6 |= (1<<24)` **3**. Setup PWM clock source (if needed) `SIM->SOPT2 |= (0x2<<24)` **4**. Enable pin as PWM (**CHECK FOR PINS THAT CAN DO CHANNELS ON SCHEMATIC**) `SIM->SCGC5 |= (1<<n); PORTx->PCR[n1] &= ~(0x700); PORTx->PCR[n1] |= 0x400` **5**. Setup Channel *n* `TPMy->CONTROLS[n].CnSC |= (0x2<<2) | (0x2<<4); TPMy->CONTROLS[n].CnV = match value` **6**. start the clock, see **7** of TPM
**Digital Sensors**: buttons, car detectors, tripwires; Analog sensors: temperature, humidity
- **Analog to Digital Converter** - partition ranges into different bit values, 2^n partitions means n-bit quantization. Sample rate is also important for accuracy, needs both. **Nyquist Limit**: to capture signal of frequency B we must sample at frequency 2B.
	- voltage divider gives analog voltage; comparators output to digital signal. Or binary search using successive approximation tactic
	- **1**. enable I/O ports `SIM->SCGC5 |= (3<<12)` **2**. enable ADC Module `SIM->SCGC6 |= (1<<27)` **3**. Setup port as Analog Input (**SEE 172-175**) **4**. Setup ADC clock `ADC0->CFG1 = 0;` **5**. Calibration: **1**. Enable Maximum Hardware Averaging `ADC0->SC3 = 0x07`; Start `ADC0->SC3 |= 0x80` **2**. Wait for COCO to become 1 `while(!(ADC0->SC1[0] & 0x80)){}` **3**. Write calibration registers `unsigned short cal_v = ADC0->CLP0 + ADC0->CLP1 + ADC0->CLP2 + ADC0->CLP3 + ADC0->CLP4 +  ADC0->CLPS; cal_v = cal_v >> 1 | 0x8000;  = ADC0->PG = cal_v; cal_v = 0; cal_v = ADC0->CLM0 + ADC0->CLM1 + ADC0->CLM2 + ADC0->CLM3 + ADC0->CLM4 + ADC0->CLMS; cal_v = cal_v >> 1 | 0x8000; ADC0->MG = cal_v;` **4**. Set Channel, start conversion `ADC0->SC1[0] = 0x03 //selects channel DAD3` **5**. wait for conversion to finish  `while(!(ADC0->SC1[0] & 0x80)){}` **6**. declare variable equal to value of result register corresponding to SC1n register `unsigned char light_val = ADC0->R[0]`. This resets Conversion flag, so go back to 4 and repeat for more conversions
- Digital to Analog converter - binary value -> voltage; binary value is the **level**; level/max level \* voltage is output; Voltage ladder using voltage dividers; 
	- The 12-bit DAC module can select one of the two reference inputs—DACREF_1 and DACREF_2 as the DAC reference voltage, Vin by C0[DACRFS]. See the module introduction for information on the source for DACREF_1 and DACREF_2. When the DAC is enabled, it converts the data in DACDAT0[11:0] or the data from the DAC data buffer to a stepped analog output voltage. The output voltage range is from Vin to Vin∕4096, and the step is Vin∕4096.
	- **1**. Enable clock gating for DAC and DAC0_Out port (PTE30) `SIM->SCGC5 |= (1<<13); SIM->SCGC6 |= (1<<31);` **2**. Set up port as DAC_OUT through GPIO method in LED section **3**. Use default settings for DAC_C0, C1, and C2. Only need C0 for enabling the module later. **4**. Decide on 12-bit level according to equation above, and then set DAC0_DAT[0]H to four most MSBs, and DAT[0]L to the rest. `DAC0->DAT[0]H = (level>>8); DAC0->DAT[0]L = (0xff & level);` **5**. Enable the DAC `DAC0->C0 |= (1<<7);`
- **Types of motors** - DC: Brushed - Coils on the inner rotor, Inexpensive, simple construction, simple control, low power to weight ratio; Brushless - permanent magnet on the inner rotor, expensive, complex control (firing coils), high power to weight ratio, precise. Stepper motors -> type of brushless motor that is expensive, has precise position control, high power usage, and specialized controls. Brushed -> wheels, pumps, appliances. Brushless -> PC fans, drones. Stepper motors -> 3D printing, precise machining.
- **Motor Circuits** - Motors require a lot of current, higher voltages, and are electrically noisy. No limit. Use transistor to have on-off motor control with **H-bridge:** Q1/Q2 and Q3/Q4 are connected in image
	- Noise caused by Back-EMF, which is caused by the stored magnetic energy within the magnetic field resisting the change in magnetic flux within the coils with an emf. magnetic field collapses.
	- Add EMF diodes going from GND to 12V, dissipating the back emf. 
	- **Managing noise**: put a capacitor parallel to the motor to smooth out the bumps.
- **Types of encoders** - ways to judge displacement, speed, absolute position: **Rotary encoders** - LED through disk with slots, photo sensor on other end that detects frequency of light pulses: **Quadrature encoder** - type of rotary encoder that uses 2 photo sensors that are slightly offset from each other to see cw vs. ccw rotation: **Absolute encoder** - rotary encoder with n-layers (n-bits) of slots, array of light sensors placed on each level, combined bits make the "angle level" of the encoder: **Optical encoder** - not precise, but cheap: **Hall effect** - more reliable in dirty environments, sense passage of magnets, very inexpensive, not much resolution: **Capacitive** - expensive, but lots of resolution, tolerant to environmental conditions
- Servos - combination of motor, control circuit, and encoder - limited range of rotation, but very precise. Take PWM signal that adjusts the position of the servo.
- **Exceptions:** *div by 0*; *Overflow*. Produces interrupt requests
- **Interrupts:** *async signal* (IRQ, Interrupt Request); *handled by software* (ISR, Interrupt Service Routine); *sends IRQ during normal execution, saves state, lookup ISR associated with IRQ through function pointer* (Table 3-7)*, executes, restores state*; **PAUSE**, not parallel ; Email notification; **Advantages:** monitor and respond to processes without continually checking on them; handle time-critical events w/o spending processor time waiting for something to happen; **Issues:** Use `volatile` to avoid cached memory issue; Use `_enable_IRQ()` and `_disable_IRQ()` to enforce atomicity/indivisibility; not too many
- **Polling:** *manual check condition per loop*; *requires active CPU cycles and program structure, result behavior may be delayed, some loops of main program will not be executed*; Daily manual email check.

**Interrupt Setup:** (1) Enable clock gating and set PCR, then enable interrupts for module (2) Set desired priority(0-urgent, 4-not), configure NVICIPRn (n is IPR register \#), field starting location is $8 \cdot (\text{IRQ}\mod 4) + 6$ and is 2 bits wide (3) NVIC_Enable(IRQ) || **Interrupt Handler(ISR)**: (1) Clear Interrupt Flag (2) Task

| \_IRQHandler for ISR | PORTA                                                                     | PORTC_PORTD                                                     | ADC0                                                                                   | DAC0                                                                                                                             | PIT                                                                                               | TPM0/1/2                         | UART0/1/2                                                                                                                                                                                                                                                          | I2C0/1                                                                                                                                                              | SPI0/1                                                                                                                                                                                                                                                                                                                                                                                                                               |
| -------------------- | ------------------------------------------------------------------------- | --------------------------------------------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------- | -------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| IRQ \#               | 30                                                                        | 31                                                              | 15                                                                                     | 25                                                                                                                               | 22                                                                                                | 17/18/19                         | 12/13/14                                                                                                                                                                                                                                                           | 8/9                                                                                                                                                                 | 10/11                                                                                                                                                                                                                                                                                                                                                                                                                                |
| IPR \#               | 7                                                                         | 7                                                               | 3                                                                                      | 6                                                                                                                                | 5                                                                                                 | 4                                | 3                                                                                                                                                                                                                                                                  | 2                                                                                                                                                                   | 2                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| EN Registers         | **PCRn\[19-16\]**: 8-logic 0; 9-rising; 10-falling; 11-either; 12-logic 1 | Same as left, also 0 is disabled, write to \[24\] to clear flag | **SC1n\[6\]**: 1-COCO(7) (conversion complete) interrupt, read Rn to clear; 0-disabled | **C0\[1\]**: 1-DAC top flag interrupt \| **C0\[0\]**: 1-DAC bottom flag interrupt \| **SR\[1-0\]**: flags in same order as above | **TCTRL\[1-0\]**: 3-interrupts and enable timer \| **TFLGn**: write 1 to clear flag for channel n | **SC\[6\]**: 1-TOF(7) interrupts | **C2\[7-6\]**: TDRE(data register empty) flag interrupt; TC(transmission complete) flag interrupt, *both cleared by writing to D register* \| **C3\[3-0\]**: Overrun; Noise Error; Framing Error; Parity Error \| **S1\[3-0\]**: flags in same order as C3 enables | **S\[1\]**: flag register, byte transfer sets as well \| **FLT\[5\]**: Bus Stop interrupt, clear before S\[1\] \| **SMB\[0\]**: SCL high, SDA low timeout interrupt | **C2\[7\]**: SPI match interrupt, if receive data buffer = MH:ML registers \| **C1\[7,5\]**: SPI interrupt, SPRF(rx buffer full)/MODF(master fault) set; SPI tx interrupt, SPTEF(tx buffer empty) set \| **CI\[7-0\] (clear interrupts) if C3\[3\]**: TFIFO error; RFIFO error; TFIFO overflow; RFIFO overflow; TFIFO near empty; RFIFO near full; TFIFO empty; RFIFO full \| **C3\[2-1\]**: TFIFO near empty EN; RFIFO near full EN |

---
- Control process variables (current measured values of a particular part of a process)
- **System Model:** UML/Block Diagram, relationship and flow of information between components | **Mathematical Model:** State Machine, Mathematical expressions, Laplace Transform, $i(t), c(t), o(t)$ for input, control, and output signals. 
- **System Response:** Transient - $o(t)/c(t)$ as a function of $t$. Frequency - $G(s)$ as a function of $s$, at steady state. For a given input, what are the outputs?
- **Types:** Open-Loop - no feedback, Dryer, $c(t) = f_1(i(t)); o(t) = f_2(c(t)); O(s) = G_1(s) G_2(s) I(s); C(s) = G_1(s) I(s)$. System Gain $G(s) = G_1(s) G_2(s)$; Closed-Loop - input -> plant (our electrical/mechanical/whatever) system -> output to device and measurement back to input, $e(t) = SP-PV; c(t) = f_1(e(t)); o(t) = f_2(c(t)); O(s) = G(s) E(s)$
- **Bang-Bang Control:** On-Off; Stateful - was it on or off?; fixed under/overshoot; Thermostats; if condition, turn on, else off; periodically check
- **P Controller:** $E = SP-PV$, control variable $u=K_p E+b$; *Steady State Error, Quick Rise Time*.
- **I Controller:** $u=K_i \sum^t_{n=0} E(n) + b$; *Eliminate Steady State Error, Slow Response(Oscillations)*.
- **D Controller:** $u =K_d(E(t)-E(t-1)) + b$; *Minimize response parameters, Low Stability*
- **PI Controller:** $u = K_p E(t) + K_i \sum^t_{n=0} E(n) + b$; *No SS Error, Quick Rise Time, Oscillations, Overshoot*.
- **PD Controller:** $u = K_p E(t) +  K_d(E(t)-E(t-1)) + b$; *SS Error, Quick Rise Time, Critically Damped*
- **PID Controller:** $u = K_p E(t) + K_i \sum^t_{n=0} E(n) + K_d(E(t)-E(t-1)) + b$; *Stable, Critically Damped, no SS Error, More parameters*.
- **Tuning:** Manual see table below; Ziegler-Nichols - search $K_P$ until stable oscillations, record as $K_{cr}$, measure $T_{cr}$. If P: $K_P = 0.5 K_{cr}$. If PI: $K_P = 0.45 K_{cr}$, $K_I = 0.54 K_{cr}/T_{cr}$. If PID: $K_P = 0.6 K_{cr}$, $K_I = 1.2K_{cr}/T_{cr}$, $K_D = 3 K_{cr} T_{cr}/40$.

| Param. Increased | Rise Time | Overshoot | Settling Time | SS Error  | Stability        |
| ---------------- | --------- | --------- | ------------- | --------- | ---------------- |
| $K_P$            | Decrease  | Increase  | Insig.        | Decrease  | Degrade          |
| $K_I$            | Decrease  | Increase  | Increase      | Eliminate | Degrade          |
| $K_D$            | Insig.    | Decrease  | Decrease      | None      | Improve if small |

- **Transient Response Properties:** *Rise Time* - how long before PV = SP; *Overshoot* - how far PV goes past SP; *Settling Time* - PV settles within threshold of SP | **Steady State Response Properties:** Phase/Amplitude, *Steady State Error* - difference between PV and SP in steady state
- **Damping:** how fast PV converges to SP; *Uncontrolled* - resonance; *Undamped* - oscillates at frequency; *Underdamped* - oscillates, amplitude decreases; *Overdamped* - never oscillate, never reach SP; *Critically damped* - oscillating time is minimally short

---
- Transfer data/messages between devices, microcontroller to sensor to display to other computers, wireless and wired
- **Types:** Parallel - all bits of "frame" are transmitted at once, multiple channels for each bit; Serial - bits of "frame" are transmitted one by one.
- (Transmitter) Tx < - channel - > Rx (Receiver) | Master - initiates communication, generates clock signals; Slave - responds to communication requests; Both can be either Tx or Rx. 
- **Channels:** Simplex (1-wire) - 1-way; Half Duplex (1-wire) - 2-way, 1-way at a time; Full Duplex (2-wire) 2-way
- **Timing:** Synchronous - aligned w/ clock, SCL (clock) and SDA (data); Asynchronous - no clock, start signal, Baud rate (could represent bits per seconds (bps) or bytes per second (Bps/Cps) depending on implementation)

- **Protocol:** set of rules defining detection of signal, start/end signal, message format. \# of bits in a frame. Start bit, stop bit, logic 0, logic 1, ACK, NACK, Baud rate/SCL, order (MSB or LSB first). How do we represent a bit? How do we start/stop a byte? What order are bits sent?
- **RS232:** Asynchronous; GPS, Ultrasonic, Fingerprint Sensors, PC-devices; **Active-Low** - low voltage = logic 1, high = logic 0; Baud rate = bits per second; **Idle** - Low Voltage or infinite logic 1's; **Start** - Logic 0 or high voltage; N data bits - usually 8; **Stop** - 1's forever, back to idle; bit order undetermined (commonly MSB first); Time to transmit 1 bit is 1/baudrate
- **UART:** Universal Asynchronous Receive & Transmit, baud rate at Rx and Tx; (UART0 Tx: PTA2, Rx: PTA1, UART1 Tx: PTE0, Rx: PTE1, UART2 Tx: PTD2, Rx: PTD3) Steps: (1) Choose Clock: Set SIM->SOPT2 bits to choose source, pick one that makes bauddiv closest to integer (2) Choose Bauddiv: $f_{UARTSRC}/(16\cdot rate)$, round to closest value (3) Enable clock gating/PCR: SIM->SCGC4 for UART clock (0x1 << 26 for 48MHz System Clock, 0x2 for 8MHz OSCERCLK), SIM->SCGC5, PTA pin mux for UART pins (4) Set Baud Divisor Registers: UART0->BDH = upper 4 bits; UART0->BDL = lower 8 bits; `UART0->C2 |= (1 << 3)` enable Tx (5) Write to UART->D and wait until UART0->S1 complete is 1; reset process/sendByte->`int dummy = UART0->S1; dummy++; UART0->D = data; while(!(UART0->S1 & (1 << 6)) {}`
- **SPI:** Serial Peripheral Interface; Synchronous, Shift Register-Based protocol, designed for communication between Host(Master) & Peripheral(Slave) devices (between microcontrollers); **SCLK** - serial clock; **SS** - slave select, *active low*; **MOSI** - Master out slave in; **MISO** - Master in slave out; on posedge SCLK, data is sampled (outputted and shifted from both master and slave), on negedge is propagated to new position
	- Multiple Slaves: independent slaves - M -> S1, S2, S3; daisy chain/cooperative slaves - M -> S1 -> S2 -> S3 -> M
	- Timing: Polarity - CPOL = 0 -> posedge is leading, CPOL = 1 -> negedge is leading; Phase - CPHA = 0 -> Sample on Leading, Transmit on Trailing, CPHA = 1 -> Sample on Trailing, Transmit on Leading
	- Advantages: full-duplex, fast, protocol-free, simple hardware, slaves don't need separate clock, address free, low pin count; Disadvantages: Higher pin count than I2C, no flow control or Slave ACK, one master, slaves cannot initiate transfers, vari. in implementation, short-distance
	- Steps for setup: (1) update C1 to enable SPI and control interrupt enables, set SPI as master or slave, determine clock phase and polarity (2) update C2 to enable additional SPI functions (3) update BR to set prescaler and baud divisor for master (4) update Hardware Match (MH:ML) with value to be compared to the receive data register if HW match interrupts are enabled (5) read S when S\[SPTEF\] = 1, then write to DH:DL to begin transfer.
```
uint8_t SPI_transfer_byte(uint8_t byte_out) {
	uint8_t byte_in; uint8_t bit;
	for (bit = 0; bit < 8; bit++) {
	// shift-out bit to the MOSI pin, MSB first
	if (byte_out & 0x80) write_MOSI(HIGH); else write_MOSI(LOW);
	byte_out <<= 1; delay(SPI_SCLK_LOW_TIME); //delay for at least the peer's setup time write_SCLK(HIGH); //pull clock line high byte_in <<= 1; //shift-in bit from the MISO line
	if (read_MISO() == HIGH) byte_in |= 1;
	delay(SPI_SCLK_HIGH_TIME); //delay for at least the peer's hold time write_SCLK(LOW); //pull clock line low
	}return byte_in;}
```

- **I2C:** Inter-Integrated Circuit Communication; Synchronous, Half-Duplex; Only 2 bus lines, SDA & SCL, active high & MSB 1st; **Advantages:** 2 bus lines, multiple masters, widely supported; **Dis:** slower than SPI, slaves must have unique addresses (112 available), fixed data transfer size (1 byte), half-duplex

| STATE | Idle | Start        | Tx logic 0 | Tx logic 1 | After 8th Data: ACK | After 8th Data: NACK | After ACK/NACK, Stop/Idle |
| ----- | ---- | ------------ | ---------- | ---------- | ------------------- | -------------------- | ------------------------- |
| SCL   | High | High         | Rising     | Rising     | High                | High                 | High                      |
| SDA   | High | Falling Edge | Low        | High       | Low                 | High                 | High                      |

- **Sending an Address:** (1) start bit (2) 7 bits of address (3) Read-1/Write-0 bit to slave (4) ACK-0/NACK-1 from slave; **Clock Stretching:** if Rx not ready after ACK, slave holds SCL low until ready; **Master Write:** on data byte, NACK means slave not ready to receive anymore. (**START** | **S Address** | **R/~W** | *A* | **DATA** | *A* | **DATA** | *A/~A* | **STOP**); **Master Read:** (**START** | **S Address** | **R/~W** | *A* | *DATA* | **A** | *DATA* | **~A** | **STOP**)
- Steps for setup: (1) Enable clock gating for I2C module and port (see top) (2) setup pin mode for I2C (see PCR) (3) Write 0 to all I2C registers (A1, C1, C2, RA, SMB, A2) (4) write 0x50 to FLT register (clears all bits) (5) clear status flags (write 1 to FLT bit 4 and 6, write 1 to S bit 4 and 1) (6) set I2C divider register (choose a clock frequency less than 100 KHz, use 14 in F\[5-0\] (ICR) with 8MHz) (7) Set bit to enable I2C module and interrupts in C1, bit 6 for interrupt requests, bit 7 for enabling (8) follow figure initialization (9) enable TX, bit 4 for transmit vs receive, bit 5 for master mode
- Slave: (6) Write C2 to enable/disable general call and select 10-bit or 7-bit addressing mode (7) A1 to set slave address (8) C1 to enable I2C module and interrupts (9) follow figure initialization
```
initI2C() {//see above}  
clearStatusFlags() {// Clear STOPF and Undocumented STARTF bit 4 in Filter Register  // Clear ARBL and IICIF bits in Status Register}
TCFWait() {// Wait for TCF bit to Set in Status Register}
IICIFWait() {// Wait for IICIF bit to Set in Status Register}
SendStart() {// Set MST and TX bits in Control 1 Register}
RepeatStart() {// Set MST, TX and RSTA bits in Control 1 Register // Wait 6 cycles}
SendStop() {// Clear MST, TX and TXAK bits in Control 1 Register // Wait for BUSY bit to go low in Status Register}
clearIICIF() {// Clear IICIF bit in Status Register}
RxAK() {// Return 1 if byte has been ACK'd. (See RXAK in Status Register)}  
I2C WriteByte (Register Address, Data) {
	clearStatusFlags(); TCFWait(); SendStart(); 
	// TODO: Write Device Address, R/W = 0 to Data Register   
	IICIFWait()/TCFWait();
	if (!RxAK()){printf("NO RESPONSE - Address"); SendStop(); return;}  
	clearIICIF(); // TODO: Write Register address to Data Register   IICIFWait();  
	if (!RxAK()){printf("NO RESPONSE - Register"); SendStop(); return;}  
	TCFWait(); clearIICIF(); // Write Data byte to Data Register   
	IICIFWait()/TCFWait(); 
	if (!RxAK()){printf("Incorrect ACK - Data");}  
	clearIICIF(); SendStop();
}  
Read Block(Register Address, Destination Data Byte Array, Length) {
	unsigned char dummy = 0; clearStatusFlags(); TCFWait(); SendStart(); dummy++; // Do something to suppress the warning.  
	//TODO: Write Device Address, R/W = 0 to Data Register   
	IICIFWait()/TCFWait();  
	if (!RxAK()){printf("NO RESPONSE - Address"); SendStop(); return 0;  }  
	clearIICIF(); 
	// Write Register address to Data Register   
	IICIFWait()/TCFWait();  
	if (!RxAK()){printf("NO RESPONSE - Register"); SendStop(); return 0;}  
	clearIICIF(); RepeatStart(); 
	// Write device address again, R/W = 1 to Data Register   
	IICIFWait()/TCFWait();  
	if (!RxAK()){printf("NO RESPONSE - Restart"); SendStop(); return 0;}  
	TCFWait(); clearIICIF(); // Switch to RX by clearing TX and TXAK bits in Control 1 register  
	if(len==1){// Set TXAK to NACK in Control 1 - No more data!}  
	dummy = I2C0->D; // Dummy Read  
	for(int index=0; index<len; index++){
	IICIFWait(); clearIICIF();  
	if(/*Second to Last Byte*/){// Set TXAK to NACK in Control 1 - No more data!}  
	if(/*Last Byte*/){SendStop();}  
	// Read Byte from Data Register into Array}
}
```

---
- **Channel Errors:** Not errors in baud rate or decoding/encoding, but errors resulting from bit flips or bit loss in the channel. *Headers* - Message  - *Trailers (error detects here)* | Parity - detect odd number of bit flips; Checksum - detect any bit errors; CRC - Cyclic Redundancy Check - most accurate for error detection.
- **Parity:** count \# of '1' bits occuring in data. **Even:** if \# of set bits is odd, Parity bit=1 to have even \# of 1's. **Odd:** if \# of set bits is even, Parity bit=1 to have odd \# of 1's. After sending message and parity bit to Rx, it calculates parity of message, and if Parity bit=1 on Rx end, error occurred. Use XOR between bits to calculate Even Parity, and XNOR for Odd Parity; only detects odd \#s of bit flips.
- **Checksum:** sum all bytes of message together, append 2's complement (flip and +1 from pos to neg) of sum to end of message. When Rx sums the bytes together, result should be 0.
- **CRC:** Uses divisor with L bits(can be given in polynomial form), append L-1 0s to data bits, perform binary division for CRC generation, Rx and Tx agree on same divisor. (1) align divisor first bit with closest 1 from the left of data (2) XOR bitwise (3) append next L data bits not XORed in (2) to end of result s.t. (4) repeat from 1 with new value until no 1's are left side from initial append (5) append rest of bits to end of result, right L-1 bits is CRC Checksum. Tx sends data.append(CRC Checksum)
- **Program Architecture**: *Monolithic Loop* - Single, infinite loop, program size keeps growing, delays, simple applications | *State Machine* - Mealy and Moore, communication protocols | *Publisher-Subscriber* - Event-driven, real-time distribution of data, GPS navigation | *Cooperative Task Scheduling* - Multitasking, OS does not initiate context switch, processes yield voluntarily, process scheduler starts/stops processes
- **Operating System**: Resource Management, Task Management, Peripherals - Interrupt Handling
- RTOS: OS with strict deadlines, prioritize tasks based on urgency, deterministic task scheduling
- Multithreading: one process - multiple threads (shared memory, shared registers (GPR), run on same processor, concurrency)
	- Switching between threads: context switching: switch on event. Context: current state of a task/thread: GPR, address spaces, data, status register, PC. **1**. Save state of current thread (push) **2**. Retrieve state of next thread (pop) **3**. start next thread
	- Round robin - fixed time duration for each thread, CPU scheduling algorithm
	- priority based scheduling - priority determines task: shortest amount of time and deadline considered
- Multiprocessing: multiple processes (no shared resources, separate address space, run on different processors, parallelism)
- **Path Planning:** how to get from start to goal. *Exploration:* Undirected, reactive, uninformed, not efficient | *Path Planning:* Goal-Oriented, predictive, prior knowledge
- State transition: intermediate steps between start and end. **Local and Global planners:** latter = rough sketch of overall path, former = specific of how robot goes from waypoint to waypoint along the latter.
- **Planning Algorithms:** *Potential field:* obstacle repels robot, goal attracts robot, think topological, add different maps, force vector according to threshold | *Graph Search:* Dijkstra's, A* | *Sampling:* random search
- **Kinematics:** resulting position of robot given inputs. *Ackerman:* steered wheels in the front and drive wheels in the back, four wheel drive and some kind of steering | *Differential Drive:* two wheels that are independent, can spin in place | *Omnidrive:* special wheels that can slide sideways, any direction is possible
- *Forward Kinematics:* give set of instructions and predict resulting configuration | *Inverse Kinematics:* need configuring, predict set of commands.
- **Inertial Measurement:** figure out pose of some kind of system: 6-axis position and orientation of object = x, y, z cartesian + roll(from front), pitch (from side), and yaw (from top) | Cartesian sensing = GPS, Orientation sensing = Gyroscopic sensing (MEMS vibrating wiggle), accelerometers (MEMS wiggle), magnetometer (hall effect, measure side voltage to know strength)
- *Sensing Heading w/ Gyro:* gives us rotation rate as $\omega$ get position = $\int \omega dt$. $\sum \omega \Delta t$ to approximate. *Accelerometer:* measures instantaneous acceleration, same integrationx2 to get velocity then position. m/s^2 or Gs, Magnetometer must know declination angle. **Calibration is necessary. Drift is real (noise) and bad.** Quaternion: **2 acos (magnitude A), rotation around z-axis is az**
- **GPS:** 30 satellites around orbit have precise clock (coordinated), ground signals tells satellites their position, knows when and where it is at all times: receiver can receive radio signals from each satellite, receiver calculates how long the radio signals took to get to them, then calculates position At least 4 satellites. 3-5m accuracy, 100Hz position update, most receivers 1-10 Hz. Signals weakened indoors. Not geosynchronous orbit
- **GPS outputs NMEA 0183 standard**: RS232 compatible serial output, 9600 baud rate: log of NMEA sentences - $GPGGA, 123519, 4807.038, N, 01131.000, E, 1, 08, 0.9, 545.4, M, 46.9, M,,,\*47
- $GPGGA = Global Positioning System Fix Data | 123519 = Fix taken at 12:35:19 UTC | 4807.038, N = latitude 48 deg 07.038' N | 01131.000, E = longitude 11 deg 31.000' E | 1 = fix quality | 08 = number of satellites being tracked | 0.9 Horizontal dilution of position | 545.4, M = altitude, meters, above mean sea level | 46.9, M = Height of geoid (mean sea level) above WGS ipsoid. \*47 = checksum data, empty fields could be seconds before last update
- $GPRMC: 1 Time Stamp | 2  validity - A-ok, V-invalid | 3 current Latitude | 4 North/South | 5 current Longitude | 6 East/West | 7 Speed in knots | 8 True course | 9 Date Stamp | 10 Variation | 11 East/West | 12 checksum
- $GPVTG: 1 Track made good | 2 T | 3 not used | 4 not used | 5 speed over ground in knots | 6 N for knots | 7 speed over ground in kph | 8 K for kph | 9 checksum | use this before $GPGGA to validify
- Decimal degree = degree + minutes/60, minutes is the '31.000' and above. **Bearing angle:** source and destination x and y coordinates - angle clockwise from north that will take us directly to destination from source. arctan2 of differences, between pi/2 and -pi/2: set heading to bearing
- Accuracy < n meters -> divide by light speed to get Rx time period needed, reciprocal for frequency.
- Pseudocode: enable clock gating (UART, PORTE), enable UART, Baud rate (9600), Send/Receive data GPGGA
- **LIDAR:** UV, visible light, near IR (green light). Sonar - sound, underwater, short distance | Radar - radio waves, long distance, fog, rain, smog. LIDAR: high accuracy, 3D, integrate data from other sources (GPS, IMU), fastest
- Airborne - planes, topography; Terrestrial - mining, road; spaceborne - satellites: Integrate to FRDM: 1. Lidar sensors datasheet to get I2C settings and time of flight 2. I2C communication, SDA and SCL 3. clock gating for I2C module and port 4. Enable I2C in registers 5. SDA/SCL PCR 6. SCL divider register 7. write to data reg
- **Quaternion:** $q = (q_0, q_1, q_2, q_3)$ where $q_0 = \cos \frac{\theta}{2}$, $q_1 = \hat{x} \sin \frac{\theta}{2}$, $q_2 = \hat{y} \sin \frac{\theta}{2}$ , $q_3 = \hat{z} \sin \frac{\theta}{2}$ where $(\hat{x}, \hat{y}, \hat{z})$ is a unit vector that defines the axis of rotation and $\theta$ is the amount of rotation around that unit vector.