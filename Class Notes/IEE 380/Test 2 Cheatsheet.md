##### Test 2 Cheat sheet

### CHECK WHETHER POPULATION STDEV IS STATED, IF NOT, USE SAMPLE STDEV

**Equations:** 
1. Discrete Uniform
	1. Finite \# of possible values with equal probability; $p(x_1)=p(x_2)...=p(x_n) = \frac{1}{n}$; $E(X) = \frac{b+a}{2}$; $V(X) = \frac{(b-a+1)^2-1}{12}$
2. Continuous Uniform
	1. $f(x) = \frac{1}{b-a}, \ a \le x \le b$; $E(X) = \frac{a+b}{2}$; $V(X) = \frac{(b-a)^2}{12}$; $F(X) = \frac{x-a}{b-a}, \ a \le x < b$ 

**6.1:** Sample variance - $\frac{\sum^n_{i=1}(x_i-\bar{x})^2}{n-1}$=$\frac{\sum^n_{i=1} x_i^2 -\frac{(\sum^n_{i=1}x_i)^2}{n}}{n-1}$ - n is sample size.

**6.3:** Histogram - \# of bins = $\sqrt{n}$, 
Lskew-slope down left
Rskew-slope down right. $\text{Rectangle height} = \frac{\text{Bin frequency}}{\text{Bin width}}$. 
Range/\# of bins = bin width. $L \le x < U$. 

**7.1:** *statistic*-function of r-variables; 
*sampling distribution*-probability distribution of statistic 
$\theta$-population parameter of interest, can represent $\mu$ or $\sigma^2$, etc.
If $X$ is a random variable w/ parameter $\theta$, and $\{X_1, X_2, \ldots, X_n\}$ is a random sample of size $n$ from $X$, the statistic $\hat{\Theta} = h(X_1, X_2, \ldots, X_n)$ is a **point estimator** of $\theta$. 

**7.2:** If $\{X_1, X_2, \ldots, X_n\}$ are independent random variables and every $X_i$ has the same probability distribution, the sample is random. If mean $\mu$, variance $\sigma^2$ and sample mean $\overline{X}$, $\frac{\overline{X}_1 -\overline{X}_2 -(\mu_1-\mu_2)}{\sqrt{\sigma_1^2 / n_1 + \sigma_2^2 / n_2}} = \frac{\overline{X} -\mu}{\sigma / \sqrt{n}} = Z$ as $n \rightarrow \infty$.  

**8.1:** $P\{L \le \mu \le U\} = 1 - \alpha \equiv P\{-z_{\alpha/2} \le \frac{\overline{X} -\mu}{\sigma / \sqrt{n}} \le z_{\alpha/2}\} = 1 - \alpha$
$P\{ \overline{X} - z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \le \mu \le \overline{X} + z_{\alpha/2} \frac{\sigma}{\sqrt{n}} \} = 1 - \alpha$; $n = (\frac{z_{\alpha/2}\sigma}{E})^2$
upper: $\mu \le \overline{X} + z_{\alpha} \frac{\sigma}{\sqrt{n}}$; lower: $\overline{X} - z_{\alpha} \frac{\sigma}{\sqrt{n}} \le \mu$
$n > 40 \rightarrow \overline{X} - z_{\alpha/2} \frac{s}{\sqrt{n}} \le \mu \le \overline{X} + z_{\alpha/2} \frac{s}{\sqrt{n}}$
$z_\alpha$: values of z on the z-axis such that the area above it is equal to $\alpha$. 

**8.2:** **TI ALWAYS DOES CDF**; replace $z_\alpha$ with $t_{\alpha, n-1}$ in all equations for 8.1.
$t_{\alpha, n-1}$: value of t on the t-axis s.t. the area above it is equal to $\alpha$ with $n-1$ degrees of freedom.  

**8.3:** mean $\mu$ variance $\sigma^2$ and sample variance $s^2$, $X^2= \frac{(n-1)s^2}{\sigma^2}$ has a $\chi^2$ distribution with $n-1$ degrees of freedom. 
mean: dof, variance 2\*dof. $P(X^2 > \chi^2_{a,n-1}) = \alpha$. $P(\frac{(n-1)s^2}{\chi^2_{\alpha/2,n-1}} \le \sigma^2 \le \frac{(n-1)s^2}{\chi^2_{1-\alpha/2,n-1}}) = 1 - \alpha$. 

**8.4:** $Z = \frac{X-np}{\sqrt{np(1-p)}}=\frac{\hat{P}-p}{\sqrt{\frac{p(1-p)}{n}}}$
$\hat{p} - z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}} \le p \le \hat{p} + z_{\alpha/2}\sqrt{\frac{\hat{p}(1-\hat{p})}{n}}$ for 100(1-a)% confidence interval. 
**Sample size:** $n = (\frac{z_{\alpha/2}}{E})^2p(1-p)$; **No estimation:** $(\frac{z_{\alpha/2}}{E})^2 0.25$; 

**Ch. 9**

### ALWAYS DO THE TEST

| Case | Null Hypothesis                       | Test Statistic                                | Alternative Hypothesis          | Fixed Significance Level Criteria for Rejection                              | P-Value                                                                                      |
| ---- | ------------------------------------- | --------------------------------------------- | ------------------------------- | ---------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| 1.   | $H_0: \mu = \mu_0$ $\sigma^2$ known   | $z_0 = \frac{\bar{x}-\mu_0}{\sigma/\sqrt{n}}$ | $H_1: \mu \neq \mu_0$           | $\|z_0\| > z_{\alpha/2}$                                                     | $P=2[1-\Phi(z_0)]$                                                                           |
|      |                                       |                                               | $H_1: \mu > \mu_0$              | $z_0 > z_{\alpha}$                                                           | $1-\Phi(z_0)$                                                                                |
|      |                                       |                                               | $H_1: \mu < \mu_0$              | $z_0 < -z_{\alpha}$                                                          | $\Phi(z_0)$                                                                                  |
| 2.   | $H_0: \mu = \mu_0$ $\sigma^2$ unknown | $t_0 = \frac{\bar{x}-\mu_0}{s/\sqrt{n}}$      | $H_1: \mu \neq \mu_0$           | $\|t_0\| > t_{\alpha/2, n-1}$                                                | Probability above $\|t_0\|$ and below $-\|t_0\|$                                             |
|      |                                       |                                               | $H_1: \mu > \mu_0$              | $t_0 > t_{\alpha, n-1}$                                                      | Probability above $t_0$                                                                      |
|      |                                       |                                               | $H_1: \mu < \mu_0$              | $t_0 < t_{\alpha, n-1}$                                                      | Probability below $t_0$                                                                      |
| 3.   | $H_0: p = p_0$                        | $z_0 = \frac{x-np_0}{\sqrt{np_0(1-p_0)}}$     | $H_1: p \neq p_0$               | $\|z_0\| > z_{\alpha/2}$                                                     | $P=2[1-\Phi(z_0)]$                                                                           |
|      |                                       |                                               | $H_1: p > p_0$                  | $z_0 > z_{\alpha}$                                                           | $1-\Phi(z_0)$                                                                                |
|      |                                       |                                               | $H_1: p < p_0$                  | $z_0 < -z_{\alpha}$                                                          | $\Phi(z_0)$                                                                                  |
| 4.   | $H_0: \sigma^2 = \sigma^2_0$          | $x_0^2=\frac{(n-1)s^2}{\sigma^2_0}$           | $H_1: \sigma^2 \neq \sigma^2_0$ | $\chi^2_0 > \chi^2_{\alpha/2, n-1}$ or $\chi^2_0 < \chi^2_{1-\alpha/2, n-1}$ | Interval of $\chi^2$ values that surrounds $\chi^2_0$ with same dof.                         |
|      |                                       |                                               | $H_1: \sigma^2 > \sigma^2_0$    | $\chi^2_0 > \chi^2_{\alpha, n-1}$                                            | Interval of $\chi^2$ values that surrounds $\chi^2_0$ with same dof, complement if less than |
|      |                                       |                                               | $H_1: \sigma^2 < \sigma^2_0$    | $\chi^2_0 < \chi^2_{1-\alpha, n-1}$                                          | same as above but greater than                                                               |

**9.1:** $P(\text{rejecting H0 when it is true}) = \alpha =$ type I error. $P(\text{failing to reject H0 when it is false}) = \beta =$ type II error.  Power = $1-\beta$

**Mean known, variance known:** $\beta = \Phi(z_{\alpha/2} - \frac{\delta \sqrt{n}}{\sigma}) - \Phi(-z_{\alpha/2} - \frac{\delta \sqrt{n}}{\sigma})$, $\delta = \mu - \mu_0$, 
two sided: $n = \frac{(z_{\alpha/2}+z_\beta)^2\sigma^2}{\delta^2}$ one sided: $n = \frac{(z_{\alpha}+z_\beta)^2\sigma^2}{\delta^2}$ 

**Population proportion:**
**two-sided:** $\beta = \Phi(\frac{p_0-p+z_{\alpha/2}\sqrt{p_0(1-p_0)/n}}{\sqrt{p(1-p)/n}})- \Phi(\frac{p_0-p-z_{\alpha/2}\sqrt{p_0(1-p_0)/n}}{\sqrt{p(1-p)/n}})$ 
$H_0:p<p_0$: $\beta = 1 - \Phi(\frac{p_0-p-z_{\alpha}\sqrt{p_0(1-p_0)/n}}{\sqrt{p(1-p)/n}})$
$H_0:p>p_0$: $\beta = \Phi(\frac{p_0-p+z_{\alpha}\sqrt{p_0(1-p_0)/n}}{\sqrt{p(1-p)/n}})$
**two-sided:** $n = [\frac{z_{\alpha/2}\sqrt{p_0(1-p_0)}+z_\beta \sqrt{p(1-p)}}{p-p_0}]^2$; one-sided: $n = [\frac{z_{\alpha}\sqrt{p_0(1-p_0)}+z_\beta \sqrt{p(1-p)}}{p-p_0}]^2$

