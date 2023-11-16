202311150145
Meta Tags: #idea #textbook 
Tags: [[physics]]

# Magnetic Field and Magnetic Forces

## Introduction

## Summary

### a. [[Magnetism]]
### b. [[Magnetic Field]]

Magnetic interactions are between **moving** charged particles. These interactions are described by the vector magnetic field, denoted by $\vec{B}$ . A particle with charge $q$ moving with velocity $\vec{v}$ in a magnetic field $\vec{B}$ experiences a force $\vec{F}_B$ that is perpendicular to both $\vec{v}$ and $\vec{B}$ . The SI unit of magnetic field is the tesla ($1 T = 1 \frac{N}{A \cdot m}$).
$$\vec{F}_B = q\vec{v} \times \vec{B}$$
![[Pasted image 20231115015303.png]]
### c. [[Magnetic Field Lines and Magnetic Flux]]

A magnetic field can be represented graphically using **magnetic field lines**. At each point, a magnetic field line is tangent to the direction of $\vec{B}$ at that point. Closer means stronger fields, and vice versa.

Magnetic flux $\Phi_B$ through an area is defined similar to electric flux; its SI unit is the weber ($1 Wb = 1 T \cdot m^2$).
$$\Phi_B = \int B \cos{\phi} \ dA = \int B_\perp \ dA = \int \vec{B} \cdot d\vec{A}$$
The net magnetic flux through any closed surface is zero (Gauss's law for magnetism), so magnetic field lines always close on themselves.
$$\oint \vec{B} \cdot d\vec{A} = 0 \ \textrm{(closed surface)}$$
![[Pasted image 20231115020256.png]]


### d. [[Motion of Charged Particles in a Magnetic Field]]

The magnetic force is always perpendicular to $\vec{v}$ ; a particle moving under the action of a magnetic field along moves with constant speed.

In a uniform field, a particle with initial velocity perpendicular to the field moves in a circle with radius $R$ that depends on the magnetic field strength $B$ and the particle mass $m$, speed $v$, and charge $q$.
$$R=\frac{mv}{|q|B}$$
![[Pasted image 20231115021604.png]]


### e. [[Applications of Motion of Charged Particles]]

Crossed electric and magnetic fields can be used as a velocity selector. The electric and magnetic forces exactly cancel when $v = E/B$ . 
![[Pasted image 20231115021837.png]]


### f. [[Magnetic Force on a Current-Carrying Conductor]]

A straight segment of a conductor carrying current $I$ in a uniform magnetic field $\vec{B}$ experiences a force $\vec{F}$ that is perpendicular to both $\vec{B}$ and the vector $\vec{l}$ , which points in the direction of the current and has magnitude equal to the length of the segment. 
$$\vec{F} = I \vec{l} \times \vec{B}$$
A similar relationship gives the force $d\vec{F}$ on an infinitesimal current-carrying segment $d\vec{l}$ .
$$d\vec{F} = I \ d\vec{l} \times \vec{B}$$
![[Pasted image 20231115022150.png]]


### g. [[Force and Torque on a Current Loop]]

A current loop with area $A$ and current $I$ in a uniform magnetic field $\vec{B}$ experiences no net magnetic force, but does experience a magnetic torque of magnitude $\tau$ . 
$$\tau = IBA \sin \phi$$
The vector torque $\vec{\tau}$ can be expressed in terms of the magnetic moment $\vec{\mu} = I\vec{A}$ of the loop, as can the potential energy $U$ of a magnetic moment in a magnetic field $\vec{B}$ . 
$$\vec{\tau} = \vec{\mu} \times \vec{B}$$
$$U = -\vec{\mu} \cdot \vec{B} = -\mu B \cos \phi$$


### h. [[The Direct-Current Motor]]

In a DC motor, a magnetic field exerts a torque on a current in the rotor. Motion of the rotor through the magnetic field causes an induced emf called a *back emf*. For a series motor, in which the rotor coil is in series with coils that produce the magnetic field, the terminal voltage is the sum of the back emf and the potential drop $Ir$ across the internal resistance.

![[Pasted image 20231115022857.png]]
### i. [[The Hall Effect]]

The Hall effect is a potential difference perpendicular to the direction of current in a conductor, when the conductor is placed in a magnetic field. 

![[Pasted image 20231115023222.png]]

The Hall potential is determined by the requirement that the associated electric field must just balance the magnetic force on a moving charge. Hall-effect measurements can be used to determine the sign of charge carriers and their concentration $n$.
$$nq = \frac{-J_xB_y}{E_z}$$


---
# *References*