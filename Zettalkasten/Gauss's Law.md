202312041615
Meta Tags: #MOC #textbook 
Tags: [[physics]]

# Gauss's Law

## Introduction

## Summary

### a. [[Charge and Electric Flux]]

Electric flux is a measure of the "flow" of electric field through a surface. 

### b. [[Calculating Electric Flux]]

Electric flux is equal to the product of an area element and the perpendicular component of $\vec{E}$ , integrated over a surface.
$$\Phi_E = \int E \cos{\phi} \ dA = \int E_\perp \ dA = \int \vec{E} \cdot d\vec{A}$$
![[Pasted image 20231204175326.png]]
### c. [[Gauss's Law Intro]]

Gauss's law states that the total electric flux through a closed surface equals a constant times the total charge $Q_{encl}$ enclosed by the surface. Gauss's law is logically equivalent to Coulomb's law, but its use greatly simplifies problems with a high degree of symmetry.
$$\Phi_E = \frac{Q_{encl}}{\epsilon_0}$$
![[Pasted image 20231204175639.png]]

When excess charge is placed on a solid conductor and is at rest, it resides entirely on the surface, and $\vec{E} = \vec{0}$ everywhere in the material of the conductor.
### d. [[Applications of Gauss's Law]]

The following table lists electric fields caused by several symmetric charge distributions. In the table, $q$, $Q$, $\lambda$, and $\sigma$ refer to the *magnitudes* of the quantities.

| Charge Distribution                                                                           | Point in Electric Field    | E-Field Magnitude                                |
| --------------------------------------------------------------------------------------------- | -------------------------- | ------------------------------------------------ |
| Single point charge $q$                                                                       | Distance $r$ from $q$      | $E = \frac{1}{4\pi\epsilon_0} \frac{q}{r^2}$     |
| Charge $q$ on surface of conducting sphere with radius $R$                                    | Outside sphere, $r > R$    | $E = \frac{1}{4\pi\epsilon_0} \frac{q}{r^2}$     |
|                                                                                               | Inside sphere, $r > R$     | $E = 0$                                          |
| Infinite wire, charge per unit wire length $\lambda$                                          | Distance $r$ from wire     | $E = \frac{1}{2\pi\epsilon_0} \frac{\lambda}{r}$ |
| Infinite conducting cylinder with radius $R$, charge per unit length $\lambda$                | Outside cylinder, $r > R$  | $E = \frac{1}{2\pi\epsilon_0} \frac{\lambda}{r}$ |
|                                                                                               | Inside cylinder, $r < R$   | $E = 0$                                          |
| Solid insulating sphere with radius $R$, charge $Q$ distributed uniformly throughout volume   | Outside sphere, $r > R$    | $E = \frac{1}{4\pi\epsilon_0} \frac{Q}{r^2}$     |
|                                                                                               | Inside sphere, $r < R$     | $E = \frac{1}{4\pi\epsilon_0} \frac{Qr}{R^3}$    |
| Infinite sheet of charge with uniform charge per unit area $\sigma$                           | Any point                  | $E = \frac{\sigma}{2\epsilon_0}$                 |
| Two oppositely charge conducting plates with surface charge densities $+\sigma$ and $-\sigma$ | Any point                  | $E = \frac{\sigma}{\epsilon_0}$                  |
| Charged Conductor                                                                             | Just outside the conductor | $E = \frac{\sigma}{\epsilon_0}$                                                 |

### e. [[Charges on Conductors]]





---
# *References*