202312052046
Meta Tags: #textbook 
Tags: [[mathematics]] [[differential equation]]

# Definitions

## Order

The **order** of a differential equation is the largest derivative present in the differential equation. 

>[!example] A fourth order differential equation
>$$y^{(4)} + 10y'''-4y'+2y=\cos{(t)}$$

## Ordinary and Partial Differential Equations

A differential equation is called an **ordinary differential equation** (ode) if it has ordinary derivatives in it. Likewise, a differential equation is called a **partial differential equation** (pde) if it has partial derivatives in it.

## Linear Differential Equations

A **linear differential equation** is any differential equation that can be written in the following form:
$$a_n(t)y^{(n)}(t)+a_{n-1}(t)y^{(n-1)}(t)+\cdots+a_0(t)y(t)=g(t)$$
If a differential equation cannot be written in the form, then it is called a **non-linear** differential equation.

## Solution

A **solution** to a differential equation on an interval $\alpha < t < \beta$ is any function $y(t)$ which satisfies the differential equation in question on the interval $\alpha < t < \beta$ . 

>[!important]
>Solutions are often accompanied by intervals and these intervals can impart important information about the solution. Consider the following example:
>>[!example]
>>Show that $y(x) = x^{-\frac{3}{2}}$ is a solution to $4x^2y'' + 12xy' + 3y = 0$ for $x > 0$.
>
>First, find the first and second derivative:
>$$y'(x) = -\frac{3}{2} x^{-\frac{5}{2}} \ \ \ \ y''(x) = \frac{15}{4} x^{-\frac{7}{2}}$$
>If you plug these into the differential equation, you will find that the given solution is indeed a solution. So why did we include the condition that $x > 0$?
>
>Recall that 
>$$y(x) = x^{-3\frac{3}{2}} = \frac{1}{\sqrt{x^3}}$$
>In this form, it is clear that we'll need to avoid $x = 0$.

As shown in the example, even if a function may symbolically satisfy a differential equation, certain restrictions brought about by the solution may cause us to not be able to use all values of the independent variable and hence, we must make a restriction on the independent variable.

## Initial Conditions

**Initial conditions** are a condition, or set of conditions, on the solution that will allow us to determine which solution that we are after. Initial conditions are of the form,
$$
y(t_0) = y_0 \ \ \ \textrm{and/or} \ \ \ y^{(k)}(t_0) = y_k
$$

## Initial Value Problem

An **Initial Value Problem** (or IVP) is a differential equation along with an appropriate number of initial conditions.

## Interval of Validity

The **interval of validity** for an IVP with initial condition(s)
$$
y(t_0) = y_0 \ \ \ \textrm{and/or} \ \ \ y^{(k)}(t_0) = y_k
$$
is the largest possible interval on which the solution is valid and contains $t_0$.

## General Solution

The **general solution** to a differential equation is the most general form that the solution can take and doesn't take any initial condition into account.

## Actual Solution

The **actual solution** to a differential equation is the specific solution that not only satisfies the differential equation, but also satisfies the given initial condition(s).

## Implicit/Explicit Solution

An **explicit solution** is any solution that is given in the form $y = y(t)$. In other words, the only place that $y$ actually shows up is once on the left side and only raised to the first power. An **implicit solution** is any solution that isn't in explicit form.






---
# *References*