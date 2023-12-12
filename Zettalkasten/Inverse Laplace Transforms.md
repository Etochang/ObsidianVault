202312052206
Meta Tags: #textbook 
Tags: [[mathematics]] [[differential equation]]

# Inverse Laplace Transforms

Finding the Laplace transform of a function is not terribly difficult if we’ve got a table of transforms in front of us to use as we saw in the last [section](https://tutorial.math.lamar.edu/Classes/DE/LaplaceTransforms.aspx). What we would like to do now is go the other way.

We are going to be give a transform, $F(s)$, and ask what function (or functions) did we have originally. In these cases, we say that we are finding the **Inverse Laplace Transform** of $F(s)$ and use the following notation:
$$f(t) = \mathcal{L}^{-1}\{F(s)\}$$
As with Laplace transforms, we’ve got the following fact to help us take the inverse transform.

>[!info]
>Given the two Laplace transforms $F(s)$ and $G(s)$, then
>$$\mathcal{L}^{-1}\{aF(s)+bG(s)\} = a\mathcal{L}^{-1}\{F(s)\} + b\mathcal{L}^{-1}\{G(s)\}$$
>for any constants $a$ and $b$.

So, we take the inverse transform of the individual transforms, put any constants back in and then add or subtract the results back up.







---
# *References*