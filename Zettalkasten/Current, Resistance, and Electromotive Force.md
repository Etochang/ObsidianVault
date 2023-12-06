202312041619
Meta Tags: #textbook #MOC 
Tags: [[physics]]

# Current, Resistance, and Electromotive Force

## Introduction
## Summary

### a. [[Current]]

Current is the amount of charge flowing through a specified area, per unit time. The SI unit of current is the ampere ($1 A = 1 C/s$). The current $I$ through an area $A$ depends on the concentration $n$ and charge $q$ of the charge carriers, as well as on the magnitude of their drift velocity $\vec{v_d}$. 
$$I = \frac{dQ}{dt} = n |q| v_d A$$
The current density is current per unit cross-sectional area. 
$$\vec{J} = nq \vec{v_d}$$
Current is usually described in terms of a flow of positive charge, even when the charges are actually negative or of both signs.
![[Pasted image 20231205005820.png]]

### b. [[Resistivity]]

The resistivity $\rho$ of a material is the ratio of the magnitudes of electric field and current density. 
$$\rho = \frac{E}{J}$$
Good conductors have small resistivity; good insulators have large resistivity.  Ohm's law, obeyed approximately by many materials, states that $\rho$ is a constant independent of the value of $E$. 

Resistivity usually increases with temperature; for small temperature changes, this variation is represented approximately by
$$\rho(T) = \rho_0[1+\alpha(T-T_0)]$$
where $\alpha$ is the temperature coefficient of resistivity. 
![[Pasted image 20231205010216.png]]

### c. [[Resistance]]

The potential difference $V$ across a sample of material that obeys Ohm's law is proportional to the current $I$ through the sample. The ratio $V/I = R$ is the **resistance** of the sample. The SI unit of resistance is the ohm ($1 \ohm = 1V/A$).
$$V = IR$$
The resistance of a cylindrical conductor is related to its resistivity $\rho$, length $L$, and cross-sectional area $A$.
$$R = \frac{\rho L}{A}$$
![[Pasted image 20231205010608.png]]

### d. [[Electromotive Force and Circuits]]

A complete circuit has a continuous current-carrying path. A complete circuit carrying a steady current must contain a source of electromotive force (emf) $\mathcal{E}$ . The SI unit of electromotive force is the volt (V). Every real source of emf has some internal resistance $r$, so its terminal potential difference $V_{ab}$ depends on current.
$$V_{ab} = \mathcal{E} - Ir \ \textrm{(source with internal resistance)}$$
![[Pasted image 20231205010950.png]]


### e. [[Energy and Power in Electric Circuits]]

A circuit element puts energy into a circuit if the current direction is from lower to higher potential in the device, and it takes energy out of the circuit if the current is opposite. The power $P$ equals the product of the potential difference $V_a - V_b = V_{ab}$ and the current $I$.
$$P = V_{ab}I \ \textrm{(general circuit element)}$$
A resistor always takes electrical energy out of a circuit.
$$P = V_{ab} I = I^2R = \frac{V_{ab}^2}{R} \ \textrm{(power delivered to a resistor)}$$
![[Pasted image 20231205011307.png]]

### f. [[Theory of Metallic Conduction]]

In a metal, current is due to the motion of electrons. They move freely through the metallic crystal but collide with positive ions. In a crude classical model of this motion, the resistivity of the material can be related to the electron mass, charge, speed of random motion, density, and mean free time between collisions.
$$\rho = \frac{m}{ne^2\tau}$$
![[Pasted image 20231205011429.png]]



---
# *References*