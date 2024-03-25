202401190920
Meta Tags: #homework
Tags: [[CSE 310]] [[asymptotic notation]] [[time complexity]]

# Homework 1

*Designed by Yiran "Lawrence" Luo, CSE 310 Spring 2024*

- **Type:** Individual. Everyone turns in their own work. No group work is allowed.
- **Synopsis:** Utilizing the time complexity formulae on the introduced concepts: divide-and-conquer, heap, and etc.
- **Keywords:** Big-O, Big-Theta, Big-Omega, Asymptotic Notations
- **Format requirements:** You may either type in your solutions or write them down on paper. You are more than welcome to use Latex for better equation formatting. For those who write on paper, you will need to photo-scan your answer sheets and upload them to Canvas in a single composite PDF file. You DO NOT need to duplicate the question texts while answering. Simply use notations like Part 1A, or Part 3B to refer to each question in your answer sheet.
- **Acceptable deliverable formats:** PDF (preferred), or MS Word DOCX. For Pages users please convert your work into PDF. 
- Deadline: **Tuesday Jan 23rd** at 2359 hours, after which late submissions will not be accepted. We also will not accept your late submission on paper in class.

## PART 1 - Observing the loops

*Find the **Big-ϴ** notations for the following pseudocode snippets with regard to n (the size of data). Please note, you must show us how to find both the **upper bound** and the **lower bound**, or you will get zero points. You may also use the l'Hopital's trick for your convenience.*

### A.

```
// Assuming n is always larger than 10
for (k = 0; k < n; k++) {
  for (j = 10; j < n; j++) { 
    // code block that takes a constant amount of runtime 'd'
  }
}
```

>Let's get the time complexity equation, assuming that the constant runtime of the code within the inner loop is equal to $d$. The first thing to do is to figure out how many times the inner loop runs for a certain $n$. 

If $n = 11$, the inner loop would run once. If $n = 12$, it would run twice. Thus, the inner loop's time complexity is:
$$t_i=d \cdot (n-10)$$
>Now, let's find how many times the outer loop runs for a certain $n$. 

If $n = 1$ (*hypothetically*), the loop would run once. If $n = 11$, the loop would run 11 times. Thus, the outer loop's (the snippet's) time complexity is:
$$t_o =f(n)= n \cdot t_i=d\cdot(n^2-10n)$$
>[!tip] Big-O, Big-$\Omega$, Big-$\Theta$ Recap
>**Big-O:**
>
>$f(n)$ is $O(g(n))$ if any positive constants $c$ and $n_0$ exist such that 
>$$0 \le f(n) \le c \cdot g(n)$$
>for $n \ge n_0$.
>
>**Big-$\Omega$:**
>
>$f(n)$ is $\Omega(g(n))$ if any positive constants $c$ and $n_0$ exist such that 
>$$0 \le c \cdot g(n) \le f(n)$$
>for $n \ge n_0$.
>
>**Big-$\Theta$:**
>
>$f(n)$ is $\Theta(g(n))$ if any positive constants $c_1$, $c_2$ and $n_0$ exist such that 
>$$c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)$$
>for $n \ge n_0$.

#### Finding the Upper Bound

This is the time complexity of our snippet:
$$f(n)=d(n^2-10n)$$
It is obvious that
$$\forall n \in \mathcal{R}^+_0, dn^2 \ge d(n^2-10n)$$
Since there is a premise of $n$ having a domain of $n \ge 11$, we know that the above statement will be true for all $n$. Thus, following the definition in the Recap, $c_2 = d$ and $g(n) = n^2$.

#### Finding the Lower Bound

Since our upper bound has a domain of $n \ge 11$, let's try to find a constant $c_1$ that will make 1) $c_1g(n) \le f(n)$ and 2) $c_1g'(n) \le f'(n)$ within our domain.

>**1)**
$$c_1g(n)=c_1n^2, f(n)=d(n^2-10n)$$
$$c_1g(n) \le f(n) \equiv c_1n^2\le d(n^2-10n)$$
$$c_1\le d(1-\frac{10}{n}), n=11 \implies c_1\le \frac{d}{11}$$

>**2)**
$$c_1g'(n)=c_1(2n), f'(n)=d(2n-10)$$
$$n=11 \implies c_1g'(n) = 22c_1,f'(n)= 12d $$
$$22c_1\le12d \equiv c_1\le\frac{6d}{11}$$

We select the lower value, $\frac{d}{11}$ to be the constant of our lower bound. Thus, $c_1 = \frac{d}{11}$.

#### The Big-$\Theta$ Notation for A
$$\forall(n \ge n_0),c_1 \cdot g(n) \le f(n) \le c_2 \cdot g(n)$$
where $c_1 = \frac{d}{11}, c_2 = d, n_0 = 11, g(n) = n^2$. 

>Thus, $f(n)$ is $\Theta(n^2)$.



### B.
```
k = 1; 
do { 
  j = 1; 
  do { 
     // code block that takes a constant amount of runtime 'd'
     j = j * 3; 
  } until (j >= 0.5*n); // if j < 0.5*n, continue the loop 
  k = k + 1; 
} until (k >= n);
```

>Let's get the time complexity equation, assuming that the constant runtime of the code within the inner loop is equal to $d$. The first thing to do is to figure out how many times the outer loop runs for a certain $n$. 

If $n=1$, then the outer loop runs one time because it is a `do while` loop. 
If $n=2$, it still runs one time because $2 \ge 2$ is true. If $n=3$, however, the outer loop runs two times. If $n=4$, it runs three times. For $n \ge 3$, 
$$t_o = (n-1)t_i$$
As such, I will use a $n_0$ that is within that range.

>Now, let's find how many times the inner loop runs for a certain $n$. 

If $1 < 0.5n \le 3$, the inner loop runs 1 time. If $3 < 0.5n \le 9$, the inner loop runs 2 times.  If $9 < 0.5n \le 27$, the inner loop runs 3 times. Since the bounds in each of these inequalities are powers of 3, let's $\log_3$ everything:
$$0<\log_3(0.5n)\le1 \ \ (\text{1 time})$$
$$1<\log_3(0.5n)\le2 \ \ (\text{2 times})$$
$$2<\log_3(0.5n)\le3 \ \ (\text{3 times})$$
So, 
$$t_i= d\lceil \log_3(0.5n) \rceil$$
Going back to our equation for $t_o$,
$$\forall n \ge 3, t_o=f(n)=d(n-1)\lceil \log_3(0.5n) \rceil$$
#### Finding the Upper Bound

>[!tip] Big-O
>$f(n)$ is $O(g(n))$ if any positive constants $c$ and $n_0$ exist such that 
>$$0 \le f(n) \le c \cdot g(n)$$
>for $n \ge n_0$.

 $\log_3(0.5n)$ is $\Theta(\lceil \log_3(0.5n) \rceil)$ since the gap between the two can only be less than one, so if you were to shift the former up by one or down by one, it would be always greater or lesser than the latter, meaning that if there was ever a gap of one caused by faster/slower growth of the left (multiply by a constant) the gap, whether it be positive or negative, would never close. 
 
 $\log_3(0.5n)$ is $\Theta(\log(0.5n))$ according to the base change theorem.

 $\log(0.5n)$ is $\Theta(\log(n))$ because $\log(0.5n)=\log0.5+\log(n)$ and $\log(n)$ is obviously bound to itself.

So, $f(n)$ is $\Theta((n-1)\log(n))$ - we can get rid of the constant $d$ when just looking at asymptotic notation - which means that if we can find a function $g(n)$ that tightly bounds $(n-1)\log(n)$, it also tightly bounds $f(n)$. 

The upper bound is very intuitive to find:
$$(n-1)\log(n)=\log(n^{n-1})$$
$$\forall n\ge 1, \log(n^n) \ge \log(n^{n-1}), $$
$$\log(n^n)=n\log(n)$$
$$\text{thus, } (n-1)\log(n)\ \text{is} \ O(n\log(n))$$
$$\because (n-1)\log n\ \text{is} \ O(n\log n); f(n) \ \text{is}\ \Theta((n-1)\log n)$$
$$\therefore f(n) \ \text{is} \ O(n\log n)$$

#### Finding the Lower Bound

Let's use the ratio tactic for this one. 

| Time Complexity Notation | Comparison Symbol | Limit                                                             |
| ------------------------ | ----------------- | ----------------------------------------------------------------- |
| $f \in O(g)$             | $f \le g$         | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} < \infty$          |
| $f \in \Theta(g)$        | $f = g$           | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} \in \mathcal{R^+}$ |
| $f \in \Omega(g)$                         | $f \ge g$                   | $\lim_{x \rightarrow \infty} \frac{f(x)}{g(x)} > 0$                                                                  |

What we are looking for is the bottom row of the above table. Let's use the same expression from finding the upper bound, $(n-1)\log(n)$ for our numerator. We will use $n \log(n)$ for the denominator - $g(n)$ has to be the same.
$$\lim_{n \rightarrow \infty} \frac{(n-1)\log(n)}{n\log(n)} > 0$$
$$\lim_{n \rightarrow \infty} \frac{n-1}{n} > 0$$
$$\lim_{n \rightarrow \infty} (1-\frac{1}{n}) > 0$$
This statement is true, so $(n-1)\log(n)$ is $\Omega(n \log(n))$. By the transitive property, $f(n)$ is $\Omega(n \log(n))$.

#### The Big-$\Theta$ Notation for B

$$\because f(n) \ \text{is} \ O(n\log(n)); f(n) \ \text{is} \ \Omega(n\log(n))$$
$$\therefore f(n) \ \text{is} \ \Theta(n\log(n))$$
## PART 2 - Comparing the orders of growth between two algorithms

### A. Is $\log(n^{1000})$ $O(\log(n^{0.0001}))$?

$$f(n)=\log(n^{1000}); g(n)=\log(n^{0.0001})$$
$$\log(n^{1000})=1000\log(n); \log(n^{0.0001})=0.0001\log(n)$$
$$0.0001\log(n)\cdot10^7=1000\log(n)=f(n)=g(n)\cdot10^7$$
>Yes. The necessary constant is $10^7$, as it satisfies the definition of Big-O. 
Since the two functions would be equal, $\forall n_0 \ge 1, f(n) \ \text{is} \ O(g(n))$.
### B. Is $\sqrt{n}$ $O(n)$?

$$\lim_{n \rightarrow \infty} \frac{\sqrt{n}}{n} < \infty \equiv \lim_{n \rightarrow \infty} \frac{1}{\sqrt{n}} < \infty \equiv 0 < \infty$$
>Yes, since the above inequality is true. To test, $c=1$ and $n_0=1$.

### C. Is $3^n$ $O(5^n)$?
$$\lim_{n \rightarrow \infty} \frac{3^n}{5^n} < \infty \equiv \lim_{n \rightarrow \infty} (\frac{3}{5})^n < \infty \equiv 0 < \infty$$
>Yes, since the above inequality is true. To test, $c=1$ and $n_0=1$.

### D. Is $(\cos n+1)$ $O(\sin n+10)$?

>Since $\sin n$ and $\cos n$ are both in-between $1$ and $-1$, $f(n)$ ranges from $[0, 2]$ while $g(n)$ ranges from $[9, 11]$.  Since $\forall n > 0,g(n) \ge f(n) \ge 0$, $f(n)$ is $O(g(n))$. 

---
# *References*
[Lecture Slide Decks: CSE 310: Data Structures and Algorithms (2024 Spring) (asu.edu)](https://canvas.asu.edu/courses/180757/pages/lecture-slide-decks)
