# Week 12 — Taylor & Power Series Expansions

**Course:** Engineering Mathematics 1
**Part:** IV — Sequences, Series & Power Series Solutions
**Kreyszig Sections:** Supplementary Notes

> **Building on Week 11:** We now know when a power series converges (Ratio Test, radius $R$) and that it can be differentiated and integrated term by term. This week answers the complementary question: *what* does a convergent power series represent? The Taylor series expresses any sufficiently differentiable function as a power series — and the Taylor Remainder theorem tells us exactly how much error we make when we truncate. The week closes with the **Power Series Method I**: substituting a power series into an ODE to derive a recurrence relation for the coefficients — the first step toward solving variable-coefficient ODEs that have no closed-form elementary solution.

---

## Lecture 1: Taylor Series and the Remainder Theorem

### Introduction

If a function $f$ has a power series representation centred at $x_0$, the uniqueness theorem from Week 11 forces the coefficients to be $c_n = f^{(n)}(x_0)/n!$. This defines the **Taylor series**. But two questions remain: does the Taylor series actually converge to $f$ (not just to some other function)? And if we truncate after $N$ terms, how large is the error?

The **Taylor Remainder Theorem** answers both. It is the bridge between formal polynomial approximations (used constantly in numerical methods and engineering) and rigorous statements about accuracy.

**Why it matters in engineering:**
- Every calculator and computer evaluates $\sin x$, $e^x$, etc. using polynomial approximations — Taylor polynomials with an error bound.
- Linearisation (small-angle approximation $\sin\theta \approx \theta$) is a Taylor truncation; knowing when it is valid requires the remainder estimate.
- Numerical ODE solvers (Euler, Runge–Kutta) are derived from Taylor expansions of the solution.

---

### Knowledge Points

---

#### 1. Why the Taylor Coefficients are $f^{(n)}(a)/n!$

Before deriving the remainder, it is worth understanding *why* the coefficients must have this form.

If $f(x) = \sum_{n=0}^\infty c_n(x-a)^n$ for $|x-a| < R$, differentiate term by term (valid inside $R$):
- $f(a) = c_0$.
- $f'(x) = \sum_{n=1}^\infty nc_n(x-a)^{n-1}$, so $f'(a) = c_1$.
- $f''(x) = \sum_{n=2}^\infty n(n-1)c_n(x-a)^{n-2}$, so $f''(a) = 2c_2$, giving $c_2 = f''(a)/2!$.
- In general: $f^{(k)}(a) = k!\,c_k$, so $c_k = f^{(k)}(a)/k!$.

This shows the Taylor coefficients are the *only possible* choice — they are forced by the function values.

---

#### 2. Taylor and Maclaurin Series — Definition

**Definition:** If $f$ has derivatives of all orders at $x_0$, the **Taylor series of $f$ centred at $x_0$** is:
$$f(x) = \sum_{n=0}^\infty \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n = f(x_0) + f'(x_0)(x-x_0) + \frac{f''(x_0)}{2!}(x-x_0)^2 + \cdots$$

The **Maclaurin series** is the special case $x_0 = 0$:
$$f(x) = \sum_{n=0}^\infty \frac{f^{(n)}(0)}{n!}x^n.$$

**Notation:** The **$N$-th Taylor polynomial** (the truncated series) is:
$$T_N(x) = \sum_{n=0}^N \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n.$$

This is the best polynomial approximation of degree $\leq N$ to $f$ near $x_0$.

---

#### 3. The Taylor Remainder — Lagrange Form and Proof

**Theorem (Taylor's Theorem with Remainder):** If $f$ has $N+1$ continuous derivatives on an open interval containing $x_0$ and $x$, then:
$$f(x) = T_N(x) + R_N(x),$$
where the **Lagrange remainder** is:
$$R_N(x) = \frac{f^{(N+1)}(\xi)}{(N+1)!}(x-x_0)^{N+1}$$
for some $\xi$ between $x_0$ and $x$ (depending on $x$ and $N$, but its exact value is generally unknown).

**Proof (4-step outline via auxiliary function):**

Define the auxiliary function
$$\varphi(t) = f(x) - f(t) - f'(t)(x-t) - \frac{f''(t)}{2!}(x-t)^2 - \cdots - \frac{f^{(N)}(t)}{N!}(x-t)^N - K(x-t)^{N+1},$$
where $K$ is chosen so that $\varphi(x_0) = 0$ (with $\varphi(x) = 0$ by construction).

**Step 1:** $\varphi(x) = 0$ trivially. Set $\varphi(x_0) = 0$ to find $K$: expanding gives $K = (f(x) - T_N(x))/(x-x_0)^{N+1}$.

**Step 2:** Differentiate $\varphi(t)$ with respect to $t$. By the product rule, telescoping cancellations occur and:
$$\varphi'(t) = -\frac{f^{(N+1)}(t)}{N!}(x-t)^N + (N+1)K(x-t)^N = (x-t)^N\left[(N+1)K - \frac{f^{(N+1)}(t)}{N!}\right].$$

**Step 3:** Apply Rolle's Theorem to $\varphi$ on $[x_0, x]$ (or $[x, x_0]$). Since $\varphi(x_0) = \varphi(x) = 0$, there exists $\xi$ between $x_0$ and $x$ with $\varphi'(\xi) = 0$.

**Step 4:** Setting $\varphi'(\xi) = 0$: $(N+1)K = f^{(N+1)}(\xi)/N!$, so $K = f^{(N+1)}(\xi)/(N+1)!$. Substituting back into the definition of $K$ gives:
$$f(x) - T_N(x) = \frac{f^{(N+1)}(\xi)}{(N+1)!}(x-x_0)^{N+1} = R_N(x). \quad\checkmark$$

**Error bound:** If $|f^{(N+1)}(t)| \leq M$ for all $t$ between $x_0$ and $x$, then:
$$|R_N(x)| \leq \frac{M}{(N+1)!}|x - x_0|^{N+1}.$$

**Convergence to $f$:** The Taylor series converges to $f(x)$ (not just to some limit) iff $R_N(x) \to 0$ as $N \to \infty$.

---

#### 4. When Does the Taylor Series Equal the Function?

**It is possible for the Taylor series to converge but NOT to $f$** — the classic counterexample is $f(x) = e^{-1/x^2}$ ($f(0) = 0$), which has all zero derivatives at $x = 0$, so its Maclaurin series is identically zero, yet $f \neq 0$.

**For functions that appear in this course** ($e^x$, $\sin x$, $\cos x$, polynomials, $\ln(1+x)$, $(1+x)^\alpha$), the Taylor series converges to the function on the natural interval. This is proved via the remainder estimate in each case.

**Proof for $e^x$:** $f^{(n)}(x) = e^x$ for all $n$. For $x \in [-M, M]$, $|f^{(N+1)}(\xi)| \leq e^M$.
$$|R_N(x)| \leq \frac{e^M}{(N+1)!}|x|^{N+1} \to 0 \quad (N \to \infty).$$
(Uses the standard limit $x^n/n! \to 0$ for any fixed $x$ — Week 11 table.) ✓

---

#### 5. Worked Example — Computing a Taylor Series from Scratch

**Find the Maclaurin series for $f(x) = \sin x$.**

| $n$ | $f^{(n)}(x)$ | $f^{(n)}(0)$ | Term |
|-----|-------------|--------------|------|
| 0 | $\sin x$ | 0 | 0 |
| 1 | $\cos x$ | 1 | $x$ |
| 2 | $-\sin x$ | 0 | 0 |
| 3 | $-\cos x$ | $-1$ | $-x^3/3!$ |
| 4 | $\sin x$ | 0 | 0 |
| 5 | $\cos x$ | 1 | $x^5/5!$ |

**Pattern:** Only odd terms survive. $f^{(2k+1)}(0) = (-1)^k$.
$$\sin x = \sum_{n=0}^\infty \frac{(-1)^n}{(2n+1)!}x^{2n+1} = x - \frac{x^3}{6} + \frac{x^5}{120} - \cdots$$

**Remainder bound:** $|f^{(N+1)}(\xi)| \leq 1$ for all $\xi$ (sine and cosine are bounded by 1). So:
$$|R_N(x)| \leq \frac{|x|^{N+1}}{(N+1)!} \to 0.$$
The series equals $\sin x$ for all $x$. ✓

---

#### 6. Taylor Series Centred at $x_0 \neq 0$

**Example:** Expand $f(x) = \ln x$ around $x_0 = 1$.

$f(x) = \ln x$, $f(1) = 0$.
$f'(x) = 1/x$, $f'(1) = 1$.
$f''(x) = -1/x^2$, $f''(1) = -1$.
$f'''(x) = 2/x^3$, $f'''(1) = 2$.
$f^{(n)}(x) = (-1)^{n-1}(n-1)!/x^n$, $f^{(n)}(1) = (-1)^{n-1}(n-1)!$ for $n \geq 1$.

$$\ln x = \sum_{n=1}^\infty \frac{(-1)^{n-1}(n-1)!}{n!}(x-1)^n = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}(x-1)^n.$$

Radius of convergence: $R = 1$ (Ratio Test). IOC: $(0, 2]$.

*(This is the same series as $\ln(1+u)$ with $u = x - 1$, as expected.)*

---

#### 7. Practical Use of the Remainder — Engineering Accuracy

**Engineering question:** How many terms of $\sin x \approx x - x^3/6$ are needed to achieve accuracy $\leq 10^{-4}$ for $|x| \leq 0.5$?

**Remainder after 2 terms** (first omitted term is $x^5/120$):
$$|R_4(x)| \leq \frac{|x|^5}{5!} \leq \frac{(0.5)^5}{120} = \frac{1/32}{120} = \frac{1}{3840} \approx 2.6 \times 10^{-4}.$$

Not sufficient. Add the $x^5/120$ term (3 terms):
$$|R_6(x)| \leq \frac{(0.5)^7}{7!} = \frac{1/128}{5040} \approx 1.5 \times 10^{-6} < 10^{-4}.$$

**Answer:** 3 terms ($x - x^3/6 + x^5/120$) suffice. ✓

**Small-angle approximation:** For small $\theta$ (in radians), $\sin\theta \approx \theta$ with error $\leq \theta^3/6$. For $\theta = 5° = 0.0873$ rad: error $\leq (0.0873)^3/6 \approx 1.1 \times 10^{-4}$ — excellent accuracy.

---

#### 8. Taylor Expansion of Composite and Implicit Functions

**Method 1 — Direct computation** (derivatives): straightforward but tedious for complicated functions.

**Method 2 — Substitution** into a known series (faster, and gives more insight):
- $e^{-x} = \sum(-1)^n x^n/n!$
- $\cos(2x) = \sum (-1)^n (2x)^{2n}/(2n)! = \sum (-1)^n 4^n x^{2n}/(2n)!$
- $\dfrac{1}{1+x^2} = \sum (-1)^n x^{2n}$ (from geometric series with $r = -x^2$)

**Method 3 — Multiplication** of series:
$$e^x\sin x = \left(1 + x + \frac{x^2}{2} + \frac{x^3}{6} + \cdots\right)\!\left(x - \frac{x^3}{6} + \cdots\right)$$
$= x + x^2 + \left(\frac{1}{2} - \frac{1}{6}\right)x^3 + \cdots = x + x^2 + \frac{x^3}{3} + \cdots$

**Method 4 — Integration** of a known series (Week 11 §6):
$\arctan x = \int_0^x \dfrac{dt}{1+t^2} = \int_0^x\sum(-1)^n t^{2n}\,dt = \sum\dfrac{(-1)^n}{2n+1}x^{2n+1}$.

---

#### 9. Summary — Lecture 1

| Concept | Key Formula |
|---------|------------|
| Why $c_n = f^{(n)}(a)/n!$ | Differentiate series term-by-term $k$ times; evaluate at $a$ |
| Taylor series | $\sum_{n=0}^\infty \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n$ |
| Maclaurin series | $x_0 = 0$: $\sum \frac{f^{(n)}(0)}{n!}x^n$ |
| Lagrange remainder | $R_N(x) = \frac{f^{(N+1)}(\xi)}{(N+1)!}(x-x_0)^{N+1}$ |
| Error bound | $|R_N(x)| \leq \frac{M}{(N+1)!}|x-x_0|^{N+1}$ where $M = \max|f^{(N+1)}|$ |
| Series $= f$? | Requires $R_N(x) \to 0$; true for $e^x$, $\sin x$, $\cos x$, etc. |

---

## Lecture 2: Key Expansions, Operations, and Combinations

### Introduction

Rather than computing Taylor series from scratch every time, we maintain a small table of standard expansions and build all other series from these by substitution, multiplication, differentiation, and integration. This is both faster and more insightful — the pattern of coefficients often reveals the function's structure directly.

The binomial series generalises $(1+x)^n$ for any real exponent $\alpha$, and is essential for expanding rational and root functions. The lecture closes with a systematic approach to combining series using the **uniqueness theorem**: if two series agree on an interval, their coefficients must match term by term.

---

### Knowledge Points

---

#### 1. The Standard Table

All of the following are Maclaurin series (centred at 0):

$$e^x = \sum_{n=0}^\infty \frac{x^n}{n!} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!} + \cdots \qquad R = \infty.$$

$$\sin x = \sum_{n=0}^\infty \frac{(-1)^n x^{2n+1}}{(2n+1)!} = x - \frac{x^3}{6} + \frac{x^5}{120} - \cdots \qquad R = \infty.$$

$$\cos x = \sum_{n=0}^\infty \frac{(-1)^n x^{2n}}{(2n)!} = 1 - \frac{x^2}{2} + \frac{x^4}{24} - \cdots \qquad R = \infty.$$

$$\sinh x = \sum_{n=0}^\infty \frac{x^{2n+1}}{(2n+1)!} = x + \frac{x^3}{6} + \frac{x^5}{120} + \cdots \qquad R = \infty.$$

$$\cosh x = \sum_{n=0}^\infty \frac{x^{2n}}{(2n)!} = 1 + \frac{x^2}{2} + \frac{x^4}{24} + \cdots \qquad R = \infty.$$

*(Note: $\sinh x = (e^x - e^{-x})/2$ and $\cosh x = (e^x+e^{-x})/2$. Their series are obtained by taking the odd/even parts of $e^x$.)*

$$\frac{1}{1-x} = \sum_{n=0}^\infty x^n = 1 + x + x^2 + \cdots \qquad R = 1.$$

$$\frac{1}{1+x} = \sum_{n=0}^\infty (-1)^n x^n = 1 - x + x^2 - \cdots \qquad R = 1.$$

$$\ln(1+x) = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}x^n = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots \qquad R = 1,\ \text{IOC:}\ (-1,1].$$

$$\arctan x = \sum_{n=0}^\infty \frac{(-1)^n}{2n+1}x^{2n+1} = x - \frac{x^3}{3} + \frac{x^5}{5} - \cdots \qquad R = 1,\ \text{IOC:}\ [-1,1].$$

$$\sinh^{-1} x = \sum_{n=0}^\infty \frac{(-1)^n(2n)!}{4^n(n!)^2(2n+1)}x^{2n+1} = x - \frac{x^3}{6} + \frac{3x^5}{40} - \cdots \qquad R = 1.$$

$$\tanh^{-1} x = \sum_{n=0}^\infty \frac{x^{2n+1}}{2n+1} = x + \frac{x^3}{3} + \frac{x^5}{5} + \cdots \qquad R = 1.$$

$$(1+x)^\alpha = \sum_{n=0}^\infty \binom{\alpha}{n}x^n \qquad R = 1 \quad \text{(any real } \alpha\text{)},$$
where $\dbinom{\alpha}{n} = \dfrac{\alpha(\alpha-1)(\alpha-2)\cdots(\alpha-n+1)}{n!}$ for $n \geq 1$, $\dbinom{\alpha}{0} = 1$.

---

#### 2. The Binomial Series in Detail

**(1+x)^α** for non-integer real $\alpha$:
$$\binom{\alpha}{0} = 1,\quad \binom{\alpha}{1} = \alpha,\quad \binom{\alpha}{2} = \frac{\alpha(\alpha-1)}{2},\quad \binom{\alpha}{3} = \frac{\alpha(\alpha-1)(\alpha-2)}{6},\ \ldots$$

**Special cases:**
- $\alpha = -1$: $(1+x)^{-1} = \sum(-1)^n x^n$ ✓ (geometric series).
- $\alpha = 1/2$: $\sqrt{1+x} = 1 + \frac{x}{2} - \frac{x^2}{8} + \frac{x^3}{16} - \cdots$
- $\alpha = -1/2$: $\dfrac{1}{\sqrt{1+x}} = 1 - \frac{x}{2} + \frac{3x^2}{8} - \frac{5x^3}{16} + \cdots$

**Endpoint behaviour:** At $x = \pm 1$, convergence depends on $\alpha$:
- $\alpha > 0$: converges at both endpoints.
- $-1 < \alpha \leq 0$: converges at $x = 1$ only (conditionally).
- $\alpha \leq -1$: diverges at both endpoints.

**Error estimate example:** For $\sqrt{1+x} \approx 1 + x/2$:
$$|R_1(x)| = \left|\frac{(1/2)(-1/2)}{2!}x^2/(1+\xi)^{3/2}\right| \leq \frac{x^2}{8}$$
for $x \in [0,1]$. So $|\sqrt{1.04} - 1.02| \leq (0.04)^2/8 = 0.0002$. ✓

**Engineering application:** $\sqrt{1 + x} \approx 1 + x/2$ for small $x$ — used in structural and acoustic approximations. $1/\sqrt{1-v^2/c^2} \approx 1 + v^2/(2c^2)$ for $v \ll c$ (relativistic kinetic energy at low velocity).

---

#### 3. Combining and Manipulating Series

**Key principle (uniqueness):** A function has at most one power series centred at a given point. Therefore, any valid manipulation that produces a power series for $f$ gives the correct Taylor series.

**Substitution examples:**

$e^{x^2} = \displaystyle\sum_{n=0}^\infty \frac{x^{2n}}{n!} = 1 + x^2 + \frac{x^4}{2!} + \frac{x^6}{3!} + \cdots \qquad R = \infty.$

$\sin(2x) = \displaystyle\sum_{n=0}^\infty \frac{(-1)^n (2x)^{2n+1}}{(2n+1)!} = 2x - \frac{4x^3}{3} + \frac{4x^5}{15} - \cdots$

$\dfrac{1}{1+x^2} = \displaystyle\sum_{n=0}^\infty (-1)^n x^{2n} \qquad R = 1.$

$\dfrac{1}{2-x} = \dfrac{1}{2}\cdot\dfrac{1}{1-x/2} = \dfrac{1}{2}\displaystyle\sum_{n=0}^\infty \left(\frac{x}{2}\right)^n = \sum_{n=0}^\infty \frac{x^n}{2^{n+1}} \qquad R = 2.$

---

#### 4. Differentiation and Integration of Series

**Differentiation example:**

From $\dfrac{1}{1-x} = \sum x^n$, differentiate both sides:
$$\frac{1}{(1-x)^2} = \sum_{n=1}^\infty n x^{n-1} = \sum_{n=0}^\infty (n+1)x^n, \qquad R = 1.$$

Differentiate again:
$$\frac{2}{(1-x)^3} = \sum_{n=2}^\infty n(n-1)x^{n-2} = \sum_{n=0}^\infty (n+2)(n+1)x^n.$$

**Integration example:**

From $\dfrac{1}{1+x} = \sum(-1)^n x^n$, integrate from 0 to $x$:
$$\ln(1+x) = \sum_{n=0}^\infty \frac{(-1)^n}{n+1}x^{n+1} = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}x^n. \qquad R = 1.$$

**Classical applications:**

**Leibniz formula for $\pi$:** $\arctan 1 = \pi/4$:
$$\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots = \sum_{n=0}^\infty \frac{(-1)^n}{2n+1}.$$
*(Convergence at $x = 1$ by the AST; the sum equals $\pi/4$ by Abel's theorem.)*

**Gregory–Leibniz for $\ln 2$:** $\ln(1+1) = \ln 2$:
$$\ln 2 = 1 - \frac{1}{2} + \frac{1}{3} - \frac{1}{4} + \cdots = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}.$$

---

#### 5. Multiplication of Series — Cauchy Product

**Formula:** $\left(\sum_{n=0}^\infty a_n x^n\right)\!\left(\sum_{n=0}^\infty b_n x^n\right) = \sum_{n=0}^\infty c_n x^n$, where $c_n = \displaystyle\sum_{k=0}^n a_k b_{n-k}$.

**Example:** Compute the first four terms of $e^x\cos x$.

$$e^x = 1 + x + \frac{x^2}{2} + \frac{x^3}{6} + \cdots$$
$$\cos x = 1 - \frac{x^2}{2} + \cdots$$

$c_0 = 1 \cdot 1 = 1$.
$c_1 = 1 \cdot 0 + 1 \cdot 1 = 1$.
$c_2 = 1 \cdot(-1/2) + 1\cdot 0 + (1/2)\cdot 1 = 0$.
$c_3 = 1\cdot 0 + 1\cdot(-1/2) + 0\cdot 0 + (1/6)\cdot 1 = -1/3$.

$$e^x\cos x = 1 + x - \frac{x^3}{3} + \cdots$$

*(Check: $(e^x\cos x)'= e^x(\cos x - \sin x)$; at $x=0$, value $= 1$. $1 + x$: derivative 1 at 0. ✓)*

**Why Cauchy product matters for ODEs:** When we substitute $y = \sum a_n x^n$ into a product term like $P(x)\cdot y'$ (where $P(x)$ is also a series), the result involves a Cauchy product. This is why the power series ODE method works term-by-term.

---

#### 6. Non-Elementary Integrals via Series

Some integrals have no closed form in elementary functions — but can be represented as series.

**Example 1 — Error function:** $\displaystyle\int_0^x e^{-t^2}\,dt$ (the error function, $\text{erf}(x)$):
$$e^{-t^2} = \sum_{n=0}^\infty \frac{(-1)^n t^{2n}}{n!}.$$
$$\int_0^x e^{-t^2}\,dt = \sum_{n=0}^\infty \frac{(-1)^n x^{2n+1}}{n!(2n+1)}.$$

This converges for all $x$ and is the definition of the error function $\sqrt{\pi}/2\,\cdot\,\text{erf}(x)$ used extensively in probability and heat transfer.

**Example 2 — Fresnel-type integral:** $\displaystyle\int_0^1 \sin(x^2)\,dx$.

$$\sin(x^2) = \sum_{n=0}^\infty \frac{(-1)^n x^{4n+2}}{(2n+1)!} = x^2 - \frac{x^6}{6} + \frac{x^{10}}{120} - \cdots$$

$$\int_0^1\sin(x^2)\,dx = \sum_{n=0}^\infty \frac{(-1)^n}{(2n+1)!\,(4n+3)}\bigg|_0^1.$$

Two-term approximation: $\dfrac{1}{3} - \dfrac{1}{6\cdot 7} = \dfrac{1}{3} - \dfrac{1}{42} \approx 0.310$.

*(The exact value is approximately $0.3103$.)*

**Example 3 — Sine integral:** $\displaystyle\int_0^1 \frac{\sin x}{x}\,dx$:
$\dfrac{\sin x}{x} = \sum_{n=0}^\infty \dfrac{(-1)^n x^{2n}}{(2n+1)!}$.
$\displaystyle\int_0^1 \frac{\sin x}{x}\,dx = \sum_{n=0}^\infty \frac{(-1)^n}{(2n+1)\cdot(2n+1)!} \approx 1 - \frac{1}{18} + \frac{1}{600} - \cdots \approx 0.9461$.

---

#### 7. Applications — Limits via Taylor Series

**Using Taylor series to evaluate indeterminate limits** (an alternative to L'Hôpital's rule):

$$\lim_{x\to 0}\frac{\sin x - x}{x^3} = \lim_{x\to 0}\frac{(x - x^3/6 + \cdots) - x}{x^3} = \lim_{x\to 0}\frac{-x^3/6 + \cdots}{x^3} = -\frac{1}{6}.$$

$$\lim_{x\to 0}\frac{1 - \cos x}{x^2} = \lim_{x\to 0}\frac{1 - (1 - x^2/2 + \cdots)}{x^2} = \lim_{x\to 0}\frac{x^2/2 + \cdots}{x^2} = \frac{1}{2}.$$

$$\lim_{x\to 0}\frac{e^x - 1 - x}{x^2} = \lim_{x\to 0}\frac{x^2/2 + \cdots}{x^2} = \frac{1}{2}.$$

**Advantage over L'Hôpital:** Series clearly reveal the order of the zero, making the limit computation mechanical.

---

#### 8. Summary — Lecture 2

| Operation | Rule | Example |
|-----------|------|---------|
| Standard table | Memorise 10 entries | $\sinh x = \sum x^{2n+1}/(2n+1)!$ |
| Substitution | Replace $x$ by $g(x)$ | $e^{-x^2} = \sum(-x^2)^n/n!$ |
| Multiply by $x^k$ | Shift index | $x/(1+x) = \sum(-1)^n x^{n+1}$ |
| Differentiate | Multiply coefficient by $n$, lower degree | $1/(1-x)^2 = \sum(n+1)x^n$ |
| Integrate | Divide coefficient by $n+1$, raise degree | $\ln(1+x) = \sum(-1)^{n-1}x^n/n$ |
| Multiply (Cauchy) | $c_n = \sum a_k b_{n-k}$ | $e^x\cos x$ |
| Limits | Substitute, keep leading terms | $(\sin x - x)/x^3 \to -1/6$ |
| Non-elementary integrals | Integrate term by term | $\int_0^1\sin(x^2)\,dx \approx 0.310$ |

---

## Lecture 3: Power Series Method I — ODEs and Recurrence Relations

### Introduction

We now combine the power series machinery with second-order ODEs. The **Power Series Method** works at an **ordinary point** $x_0$ of the ODE: we assume the solution has a power series $y = \sum_{n=0}^\infty c_n(x - x_0)^n$, substitute into the ODE, and collect terms by power of $(x-x_0)$. Setting each coefficient to zero yields a **recurrence relation** — a formula for $c_{n+2}$ (or $c_{n+k}$) in terms of earlier coefficients. The two free parameters $c_0$ and $c_1$ correspond to the two arbitrary constants in the general solution, just as expected.

This lecture develops the method through complete worked examples. The connection to familiar solutions ($\cos x$, $\sin x$, $e^x$, polynomials) will confirm that the method is consistent with what we already know.

**Why it matters:**
- Legendre's and Bessel's equations (Week 13) have no elementary closed-form solutions — the power series method is how their solutions are constructed and defined.
- The method applies to any ODE with analytic (power-series representable) coefficients at an ordinary point.

---

### Knowledge Points

---

#### 1. Ordinary Points — When the Method Applies

**Definition:** For $y'' + P(x)y' + Q(x)y = 0$ (standard form), the point $x_0$ is an **ordinary point** if $P(x)$ and $Q(x)$ are both analytic (representable by power series) at $x_0$.

**Theorem:** If $x_0$ is an ordinary point and $P, Q$ are analytic in $|x - x_0| < \rho$, then the ODE has two linearly independent power series solutions $\sum c_n(x-x_0)^n$, each with radius of convergence $R \geq \rho$.

**Examples of ordinary points:**
- $y'' + y = 0$: $P = 0$, $Q = 1$ — analytic everywhere. Every point is ordinary; $R = \infty$.
- $(1-x^2)y'' - 2xy' + n(n+1)y = 0$ (Legendre): $P = -2x/(1-x^2)$, $Q = n(n+1)/(1-x^2)$. Singular points at $x = \pm 1$; $x_0 = 0$ is ordinary. $R \geq 1$.
- $xy'' + y' + xy = 0$ (Bessel, $n=0$): $x = 0$ is singular (coefficient of $y''$ vanishes). Requires Frobenius method (Week 13).

---

#### 2. Setup — Substituting into an ODE

**General procedure** for $y'' + P(x)y' + Q(x)y = r(x)$ at $x_0 = 0$:

**Step 1:** Assume $y = \displaystyle\sum_{n=0}^\infty c_n x^n$.

**Step 2:** Compute $y' = \displaystyle\sum_{n=1}^\infty n\,c_n x^{n-1}$ and $y'' = \displaystyle\sum_{n=2}^\infty n(n-1)c_n x^{n-2}$.

**Step 3:** Re-index so all series start at the same power. The standard re-indexing for $y''$:
$$y'' = \sum_{n=2}^\infty n(n-1)c_n x^{n-2} = \sum_{n=0}^\infty (n+2)(n+1)c_{n+2}\,x^n.$$

**Step 4:** Substitute into the ODE and collect coefficients of $x^n$.

**Step 5:** Set each coefficient of $x^n$ equal to zero → **recurrence relation**.

**Step 6:** Use $c_0$ and $c_1$ (free) to generate all higher coefficients; write the two independent solutions $y_1$ (even series, $c_0 = 1$, $c_1 = 0$) and $y_2$ (odd series, $c_0 = 0$, $c_1 = 1$).

---

#### 3. Warm-Up — $y' + 2y = 0$ (Recovering $e^{-2x}$)

Before tackling second-order equations, verify the method works for a simple first-order ODE.

**Assume** $y = \sum_{n=0}^\infty c_n x^n$. Then $y' = \sum_{n=1}^\infty nc_n x^{n-1} = \sum_{n=0}^\infty (n+1)c_{n+1}x^n$.

**Substitute** into $y' + 2y = 0$:
$$\sum_{n=0}^\infty (n+1)c_{n+1}x^n + 2\sum_{n=0}^\infty c_n x^n = 0.$$

**Coefficient of $x^n$:** $(n+1)c_{n+1} + 2c_n = 0$, so $c_{n+1} = \dfrac{-2}{n+1}c_n$.

**Starting from $c_0 = 1$:** $c_1 = -2$, $c_2 = 2^2/2! = 2$, $c_3 = -2^3/3!$, ..., $c_n = (-2)^n/n!$.

$$y = \sum_{n=0}^\infty \frac{(-2)^n}{n!}x^n = e^{-2x}. \quad\checkmark$$

---

#### 4. Worked Example 1 — $y'' + y = 0$ (Recovering $\cos x$ and $\sin x$)

**Substitute:** $\sum_{n=0}^\infty(n+2)(n+1)c_{n+2}x^n + \sum_{n=0}^\infty c_n x^n = 0$.

**Coefficient of $x^n$:** $(n+2)(n+1)c_{n+2} + c_n = 0$.

**Recurrence relation:**
$$c_{n+2} = -\frac{c_n}{(n+2)(n+1)}.$$

**Even series** ($c_0 = 1$, $c_1 = 0$):
$$c_2 = -\frac{1}{2}, \quad c_4 = \frac{1}{4\cdot 3}\cdot\frac{1}{2} = \frac{1}{24}, \quad c_{2k} = \frac{(-1)^k}{(2k)!}.$$
$$y_1 = \sum_{k=0}^\infty\frac{(-1)^k}{(2k)!}x^{2k} = \cos x. \checkmark$$

**Odd series** ($c_0 = 0$, $c_1 = 1$):
$$c_3 = -\frac{1}{6}, \quad c_5 = \frac{1}{120}, \quad c_{2k+1} = \frac{(-1)^k}{(2k+1)!}.$$
$$y_2 = \sum_{k=0}^\infty\frac{(-1)^k}{(2k+1)!}x^{2k+1} = \sin x. \checkmark$$

**General solution:** $y = c_0\cos x + c_1\sin x$. ✓

---

#### 5. Worked Example 2 — $y'' + xy' + y = 0$ (Recovering $e^{-x^2/2}$)

**Substitute** (re-index middle term: $xy' = x\sum_{n=1}^\infty nc_n x^{n-1} = \sum_{n=1}^\infty nc_n x^n = \sum_{n=0}^\infty nc_n x^n$):

$$\sum_{n=0}^\infty(n+2)(n+1)c_{n+2}x^n + \sum_{n=0}^\infty nc_n x^n + \sum_{n=0}^\infty c_n x^n = 0.$$

**Coefficient of $x^n$:** $(n+2)(n+1)c_{n+2} + (n+1)c_n = 0$.

**Recurrence relation:**
$$c_{n+2} = -\frac{c_n}{n+2}.$$

**Even series** ($c_0 = 1$, $c_1 = 0$):
$$c_2 = -\frac{1}{2}, \quad c_4 = \frac{c_2}{4} = \frac{1}{8} = \frac{1}{2^2\cdot 2!}, \quad \ldots,\quad c_{2k} = \frac{(-1)^k}{2^k k!}.$$
$$y_1 = \sum_{k=0}^\infty \frac{(-1)^k x^{2k}}{2^k k!} = \sum_{k=0}^\infty \frac{(-x^2/2)^k}{k!} = e^{-x^2/2}. \quad\checkmark$$

*(This is a **Gaussian** — the solution decays to 0 as $x \to \pm\infty$.)*

*(Verify: $y_1' = -xe^{-x^2/2}$, $y_1'' = (x^2-1)e^{-x^2/2}$; $(x^2-1+x(-x)+1)e^{-x^2/2} = 0$. ✓)*

**Odd series** ($c_0 = 0$, $c_1 = 1$): Non-terminating infinite series (no elementary closed form).

---

#### 6. Worked Example 3 — $y'' - 2xy' + 4y = 0$ (Hermite-type, terminating)

**Substitute** and re-index: coefficient of $x^n$ gives:
$$(n+2)(n+1)c_{n+2} - 2nc_n + 4c_n = 0.$$

**Recurrence:**
$$c_{n+2} = \frac{2(n-2)}{(n+2)(n+1)}c_n.$$

**Even series** ($c_0 = 1$, $c_1 = 0$):
$$c_2 = \frac{2(0-2)}{2\cdot1}c_0 = -2, \quad c_4 = \frac{2(2-2)}{4\cdot 3}c_2 = 0.$$
Since $c_4 = 0$, all higher even coefficients vanish.
$$y_1 = 1 - 2x^2.$$

This is a **polynomial** solution! Termination occurs because the numerator factor $(n-2) = 0$ at $n = 2$.

**Odd series** ($c_0 = 0$, $c_1 = 1$): Non-terminating, infinite radius of convergence.

**Hermite polynomials (general pattern):** For $y'' - 2xy' + 2\lambda y = 0$:
- $\lambda = 0$: $y_1 = 1$ (constant).
- $\lambda = 1$: $y_2 = x$ (terminates odd series).
- $\lambda = 2$: $y_1 = 1 - 2x^2$ (terminates even series). ✓

Polynomial solutions arise exactly when $\lambda = n$ (a non-negative integer). This is the mechanism behind **Legendre polynomials** (Week 13).

---

#### 7. Airy Equation Centred at $x_0 = 1$

The standard Airy equation $y'' - xy = 0$ can also be solved by the power series method centred at $x_0 = 1$ (shifting to expand around a different ordinary point).

Let $t = x - 1$ (so $x = t+1$) and assume $y = \sum_{n=0}^\infty a_n t^n$:

$$y'' = \sum_{n=0}^\infty(n+2)(n+1)a_{n+2}t^n, \qquad xy = (t+1)\sum_{n=0}^\infty a_n t^n = \sum_{n=0}^\infty a_{n-1}t^n + \sum_{n=0}^\infty a_n t^n.$$

(where $a_{-1} \equiv 0$.)

**Coefficient of $t^n$:** $(n+2)(n+1)a_{n+2} = a_{n-1} + a_n$.

**Coupled recurrence:**
$$a_{n+2} = \frac{a_{n-1} + a_n}{(n+2)(n+1)}.$$

This couples three consecutive coefficients rather than two — solving requires tracking both $a_0$ and $a_1$ as free parameters. The first few terms:

For $a_0 = 1$, $a_1 = 0$: $a_2 = a_{-1}+a_0/(2\cdot1) = 1/2$, $a_3 = (a_0+a_1)/(3\cdot 2) = 1/6$, ...

*(This example demonstrates that shifting the centre changes the recurrence structure, but the method still works.)*

---

#### 8. Non-Homogeneous Equations

**Extension:** If $y'' + P(x)y' + Q(x)y = r(x)$ and $r(x)$ is also expanded as a power series, the method extends directly: the recurrence relation picks up an additional forcing term from $r(x)$.

**Example:** $y'' + y = x^2$.

$\sum(n+2)(n+1)c_{n+2}x^n + \sum c_n x^n = x^2$.

**Coefficients of $x^n$:** $(n+2)(n+1)c_{n+2} + c_n = \begin{cases}1 & n=2 \\ 0 & n\neq 2\end{cases}$.

So for $n \neq 2$: $c_{n+2} = -c_n/[(n+2)(n+1)]$ — same as before (the homogeneous recurrence).
For $n = 2$: $4 \cdot 3 \cdot c_4 + c_2 = 1 \Rightarrow c_4 = (1 - c_2)/12$.

The general solution is $y_h + y_p$ as usual; the series approach incorporates both automatically.

---

#### 9. Radius of Convergence of Series Solutions

**Theorem:** If $x_0$ is an ordinary point and the nearest singular point is at distance $\rho$ from $x_0$ (in the complex plane), then the series solutions converge for $|x - x_0| < \rho$.

**Examples:**
- $y'' + y = 0$: no singular points → $\rho = \infty$, $R = \infty$.
- Legendre's equation (singular points at $x = \pm 1$, $x_0 = 0$): $\rho = 1$, $R \geq 1$.
- $(1+x^2)y'' + y = 0$ (singular points at $x = \pm i$ in complex plane, distance 1 from origin): $R \geq 1$.

**Practical rule:** The series converges at least up to the nearest point where the coefficient of $y''$ vanishes or a coefficient blows up.

---

#### 10. Re-Indexing Reference

The following re-indexings are used constantly in the Power Series Method:

$$\sum_{n=2}^\infty n(n-1)c_n x^{n-2} \stackrel{m=n-2}{=} \sum_{m=0}^\infty (m+2)(m+1)c_{m+2}x^m.$$

$$\sum_{n=1}^\infty nc_n x^{n-1} \stackrel{m=n-1}{=} \sum_{m=0}^\infty (m+1)c_{m+1}x^m.$$

$$x \cdot \sum_{n=0}^\infty c_n x^n = \sum_{n=0}^\infty c_n x^{n+1} = \sum_{n=1}^\infty c_{n-1}x^n.$$

$$x^2 \cdot \sum_{n=0}^\infty c_n x^n = \sum_{n=2}^\infty c_{n-2}x^n.$$

Mastering these re-indexings is the main technical skill of the Power Series Method.

---

#### 11. Summary — Lecture 3

| Step | Action |
|------|--------|
| 1 | Assume $y = \sum c_n x^n$; compute $y'$, $y''$ |
| 2 | Re-index $y''$ to $\sum(n+2)(n+1)c_{n+2}x^n$ |
| 3 | Substitute into ODE; collect by power of $x$ |
| 4 | Set each coefficient to zero → recurrence |
| 5 | Solve recurrence starting from $c_0 = 1, c_1 = 0$ (even $y_1$) and $c_0 = 0, c_1 = 1$ (odd $y_2$) |
| 6 | Write $y = c_0 y_1 + c_1 y_2$; check for termination (polynomial solutions) |

**Termination:** If the numerator of the recurrence vanishes at some $n = N$, the series terminates → polynomial solution of degree $N$.

**Key examples recovered:**
- $y'' + y = 0$: $y_1 = \cos x$, $y_2 = \sin x$.
- $y'' + xy' + y = 0$: $y_1 = e^{-x^2/2}$ (Gaussian).
- $y'' - 2xy' + 4y = 0$: $y_1 = 1-2x^2$ (terminates).
- $y'' - 2xy' + 2\lambda y = 0$: Hermite polynomial when $\lambda = 0,1,2,\ldots$

---

## Practice Session

**Theme:** Taylor series derivation and error bounds; operations on series; limits via series; power series method for ODEs; recurrence relations.

---

### Practice Problems

**Set A — Taylor Series: Derivation and Remainder**

1. Find the Maclaurin series for each function and state the radius of convergence:
   (a) $f(x) = e^{2x}$
   (b) $f(x) = \cosh x$ *(obtain from the $e^x$ series directly)*
   (c) $f(x) = x^2\sin x$
   (d) $f(x) = \dfrac{1}{(1-x)^2}$ *(differentiate the geometric series)*

2. Find the Taylor series for $f(x) = \ln x$ centred at $x_0 = 1$ up to the $(x-1)^4$ term. State the IOC.

3. (a) Use the Maclaurin series for $e^x$ to show that the error in the approximation $e^x \approx 1 + x + x^2/2$ satisfies $|R_2(x)| \leq e|x|^3/6$ for $|x| \leq 1$.
   (b) Use the Lagrange remainder to find how many terms of the Maclaurin series for $\sin x$ are needed to compute $\sin(0.5)$ with error less than $10^{-6}$.

4. Use Taylor series to evaluate the following limits:
   (a) $\displaystyle\lim_{x\to 0}\frac{e^x - 1 - x - x^2/2}{x^3}$
   (b) $\displaystyle\lim_{x\to 0}\frac{\cos x - 1 + x^2/2}{x^4}$
   (c) $\displaystyle\lim_{x\to 0}\frac{\ln(1+x) - x}{x^2}$
   (d) $\displaystyle\lim_{x\to 0}\frac{\sinh x - \sin x}{x^3}$ *(use the series for both functions)*

**Set B — Operations on Power Series**

5. Find the Maclaurin series up to $x^5$ for:
   (a) $f(x) = e^x\cos x$
   (b) $f(x) = \dfrac{\sin x}{1-x}$
   (c) $f(x) = (1+x)^{1/2}$ *(binomial series — first 4 terms)*

6. Use differentiation or integration of known series to find a series for:
   (a) $f(x) = \dfrac{1}{(1+x)^2}$
   (b) $f(x) = \arctan(2x)$
   (c) $f(x) = \displaystyle\int_0^x \frac{1-\cos t}{t^2}\,dt$

7. Compute $\displaystyle\int_0^{0.5} \sin(x^2)\,dx$ using the power series, retaining enough terms to achieve accuracy $10^{-4}$.

8. Find the power series representation of $f(x) = \dfrac{x}{4+x^2}$ centred at $0$ and state the IOC.
   *(Hint: write as $\frac{x}{4}\cdot\frac{1}{1+(x/2)^2}$ and use the geometric series.)*

**Set C — Power Series Method for ODEs**

9. Use the Power Series Method to find the general solution of $y'' + 4y = 0$:
   (a) Derive the recurrence relation.
   (b) Find the even series $y_1$ and odd series $y_2$.
   (c) Identify both in terms of elementary functions and verify by substitution.

10. Apply the Power Series Method to $y'' - xy' - 2y = 0$:
    (a) Derive the recurrence relation.
    (b) Compute the first 4 non-zero terms of $y_1$ (even) and $y_2$ (odd).
    (c) Check whether either series terminates (polynomial solution).

11. Consider $(1-x^2)y'' - 2xy' + 6y = 0$ (Legendre equation with $n=2$):
    (a) Is $x_0 = 0$ an ordinary point? Justify.
    (b) Derive the recurrence relation (centred at $x_0 = 0$).
    (c) Show that the even series terminates, giving a polynomial solution. Identify it (up to scalar multiple) as $P_2(x) = \frac{1}{2}(3x^2 - 1)$.

12. Use the Power Series Method to find a particular series solution of $y'' + y = x^2$, $y(0) = 0$, $y'(0) = 0$.
    (a) Derive the recurrence relation for the forced problem.
    (b) Compute the first 4 terms of $y_p$.
    (c) Compare with the particular solution found by the UC method (Week 9) and verify consistency.
