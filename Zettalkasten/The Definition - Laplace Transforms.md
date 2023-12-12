202312052139
Meta Tags: #textbook 
Tags: [[mathematics]] [[differential equation]]

# The Definition - Laplace Transforms

You know, it’s always a little scary when we devote a whole section just to the definition of something. Laplace transforms (or just transforms) can seem scary when we first start looking at them. However, as we will see, they aren’t as bad as they may appear at first.

Before we start with the definition of the Laplace transform we need to get another definition out of the way.

## Piecewise Continuous Functions

A function is called **piecewise continuous** on an interval if the interval can be broken into a finite number of subintervals on which the function is continuous on each open subinterval and has a finite limit at the endpoints of each subinterval. 
![[Pasted image 20231205214050.png]]

In other words, a piecewise continuous function is a function that has a finite number of breaks in it and doesn’t blow up to infinity anywhere.

## Definition of the Laplace Transform

>[!info] Definition
>Suppose that $f(t)$ is a piecewise continuous function. The Laplace transform of $f(t)$ is denoted $\mathcal{L}\{f(t)\}$ and defined as
>$$\mathcal{L}\{f(t)\} = \int^\infty_0 e^{-st}f(t) \ dt$$

For the sake of convenience, we will often denote Laplace transforms as
$$\mathcal{L}\{f(t)\} = F(s)$$
>[!note]
>Note that the transform is acutally a function of a new variable, $s$, and that all the $t$'s will drop out in the integration process.







---
# *References*