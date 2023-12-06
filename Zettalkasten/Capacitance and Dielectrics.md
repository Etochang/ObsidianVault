202312041618
Meta Tags: #textbook #MOC 
Tags: [[physics]]

# Capacitance and Dielectrics

## Introduction
## Summary
### a. [[Capacitors and Capacitance]]

A capacitor is any pair of conductors separated by an insulating material. When the capacitor is charged, there are charges of equal magnitude $Q$ and opposite sign on the two conductors, and the potential $V_{ab}$ of the positively charged conductor with respect to the negatively charged conductor is proportional to $Q$. The capacitance $C$ is defined as the ratio of $Q$ to $V_{ab}$ . The SI unit of capacitance is the farad (F): $1 F = 1 C/V$.
$$C = \frac{Q}{V_{ab}}$$
A parallel-plate capacitor consists of two parallel conducting plates, each with area $A$, separated by a distance $d$. If they are separated by vacuum, the capacitance depends on only $A$ and $d$. For other geometries, the capacitance can be found by using the definition $C = Q/V_{ab}$. 
$$C = \frac{Q}{V_{ab}} = \epsilon_0 \frac{A}{d}$$
![[Pasted image 20231205003742.png]]

### b. [[Capacitors in Series and Parallel]]

When capacitors with capacitances $C_1$, $C_2$, $C_3$, $...$ are connected in series, the reciprocal of the equivalent capacitance $C_{eq}$ equals the sum of the reciprocals of the individual capacitances.
$$\frac{1}{C_{eq}} = \frac{1}{C_{1}} + \frac{1}{C_{2}} + \frac{1}{C_{3}} + \cdots \ \textrm{capacitors in series}$$
When capacitors are connected in parallel, the equivalent capacitance $C_{eq}$ equals the sum of the individual capacitances.
$$C_{eq} = C_1 + C_2 + C_3 + \cdots \ \textrm{capacitors in parallel}$$
![[Pasted image 20231205004110.png]]

### c. [[Energy Storage in Capacitors and Electric-Field Energy]]

The energy $U$ required to charge a capacitor $C$ to a potential difference $V$ and a charge $Q$ is equal to the energy stored in the capacitor. 
$$U = \frac{Q^2}{2C} = \frac{1}{2} CV^2 = \frac{1}{2} QV$$
This energy can be thought of as residing in the electric field between the conductors; the energy density $u$ (energy per unit volume) is proportional to the square of the electric-field magnitude.
$$u = \frac{1}{2} \epsilon_0 E^2$$
![[Pasted image 20231205004519.png]]

### d. [[Dielectrics]]

When the space between the conductors is filled with a dielectric material, the capacitance increases by a factor $K$, the dielectric constant of the material. The quantity $\epsilon = K \epsilon_0$ is the permittivity of the dielectric. For a fixed amount of charge on the capacitor plates, induced charges on the surface of the dielectric decrease the electric field and potential difference between the plates by the same factor $K$. The surface charge results from polarization, a microscopic rearrangement of charge in the dielectric.
$$C = KC_0 = K\epsilon_0 \frac{A}{d} = \epsilon \frac{A}{d} \ \textrm{parallel-plate w/ dielectric}$$
Under sufficiently strong electric fields, dielectrics can become conductors, a situation called dielectric breakdown. The maximum field that a material can withstand without breakdown is called its dielectric strength.

In a dielectric, the expression for the energy density is the same as in a vacuum but with $\epsilon_0$ replaced by $\epsilon = K\epsilon_0$.
$$u = \frac{1}{2} K \epsilon_0 E^2 = \frac{1}{2} \epsilon E^2$$
![[Pasted image 20231205005427.png]]

### e. [[Molecular Model of Induced Charge]]
### f. [[Gauss's Law in Dielectrics]]

Gauss's law in a dielectric has almost the same form as in a vacuum, with two key differences: $\vec{E}$ is replaced by $K\vec{E}$ and $Q_{encl}$ is replaced by $Q_{encl-free}$, which includes only the free charge (not bound charge) enclosed by the Gaussian surface.
$$\oint K \vec{E} \cdot d\vec{A} = \frac{Q_{encl-free}}{\epsilon_0}$$




---
# *References*