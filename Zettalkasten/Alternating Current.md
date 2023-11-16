202311141757
Meta Tags: #MOC #textbook 
Tags: [[physics]]

# Alternating Current

## Introduction

## Summary

### a. [[Phasors and Alternating Currents]]

An alternator or AC source produces an emf that varies sinusoidally with time. A sinusoidal voltage or current can be represented by a phasor, a vector that rotates counterclockwise with constant angular velocity $\omega$ equal to the angular frequency of the sinusoidal quantity.  Its projection on the horizontal axis at any instant represents the instantaneous value of the quantity.

![[Pasted image 20231116001603.png]]

For a sinusoidal current, the rectified average and rms (root-mean-square) currents are proportional to the current amplitude $I$. Similarly, the rms value of a sinusoidal voltage is proportional to the voltage amplitude $V$.
$$I_{rav} = \frac{2}{\pi}I;\ I_{rms} = \frac{I}{\sqrt{2}};\ V_{rms} = \frac{V}{\sqrt{2}}$$
In general, the instantaneous voltage $v = V \cos{(\omega t + \phi)}$ between two points in an AC circuit is not in phase with the instantaneous current passing through those points. The quantity $\phi$ is called the phase angle of the voltage relative to the current. 
![[Pasted image 20231116002031.png]]

### b. [[Resistance and Reactance]]

The voltage across a resistor $R$ is in phase with the current. The voltage across an inductor $L$ leads the current by $90 \degree (\phi = + 90 \degree)$, while the voltage across a capacitor $C$ lags the current by $90 \degree ( \phi = - 90 \degree)$. The voltage amplitude across each type of device is proportional to the current amplitude $I$.
$$V_R = IR$$
$$V_L = IX_L;\ X_L = \omega L$$
$$V_C = IX_C;\ X_C = \frac{1}{\omega C}$$
![[Pasted image 20231116002349.png]]

### c. [[The L-R-C Series Circuit]]

In a general AC circuit, the voltage and current amplitudes are related by the circuit impedance $Z$. In an $L-R-C$ series circuit, the values of $L$, $R$, $C$, and the angular frequency $\omega$ determine the impedance and the phase angle $\phi$ of the voltage relative to the current.
$$V = IZ;\ Z = \sqrt{R^2+(X_L-X_C)^2}$$
$$\tan{\phi} = \frac{X_L - X_C}{R}$$
![[Pasted image 20231116002707.png]]


### d. [[Power in Alternating-Current Circuits]]

The average power input $P_{av}$ to an AC circuit depends on the voltage and current amplitudes (or, equivalently, their rms values) and the phase angle $\phi$ of the voltage relative to the current. The quantity $\cos \phi$ is called the power factor.
$$P_{av} = \frac{1}{2}VI \cos \phi = V_{rms}I_{rms} \cos \phi$$
![[Pasted image 20231116002912.png]]

### e. [[Resonance in Alternating-Current Circuits]]

In an $L-R-C$ series circuit, the current becomes maximum and the impedance becomes minimum at an angular frequency called the **resonance angular frequency**. This phenomenon is called resonance. At resonance, the voltage and current are in phase, and the impedance $Z$ is equal to the resistance $R$. 
$$\omega_0 = \frac{1}{\sqrt{LC}}$$
![[Pasted image 20231116003114.png]]


### f. [[Transformers]]

A transformer is used to transform the voltage and current levels in an AC circuit. In an ideal transformer with no energy losses, if the primary winding has $N_1$ turns and the secondary winding has $N_2$ turns, the amplitudes (or rms values) of the two voltages are related by:
$$\frac{V_2}{V_1} = \frac{N_2}{N_1}$$
$P_1 = P_2;\ V_1I_1 = V_2I_2$ 
$$\frac{V_1}{I_1} = \frac{R}{(N_2/N_1)^2}$$


---
# *References*

Pearson PHY 131 at ASU