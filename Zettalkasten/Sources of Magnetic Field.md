202311150259
Meta Tags: #MOC #textbook 
Tags: [[physics]]

# Sources of Magnetic Field

## Introduction

## Summary

### a. [[Magnetic Field of a Moving Charge]]

The magnetic field $\vec{B}$ created by a charge $q$ moving with velocity $\vec{v}$ depends on the distance $r$ from the source point (the location of $q$) to the field point (where $\vec{B}$ is measured). The magnetic field is perpendicular to $\vec{v}$ and to $\hat{r}$ , the unit vector directed from the source point to the field point.
$$\vec{B} = \frac{\mu_0}{4\pi} \frac{q \vec{v} \times \hat{r}}{r^2}$$
![[Pasted image 20231115032759.png]]
The principle of superposition of magnetic fields states that the total magnetic field produced by several moving charges is the vector sum of the fields produced by the individual charges. 
### b. [[Magnetic Field of a Current Element]]

The Biot-Savart law gives the magnetic field $d\vec{B}$ created by an element $d\vec{l}$ of a conductor carrying current $I$. The field $d\vec{B}$ is perpendicular to both $d\vec{l}$ and $\hat{r}$ , the unit vector from the element to the field point. The magnetic field created by a finite current-carrying conductor is the integral of $d\vec{B}$ over the length of the conductor.
$$d\vec{B} = \frac{\mu_0}{4\pi} \frac{I \ d\vec{l} \times \hat{r}}{r^2}$$
![[Pasted image 20231115113106.png]]
### c. [[Magnetic Field of a Straight Current-Carrying Conductor]]

The magnetic field $\vec{B}$ at a distance $r$ from a long, straight conductor carrying a current $I$ has a magnitude that is inversely proportional to $r$. The magnetic field lines are circles coaxial with the wire, with directions given by the right-hand rule.
$$B=\frac{\mu_0 I}{2\pi r}$$
![[Pasted image 20231115113531.png]]
### d. [[Force Between Parallel Conductors]]

Two long, parallel, current-carrying conductors attract if the currents are in the same direction and repel if the currents are in opposite directions. The magnetic force per unit length between the inductors depends on their currents $I$ and $I’$ as well as separation $r$. The definition of the ampere is based on this relationship. 
$$\frac{F}{L} = \frac{\mu_0II’}{2\pi r}$$
![[Pasted image 20231115113949.png]]
### e. [[Magnetic Field of a Circular Current Loop]]

The Biot-Savart law allows us to calculate the magnetic field produced along the axis of a circular conducting loop of radius $a$ carrying current $I$ . The field depends on the distance $x$ along the axis from the center of the loop to the field point. If there are $N$ loops, the field is multiplied by $N$. At the center of the loop, $x=0$ .
$$B_x = \frac{\mu_0NIa^2}{2(x^2+a^2)^\frac{3}{2}} \ \textrm{(N circular loops)}$$
$$B_x=\frac{\mu_0NI}{2a} \ \textrm{(center of N circular loops)}$$
![[Pasted image 20231115114433.png]]

### f. [[Ampere's Law]]

Ampere’s law states that the line integral of $\vec{B}$ around any closed path equals $\mu_0$ times the net current through the area enclosed by the path. The positive sense of current is determined by a right-hand rule.
$$\oint \vec{B} \cdot d\vec{l} = \mu_0 I_{encl}$$
![[Pasted image 20231115114714.png]]
### g. [[Applications of Ampere's Law]]

| Current Distribution                                                           | Point in Magnetic Field                                                    | $\vec{B}$ Magnitude                          |
| ------------------------------------------------------------------------------ | -------------------------------------------------------------------------- | -------------------------------------------- |
| Long, straight conductor                                                       | Distance $r$ from conductor                                                | $B=\frac{\mu_0I}{2\pi r}$                    |
| Circular loop of radius $a$ (for $N$ loops, multiply expressions by $N$)       | On axis of loop                                                            | $B=\frac{\mu_0Ia^2}{2(x^2+a^2)^\frac{3}{2}}$ |
|                                                                                | At center of loop                                                          | $B=\frac{\mu_0I}{2a}$                        |
| Long cylindrical conductor of radius $R$                                       | Inside conductor, $r < R$                                                  | $B=\frac{\mu_0I}{2\pi}\frac{r}{R^2}$         |
|                                                                                | Outside conductor, $r > R$                                                 | $B=\frac{\mu_0I}{2\pi r}$                    |
| Long, closely wound solenoid with $n$ turns per unit length, near its midpoint | Inside solenoid, near center                                               | $B=\mu_0nI$                                  |
|                                                                                | Outside solenoid                                                           | $B \approx 0$                                |
| Tightly wound toroidal solenoid (toroidal) with $N$ turns                      | Within the space enclosed by the windings, distance $r$ from symmetry axis | $B=\frac{\mu_0NI}{2\pi r}$                   |
|                                                                                | Outside the space enclosed by the windings                                 | $B \approx 0$                                |

### h. [[Magnetic Materials]]

When magnetic materials are present, the magnetization of the material causes an additional contribution to $\vec{B}$ . 

For paramagnetic and diamagnetic materials, $\mu_0$ is replaced in magnetic-field expressions by $\mu = K_m \mu_0$ , where $\mu$ is the **permeability** of the material and $K_m$ is its **relative permeability**. The magnetic susceptibility $\chi_m$ is defined as $\chi_m = K_m - 1$ . Magnetic susceptibilities for paramagnetic materials are small positive quantities; those for diamagnetic materials are small negative quantities. For ferromagnetic materials, $K_m$ is much larger than unity (1) and is not constant. Some ferromagnetic materials are permanent magnets, retaining their magnetization even after the external magnetic field is removed. 

- Paramagnetic: magnetic field is greater than before, $K_m$ is greater than unity by a small amount
- Diamagnetic: magnetic field is less than before, $K_m$ is less than unity by a small amount.
- Ferromagnetic: magnetic field is much greater than before, magnetizing the material; $K_m$ is greater than unity by a very large amount. 
	- Hysteresis loop:
	![[Pasted image 20231115135505.png]]




---
# *References*

Pearson PHY 131 at ASU