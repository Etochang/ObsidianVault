202311150043
Meta Tags: #MOC
Tags: [[physics]]

# Direct-Current Circuits

## Introduction

## Summary

### a. [[Resistors in Series and Parallel]]

When several resistors $R_1, R_2, R_3, ...$ are connected in series, the equivalent resistance $R_{eq}$ is the sum of the individual resistances. The same *current* flows through all the resistors in a series connection. 
$$R_{eq} = R_1 + R_2 + R_3 + \cdots \textrm{(resistors in series)}$$
When several resistors are connected in parallel, the reciprocal of $R_{eq}$ is the sum of the reciprocals of the individual resistances. All resistors in a parallel connection have the same *potential difference* between their terminals.
$$\frac{1}{R_{eq}} = \frac{1}{R_{1}} + \frac{1}{R_{2}} + \frac{1}{R_{3}} \cdots \textrm{(resistors in parallel)}$$
![[Pasted image 20231115013357.png]]

### b. [[Kirchhoff's Rules]]

Kirchhoff's junction rule:
- based on conservation of charge
- states that the algebraic sum of the currents into any junction must be zero
$$\sum I = 0$$

Kirchhoff's loop rule:
- based on conservation of energy and the conservative nature of electrostatic fields
- states that the algebraic sum of potential differences around any loop must be zero
$$\sum V = 0$$
```ad-warning
Careful use of sign rules is essential in applying Kirchhoff's rules.

```
![[Pasted image 20231115013348.png]]

### c. [[Electrical Measuring Instruments]]

In a d'Arsonval galvanometer, the deflection is proportional to the current in the coil. For a larger current range, a shunt resistor is added, so some of the current bypasses the meter coil. Such an instrument is called an ammeter. If the coil and any additional series resistance included obey Ohm's law, the meter can also be calibrated to read potential difference or voltage. The instrument is then called a voltmeter. Ideal ammeter has very low resistance, while ideal voltmeter has very high resistance.
![[Pasted image 20231115013332.png]]
### d. [[R-C Circuits]]

When a capacitor is charged by a battery in series with a resistor, the current and capacitor charge are not constant. The charge approaches its final value asymptotically and the current approaches zero asymptotically. After a time $\tau = RC$, the charge has approached within $1/e$ of its final value. $\tau$ is called the *time constant* of the circuit. 

**Capacitor charging:**
$$q = C\epsilon(1-e^{\frac{-t}{RC}})=Q_f(1-e^{\frac{-t}{RC}})$$
$$i = \frac{dq}{dt} = \frac{\epsilon}{R}e^{\frac{-t}{RC}} = I_0e^{\frac{-t}{RC}}$$

**Capacitor discharging:**
$$q=Q_0e^{\frac{-t}{RC}}$$
$$i = \frac{dq}{dt} = \frac{Q_0}{RC}e^{\frac{-t}{RC}}=I_0e^{\frac{-t}{RC}}$$
![[Pasted image 20231115014429.png]]


### e. [[Power Distribution Systems]]



---
# *References*

Pearson PHY 131 at ASU