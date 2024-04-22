>PORTX->PCR\[1-0\] - Pull Enable; Pull Select(1-pullup, 0-pulldown)
>SIM->SCGC5 (9-13 = PORTA-PORTE); SCGC4 (23-22 = SPI1-0), (12-10 = UART2-0), (7-6 = I2C1-0); SCGC6 (31 = DAC0), (27 = ADC0), (26-24 = TPM2-0), (23 = PIT) 

---
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

- **Transient Response Properties:** *Rise Time* - how long before PV = SP; *Overshoot* - how far PV goes past SP; *Settling Time* - PV settles within threshold of SP; *Steady State Error* - difference between PV and SP in steady state | **Steady State Response Properties:** Phase/Amplitude
- **Damping:** how fast PV converges to SP; *Uncontrolled* - resonance; *Undamped* - oscillates at frequency; *Underdamped* - oscillates, amplitude decreases; *Overdamped* - never oscillate, never reach SP; *Critically damped* - oscillating time is minimally short

---
- Transfer data/messages between devices, microcontroller to sensor to display to other computers, wireless and wired
- **Types:** Parallel - all bits of "frame" are transmitted at once, multiple channels for each bit; Serial - bits of "frame" are transmitted one by one.
- (Transmitter) Tx < - channel - > Rx (Receiver) | Master - initiates communication, generates clock signals; Slave - responds to communication requests; Both can be either Tx or Rx. 
- **Channels:** Simplex (1-wire) - 1-way; Half Duplex (1-wire) - 2-way, 1-way at a time; Full Duplex (2-wire) 2-way
- **Timing:** Synchronous - aligned w/ clock, SCL (clock) and SDA (data); Asynchronous - no clock, start signal, Baud rate (could represent bits per seconds (bps) or bytes per second (Bps/Cps) depending on implementation)

- **Protocol:** set of rules defining detection of signal, start/end signal, message format. \# of bits in a frame. Start bit, stop bit, logic 0, logic 1, ACK, NACK, Baud rate/SCL, order (MSB or LSB first). How do we represent a bit? How do we start/stop a byte? What order are bits sent?
- **RS232:** Asynchronous; GPS, Ultrasonic, Fingerprint Sensors, PC-devices; **Active-Low** - low voltage = logic 1, high = logic 0; Baud rate = bits per second; **Idle** - Low Voltage or infinite logic 1's; **Start** - Logic 0 or high voltage; N data bits - usually 8; **Stop** - 1's forever, back to idle; bit order undetermined (commonly MSB first); Time to transmit 1 bit is 1/baudrate
- **UART:** Universal Asynchronous Receive & Transmit, baud rate at Rx and Tx; Steps: (1) Choose Clock: Set SIM->SOPT2 bits to choose source, pick one that makes bauddiv closest to integer (2) Choose Bauddiv: $f_{UARTSRC}/(16\cdot rate)$, round to closest value (3) Enable clock gating/PCR: SIM->SCGC4 for UART clock (0x1 << 26 for 48MHz System Clock, 0x2 for 8MHz OSCERCLK), SIM->SCGC5, PTA pin mux for UART pins (4) Set Baud Divisor Registers: UART0->BDH = upper 4 bits; UART0->BDL = lower 8 bits; `UART0->C2 |= (1 << 3)` enable Tx (5) Write to UART->D and wait until UART0->S1 complete is 1; reset process/sendByte->`int dummy = UART0->S1; dummy++; UART0->D = data; while(!(UART0->S1 & (1 << 6)) {}`
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
clearStatusFlags() {// Clear STOPF and Undocumented STARTF bit 4 in Filter Register  // Clear ARBL and IICIF bits in Status Register} || TCFWait() {// Wait for TCF bit to Set in Status Register} || IICIFWait() {// Wait for IICIF bit to Set in Status Register} || SendStart() {// Set MST and TX bits in Control 1 Register} || RepeatStart() {// Set MST, TX and RSTA bits in Control 1 Register // Wait 6 cycles} || SendStop() {// Clear MST, TX and TXAK bits in Control 1 Register // Wait for BUSY bit to go low in Status Register} || clearIICIF() {// Clear IICIF bit in Status Register} || RxAK() {// Return 1 if byte has been ACK'd. (See RXAK in Status Register)}  
I2C WriteByte (Register Address, Data) {
	clearStatusFlags(); TCFWait(); SendStart(); 
	// TODO: Write Device Address, R/W = 0 to Data Register   IICIFWait();
	if (!RxAK()){printf("NO RESPONSE - Address"); SendStop(); return;}  
	clearIICIF(); // TODO: Write Register address to Data Register   IICIFWait();  
	if (!RxAK()){printf("NO RESPONSE - Register"); SendStop(); return;}  
	TCFWait(); clearIICIF(); // Write Data byte to Data Register   IICIFWait();  
	if (!RxAK()){printf("Incorrect ACK - Data");}  
	clearIICIF(); SendStop();
}  
Read Block(Register Address, Destination Data Byte Array, Length) {
	unsigned char dummy = 0; clearStatusFlags(); TCFWait(); SendStart(); dummy++; // Do something to suppress the warning.  
	//TODO: Write Device Address, R/W = 0 to Data Register   IICIFWait();  
	if (!RxAK()){printf("NO RESPONSE - Address"); SendStop(); return 0;  }  
	clearIICIF(); // Write Register address to Data Register   IICIFWait();  
	if (!RxAK()){printf("NO RESPONSE - Register"); SendStop(); return 0;}  
	clearIICIF(); RepeatStart(); // Write device address again, R/W = 1 to Data Register   IICIFWait();  
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
- **CRC:** Uses divisor with L bits(can be given in polynomial form), append L-1 bits to data bits, perform binary division for CRC generation, Rx and Tx agree on same divisor. (1) align divisor first bit with closest 1 from the left of data (2) XOR bitwise (3) append next data bits to end of result s.t. distance from last bit of append is L bits away from next closest 1 (4) repeat until no 1's are left side from initial append (5) append rest of bits to end of result, right L-1 bits is CRC Checksum. Tx sends data.append(CRC Checksum)
