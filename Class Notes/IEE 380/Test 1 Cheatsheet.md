### Test 1 Cheat sheet

1. Define the Random Variable X, and figure out if it is discrete or continuous
	1. **Discrete**
		1. the $=$ matters: $P(X\ge3) = P(X > 2)$
		2. pmf represented by $p(x)$, denoted as $P(X=x)$.
		3. CDF(cumulative distributive function), all probabilities summed $F(x)=\sum_{Xmin}^x p(Xmin)+p(Xmin+1)\cdots p(x)$ denoted as $P(X \le x)$. **Requires** equals sign, see 2.
		4. $\mu=E(X) = \sum_x xf(x)$; $\sigma^2 = V(X) = E(X-\mu)^2 = E(X^2)-(E(X))^2$; $E[h(X)] = \sum_x h(x)f(x)$; $E(aX+b) = aE(X)+b$; $V(aX+b)=a^2V(X)$
	2. **Continuous**
		7. the $=$ doesn't matter: $P(X\ge3) = P(X>3)$
		8. pdf represented by $f(x)$, denoted as $P(X=x)$, which is always equal to $0$.
		9. CDF(cumulative distributive function), all probabilities summed $F(x)=\sum_{Xmin}^x f(Xmin)+\cdots f(x)$ denoted as $P(X \le x)$.  See 7.
		10. $P(a \le X \le b) = \int_a^b f(x)dx$; $F(x) = P(X \le x) = \int_{-\infty}^x f(u)du$; $E(X) = \int^\infty_{-\infty} xf(x)dx$; $V(X) = \int^\infty_{-\infty} x^2f(x)dx-\mu^2$
2. Sample Space: **Set of all possibilities/outcomes** of a random experiment.
	1. $S = \{x|x>0\}$; $S=\{x|1.5 < x < 5\}$; $S=\{low, medium, high\}$
	2. **Discrete** if outcomes are finite or countably infinite, **Continuous** if it contains an interval of real numbers.
3. Event: **Subset** of **Sample Space**
	1. *union* consists of all outcomes in either; *intersection* consists of all outcomes in both; *complement* consists of all outcomes outside of event but in sample space.
	2. **MUTUALLY EXCLUSIVE**: $E_1 \cap E_2 = \emptyset$      
4. Probability Distribution: description of the probabilities associated with the possible values of the random variable.
	1. **Discrete**: Map value to probability
	2. **Continuous**: Map range to probability function
5. Is it a named distribution?
	1. Discrete Uniform
		1. Finite \# of possible values with equal probability; $p(x_1)=p(x_2)...=p(x_n) = \frac{1}{n}$; $E(X) = \frac{b+a}{2}$; $V(X) = \frac{(b-a+1)^2-1}{12}$
	2. Poisson
		1. **Poisson Process**: consider subintervals of small length $\Delta t$ and assume as $\Delta t$ tends to zero:
			1. Probability of more than one event in a subinterval tends to zero.
			2. The probability of one event in a subinterval tends to $\lambda \Delta t$.
			3. The event in each subinterval is independent of other subintervals.
		2. $f(x) = \frac{e^{-\lambda T}(\lambda T)^x}{x!}$, $x = 0, 1, 2, \ldots$ ; countably infinite range; $E(X) = \lambda T$; $V(X) = \lambda T$
	3. Bernoulli trial
		1. Only 2 possible outcomes; trials are independent; probability of each outcome in each trial is constant. $E(X) = p$; $V(X) = p(1-p)$; finite range
	4. Binomial
		1. Consists of $n$ Bernoulli trials(See above for constraints); $p(x) = \binom{n}{x} p^x (1-p)^{n-x}$, $x = 0,1,\ldots ,n$; $E(X) = np$; $V(X) = np(1-p)$; finite range
	5. Continuous Uniform
		1. $f(x) = \frac{1}{b-a}, \ a \le x \le b$; $E(X) = \frac{a+b}{2}$; $V(X) = \frac{(b-a)^2}{12}$; $F(X) = \frac{x-a}{b-a}, \ a \le x < b$ 
	6. Standard Normal
		1. Normal w/ $\mu = 0$ and $\sigma^2=1$, denoted as $Z$
		2. $\frac{X-\mu}{\sigma} = Z$; $\frac{x-\mu}{\sigma} = z$(zscore); 
	7. Normal
		1. $f(x) = \frac{1}{\sqrt{2\pi}\sigma} e^\frac{-(x-\mu)^2}{2\sigma^2}$; $E(X) = \mu$; $
	8. Exponential
		1. $X$ equals **distance between successive events** from a Poisson process with mean number of events $\lambda$ per unit interval is an *exponential random variable*.
		2. $f(x) = \lambda e^{-\lambda x}$ for $0 \le x < \infty$; $E(X) = \frac{1}{\lambda}; V(X) = \frac{1}{\lambda^2}$
		3. Lack of Memory Property: $P(X < t_1 + t_2 | X>t_1) = P(X < t_2)$