202311141801
Meta Tags: #textbook
Tags: [[physics]]

# Resistance and Reactance

## Introduction

We will derive **voltage-current relationships** for:

- resistors
- inductors
- capacitors

carrying a **sinusoidal current**.

## Resistor in an AC Circuit

First, let's consider a resistor R with a sinusoidal current given by
$$i = I\cos(\omega t)$$
The positive direction of this current is counterclockwise around this circuit:

---

![[Pasted image 20231115013504.png]]

---

The current amplitude (max current) is $I$. From Ohm's law, the instantaneous potential $v_R$ of point $a$ with respect to point $b$ (the instantaneous voltage across the resistor) is
$$v_R = iR = (IR) \cos(\omega t)$$
The maximum value of the voltage is $V_R$ , the *voltage amplitude*:
$$V_R = IR$$
We can hence write
$$v_R = V_R \cos (\omega t)$$
Both the current $i$ and the voltage $v_R$ are proportional to $\cos (\omega t)$, so the current is ***in phase*** with the voltage. We can also see that the current and voltage amplitudes are related in the same way as in a DC circuit.

```ad-seealso
![[Pasted image 20231115013517.png]]
Graphs of $i$ and $v_R$ as functions of time. The vertical scales for current and voltage are different, so the relative heights of the two curves are not significant. The corresponding phasor diagram is:
![[Pasted image 20231115013530.png]]
Since $i$ and $v_R$ are *in phase* and have the same frequency, the current and voltage phasors rotate together; they are parallel at each instant. Their projections on the horizontal axis represent the instantaneous current and voltage, respectively.
```

## Inductor in an AC Circuit

Now we replace the resistor with a pure inductor with self-inductance $L$ and zero resistance:

---

![[Pasted image 20231115013541.png]]

---

The current is still $i = I \cos (\omega t)$, and the positive direction of current is still ccw. Although there is no resistance, there is a potential difference $v_L$ between the inductor terminals $a$ and $b$ because the current varies with time, giving rise to a self-induced emf. The induced emf in the direction of $i$ is given by $\mathcal{E} = -L \frac{di}{dt}$; however, the voltage $v_L$ is not simply equal to $\mathcal{E}$. Notice that if the current in the inductor is in the positive and the induced emf is directed to the left to oppose the increase in current, point $a$ is at a higher potential than point $b$. Thus, $v_L = L \frac{di}{dt}$, the *negative* of induced emf.

$$v_L = L \frac{di}{dt} = L \frac{d}{dt} (I \cos(\omega t)) = -I\omega L \sin (\omega t)$$

The voltage $v_L$ across the inductor is proportional to the *rate of change* of the current. The points of maximum voltage on the graph correspond to the maximum steepness of the current curve, and the points of zero voltage are the points where the current curve has its maximum and minimum values:

![[Pasted image 20231115013546.png]]

The voltage and current are *out of phase* by a quarter-cycle. Since the voltage peaks occur a quarter-cycle earlier than the current peaks, we say that the voltage *leads* the current by $\pi/2$. The phasor diagram also shows this:

![[Pasted image 20231115013551.png]]

We can also conclude this with the identity $\cos (A + \pi/2) = -\sin (A)$:
$$v_L = I \omega L \cos (\omega t + \pi/2)$$
```ad-important
We'll usually describe the phase of the *voltage* relative to the *current*, not the reverse. Thus, if the current $i$ in a circuit is
$$i = I \cos (\omega t)$$
and the voltage $v$ of one point with respect to another is
$$v = V \cos (\omega t + \phi)$$
we call $\phi$ the **phase angle**; it gives the phase of the *voltage* relative to the *current*. For a pure resistor, $\phi = 0$, and for a pure inductor, $\phi = \pi/2$. 
```

The amplitude $V_L$ of the inductor voltage is $I \omega L$. We define the **inductive reactance** $X_L$ of an inductor as $X_L = \omega L$. Using this, we can write a similar equation for the voltage amplitude as the one for a resistor:
$$ V_L = I X_L$$
The unit for $X_L$ is the $\ohm$.

```ad-warning
**Inductor voltage and current are NOT IN PHASE!**

The equation above relates the *amplitudes* of the oscillating voltage and current.
```

## The Meaning of Inductive Reactance


---
# *References*

ASU PHY 131 Pearson