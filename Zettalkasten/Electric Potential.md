202312041617
Meta Tags: #textbook #MOC  
Tags: [[physics]]

# Electric Potential

## Introduction
## Summary

### a. [[Electric Potential Energy]]

The electric force caused by any collection of charges at rest is a **conservative force**. The work $W$ done by the electric force on a charge particle moving in an electric field can be represented by the charge in a potential-energy function $U$. 
$$W_{a \rightarrow b} = U_a - U_b$$
The electric potential energy for two point charges $q$ and $q_0$ depend on their separation $r$.
$$U = \frac{1}{4\pi\epsilon_0} \frac{qq_0}{r}$$
The electric potential energy for a charge $q_0$ in the presence of a collection of charges $q_1$, $q_2$, $q_3$ depends on the distance from $q_0$ to each of these other charges.
$$U = \frac{q_0}{4\pi\epsilon_0} \sum_i \frac{q_i}{r_i}$$
The electric potential energy of a system of charges extends over all *pairs* of charges:
$$U = \frac{1}{4\pi\epsilon_0} \sum_{i < j} \frac{q_iq_j}{r_{ij}}$$

### b. [[Electric Potential Intro]]

Potential, denoted by $V$, is potential energy per unit charge. The potential difference between two points equals the amount of work per charge that would be required to move a positive test charge between those points. 
### c. [[Calculating Electric Potential]]

The potential $V$ due to a quantity of charge can be calculated by summing (if the charge is a collection of point charges) or by integrating (if the charge is a distribution).
$$V = \frac{1}{4\pi\epsilon_0} \frac{q}{r} \ \textrm{(due to a point charge)}$$
$$V = \frac{1}{4\pi\epsilon_0} \sum_i \frac{q_i}{r_i} \ \textrm{(due to a collection of point charges)}$$
$$V = \frac{1}{4\pi\epsilon_0} \int \frac{dq}{r} \ \textrm{(due to a charge distribution)}$$
The potential difference between two points $a$ and $b$ , also called the potential of $a$ with respect to $b$ , is given by the line integral of $\vec{E}$ . The potential at a give point can be found by first finding $\vec{E}$ and then carrying out this integral.
$$V_{ab} = V_a - V_b = \int^b_a \vec{E} \cdot d\vec{l} = \int^b_a E \cos{\phi} \ dl$$
![[Pasted image 20231204183022.png]]

### d. [[Equipotential Surfaces]]

An equipotential surface is a surface on which the potential has the same value at every point. At a point where a field line crosses an equipotential surface, the two are perpendicular. When all charges are at rest, the surface of a conductor is always an equipotential surface and all points in the interior of a conductor are at the same potential. When a cavity within a conductor contains no charge, the entire cavity is an equipotential region and there is no surface charge anywhere on the surface of the cavity.
![[Pasted image 20231204183241.png]]

### e. [[Potential Gradient]]

If the potential $V$ is a function of $x$, $y$, and $z$, the components of electric field $\vec{E}$ at any point are given by partial derivatives of $V$.
$$E_x = -\frac{\partial V}{\partial x} \ \ \ E_y = -\frac{\partial V}{\partial y} \ \ \ E_z = -\frac{\partial V}{\partial z}$$


---
# *References*