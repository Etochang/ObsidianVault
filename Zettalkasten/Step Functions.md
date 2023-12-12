202312052219
Meta Tags: #textbook 
Tags: [[mathematics]] [[differential equation]]

# Step Functions

Before proceeding into solving differential equations, we should take a look at one more function. Without Laplace transforms, it would be much more difficult to solve differential equations that involve this function in $g(t)$.

The function is the Heaviside function and is defined as,
$$
u_c(t) = \begin{cases}
	0 & \textrm{if} \ \ t < c \\
	1 & \textrm{if} \ \ t \geq c
\end{cases}
$$
Here is a graph of the Heaviside function.
![[Pasted image 20231205222529.png]]

Heaviside functions are often called step functions. Here is some alternate notation for Heaviside functions.
$$u_c(t) = u(t-c) = H(t-c)$$
We can think of the Heaviside function as a switch that is off until $t=c$ at which point it turns on and takes a value of 1. So, what if we want a switch that will turn on and takes some other value, say 4, or -7?

Heaviside functions can only take values of 0 or 1, but we can use them to get other kinds of switches. For instance, $4u_c(t)$ is a switch that is off until $t=c$ and then turns on and takes a value of 4. Likewise, $-7u_c(t)$ will be a switch that will take a value of -7 when it turns on.

Now, suppose that we want a switch that is on (with a value of 1) and then turns off at $t=c$. We can use Heaviside functions to represent this as well. The following function will exhibit this kind of behavior.
$$1-u_c(t) = \begin{cases}
	1-0=1 & \textrm{if} \ t < c \\
	1-1=0 & \textrm{if} \ t \geq c
\end{cases}
$$
All of this is fine, but if we continue the idea of using Heaviside function to represent switches, we really need to acknowledge that most switches will not turn on and take constant values. Most switches will turn on and vary continually with the value of _t._

So, let’s consider the following function.
![[Pasted image 20231205222924.png]]

We would like a switch that is off until $t=c$ and then turns on and takes the values above. By this we mean that when $t=c$ we want the switch to turn on and take the value of $f(0)$ and when $t=c+4$ we want the switch to turn on and take the value of $f(4)$, _etc._ In other words, we want the switch to look like the following,
![[Pasted image 20231205223018.png]]
Notice that in order to take the values that we want the switch to take it needs to turn on and take the values of $f(t-c)$! We can use Heaviside functions to help us represent this switch as well. Using Heaviside functions this switch can be written as
$$g(t) = u_c(t)f(t-c)$$
Okay, we’ve talked a lot about Heaviside functions to this point, but we haven’t even touched on Laplace transforms yet. So, let’s start thinking about that.

Let's determine the Laplace transform of 
$$g(t) = u_c(t)f(t-c)$$
by plugging into the [[The Definition - Laplace Transforms|definition]] of the Laplace transform: 








$$\mathcal{L}\{u_c(t)f(t-c)\} = e^{-cs}F(s)$$
$$\mathcal{L}\{u_c(t)\} = \frac{e^{-cs}}{s} \ \ \ \ \ \mathcal{L}^{-1}\{\frac{e^{-cs}}{s}\} = u_c(t)$$



---
# *References*