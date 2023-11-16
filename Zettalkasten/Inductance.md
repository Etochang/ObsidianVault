202311151720
Meta Tags: #MOC #textbook
Tags: [[physics]]

# Inductance

## Introduction

## Summary

### a. [[Mutual Inductance]]

When a changing current $i_1$ in one circuit causes a changing magnetic flux in a second circuit, an emf $\mathcal{E}_2$ is induced in the second circuit, and vice versa.
$$\mathcal{E}_2 = -M\frac{di_1}{dt}$$
$$\mathcal{E}_1 = -M\frac{di_2}{dt}$$
If the circuits are coils of wire with $N_1$ and $N_2$ turns, the mutual inductance $M$ can be expressed in terms of the average flux $\Phi_{B2}$ through each turn of coil 2 caused by the current $i_1$ in coil 1, or vice versa.
$$M=\frac{N_2\Phi_{B2}}{i_1}=\frac{N_1\Phi_{B1}}{i_2}$$
![[Pasted image 20231115173725.png]]

### b. [[Self-Inductance and Inductors]]

A changing current $i$ in any circuit causes a self-induced emf $\mathcal{E}$ . 
$$\mathcal{E} = -L\frac{di}{dt}; V_{ab} = -\mathcal{E}$$
The inductance (or self-inductance) $L$ depends on the geometry of the circuit and the material surrounding it. The inductance of a coil of $N$ turns is related to the average flux $\Phi_B$ through each turn caused by the current $i$ in the coil. 
$$L=\frac{N\Phi_B}{i}$$
An inductor is a circuit device, usually including a coil of wire, intended to have a substantial inductance.
![[Pasted image 20231115175948.png]]

### c. [[Magnetic-Field Energy]]

An inductor with inductance $L$ carrying current $I$ has energy $U$ associated with the inductor's magnetic field.
$$U=\frac{1}{2} LI^2$$
The magnetic energy density $u$ (energy per unit volume) is proportional to the square of the magnetic-field magnitude.
$$u=\frac{B^2}{2\mu} \ \textrm{(in material with magnetic permeability } \mu)$$
```ad-help
See [[Magnetic Materials]] for info on $\mu$.

```
![[Pasted image 20231115180547.png]]
### d. [[The R-L Circuit]]

In a circuit containing a resistor $R$, an inductor $L$, and a source of emf, the growth and decay of current are exponential. The time constant $\tau$ is the time required for the current to approach within a fraction $1/e$ of its final value.
$$\epsilon -iR -L\frac{di}{dt} = 0 \ \textrm{(differential equation)}$$
$$\tau = \frac{L}{R}$$

![[Pasted image 20231115180848.png]]

### e. [[The L-C Circuit]]

A circuit that contains inductance $L$ and capacitance $C$ undergoes electrical oscillations with an angular frequency $\omega$ that depends on $L$ and $C$. This is analogous to a mechanical harmonic oscillator, with inductance $L$ analogous to mass $m$, the reciprocal of capacitance $\frac{1}{C}$ to force constant $k$, charge $q$ to displacement $x$, and current $i$ to velocity $v_x$.
$$\omega = \sqrt{\frac{1}{LC}}$$
![[Pasted image 20231115183334.png]]

### f. [[The L-R-C Series Circuit]]

A circuit that contains inductance, resistance, and capacitance undergoes damped oscillations for sufficiently small resistance. The frequency $\omega'$ of damped oscillations depends on the values of $L$, $R$, and $C$ . As $R$ increases, the damping increases; if $R$ is greater than a certain value, the behavior becomes overdamped and no longer oscillates.
$$\omega ' = \sqrt{\frac{1}{LC} - \frac{R^2}{4L^2}}$$
$$\mathcal{E} - \frac{q}{C} - iR - L\frac{di}{dt} = 0 \ \textrm{(differential equation)}$$
#### Proof for Oscillation Frequency:
$\frac{q}{C} + iR + L\frac{di}{dt} = \mathcal{E}$
$\frac{1}{C}q + Rq' + Lq'' = \mathcal{E}$
$Lq'' + Rq' + \frac{1}{C}q= \mathcal{E}$
$q'' + \frac{R}{L}q' + \frac{1}{LC}q= \frac{\mathcal{E}}{L}$
Characteristic Equation:
$r^2 + \frac{R}{L}r + \frac{1}{LC} = 0$
$r = \frac{-\frac{R}{L} \pm \sqrt{\frac{R^2}{L^2}-\frac{4}{LC}}}{2} = -\frac{R}{2L} \pm \sqrt{\frac{R^2}{4L^2}-\frac{1}{LC}} = -\frac{R}{2L} \pm \sqrt{\frac{1}{LC}-\frac{R^2}{4L^2}} i$ 
Because of complex roots rules for 2nd order odes, $\omega ' = \sqrt{\frac{1}{LC} - \frac{R^2}{4L^2}}$ 




---
# *References*

Pearson PHY 131 at ASU