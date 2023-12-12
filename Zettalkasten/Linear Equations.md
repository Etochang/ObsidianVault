202312052122
Meta Tags: #textbook 
Tags: [[mathematics]] [[differential equation]]

# Linear Equations

In order to solve a linear first order de, we MUST start with the de in the form shown below:
$$\frac{dy}{dt} + p(t)y = g(t)$$
Where both $p(t)$ and $g(t)$ are **continuous** functions.

Now, we are going to assume that there is some magical function somewhere out there in the world, $\mu(t)$, called an **integrating factor**. Assuming the existence of $\mu(t)$, multiply everything in the de by it.
$$\mu(t) \frac{dy}{dt} + \mu(t)p(t)y = \mu(t)g(t)$$
Now, assume that whatever $\mu(t)$ is, it will satisfy the following:
$$\mu(t)p(t) = \mu'(t)$$
Substituting this into the de, we now arrive at
$$\mu(t) \frac{dy}{dt} + \mu'(t)y = \mu(t)g(t)$$
Using the product rule, we get
$$(\mu(t)y(t))' = \mu(t)g(t)$$
Integrating both sides, we get
$$\mu(t)y(t)+c_1 = \int\mu(t)g(t) \ dt$$
Solving for $y(t)$, we get
$$y(t) = \frac{\int \mu(t)g(t) \ dt 
+ c}{\mu(t)}, c = -c_1$$
To determine what $\mu(t)$ is, we go back to the assumption that
$$\mu(t)p(t) = \mu'(t)$$
and rearrange it to
$$\frac{\mu'(t)}{\mu(t)} = p(t),$$
which becomes
$$(\ln{\mu(t)})' = p(t).$$
Integrating both sides will get
$$\ln{\mu(t)}+k_1 = \int p(t) \ dt$$
$$\ln{\mu(t)} = \int p(t) \ dt + k, k = -k_1$$
From logarithmic rules,
$$\mu(t) = e^{\int p(t) \ dt + k}.$$


---
# *References*