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
If $v_{gs} << 2V_{OV}$, we can express $i_D$ as 
$$i_D \approx I_D+i_d$$
where
$$i_d = k_n (V_{GS}-V_t)v_{gs}$$

The parameter that relates $i_d$ and $v_{gs}$ is the MOSFET **transconductance** $g_m$:
$$g_m \equiv \frac{i_d}{v_{gs}} = k_nV_{OV}$$
#### The Voltage Gain

We can now express the total instantaneous drain voltage $v_{DS}$ as follows:
$$v_{DS} = V_{DS} - R_Di_d$$

Thus the signal component of the drain voltage is 
$$v_{ds} = -i_dR_D = -g_mv_{gs}R_D$$
which indicates that the voltage gain is given by
$$A_v \equiv \frac{v_{ds}}{v_{gs}} = -g_mR_D$$
#### Separating the DC Analysis and the Signal Analysis

We see that under the small-signal approximation, signal quantities are superimposed on dc quantities. It follows that we can greatly simplify the analysis and design by separating dc or bias calculations from small-signal calculations. **That is, once we have stablished a stable dc operating point and have calculated all dc quantities, we can perform signal analysis ignoring dc quantities.**

#### Small-Signal Equivalent-Circuit Models

From a signal point of view, the FET behaves as a voltage-controlled current source. It accepts a signal $v_{gs}$ between its gate and source and provides a current $g_mv_{gs}$ a the drain terminal. Both the input and output resistance have been assumed to be infinite. 

Putting this together, we arrive at the circuit below, which represents the small-signal operation of the MOSFET and is thus a **small-signal model** or a **small-signal equivalent circuit**.

![[Pasted image 20241115193849.png]]

(a) neglects the dependence of $i_D$ on $v_{DS}$, while (b) includes the effect of channel-length modulation, modeled by $r_o = \frac{|V_A|}{I_D}$, where $V_A = 1/\lambda$. 

It is important to note that the small-signal model parameters $g_m$ and $r_o$ depend on the dc bias point (Q) of the MOSFET.

![[Pasted image 20241115194516.png]]

Replacing the MOSFET with the small-signal model and eliminating the dc sources results in the circuit above, from which the following expression for the voltage gain can be found:
$$A_v = \frac{v_{ds}}{v_{gs}} = -g_m(R_D||r_o)$$
Thus, the finite output resistance $r_o$ reduces the magnitude of the voltage gain.

#### The Transconductance $g_m$

$$g_m=k_n'(W/L)V_{OV}$$
$$g_m = \sqrt{2k_n'} \sqrt{W/L} \sqrt{I_D}$$
1. For a given MOSFET, $g_m$ is proportional to the square root of the dc bias current
2. At a given bias current, $g_m$ is proportional to $\sqrt{W/L}$

In contrast, the transconductance of the BJT is proportional to the bias current and is independent of they physical size and geometry of the device. 
$$g_m = \frac{I_D}{(V_{OV}/2)}$$
## 7.3 Basic Configurations

### The Three Basic Configurations

![[Pasted image 20241122180747.png]]
![[Pasted image 20241122180755.png]]
![[Pasted image 20241122180801.png]]
![[Pasted image 20241122180811.png]]
![[Pasted image 20241122180819.png]]
![[Pasted image 20241122180827.png]]

### Characterizing Amplifiers

![[Pasted image 20241122181047.png]]

$$R_{in} \equiv \frac{v_i}{i_i}$$
$$v_i = \frac{R_{in}}{R_{in}+R_{sig}}v_{sig}$$
**open-circuit voltage gain:**
$$A_{vo} \equiv \frac{v_o}{v_i} \Bigr\rvert_{R_L = \infty}$$
$$R_o = \frac{v_x}{i_x}$$
**voltage gain of the amplifier proper:**
$$A_v \equiv \frac{v_o}{v_i} = A_{vo}\frac{R_L}{R_L+R_o}$$
**overall voltage gain:**
$$G_v = \frac{v_o}{v_{sig}} = \frac{R_{in}}{R_{in}+R_{sig}}A_{vo}\frac{R_
L}{R_L+R_o}$$
Sometimes it is more convenient to represent the amplifier output with a current output. This is the **short-circuit transconductance** of the amplifier:
$$G_m \equiv \frac{i_o}{v_i} \Bigr\rvert_{v_o=0}$$
$$A_{vo} \equiv G_mR_o$$






---
# *References*