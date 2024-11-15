202411141824
Meta Tags: #textbook 
Tags: [[circuits]]

# CH 7

## 7.1 Basic Principles

### 7.1.1. The Basis for Amplifier Operation

>When we operate a transistor in the active region, we create a voltage-controlled current source.

For a MOSFET, this is the saturation/pinch-off region, where the voltage between gate and source, $v_{GS}$, controls the drain current $i_D$:
$$i_D = \frac{1}{2} k_n (v_{GS} - V_{tn})^2$$
For a BJT, this is the active region, where the base-emitter voltage $v_{BE}$ controls the collector current $i_C$ :
$$i_C = I_S e^{v_{BE}/V_T}$$

![[Pasted image 20241114184316.png]]

In the MOSFET model, $i_D$ doesn't depend on $v_{DS}$ because the channel is pinched off, "isolating" the drain ($v_{GD} \le V_{tn}$). Similarly, in the BJT model, $i_C$ doesn't depend on $v_{CE}$ because the CBJ is reverse-biased, thus "isolating" the connector ($v_{BC} \le 0.4$).




---
# *References*