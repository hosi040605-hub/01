# Week 2 — Integration: Theory, Applications & Techniques

**Course:** Engineering Mathematics 1
**Part:** I — Calculus Foundations (Review)
**Supplementary Material:** `02-1 eng_math_definite_integralsl.pdf`, `02-2 eng_math_applicaion_integral.pdf`

> **Forward links for this week:**
> - Improper Integrals → Week 14 (the Laplace transform $\int_0^\infty e^{-st}f(t)\,dt$ is a Type I improper integral; convergence at infinity is required)
> - Gamma Function → Week 14 ($\mathcal{L}\{t^\alpha\} = \Gamma(\alpha+1)/s^{\alpha+1}$ for non-integer $\alpha$; appears in Bessel functions in Week 13)
> - Partial Fractions → Week 14 (computing inverse Laplace transforms of rational $F(s)$)
> - Completing the Square → Week 14 (irreducible quadratic denominators $(s+a)^2+b^2$ in the $s$-domain)

---

## Lecture 1: Definite Integral and Improper Integrals

### Introduction

If differentiation asks *how fast is something changing*, integration asks *how much has accumulated*. The **Fundamental Theorem of Calculus** is the profound link between these two operations — it says that they are inverses of each other. This lecture establishes that bridge rigorously, then develops the two most essential integration techniques: **u-substitution** (the chain rule in reverse) and **integration by parts** (the product rule in reverse).

The lecture then extends the definite integral to **improper integrals**, handling infinite limits (Type I) and integrand singularities (Type II). These are essential for defining the Laplace transform and for convergence arguments throughout engineering mathematics.

**Why it matters in engineering:**
- Work done by a variable force, charge stored in a capacitor, energy dissipated in a resistor — all computed via definite integrals.
- Solving ODEs often requires computing integrals; u-substitution and IBP are the primary tools.
- The Laplace transform $\int_0^\infty e^{-st}f(t)\,dt$ is a Type I improper integral, requiring fluency with limits at infinity.

---

### Knowledge Points

---

#### 1. The Definite Integral — From Areas to Limits

**Motivation:** Given a non-negative function $f$ on $[a,b]$, how do we compute the exact area under the curve?

**General Partition:** A **partition** of $[a,b]$ is a finite set of points
$$P = \{x_0,\, x_1,\, \ldots,\, x_n\}, \qquad a = x_0 < x_1 < \cdots < x_n = b.$$
The subintervals need not have equal width; the $i$-th subinterval has width $\Delta x_i = x_i - x_{i-1}$.

**Mesh (norm) of a partition:**
$$\|P\| = \max_{1 \le i \le n} \Delta x_i$$
the length of the widest subinterval. Requiring $\|P\| \to 0$ forces *every* subinterval to shrink, regardless of how the partition points are spaced.

**Riemann Sum:** Choose any **sample point** $x_i^* \in [x_{i-1}, x_i]$ in each subinterval. The corresponding Riemann sum is:
$$S(f, P, \{x_i^*\}) = \sum_{i=1}^{n} f(x_i^*)\,\Delta x_i$$

**Definition (Definite Integral):** $f$ is **Riemann integrable** on $[a,b]$, with integral $I$, if for every $\varepsilon > 0$ there exists $\delta > 0$ such that
$$\|P\| < \delta \implies \left|S(f, P, \{x_i^*\}) - I\right| < \varepsilon$$
for *every* partition $P$ with $\|P\| < \delta$ and *every* choice of sample points. We write:
$$I = \int_a^b f(x)\,dx = \lim_{\|P\| \to 0} \sum_{i=1}^{n} f(x_i^*)\,\Delta x_i$$

**Example:** Estimate $\int_0^1 x^2\,dx$ using uniform partition $n = 4$, right-endpoint sample points:
$$S = (0.25^2 + 0.5^2 + 0.75^2 + 1^2)\times 0.25 = 0.46875$$
Exact value: $1/3 \approx 0.333$. The approximation improves as $\|P\| \to 0$.

---

#### 2. Properties of the Definite Integral

**Linearity:**
$$\int_a^b [cf(x) + g(x)]\,dx = c\int_a^b f(x)\,dx + \int_a^b g(x)\,dx$$

**Additivity over intervals:**
$$\int_a^b f(x)\,dx = \int_a^c f(x)\,dx + \int_c^b f(x)\,dx$$

**Reversal of limits:**
$$\int_a^b f(x)\,dx = -\int_b^a f(x)\,dx, \qquad \int_a^a f(x)\,dx = 0$$

**Comparison:**
$$f(x) \leq g(x) \text{ on } [a,b] \implies \int_a^b f(x)\,dx \leq \int_a^b g(x)\,dx$$

**Boundedness:**
$$m(b-a) \leq \int_a^b f(x)\,dx \leq M(b-a)$$
where $m$ and $M$ are the minimum and maximum of $f$ on $[a,b]$.

---

#### 3. Antiderivatives and the Indefinite Integral

**Definition:** $F$ is an **antiderivative** of $f$ on an interval if $F'(x) = f(x)$ for all $x$ in that interval.

**Theorem:** If $F$ is one antiderivative of $f$, then every antiderivative has the form $F(x) + C$ for some constant $C$. This is the **indefinite integral**:
$$\int f(x)\,dx = F(x) + C$$

**Basic antiderivative table:**

| $f(x)$ | $\int f(x)\,dx$ |
|--------|----------------|
| $x^n\ (n\neq -1)$ | $\dfrac{x^{n+1}}{n+1} + C$ |
| $\dfrac{1}{x}$ | $\ln|x| + C$ |
| $e^x$ | $e^x + C$ |
| $a^x$ | $\dfrac{a^x}{\ln a} + C$ |
| $\sin x$ | $-\cos x + C$ |
| $\cos x$ | $\sin x + C$ |
| $\sec^2 x$ | $\tan x + C$ |
| $\dfrac{1}{\sqrt{1-x^2}}$ | $\arcsin x + C$ |
| $\dfrac{1}{1+x^2}$ | $\arctan x + C$ |

---

#### 4. Fundamental Theorem of Calculus — Part 1

**Theorem (FTC Part 1):** If $f$ is continuous on $[a,b]$, define the accumulation function:
$$g(x) = \int_a^x f(t)\,dt$$
Then $g$ is differentiable **on $(a,b)$** and
$$g'(x) = f(x) \quad \text{for all } x \in (a,b).$$
(One-sided derivatives hold at the endpoints $x = a$ and $x = b$.)

**Intuition:** The rate of change of the accumulated area equals the current height $f(x)$. Adding a thin slice of width $dx$ and height $f(x)$ changes the area by $f(x)\,dx$.

**Example 1:** $g(x) = \displaystyle\int_1^x \sin(t^2)\,dt$. Then $g'(x) = \sin(x^2)$.

**Example 2 (Chain Rule combined):** $g(x) = \displaystyle\int_1^{x^3} \sqrt{1+t}\,dt$.
$$g'(x) = \sqrt{1+x^3} \cdot 3x^2$$

**Example 3:** $g(x) = \displaystyle\int_x^5 e^{t^2}\,dt = -\int_5^x e^{t^2}\,dt$.
$$g'(x) = -e^{x^2}$$

---

#### 5. Fundamental Theorem of Calculus — Part 2

**Theorem (FTC Part 2):** If $f$ is continuous on $[a,b]$ and $F$ is any antiderivative of $f$, then:
$$\int_a^b f(x)\,dx = F(b) - F(a) \equiv \Big[F(x)\Big]_a^b$$

**Proof idea:** Define $g(x) = \int_a^x f(t)\,dt$. By FTC Part 1, $g'(x) = f(x)$, so $g(x) = F(x) + C$. Setting $x = a$: $C = -F(a)$. At $x = b$: $g(b) = F(b) - F(a)$.

**Example 1:** $\displaystyle\int_1^4 (3x^2 - 2x + 1)\,dx = \Big[x^3 - x^2 + x\Big]_1^4 = 52 - 1 = 51$

**Example 2:** $\displaystyle\int_0^{\pi/2} \cos x\,dx = \Big[\sin x\Big]_0^{\pi/2} = 1 - 0 = 1$

**Example 3:** $\displaystyle\int_1^e \frac{1}{x}\,dx = \Big[\ln x\Big]_1^e = 1 - 0 = 1$

---

#### 6. u-Substitution — The Method

**Procedure for $\int f(g(x))g'(x)\,dx$:**
1. Choose $u = g(x)$ (the inner function).
2. Compute $du = g'(x)\,dx$.
3. Rewrite the entire integral in terms of $u$.
4. Integrate in $u$.
5. Back-substitute $u = g(x)$ to return to $x$.

For **definite** integrals, convert the limits to $u$-values; do not back-substitute.

**Example 1:** $\displaystyle\int \frac{e^{\sqrt{x}}}{\sqrt{x}}\,dx$. Let $u = \sqrt{x}$: $2e^u + C = 2e^{\sqrt{x}} + C$.

**Example 2:** $\displaystyle\int \tan x\,dx = \int \frac{\sin x}{\cos x}\,dx$. Let $u = \cos x$: $-\ln|\cos x| + C = \ln|\sec x| + C$.

**Example 3:** $\displaystyle\int x^2\sqrt{x^3+1}\,dx$. Let $u = x^3+1$: $\frac{2}{9}(x^3+1)^{3/2} + C$.

**Definite example:** $\displaystyle\int_0^{\pi/4} \frac{\sin x}{\cos^2 x}\,dx$. Let $u = \cos x$, limits $1 \to 1/\sqrt{2}$:
$$\Big[1/u\Big]_1^{1/\sqrt{2}} = \sqrt{2} - 1$$

---

#### 7. Integration by Parts — Formula and LIATE Rule

**Origin (product rule reversed):**
$$\int u\,dv = uv - \int v\,du$$

**LIATE Rule** for choosing $u$ (priority order, highest first):
- **L** — Logarithmic: $\ln x$, $\log x$
- **I** — Inverse trigonometric: $\arcsin x$, $\arctan x$
- **A** — Algebraic (polynomials): $x^n$
- **T** — Trigonometric: $\sin x$, $\cos x$
- **E** — Exponential: $e^x$, $a^x$

**Example 1:** $\int x e^x\,dx$. $u=x$, $dv=e^x\,dx$: $(x-1)e^x + C$.

**Example 2:** $\int x^2\sin x\,dx$. IBP twice: $-x^2\cos x + 2x\sin x + 2\cos x + C$.

**Example 3:** $\int \ln x\,dx$. $u=\ln x$, $dv=dx$: $x\ln x - x + C$.

**Cycling (for $e^x \times$ trig):** $\int e^x\sin x\,dx$. Apply IBP twice; let $I$ denote the integral:
$$I = e^x\sin x - e^x\cos x - I \implies I = \frac{e^x(\sin x - \cos x)}{2} + C$$

**Tabular method** (for polynomial $\times$ function, e.g. $\int x^3 e^x\,dx$): repeatedly differentiate $u$ and integrate $dv$, multiply diagonally with alternating signs:
$$\int x^3 e^x\,dx = (x^3 - 3x^2 + 6x - 6)e^x + C$$

**Definite IBP:** $\displaystyle\int_1^e x\ln x\,dx = \Big[\frac{x^2\ln x}{2}\Big]_1^e - \int_1^e\frac{x}{2}\,dx = \frac{e^2+1}{4}$

---

#### 8. Improper Integrals — Motivation

**The problem:** The definite integral $\int_a^b f(x)\,dx$ requires a *bounded* interval $[a,b]$ and a *bounded* function $f$. Engineering constantly requires:
- **Type I:** Integration over an infinite range, e.g. $\int_0^\infty e^{-st}f(t)\,dt$ (Laplace transform).
- **Type II:** Integration near a singularity, e.g. $\int_0^1 \frac{1}{\sqrt{x}}\,dx$ (integrand $\to\infty$ as $x\to0$).

Both types are defined using **limits**.

---

#### 9. Type I — Infinite Limits

**Definitions:**
$$\int_a^\infty f(x)\,dx = \lim_{b\to\infty}\int_a^b f(x)\,dx$$
$$\int_{-\infty}^b f(x)\,dx = \lim_{a\to-\infty}\int_a^b f(x)\,dx$$
$$\int_{-\infty}^\infty f(x)\,dx = \int_{-\infty}^c f(x)\,dx + \int_c^\infty f(x)\,dx \quad \text{(split at any finite } c\text{)}$$

The integral **converges** if the limit exists and is finite; otherwise it **diverges**.

**Example 1 (converges):** $\displaystyle\int_1^\infty \frac{1}{x^2}\,dx = \lim_{b\to\infty}\Big[-\frac{1}{x}\Big]_1^b = 1$

**Example 2 (diverges):** $\displaystyle\int_1^\infty \frac{1}{x}\,dx = \lim_{b\to\infty}\ln b = \infty$

---

#### 10. The p-Test for Type I Integrals

**Theorem:**
$$\int_1^\infty \frac{1}{x^p}\,dx \begin{cases} \text{converges to } \dfrac{1}{p-1} & \text{if } p > 1 \\[6pt] \text{diverges} & \text{if } p \leq 1 \end{cases}$$

**Proof:** For $p\neq1$: $\int_1^b x^{-p}\,dx = \frac{b^{1-p}-1}{1-p}$. As $b\to\infty$: $b^{1-p}\to0$ if $p>1$; $\to\infty$ if $p<1$.

---

#### 11. Comparison Test for Improper Integrals

**Theorem:** Suppose $0 \leq f(x) \leq g(x)$ for all $x \geq a$. Then:
- **Convergence:** If $\int_a^\infty g(x)\,dx$ converges, then $\int_a^\infty f(x)\,dx$ converges.
- **Divergence:** If $\int_a^\infty f(x)\,dx$ diverges, then $\int_a^\infty g(x)\,dx$ diverges.

**Example (convergence):** $0 \leq \dfrac{\sin^2 x}{x^2} \leq \dfrac{1}{x^2}$ and $\int_1^\infty x^{-2}\,dx$ converges ($p=2>1$) $\Rightarrow$ $\int_1^\infty\frac{\sin^2 x}{x^2}\,dx$ converges.

**Example (divergence):** $\dfrac{2+\cos x}{x} \geq \dfrac{1}{x} > 0$ and $\int_1^\infty x^{-1}\,dx$ diverges ($p=1$) $\Rightarrow$ $\int_1^\infty\frac{2+\cos x}{x}\,dx$ diverges.

*(Both directions of the Comparison Test are needed in Lecture 2: the convergence direction verifies Gabriel's Horn volume; the divergence direction proves its surface area is infinite.)*

---

#### 12. Type II — Discontinuous Integrands

**Setup:** $f$ has a singularity (vertical asymptote) at some point in $[a,b]$.

**Case: singularity at left endpoint $a$:**
$$\int_a^b f(x)\,dx = \lim_{\varepsilon\to 0^+}\int_{a+\varepsilon}^b f(x)\,dx$$

**Case: singularity at right endpoint $b$:**
$$\int_a^b f(x)\,dx = \lim_{\varepsilon\to 0^+}\int_a^{b-\varepsilon} f(x)\,dx$$

**Case: singularity at interior point $c \in (a,b)$:** split into two Type II integrals — *both* must converge.

**Example 1 (converges):** $\displaystyle\int_0^1 \frac{1}{\sqrt{x}}\,dx = \lim_{\varepsilon\to0^+}\Big[2\sqrt{x}\Big]_\varepsilon^1 = 2$

**Example 2 (diverges):** $\displaystyle\int_0^1 \frac{1}{x}\,dx = \lim_{\varepsilon\to0^+}(0 - \ln\varepsilon) = +\infty$

**The p-test for Type II** (singularity at 0):
$$\int_0^1 \frac{dx}{x^p} \begin{cases} \text{converges} & \text{if } p < 1 \\[4pt] \text{diverges} & \text{if } p \geq 1 \end{cases}$$
*Note: opposite condition from Type I!*

---

#### 13. Summary — Lecture 1

**Decision flowchart for integration:**

```
Is there an obvious antiderivative from the table?
    YES → Apply directly
    NO  → Is there a composite function (inner/outer structure)?
              YES → Try u-substitution
              NO  → Is it a product of two different types?
                        YES → Try Integration by Parts (LIATE)
                        NO  → See Lecture 3 (completing the square, PFD, trig sub, ...)
```

**Key formulas:**
$$\text{FTC Part 1: } g'(x)=f(x),\; x\in(a,b) \quad\text{FTC Part 2: }\int_a^b f\,dx = F(b)-F(a)$$
$$\text{u-sub: } \int f(g(x))g'(x)\,dx = \int f(u)\,du \qquad \text{IBP: } \int u\,dv = uv - \int v\,du$$

**Improper integral convergence summary:**

| Type | Integral | Converges when |
|------|----------|---------------|
| Type I | $\int_1^\infty x^{-p}\,dx$ | $p > 1$ |
| Type II | $\int_0^1 x^{-p}\,dx$ | $p < 1$ |

---

## Lecture 2: Applications of Integration

### Introduction

Integration accumulates any continuously varying quantity over an interval. This lecture develops the main geometric and physical applications:

- **Area and volume** — the classical geometric applications, using three complementary methods (cross-section, disk/washer, shell).
- **Arc length and surface area** — measuring the geometry of curves.
- **Center of mass** — the weighted average position of a distributed mass.
- **Natural logarithm and exponential** — defined rigorously via integration.
- **Gamma function** — extends the factorial to real arguments; bridges integration and special functions.
- **Remarkable improper integrals** — Gabriel's Horn (Torricelli's paradox) and the Gaussian integral, two of the most celebrated results in analysis.

**Why it matters in engineering:**
- Volumes of revolution arise in shaft design, pressure vessels, and fuel tanks.
- Arc length gives cable lengths, gear tooth profiles, and fiber optic path lengths.
- The Gamma function governs the Laplace transform of $t^\alpha$ and the chi-squared distribution.
- The Gaussian integral is the foundation of probability theory and signal processing.

---

### Knowledge Points

---

#### 1. Area Between Curves

**Formula:** The area between $y = f(x)$ (upper) and $y = g(x)$ (lower) on $[a,b]$:
$$A = \int_a^b [f(x) - g(x)]\,dx$$

**Finding the limits:** Intersections occur where $f(x) = g(x)$; solve to find $a$ and $b$.

**Example 1:** Area between $y = x$ and $y = x^2$ on $[0,1]$:
$$A = \int_0^1(x - x^2)\,dx = \Big[\frac{x^2}{2} - \frac{x^3}{3}\Big]_0^1 = \frac{1}{2} - \frac{1}{3} = \frac{1}{6}$$

**Example 2:** Area between $y = 2x$ and $y = x^2$. Intersections: $x^2 = 2x \Rightarrow x = 0, 2$.
$$A = \int_0^2(2x - x^2)\,dx = \Big[x^2 - \frac{x^3}{3}\Big]_0^2 = 4 - \frac{8}{3} = \frac{4}{3}$$

---

#### 2. Volume by Cross-Section

**General principle:** If a solid has cross-sectional area $A(x)$ at position $x$:
$$V = \int_a^b A(x)\,dx$$

**Example — Square pyramid:** Base $L\times L$, height $h$. At height $x$ from apex, $A(x) = L^2(1-x/h)^2$:
$$V = L^2\int_0^h\!\left(1-\frac{x}{h}\right)^2\!dx = L^2\cdot\frac{h}{3} = \frac{L^2 h}{3}$$

**Example — Sphere of radius $r$:** At position $x$, $A(x) = \pi(r^2-x^2)$:
$$V = \pi\int_{-r}^{r}(r^2-x^2)\,dx = \pi\Big[r^2 x - \frac{x^3}{3}\Big]_{-r}^r = \frac{4\pi r^3}{3}$$

---

#### 3. Disk and Washer Methods

**Disk method** (revolving $y = f(x) \geq 0$ about the $x$-axis):
$$V = \pi\int_a^b [f(x)]^2\,dx$$

**Washer method** (revolving the region between $y = R(x)$ and $y = r(x)$):
$$V = \pi\int_a^b\!\left([R(x)]^2 - [r(x)]^2\right)dx$$

**Example — Disk:** $y = \sqrt{x}$, $x\in[0,4]$, revolved about $x$-axis:
$$V = \pi\int_0^4 x\,dx = \pi\cdot 8 = 8\pi$$

**Example — Washer:** Region between $y = x$ (outer) and $y = x^2$ (inner), $x\in[0,1]$, revolved about $x$-axis:
$$V = \pi\int_0^1(x^2 - x^4)\,dx = \pi\!\left[\frac{x^3}{3}-\frac{x^5}{5}\right]_0^1 = \frac{2\pi}{15}$$

---

#### 4. Shell Method

**Formula** (revolving the region under $y = f(x) \geq 0$ on $[a,b]$ about the axis $x = L$):
$$V = 2\pi\int_a^b |x - L|\,f(x)\,dx$$

For rotation about the $y$-axis ($L = 0$): $V = 2\pi\int_a^b x\,f(x)\,dx$.

**Example:** $y = \sqrt{x}$, $x\in[0,4]$, revolved about $x = -1$:
$$V = 2\pi\int_0^4(x+1)\sqrt{x}\,dx = 2\pi\left[\frac{2x^{5/2}}{5}+\frac{2x^{3/2}}{3}\right]_0^4 = \frac{544\pi}{15}$$

**Pappus's Theorem:** For a plane region of area $A$ with centroid at distance $\bar d$ from the axis of revolution:
$$V = 2\pi\bar{d}\,A$$

**Example (Pappus):** Torus formed by rotating the unit disk centered at $(4,0)$ about the $y$-axis: $V = 2\pi\cdot 4\cdot\pi = 8\pi^2$.

---

#### 5. Arc Length

**Derivation:** Approximate the curve on $[x_{i-1},x_i]$ by a chord; chord length $\approx\sqrt{1+[f'(x_i^*)]^2}\,\Delta x_i$. Sum and take $\|P\|\to0$:
$$L = \int_a^b\sqrt{1 + [f'(x)]^2}\,dx$$

**Example — Cone surface generator:** $y = \frac{r}{h}x$ on $[0,h]$: $L = \sqrt{h^2+r^2}$ (slant height). ✓

**Note:** Arc length integrals often require trig substitution (Lecture 3) — e.g. $\sqrt{1+(r/h)^2} = \ell/h$ where $\ell$ is the slant height.

---

#### 6. Surface Area of Revolution

Rotating $y = f(x) \geq 0$ about the $x$-axis:
$$S = 2\pi\int_a^b f(x)\sqrt{1 + [f'(x)]^2}\,dx$$

**Example — Cone lateral surface:** $y = \frac{r}{h}x$, $x\in[0,h]$:
$$S = 2\pi\int_0^h\frac{r}{h}x\cdot\frac{\ell}{h}\,dx = \frac{2\pi r\ell}{h^2}\cdot\frac{h^2}{2} = \pi r\ell$$
where $\ell = \sqrt{h^2+r^2}$ is the slant height. ✓

**Example — Sphere:** $y = \sqrt{r^2-x^2}$, $f'(x) = -x/\sqrt{r^2-x^2}$, so $\sqrt{1+(f')^2} = r/\sqrt{r^2-x^2}$:
$$S = 2\pi\int_{-r}^r\sqrt{r^2-x^2}\cdot\frac{r}{\sqrt{r^2-x^2}}\,dx = 2\pi r\cdot 2r = 4\pi r^2 \checkmark$$

---

#### 7. Center of Mass

For a rod on $[a,b]$ with linear density $\delta(x)$:
$$M = \int_a^b\delta(x)\,dx \quad\text{(total mass)}, \qquad M_0 = \int_a^b x\,\delta(x)\,dx \quad\text{(first moment)}$$
$$\bar x = \frac{M_0}{M} \quad\text{(center of mass)}$$

**Example:** $\delta(x) = 3x^2$ on $[0,2]$:
$$M = \int_0^2 3x^2\,dx = \Big[x^3\Big]_0^2 = 8, \quad M_0 = \int_0^2 3x^3\,dx = \Big[\frac{3x^4}{4}\Big]_0^2 = 12, \quad \bar x = \frac{12}{8} = \frac{3}{2}$$

---

#### 8. Natural Logarithm as an Integral

**Definition via integration:**
$$\ln x = \int_1^x \frac{1}{t}\,dt, \quad x > 0$$

This definition makes $(\ln x)' = 1/x$ immediate by FTC Part 1, and allows rigorous derivation of all logarithm properties:
- $\ln(ab) = \ln a + \ln b$ (from additivity of the integral over $[1,a]$ and $[a,ab]$)
- $\ln(1) = 0$ (empty integral)
- $\ln(1/x) = -\ln x$

---

#### 9. The Exponential Function

**Definition:** $\exp$ is the inverse of $\ln$, i.e. $e^x = \exp(x)$ satisfies $\ln(e^x) = x$.

**Differentiation:** Differentiating $\ln(e^x) = x$ implicitly: $\frac{(e^x)'}{e^x} = 1$, so $(e^x)' = e^x$.

**Consequence:** $\int e^x\,dx = e^x + C$.

---

#### 10. The Gamma Function — Definition

**Definition:**
$$\Gamma(x) = \int_0^\infty t^{x-1}e^{-t}\,dt, \quad x > 0$$

This is a Type I improper integral (infinite upper limit) that also has a Type II singularity at $t = 0$ for $x < 1$. It converges for all $x > 0$.

**Why define it?** The Gamma function extends the factorial to non-integer arguments and appears in:
- Laplace transforms of $t^\alpha$ for non-integer $\alpha$ (Week 14)
- Bessel functions (Week 13)
- Probability distributions (Chi-squared, Student's $t$, $F$-distributions)
- Signal processing and fractional calculus

---

#### 11. Gamma Function — Key Properties

**Recurrence relation:**
$$\Gamma(x+1) = x\,\Gamma(x)$$

**Proof:** IBP with $u = t^x$, $dv = e^{-t}\,dt$, $v = -e^{-t}$:
$$\Gamma(x+1) = \Big[-t^x e^{-t}\Big]_0^\infty + x\int_0^\infty t^{x-1}e^{-t}\,dt = 0 + x\,\Gamma(x)$$
(The boundary term vanishes: $t^x e^{-t}\to0$ as $t\to\infty$ and as $t\to0^+$ for $x>0$.)

**Connection to factorials:** $\Gamma(1) = \int_0^\infty e^{-t}\,dt = 1$, and by recurrence:
$$\Gamma(n+1) = n! \quad \text{for } n = 0,1,2,\ldots$$

**Special value:** $\Gamma(1/2) = \sqrt{\pi}$ (proved via the Gaussian integral — see §13 below).

**From recurrence:** $\Gamma(3/2) = \frac{1}{2}\Gamma(1/2) = \dfrac{\sqrt{\pi}}{2}$, $\quad\Gamma(5/2) = \dfrac{3\sqrt{\pi}}{4}$.

**Laplace transform connection (forward link to Week 14):**
$$\mathcal{L}\{t^n\} = \frac{n!}{s^{n+1}}, \quad \mathcal{L}\{t^{1/2}\} = \frac{\Gamma(3/2)}{s^{3/2}} = \frac{\sqrt{\pi}}{2s^{3/2}}$$

---

#### 12. Gabriel's Horn — Finite Volume, Infinite Surface Area

**Setup (Torricelli, 1643):** Rotate $y = 1/x$, $x \geq 1$, about the $x$-axis.

**Volume (disk method):**
$$V = \pi\int_1^\infty x^{-2}\,dx = \pi\lim_{b\to\infty}\Big[-\frac{1}{x}\Big]_1^b = \pi$$
Converges because $p = 2 > 1$ (p-test Type I).

**Surface area (lower bound via Comparison Test — divergence direction):**
$$S = 2\pi\int_1^\infty\frac{1}{x}\sqrt{1 + x^{-4}}\,dx \geq 2\pi\int_1^\infty\frac{dx}{x} = \infty$$
Since $\sqrt{1+x^{-4}} \geq 1$, the Comparison Test (divergence direction) applies: the integrand is bounded below by $1/x$, and $\int_1^\infty x^{-1}\,dx$ diverges ($p = 1$). *(This is why the divergence direction of the Comparison Test, stated in §11 above, must be established before this result.)*

**Torricelli's paradox:** The horn can be filled with $\pi$ units of paint, yet its inner wall cannot be coated with any finite amount of paint — a celebrated paradox in the history of calculus.

---

#### 13. The Gaussian Integral — $\int_{-\infty}^{\infty} e^{-x^2}\,dx = \sqrt{\pi}$

**Proof via the Gamma function:**
Substitute $t = x^2$, $dt = 2x\,dx$, $dx = dt/(2\sqrt{t})$:
$$\int_0^\infty e^{-x^2}\,dx = \int_0^\infty e^{-t}\cdot\frac{dt}{2\sqrt{t}} = \frac{1}{2}\int_0^\infty t^{1/2-1}e^{-t}\,dt = \frac{1}{2}\,\Gamma\!\left(\frac{1}{2}\right) = \frac{\sqrt{\pi}}{2}$$

By the evenness of $e^{-x^2}$:
$$\int_{-\infty}^\infty e^{-x^2}\,dx = 2\cdot\frac{\sqrt{\pi}}{2} = \sqrt{\pi}$$

This proves $\Gamma(1/2) = \sqrt{\pi}$.

**Normal distribution:** For $\sigma > 0$, substitute $u = x/(\sigma\sqrt{2})$:
$$\int_{-\infty}^\infty e^{-x^2/(2\sigma^2)}\,dx = \sigma\sqrt{2}\int_{-\infty}^\infty e^{-u^2}\,du = \sigma\sqrt{2\pi}$$
This is the normalization constant of the Gaussian (normal) distribution in probability and statistics.

---

#### 14. Summary — Lecture 2

| Application | Formula |
|---|---|
| Area between curves | $\int_a^b[f(x)-g(x)]\,dx$ |
| Volume (cross-section) | $\int_a^b A(x)\,dx$ |
| Volume (disk) | $\pi\int_a^b[f(x)]^2\,dx$ |
| Volume (washer) | $\pi\int_a^b(R^2-r^2)\,dx$ |
| Volume (shell, about $y$-axis) | $2\pi\int_a^b x\,f(x)\,dx$ |
| Arc length | $\int_a^b\sqrt{1+[f'(x)]^2}\,dx$ |
| Surface area (rev. about $x$-axis) | $2\pi\int_a^b f(x)\sqrt{1+[f'(x)]^2}\,dx$ |
| Center of mass | $\bar x = \int x\,\delta\,dx \big/ \int\delta\,dx$ |
| Gamma recurrence | $\Gamma(x+1) = x\,\Gamma(x)$;\; $\Gamma(n+1)=n!$;\; $\Gamma(1/2)=\sqrt{\pi}$ |
| Gaussian integral | $\int_{-\infty}^\infty e^{-x^2}\,dx = \sqrt{\pi}$ |

---

## Lecture 3: Techniques of Integration

### Introduction

Many integrands resist u-substitution and IBP. This lecture builds a complete toolkit of **seven techniques**, ordered from simplest to most general:

1. **Completing the square** — algebraic rewriting; prerequisite tool for the others.
2. **Partial fractions** — decomposes rational functions; guaranteed by the Fundamental Theorem of Algebra.
3. **Trigonometric integrals** — $\int\sin^m\cos^n\,dx$ and $\int\tan^m\sec^n\,dx$; arise as intermediate steps in trig substitution.
4. **Reduction formulas** — lower the power systematically via IBP; close the gap for PFD Case 4.
5. **Trigonometric substitution** — eliminates $\sqrt{a^2\pm x^2}$, $\sqrt{x^2-a^2}$ via Pythagorean identities.
6. **Euler substitutions** — rationalizes any $\int R(x,\sqrt{ax^2+bx+c})\,dx$; more general than trig sub.
7. **Weierstrass substitution** $t=\tan(x/2)$ — converts any $\int R(\sin x,\cos x)\,dx$ into a rational function.

**Why it matters:** Partial fractions is indispensable for inverse Laplace transforms (Week 14). Trig substitution appears in arc length and surface area integrals (Lecture 2). Euler and Weierstrass are the last-resort methods that guarantee rationalization.

---

### Knowledge Points

---

#### 1. Completing the Square — Method

**For $ax^2 + bx + c$:**
$$ax^2 + bx + c = a\!\left(x + \frac{b}{2a}\right)^2 + \left(c - \frac{b^2}{4a}\right)$$

**Steps:** (1) Factor out $a$. (2) Add and subtract $(b/2a)^2$ inside. (3) Identify the perfect square and remainder.

**Examples:**

| Original | Completed form |
|----------|---------------|
| $x^2 + 6x + 10$ | $(x+3)^2 + 1$ |
| $x^2 - 4x + 7$ | $(x-2)^2 + 3$ |
| $2x^2 + 4x + 6$ | $2(x+1)^2 + 4$ |
| $-x^2 + 2x + 3$ | $-(x-1)^2 + 4$ |

---

#### 2. Completing the Square — Applied to Integration

**Standard results** (with $u = x + p$, $a^2 = q > 0$):

$$\int \frac{dx}{(x+p)^2 + a^2} = \frac{1}{a}\arctan\!\frac{x+p}{a} + C$$
$$\int \frac{(x+p)\,dx}{(x+p)^2+a^2} = \frac{1}{2}\ln\!\left[(x+p)^2+a^2\right] + C$$

**Example 1:** $\displaystyle\int \frac{dx}{x^2+4x+8} = \int\frac{dx}{(x+2)^2+4} = \frac{1}{2}\arctan\!\frac{x+2}{2} + C$

**Example 2:** $\displaystyle\int \frac{2x+3}{x^2+4x+8}\,dx$. Split: $2x+3 = 2(x+2) - 1$:
$$= \ln\!\left[(x+2)^2+4\right] - \frac{1}{2}\arctan\!\frac{x+2}{2} + C$$

---

#### 3. Rational Functions and Partial Fractions — Motivation

**Problem:** Rational functions $P(x)/Q(x)$ arise in inverse Laplace transforms and circuit analysis. Direct integration is usually impossible, but **partial fraction decomposition** breaks them into integrable pieces.

**Key step 0:** If $\deg P \geq \deg Q$, perform **polynomial long division** first:
$$\frac{P(x)}{Q(x)} = S(x) + \frac{R(x)}{Q(x)}, \quad \deg R < \deg Q$$

**Example:** $\dfrac{x^3}{x^2-1}$: quotient $x$, remainder $x$ → $\dfrac{x^3}{x^2-1} = x + \dfrac{x}{x^2-1}$.

---

#### 4. Factoring the Denominator — the Fundamental Theorem of Algebra

**Theorem (FTA):** Every degree-$n$ polynomial has exactly $n$ roots in $\mathbb{C}$ (counted with multiplicity). For real polynomials, complex roots come in conjugate pairs $\alpha \pm\beta i$, whose product $(x-\alpha)^2+\beta^2$ is an irreducible real quadratic.

Therefore every $Q(x)\in\mathbb{R}[x]$ factors completely over $\mathbb{R}$ into:
- **Linear factors:** $(x-r)^m$, $r$ a real root, multiplicity $m$
- **Irreducible quadratic factors:** $(x^2+bx+c)^m$ (monic form; general: $ax^2+bx+c$ with discriminant $b^2-4ac < 0$)

The partial fraction decomposition is **unique**.

---

#### 5. Case 1 — Distinct Linear Factors

**Form:** $Q(x) = (x-r_1)\cdots(x-r_n)$, all $r_i$ distinct:
$$\frac{P(x)}{Q(x)} = \frac{A_1}{x-r_1} + \cdots + \frac{A_n}{x-r_n}$$

**Cover-up method:** Multiply by $(x-r_i)$ and set $x = r_i$.

**Example:** $\displaystyle\int \frac{3x+1}{(x-1)(x+2)}\,dx$

Cover-up: $A = \frac{4}{3}$, $B = \frac{5}{3}$. Result: $\dfrac{4}{3}\ln|x-1| + \dfrac{5}{3}\ln|x+2| + C$.

---

#### 6. Case 2 — Repeated Linear Factors

**Form:** $(x-r)^m$ contributes $\dfrac{A_1}{x-r} + \dfrac{A_2}{(x-r)^2} + \cdots + \dfrac{A_m}{(x-r)^m}$.

**Integration:** $\displaystyle\int \frac{A}{(x-r)^k}\,dx = \frac{A}{(1-k)(x-r)^{k-1}} + C$ for $k \geq 2$.

**Example:** $\displaystyle\int \frac{x+3}{(x-1)^2(x+2)}\,dx$

Cover-up: $B = 4/3$, $C = 1/9$; coefficient comparison: $A = -1/9$.
$$= -\frac{1}{9}\ln|x-1| - \frac{4}{3(x-1)} + \frac{1}{9}\ln|x+2| + C$$

---

#### 7. Case 3 — Irreducible Quadratic Factors

**Recognition:** $ax^2 + bx + c$ is irreducible when $b^2 - 4ac < 0$.

**Form:** Each distinct irreducible quadratic $(ax^2+bx+c)$ contributes $\dfrac{Ax+B}{ax^2+bx+c}$.

**Key integrals:**
$$\int \frac{dx}{x^2+a^2} = \frac{1}{a}\arctan\!\frac{x}{a} + C, \qquad \int \frac{x\,dx}{x^2+a^2} = \frac{1}{2}\ln(x^2+a^2) + C$$

**Example:** $\displaystyle\int \frac{2x+3}{(x-1)(x^2+4)}\,dx$

$A = 1$, $B = -1$, $C = 1$. Result: $\ln|x-1| - \frac{1}{2}\ln(x^2+4) + \frac{1}{2}\arctan\frac{x}{2} + C$.

---

#### 8. Case 4 — Repeated Irreducible Quadratic Factors

**Form:** $(x^2+bx+c)^m$ contributes $\displaystyle\sum_{k=1}^m \frac{A_k x+B_k}{(x^2+bx+c)^k}$.

**Engineering relevance:** Appears when Laplace denominators have complex double poles — e.g. $\mathcal{L}\{t\sin(\omega t)\}$ involves $1/(s^2+\omega^2)^2$. The integral $\int dx/(x^2+a^2)^n$ is handled by the reduction formula in §12.

---

#### 9. Complete Worked Example

**Integrate:** $\displaystyle\int \frac{x^3 - x + 1}{x^2 + x - 2}\,dx$

**Step 1 — Long division** (degree 3 > 2):
$$x^3-x+1 = (x-1)(x^2+x-2) + (2x-1) \quad\Rightarrow\quad \frac{x^3-x+1}{x^2+x-2} = x-1+\frac{2x-1}{x^2+x-2}$$

**Step 2 — Factor:** $x^2+x-2 = (x+2)(x-1)$.

**Step 3 — PFD:** $A = 5/3$, $B = 1/3$.

**Step 4 — Integrate:**
$$\frac{x^2}{2} - x + \frac{5}{3}\ln|x+2| + \frac{1}{3}\ln|x-1| + C$$

---

#### 10. Connection to Inverse Laplace Transforms (Forward Link to Week 14)

Completing the square plus partial fractions is the exact toolchain for computing $\mathcal{L}^{-1}\{F(s)\}$:

**Preview:** $\mathcal{L}^{-1}\!\left\{\dfrac{1}{s^2+2s+5}\right\}$: complete the square, $s^2+2s+5=(s+1)^2+4$:
$$= \frac{1}{2}\,e^{-t}\sin(2t)$$

**Preview:** $\mathcal{L}^{-1}\!\left\{\dfrac{s+1}{(s+1)^2+4}\right\} = e^{-t}\cos(2t)$.

---

#### 11. Trigonometric Integrals — $\int\sin^m x\cos^n x\,dx$

**Strategy:**

| Condition | Strategy |
|---|---|
| $m$ odd | Factor $\sin x$, write $\sin^{m-1}x = (1-\cos^2 x)^{(m-1)/2}$, substitute $u = \cos x$ |
| $n$ odd | Factor $\cos x$, write $\cos^{n-1}x = (1-\sin^2 x)^{(n-1)/2}$, substitute $u = \sin x$ |
| Both even | Apply $\sin^2 x = \frac{1-\cos2x}{2}$, $\cos^2 x = \frac{1+\cos2x}{2}$, repeat |

**Example — one odd power:** $\displaystyle\int\sin^3 x\cos^2 x\,dx$

Factor $\sin x$: $\int(1-\cos^2 x)\cos^2 x\sin x\,dx$. Let $u=\cos x$: $\int(u^2-1)u^2\,(-du) = -\frac{u^3}{3}+\frac{u^5}{5}+C = -\frac{\cos^3 x}{3}+\frac{\cos^5 x}{5}+C$.

**Example — both even:** $\displaystyle\int\sin^2 x\cos^2 x\,dx = \int\frac{1-\cos4x}{8}\,dx = \frac{x}{8}-\frac{\sin4x}{32}+C$

---

#### 12. Trigonometric Integrals — $\int\tan^m x\sec^n x\,dx$

| Condition | Strategy |
|---|---|
| $n$ even | Factor $\sec^2 x$, write remaining $\sec$ in terms of $\tan$, substitute $u=\tan x$ |
| $m$ odd | Factor $\sec x\tan x$, write remaining $\tan$ in terms of $\sec$, substitute $u=\sec x$ |

**Example — $n$ even:** $\displaystyle\int\tan^2 x\sec^4 x\,dx$. Write $\sec^4 x = (1+\tan^2 x)\sec^2 x$, $u=\tan x$:
$$\int u^2(1+u^2)\,du = \frac{\tan^3 x}{3}+\frac{\tan^5 x}{5}+C$$

**Example — $m$ odd:** $\displaystyle\int\tan^3 x\sec x\,dx$. Write $\tan^2 x = \sec^2 x-1$, $u=\sec x$:
$$\int(u^2-1)\,du = \frac{\sec^3 x}{3}-\sec x+C$$

---

#### 13. Reduction Formulas — $\int\sin^n x\,dx$ and $\int\cos^n x\,dx$

$$\int\sin^n x\,dx = -\frac{\sin^{n-1}x\cos x}{n}+\frac{n-1}{n}\int\sin^{n-2}x\,dx$$
$$\int\cos^n x\,dx = \frac{\cos^{n-1}x\sin x}{n}+\frac{n-1}{n}\int\cos^{n-2}x\,dx$$

**Proof (sine):** IBP with $u = \sin^{n-1}x$, $dv = \sin x\,dx$; use $\cos^2 x = 1-\sin^2 x$ and solve for the integral.

**Example:** $\displaystyle\int\sin^4 x\,dx$. Apply twice ($n=4$, then $n=2$):
$$= -\frac{\sin^3 x\cos x}{4}+\frac{3x}{8}-\frac{3\sin2x}{16}+C$$

---

#### 14. Reduction Formula — $\int\sec^n x\,dx$

$$\int\sec^n x\,dx = \frac{\sec^{n-2}x\tan x}{n-1}+\frac{n-2}{n-1}\int\sec^{n-2}x\,dx$$

**Classic result** ($n=3$):
$$\int\sec^3 x\,dx = \frac{\sec x\tan x + \ln|\sec x+\tan x|}{2}+C$$

**Why it matters:** Every trig substitution $x = a\tan\theta$ involving $\sqrt{a^2+x^2}$ to an odd power eventually requires $\int\sec^3\theta\,d\theta$.

---

#### 15. Reduction Formula — $\int\frac{dx}{(x^2+a^2)^n}$ (Closes PFD Case 4)

$$\int\frac{dx}{(x^2+a^2)^n} = \frac{x}{2a^2(n-1)(x^2+a^2)^{n-1}}+\frac{2n-3}{2a^2(n-1)}\int\frac{dx}{(x^2+a^2)^{n-1}}$$

**Example** ($n=2$, $a=1$):
$$\int\frac{dx}{(x^2+1)^2} = \frac{x}{2(x^2+1)}+\frac{1}{2}\arctan x+C$$

---

#### 16. Trigonometric Substitution — Three Patterns

| Radical form | Substitution | Range | Identity used |
|---|---|---|---|
| $\sqrt{a^2-x^2}$ | $x = a\sin\theta$ | $\theta\in[-\pi/2,\pi/2]$ | $1-\sin^2\theta=\cos^2\theta$ |
| $\sqrt{a^2+x^2}$ | $x = a\tan\theta$ | $\theta\in(-\pi/2,\pi/2)$ | $1+\tan^2\theta=\sec^2\theta$ |
| $\sqrt{x^2-a^2}$ | $x = a\sec\theta$ | $\theta\in[0,\tfrac{\pi}{2})\cup(\tfrac{\pi}{2},\pi]$ | $\sec^2\theta-1=\tan^2\theta$ |

*Note on the sec range: $\theta\in[0,\pi/2)$ covers $x\geq a$; $\theta\in(\pi/2,\pi]$ covers $x\leq -a$. Both branches are needed for integrals over intervals crossing zero.*

**After integrating:** Use the reference triangle to convert all trig expressions back to $x$.

---

#### 17. Trig Substitution — Examples

**Pattern 1:** $\displaystyle\int\sqrt{4-x^2}\,dx$, $x=2\sin\theta$:
$$= 2\arcsin\frac{x}{2} + \frac{x\sqrt{4-x^2}}{2} + C$$

**Pattern 2:** $\displaystyle\int\frac{dx}{\sqrt{x^2+1}}$, $x=\tan\theta$:
$$\int\sec\theta\,d\theta = \ln|x+\sqrt{x^2+1}| + C$$
*(equals $\sinh^{-1}x + C$)*

**Pattern 3:** $\displaystyle\int\frac{\sqrt{x^2-9}}{x}\,dx$, $x=3\sec\theta$:
$$= \sqrt{x^2-9} - 3\,\text{arcsec}\frac{x}{3} + C$$

**Combined with completing the square:** $\displaystyle\int\frac{dx}{\sqrt{-x^2+4x-3}}$

Complete: $-x^2+4x-3 = 1-(x-2)^2$. Let $u=x-2$: Pattern 1 with $a=1$ gives $\arcsin(x-2)+C$.

---

#### 18. Euler Substitutions — Three Types

For integrals of the form $\int R\!\left(x, \sqrt{ax^2+bx+c}\right)dx$, Euler substitutions rationalize the radical algebraically:

| Type | Condition | Substitution | Resulting expression for $t$ |
|---|---|---|---|
| 1 | $a > 0$ | $\sqrt{ax^2+bx+c} = t - \sqrt{a}\,x$ | $t = \sqrt{a}\,x + \sqrt{ax^2+bx+c}$ |
| 2 | $c > 0$ | $\sqrt{ax^2+bx+c} = tx + \sqrt{c}$ | $t = \dfrac{\sqrt{ax^2+bx+c}-\sqrt{c}}{x}$ |
| 3 | Two real roots $r,s$ | $\sqrt{a(x-r)(x-s)} = t(x-r)$ | $t = \dfrac{\sqrt{ax^2+bx+c}}{x-r}$ |

**Key idea:** In each case, squaring both sides gives a *linear* equation in $x$, so $x$, $dx$, and $\sqrt{\cdots}$ are all expressed as rational functions of $t$. The result is then handled by partial fractions.

**Scope:** Applies to *any* quadratic radicand — more general than trig substitution, which first requires completing the square to a perfect square plus a constant.

---

#### 19. Euler Type 1 Example

**Integrate** $\displaystyle\int\frac{dx}{\sqrt{x^2+x+1}}$ using Type 1 ($a=1>0$).

Set $\sqrt{x^2+x+1} = t - x$. Squaring: $x^2+x+1 = t^2-2tx+x^2$, so $x+1 = t^2-2tx$:
$$x = \frac{t^2-1}{1+2t}, \qquad dx = \frac{2(t^2+t+1)}{(1+2t)^2}\,dt, \qquad \sqrt{x^2+x+1} = \frac{t^2+t+1}{1+2t}$$

Substituting:
$$\int\frac{2(t^2+t+1)/(1+2t)^2}{(t^2+t+1)/(1+2t)}\,dt = \int\frac{2}{1+2t}\,dt = \ln|1+2t|+C$$

Back-substitute $t = x+\sqrt{x^2+x+1}$:
$$\int\frac{dx}{\sqrt{x^2+x+1}} = \ln\!\left|1+2x+2\sqrt{x^2+x+1}\right|+C$$

---

#### 20. Weierstrass Substitution — $t = \tan(x/2)$

**Setup:** Set $t = \tan\dfrac{x}{2}$. Then:
$$\sin x = \frac{2t}{1+t^2}, \qquad \cos x = \frac{1-t^2}{1+t^2}, \qquad dx = \frac{2\,dt}{1+t^2}$$

**Effect:** Any rational function $\int R(\sin x, \cos x)\,dx$ becomes a rational function of $t$, then handled by partial fractions. It is the *last resort* that always works when all other trig methods fail.

**Example:** $\displaystyle\int\frac{dx}{1+\sin x}$. Then $1+\sin x = (1+t)^2/(1+t^2)$:
$$\int\frac{2/(1+t^2)}{(1+t)^2/(1+t^2)}\,dt = \int\frac{2}{(1+t)^2}\,dt = -\frac{2}{1+\tan(x/2)}+C$$

**Engineering application:** For $a > |b| > 0$, split $[0,2\pi]$ at $\theta=\pi$ (where $\tan(\theta/2)\to\pm\infty$):
$$\int_0^{2\pi}\frac{d\theta}{a+b\cos\theta} = \frac{2\pi}{\sqrt{a^2-b^2}}$$
This result appears in Poisson's integral formula and the Nyquist stability criterion.

**Caveat:** $\tan(x/2)\to\pm\infty$ as $x\to\pi^\pm$. For definite integrals over a full period $[0,2\pi]$, the interval must be split at $x=\pi$ and both pieces treated as improper integrals. They combine cleanly but the step must not be omitted.

---

#### 21. Summary — Lecture 3

**Completing the square:** $ax^2+bx+c = a(x+p)^2+q$ where $p=b/(2a)$, $q=c-b^2/(4a)$.

**PFD cases:**

| Factor type in $Q(x)$ | Partial fraction form |
|---|---|
| $(x-r)$ | $\dfrac{A}{x-r}$ |
| $(x-r)^m$ | $\displaystyle\sum_{k=1}^m\dfrac{A_k}{(x-r)^k}$ |
| $(x^2+bx+c)$, $\Delta<0$ | $\dfrac{Ax+B}{x^2+bx+c}$ |
| $(x^2+bx+c)^m$, $\Delta<0$ | $\displaystyle\sum_{k=1}^m\dfrac{A_kx+B_k}{(x^2+bx+c)^k}$ |

**Trig integrals:** For $\int\sin^m\cos^n$: one odd → factor & $u$-sub; both even → half-angle. For $\int\tan^m\sec^n$: $n$ even → $u=\tan$; $m$ odd → $u=\sec$.

**Reduction formulas:** $\int\sin^n$, $\int\sec^n$, $\int dx/(x^2+a^2)^n$ — each reduces to a lower power.

**Trig substitution:** $\sqrt{a^2-x^2}\to a\sin\theta$; $\sqrt{a^2+x^2}\to a\tan\theta$; $\sqrt{x^2-a^2}\to a\sec\theta$.

**Euler:** Type 1 ($a>0$), Type 2 ($c>0$), Type 3 (two real roots) — always rationalizes $\sqrt{ax^2+bx+c}$.

**Weierstrass** $t=\tan(x/2)$: $\sin x=2t/(1+t^2)$, $\cos x=(1-t^2)/(1+t^2)$, $dx=2\,dt/(1+t^2)$ — last resort.

---

## Practice Session

**Theme:** Improper integrals; geometric applications; complete integration techniques.

---

### Practice Problems

**Set A — Improper Integrals**

1. Evaluate $\displaystyle\int_0^\infty xe^{-x}\,dx$ using IBP. *(Answer: 1)*
2. Determine convergence/divergence of $\displaystyle\int_1^\infty \frac{x}{1+x^3}\,dx$ using the Comparison Test. *(Hint: $x/(1+x^3)\sim x^{-2}$)*
3. Show that $\displaystyle\int_0^1 \frac{\ln x}{\sqrt{x}}\,dx$ converges and find its value. *(Type II + IBP; answer: $-4$)*
4. Compute $\displaystyle\int_0^\infty t^4 e^{-t}\,dt$ using the Gamma function. *(Answer: $\Gamma(5) = 24$)*

**Set B — Applications of Integration**

5. Find the volume of the solid obtained by rotating $y = \sqrt{x}$, $y = 0$, $x = 4$ about the $x$-axis. *(Disk method; answer: $8\pi$)*
6. Find the volume when the region between $y = x^2$ and $y = x$ (first quadrant) is rotated about the $y$-axis. *(Shell method)*
7. Find the volume when $y = e^x$, $y = 0$, $x = 0$, $x = 1$ is rotated about $y = -1$. *(Washer method)*
8. Verify that a sphere of radius $r$ has volume $\frac{4}{3}\pi r^3$ using the disk method applied to $y = \sqrt{r^2-x^2}$.
9. Find the arc length of $y = \frac{2}{3}x^{3/2}$ from $x = 0$ to $x = 3$.
10. Find the surface area of revolution when $y = \sqrt{x}$, $x\in[0,4]$ is rotated about the $x$-axis.

**Set C — Integration Techniques (Mixed)**

11. $\displaystyle\int \frac{3x^2 - 2}{(x-1)(x^2+1)}\,dx$ *(PFD Cases 1 and 3)*
12. $\displaystyle\int \frac{dx}{x^2+6x+13}$ *(completing the square)*
13. $\displaystyle\int \frac{\sqrt{x^2-4}}{x}\,dx$ *(trig substitution, Pattern 3)*
14. $\displaystyle\int\sin^4 x\cos^3 x\,dx$ *(trig integrals: $m=4$ even, $n=3$ odd; substitute $u=\sin x$)*
15. $\displaystyle\int\tan^4 x\,dx$ *(trig integrals + reduction: write $\tan^4 x = \tan^2 x(\sec^2 x-1)$)*
16. $\displaystyle\int\sec^5 x\,dx$ *(sec reduction formula applied twice)*
17. $\displaystyle\int\frac{dx}{\sqrt{x^2+2x+2}}$ *(complete the square, then Euler Type 1 or trig sub)*
18. $\displaystyle\int\frac{d\theta}{2+\cos\theta}$ *(Weierstrass substitution)*
