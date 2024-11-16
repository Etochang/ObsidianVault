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

In the MOSFET model, $i_D$ doesn't depend on $v_{DS}$ because the channel is pinched off, "isolating" the drain ($v_{GD} \le V_{tn}$ | $v_{DS} \ge v_{OV}$). Similarly, in the BJT model, $i_C$ doesn't depend on $v_{CE}$ because the CBJ is reverse-biased, thus "isolating" the connector ($v_{BC} \le 0.4$ | $v_{CE} \ge 0.3$).

### 7.1.2 Obtaining a Voltage Amplifier

We see from above that the transistor is basically a **transconductance amplifier**: that is, an amplifier with an input voltage and output current. 

A simple way to convert a transconductance amplifier to a voltage amplifier is to pass the output current through a resistor and take the voltage across the resistor as the output.

![[Pasted image 20241114191946.png]]

In the figures above, the output voltage is taken between the drain/collector and ground instead of across the load resistor because a **common ground reference** is needed between the input and output signals. 
$$v_{DS} = V_{DD} - i_DR_D$$
$$v_{CE} = V_{CC}-i_CR_C$$

### 7.1.3 The Voltage-Transfer Characteristic (VTC)

The VTC is simply a plot of the output voltage versus the input voltage. 

![[Pasted image 20241114191946.png]]

The segment of greatest slope (hence potentially largest amplifier gain) is AB, which corresponds to operation in the active region. **To use a transistor as an amplifier, we confine its operating point to the segment AB**. 

The coordinates of B for MOSFET are:
$$V_{GS} \Bigr\rvert_B = V_t + \frac{\sqrt{2k_nR_DV_{DD}+1}-1}{k_nR_D}$$
$$V_{DS}\Bigr\rvert_B = V_{OV}\Bigr\rvert_B \equiv \frac{\sqrt{2k_nR_DV_{DD}+1}-1}{k_nR_D}$$
For BJT:
$$V_{BE} \Bigr\rvert_B = 0.7 V$$
$$V_{CE} \Bigr\rvert_B = 0.3 V$$

### 7.1.4 Obtaining Linear Amplification by Biasing the Transistor

Biasing enables us to obtain almost-linear amplification from the MOSFET and the BJT. 

We select a dc input voltage $V_{GS}$ or $V_{BE}$ to obtain operation at a point Q on the segment AB of the VTC. Point Q is known as the **bias point** or the **dc operating point**. It is also known as the **quiescent point**.

Next, the signal to be amplified, $v_{gs}$ or $v_{be}$, a function of time $t$, is superimposed on the bias voltage, and the resulting $v_{DS}(t)$ or $v_{BE}(t)$ can be obtained using the active region VTC equations.

![[Pasted image 20241114194843.png]]

The amplitude of $v_{gs}$ is small enough to restrict the excursion from Q to a short, almost-linear segment. The shorter the segment, the greater the linearity achieved.

>[!warning] increasing the amplitude of the input signal
>As the instantaneous operating point is no longer confined to the almost-linear segment of the VTC, $v_{ds}$ loses linearity. 
>
>If the input signal amplitude becomes sufficiently large, the instantaneous operating point may leave AB altogether. If this happens at the negative peaks of $v_{gs}$, the transistor will cut off the positive peaks of $v_{ds}$. If this happens at the positive peaks of $v_{gs}$, the transistor will enter the triode region and flatten the negative peaks of $v_{ds}$. 
>
>The maximum allowable amplitude of $v_{ds}$, referred to as the *allowable signal swing at the output*, is greatly affected by the location of the bias point Q.
>
>For a BJT, the same logic follows.

### 7.1.5 The Small-Signal Voltage Gain

#### The MOSFET Case

![[Pasted image 20241115174021.png]]

If the input signal $v_{gs}$ is kept small, $v_{ds}$ will be nearly proportional to it. The constant of proportionality will be the slope of the almost-linear segment of the VTC around Q, which is also the **voltage gain of the amplifier**:
$$A_v = \frac{dv_{DS}}{dv_{GS}} \Bigr\rvert_{v_{GS}=V_{GS}}$$
$$A_v = -k_n(V_{GS}-V_t)R_D$$
$$A_v=-k_nV_{OV}R_D$$
$$A_v = -\frac{I_DR_D}{V_{OV}/2}$$
$$A_v=-\frac{V_{DD}-V_{DS}}{V_{OV}/2}$$
1. The gain is negative, which means the amplifier is inverting (180° phase shift between input and output)
2. The gain is proportional to the load resistance $R_D$, the transistor transconductance parameter $k_n$, and the overdrive voltage $V_{OV}$

The maximum gain magnitude $|A_{vmax}|$ is obtained by biasing the transistor at point B. To maximize the gain, the bias point Q should be as close to point B as possible, consistent with the required signal swing at the output.

#### The BJT Case

$$A_v = \frac{dv_{CE}}{dv_{BE}} \Bigr\rvert_{v_{BE}=V_{BE}}$$
$$A_v = -(\frac{I_C}{V_T})R_C$$
$$A_v=-\frac{V_{CC}-V_{CE}}{V_T}$$

1. The gain is negative, which means the amplifier is inverting (180° phase shift between input and output)
2. The gain is proportional to the collector bias current $I_C$ and to the load resistance $R_C$

The maximum gain is achieved when $V_{CE}$ is about 0.3V. 

## 7.2 Small-Signal Operation and Models

### 7.2.1 The MOSFET Case

![[Pasted image 20241115183037.png]]

#### The DC Bias Point

We can find the DC bias current $I_D$ by setting the signal $v_{gs}$ to zero:
$$I_D= \frac{1}{2}k_nV_{OV}^2$$
To ensure saturation-region operation, we must have $$V_{DS} > V_{OV}$$
#### The Signal Current in the Drain Terminal

The total instantaneous gate-to-source voltage will be:
$$v_{GS} = V_{GS}+v_{gs}$$
resulting in a total instantaneous drain current:
$$i_D=\frac{1}{2} k_n(V_{GS}+v_{gs}-V_t)^2$$






---
# *References*