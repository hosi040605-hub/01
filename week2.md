# Week 2 — Integration Theory & Techniques

**Course:** Engineering Mathematics 1
**Part:** I — Calculus Foundations (Review)
**Supplementary Material:** `02-1 eng_math_definite_integralsl.pdf`, `02-2 eng_math_applicaion_integral.pdf`

> **Forward links for this week:**
> - Partial Fractions → Week 14 (computing inverse Laplace transforms)
> - Completing the Square → Week 14 (irreducible quadratic denominators in the s-domain)
> - Improper Integrals → Week 14 (the definition of the Laplace transform requires convergence of ∫₀^∞)

---

## Lecture 1: Fundamental Theorem of Calculus, u-Substitution, and Integration by Parts

### Introduction

If differentiation asks *how fast is something changing*, integration asks *how much has accumulated*. The **Fundamental Theorem of Calculus** is the profound link between these two operations — it says that they are inverses of each other. This lecture establishes that bridge rigorously, then develops the two most essential integration techniques: **u-substitution** (the chain rule in reverse) and **integration by parts** (the product rule in reverse).

These two techniques, together with the basic antiderivative table, solve the majority of integrals encountered in engineering mathematics. Every subsequent technique in Weeks 2–3 and the Laplace transform method in Weeks 14–15 builds directly on this foundation.

**Why it matters in engineering:**
- Work done by a variable force, charge stored in a capacitor, energy dissipated in a resistor — all computed via definite integrals.
- Solving ODEs often requires computing integrals; u-substitution and IBP are the primary tools.
- The Laplace transform is itself an improper integral, requiring fluency with all integration techniques.

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

**Intuition:** The limit must be the same number regardless of how the partition is refined and regardless of where the sample points are chosen within each subinterval. This is a much stronger requirement than merely taking $n \to \infty$ with equal widths.

**Uniform partition as a special case:** If we require equal widths $\Delta x_i = (b-a)/n$ for all $i$, the condition $\|P\| \to 0$ reduces to $n \to \infty$. For continuous $f$, both approaches give the same integral — but the general definition applies even to non-uniform partitions, which arise naturally in numerical integration and in the proof of the FTC.

**Example:** Estimate $\int_0^1 x^2\,dx$ using the uniform partition with $n = 4$ and right-endpoint sample points:
$$\Delta x_i = 0.25 \text{ (uniform)}, \quad S = (0.25^2 + 0.5^2 + 0.75^2 + 1^2)\times 0.25 = 0.46875$$
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
$$g(x) = \int_a^x f(t)\,dt, \quad x \in [a,b]$$
Then $g$ is differentiable and $g'(x) = f(x)$.

**Intuition:** The rate of change of the accumulated area is simply the height of the function at that point. Adding a thin slice of width $dx$ and height $f(x)$ changes the area by $f(x)\,dx$.

**Geometric interpretation:** $g(x)$ is the "running area" from $a$ to $x$. Its slope at $x$ equals $f(x)$.

**Example 1:** $g(x) = \displaystyle\int_1^x \sin(t^2)\,dt$. Then $g'(x) = \sin(x^2)$.

**Example 2 (Chain Rule combined):** $g(x) = \displaystyle\int_1^{x^3} \sqrt{1+t}\,dt$.
$$g'(x) = \sqrt{1+x^3} \cdot 3x^2$$

**Example 3:** $g(x) = \displaystyle\int_x^5 e^{t^2}\,dt = -\int_5^x e^{t^2}\,dt$.
$$g'(x) = -e^{x^2}$$

---

#### 5. Fundamental Theorem of Calculus — Part 2

**Theorem (FTC Part 2):** If $f$ is continuous on $[a,b]$ and $F$ is any antiderivative of $f$, then:
$$\int_a^b f(x)\,dx = F(b) - F(a) \equiv \Big[F(x)\Big]_a^b$$

**Proof idea:** Define $g(x) = \int_a^x f(t)\,dt$. By FTC Part 1, $g'(x) = f(x)$, so $g$ is an antiderivative of $f$. Therefore $g(x) = F(x) + C$ for some constant $C$. Setting $x = a$: $g(a) = 0 = F(a) + C$, so $C = -F(a)$. At $x = b$: $g(b) = F(b) - F(a)$.

**Significance:** FTC Part 2 converts the hard problem of computing a limit of Riemann sums into the simple task of finding one antiderivative and evaluating it at two points.

**Example 1:** $\displaystyle\int_1^4 (3x^2 - 2x + 1)\,dx = \Big[x^3 - x^2 + x\Big]_1^4 = (64-16+4)-(1-1+1) = 52 - 1 = 51$

**Example 2:** $\displaystyle\int_0^{\pi/2} \cos x\,dx = \Big[\sin x\Big]_0^{\pi/2} = 1 - 0 = 1$

**Example 3:** $\displaystyle\int_1^e \frac{1}{x}\,dx = \Big[\ln x\Big]_1^e = 1 - 0 = 1$

---

#### 6. u-Substitution — Motivation

**The problem:** How do we integrate $\int 2x\cos(x^2)\,dx$? No rule in our basic table handles this directly.

**Key observation:** The integrand has the form $g'(x)\cdot f(g(x))$ — the derivative of an inner function multiplied by an outer function evaluated at the inner. This is the chain rule in reverse.

**Setup:** Let $u = x^2$. Then $du = 2x\,dx$, and the integral becomes:
$$\int 2x\cos(x^2)\,dx = \int \cos u\,du = \sin u + C = \sin(x^2) + C$$

**Verification:** $\frac{d}{dx}[\sin(x^2)] = \cos(x^2) \cdot 2x$ ✓

---

#### 7. u-Substitution — The Method

**Procedure for $\int f(g(x))g'(x)\,dx$:**
1. Choose $u = g(x)$ (the inner function).
2. Compute $du = g'(x)\,dx$.
3. Rewrite the entire integral in terms of $u$ (no $x$ should remain).
4. Integrate in $u$.
5. Back-substitute $u = g(x)$ to return to $x$.

**Choosing $u$:** Look for a function whose derivative also appears (possibly up to a constant factor). Common patterns:
- Exponent: $e^{x^2}$ → try $u = x^2$
- Inside trig: $\sin(3x+1)$ → try $u = 3x+1$
- Inside square root: $\sqrt{x^3+1}$ → try $u = x^3+1$
- Denominator: $1/(x^2+4)^3$ → try $u = x^2+4$

---

#### 8. u-Substitution — Indefinite Integral Examples

**Example 1:** $\displaystyle\int \frac{e^{\sqrt{x}}}{\sqrt{x}}\,dx$

Let $u = \sqrt{x}$, $du = \frac{1}{2\sqrt{x}}dx$, so $\frac{dx}{\sqrt{x}} = 2\,du$:
$$\int e^u \cdot 2\,du = 2e^u + C = 2e^{\sqrt{x}} + C$$

**Example 2:** $\displaystyle\int \tan x\,dx = \int \frac{\sin x}{\cos x}\,dx$

Let $u = \cos x$, $du = -\sin x\,dx$:
$$\int \frac{-du}{u} = -\ln|u| + C = -\ln|\cos x| + C = \ln|\sec x| + C$$

**Example 3:** $\displaystyle\int x^2\sqrt{x^3+1}\,dx$

Let $u = x^3+1$, $du = 3x^2\,dx$:
$$\frac{1}{3}\int \sqrt{u}\,du = \frac{1}{3}\cdot\frac{2}{3}u^{3/2} + C = \frac{2}{9}(x^3+1)^{3/2} + C$$

---

#### 9. u-Substitution — Definite Integrals

**Key rule:** When substituting in a **definite** integral, change the **limits** to $u$-values. Do not back-substitute.

**Procedure:** If $u = g(x)$, then:
- Lower limit: $x = a$ → $u = g(a)$
- Upper limit: $x = b$ → $u = g(b)$

**Example:** $\displaystyle\int_0^1 2xe^{x^2}\,dx$

Let $u = x^2$, $du = 2x\,dx$. New limits: $u(0) = 0$, $u(1) = 1$.
$$\int_0^1 e^u\,du = \Big[e^u\Big]_0^1 = e - 1$$

**Example:** $\displaystyle\int_0^{\pi/4} \frac{\sin x}{\cos^2 x}\,dx$

Let $u = \cos x$, $du = -\sin x\,dx$. Limits: $u(0) = 1$, $u(\pi/4) = 1/\sqrt{2}$.
$$\int_1^{1/\sqrt{2}} \frac{-du}{u^2} = \Big[\frac{1}{u}\Big]_1^{1/\sqrt{2}} = \sqrt{2} - 1$$

---

#### 10. Integration by Parts — Motivation

**The problem:** How do we integrate $\int x e^x\,dx$ or $\int x\ln x\,dx$? These are products of two functions, but u-substitution does not help because no inner function has its derivative nearby.

**Origin:** Start from the product rule:
$$\frac{d}{dx}[u(x)v(x)] = u'(x)v(x) + u(x)v'(x)$$

Integrate both sides:
$$u(x)v(x) = \int u'(x)v(x)\,dx + \int u(x)v'(x)\,dx$$

Rearranging:
$$\int u(x)v'(x)\,dx = u(x)v(x) - \int v(x)u'(x)\,dx$$

---

#### 11. Integration by Parts — Formula and LIATE Rule

**Formula:**
$$\int u\,dv = uv - \int v\,du$$

**How to use:** Choose one factor as $u$ (differentiate it) and the other as $dv$ (integrate it).

**LIATE Rule** for choosing $u$ (priority order, highest first):
- **L** — Logarithmic functions: $\ln x$, $\log x$
- **I** — Inverse trigonometric: $\arcsin x$, $\arctan x$
- **A** — Algebraic (polynomials): $x^n$
- **T** — Trigonometric: $\sin x$, $\cos x$
- **E** — Exponential: $e^x$, $a^x$

**Intuition:** Choose $u$ to be the factor that becomes *simpler* after differentiation; choose $dv$ to be the factor that can be *easily* integrated.

---

#### 12. Integration by Parts — Examples

**Example 1:** $\displaystyle\int x e^x\,dx$

LIATE: $u = x$ (A before E), $dv = e^x\,dx$
$$u = x,\ du = dx;\qquad v = e^x$$
$$\int xe^x\,dx = xe^x - \int e^x\,dx = xe^x - e^x + C = (x-1)e^x + C$$

**Example 2:** $\displaystyle\int x^2\sin x\,dx$

$u = x^2$, $dv = \sin x\,dx$, so $du = 2x\,dx$, $v = -\cos x$:
$$= -x^2\cos x + 2\int x\cos x\,dx$$
Apply IBP again: $u = x$, $dv = \cos x\,dx$, $v = \sin x$:
$$= -x^2\cos x + 2(x\sin x - \int\sin x\,dx) = -x^2\cos x + 2x\sin x + 2\cos x + C$$

**Example 3:** $\displaystyle\int \ln x\,dx$

LIATE: $u = \ln x$ (L first), $dv = dx$:
$$u = \ln x,\ du = \frac{1}{x}dx;\qquad v = x$$
$$\int \ln x\,dx = x\ln x - \int x\cdot\frac{1}{x}\,dx = x\ln x - x + C$$

---

#### 13. Cycling IBP and the Tabular Method

**Cycling (for $e^x$ times trig):** $\displaystyle\int e^x\sin x\,dx$

$u = \sin x$, $dv = e^x\,dx$, $v = e^x$:
$$= e^x\sin x - \int e^x\cos x\,dx$$
Apply IBP again: $u = \cos x$, $dv = e^x\,dx$:
$$= e^x\sin x - (e^x\cos x + \int e^x\sin x\,dx)$$

Let $I = \int e^x\sin x\,dx$: $\quad I = e^x\sin x - e^x\cos x - I \implies 2I = e^x(\sin x - \cos x)$
$$\int e^x\sin x\,dx = \frac{e^x(\sin x - \cos x)}{2} + C$$

**Tabular Method** (for polynomial × function): Repeatedly differentiate $u$ and integrate $dv$ in a table, multiplying diagonally with alternating signs.

For $\int x^3 e^x\,dx$:

| Sign | $u$ (differentiate) | $dv$ (integrate) |
|------|---------------------|-----------------|
| $+$ | $x^3$ | $e^x$ |
| $-$ | $3x^2$ | $e^x$ |
| $+$ | $6x$ | $e^x$ |
| $-$ | $6$ | $e^x$ |
| $+$ | $0$ | $e^x$ |

Result: $(x^3 - 3x^2 + 6x - 6)e^x + C$

---

#### 14. Definite Integral Version of IBP

$$\int_a^b u\,dv = \Big[uv\Big]_a^b - \int_a^b v\,du$$

**Example:** $\displaystyle\int_1^e x\ln x\,dx$

$u = \ln x$, $dv = x\,dx$, so $du = dx/x$, $v = x^2/2$:
$$= \Big[\frac{x^2\ln x}{2}\Big]_1^e - \int_1^e \frac{x^2}{2}\cdot\frac{1}{x}\,dx = \frac{e^2}{2} - \frac{1}{2}\int_1^e x\,dx = \frac{e^2}{2} - \frac{1}{2}\cdot\frac{e^2-1}{2} = \frac{e^2+1}{4}$$

---

#### 15. Summary — Lecture 1

**Decision flowchart for integration:**

```
Is there an obvious antiderivative from the table?
    YES → Apply directly
    NO  → Is there a composite function (inner/outer structure)?
              YES → Try u-substitution
              NO  → Is it a product of two different types?
                        YES → Try Integration by Parts (LIATE)
                        NO  → See Lectures 2–3 (partial fractions, trig sub)
```

**Key formulas:**
$$\text{FTC: } \int_a^b f(x)\,dx = F(b) - F(a)$$
$$\text{u-sub: } \int f(g(x))g'(x)\,dx = \int f(u)\,du$$
$$\text{IBP: } \int u\,dv = uv - \int v\,du$$

---

## Lecture 2: Partial Fractions and Completing the Square

### Introduction

Many integrals that appear in engineering — and virtually all **inverse Laplace transforms** — involve rational functions $P(x)/Q(x)$. Integrating these directly is usually impossible, but **partial fraction decomposition** breaks them into simpler pieces that are straightforward to integrate. **Completing the square** handles the irreducible quadratic pieces that arise, converting them into forms involving $\arctan$ or shifted exponentials.

These two techniques are inseparable from the Laplace transform method taught in Weeks 14–15. Every time a student computes $\mathcal{L}^{-1}\{F(s)\}$ from a rational function $F(s)$, they are using exactly what is covered in this lecture.

**Why it matters:**
- Inverse Laplace transforms of ODE solutions are always rational functions in $s$.
- Partial fractions appear in circuit analysis (transfer functions), control theory, and signal processing.
- Completing the square converts integrals involving $1/(s^2 + bs + c)$ into recognizable Laplace pairs.

---

### Knowledge Points

---

#### 1. Rational Functions — Proper vs. Improper

**Definition:** A **rational function** is $R(x) = P(x)/Q(x)$ where $P$ and $Q$ are polynomials.

- **Proper:** degree of $P$ < degree of $Q$ (e.g., $(x+1)/(x^2+3)$)
- **Improper:** degree of $P$ \geq degree of $Q$ (e.g., $(x^3+1)/(x^2-1)$)

**Key requirement:** Partial fraction decomposition applies only to **proper** rational functions.

**Step 0 — Polynomial Long Division:** If $R(x)$ is improper, divide first:
$$\frac{P(x)}{Q(x)} = S(x) + \frac{R(x)}{Q(x)}$$
where $S(x)$ is the quotient polynomial and $R(x)$ is the remainder (now proper).

**Example:** $\dfrac{x^3}{x^2 - 1}$: divide $x^3 \div (x^2-1)$ to get quotient $x$, remainder $x$:
$$\frac{x^3}{x^2-1} = x + \frac{x}{x^2-1}$$
Now decompose the proper part $\frac{x}{x^2-1}$.

---

#### 2. The Idea of Partial Fraction Decomposition

**Key theorem:** Every proper rational function $P(x)/Q(x)$ (with $Q$ fully factored over $\mathbb{R}$) can be written as a sum of simpler fractions.

The factors of $Q(x)$ over $\mathbb{R}$ come in two types:
1. **Linear factors:** $(x - r)$ where $r$ is a real root
2. **Irreducible quadratic factors:** $(x^2 + bx + c)$ where $b^2 - 4c < 0$ (no real roots)

Each factor type generates a specific partial fraction form. The decomposition is unique.

---

#### 3. Case 1 — Distinct Linear Factors

**Form:** If $Q(x) = (x-r_1)(x-r_2)\cdots(x-r_n)$ with all $r_i$ distinct:
$$\frac{P(x)}{Q(x)} = \frac{A_1}{x-r_1} + \frac{A_2}{x-r_2} + \cdots + \frac{A_n}{x-r_n}$$

**Finding coefficients — cover-up method:** Multiply both sides by $(x - r_i)$ and set $x = r_i$.

**Example:** $\displaystyle\int \frac{3x+1}{(x-1)(x+2)}\,dx$

$$\frac{3x+1}{(x-1)(x+2)} = \frac{A}{x-1} + \frac{B}{x+2}$$

Cover-up: $A = \frac{3(1)+1}{1+2} = \frac{4}{3}$, $B = \frac{3(-2)+1}{-2-1} = \frac{-5}{-3} = \frac{5}{3}$

$$\int \left(\frac{4/3}{x-1} + \frac{5/3}{x+2}\right)dx = \frac{4}{3}\ln|x-1| + \frac{5}{3}\ln|x+2| + C$$

---

#### 4. Case 2 — Repeated Linear Factors

**Form:** If $(x-r)^m$ is a factor of $Q(x)$:
$$\frac{A_1}{x-r} + \frac{A_2}{(x-r)^2} + \cdots + \frac{A_m}{(x-r)^m}$$

**Why extra terms?** Each power $(x-r)^k$ with $k \leq m$ independently contributes to the numerator. The cover-up method gives $A_m$ directly; other coefficients require substituting other values of $x$ or comparing coefficients.

**Integration of repeated factors:**
$$\int \frac{A}{(x-r)^k}\,dx = \frac{A}{(1-k)(x-r)^{k-1}} + C \quad (k \geq 2)$$

**Example:** $\displaystyle\int \frac{x+3}{(x-1)^2(x+2)}\,dx$

$$\frac{x+3}{(x-1)^2(x+2)} = \frac{A}{x-1} + \frac{B}{(x-1)^2} + \frac{C}{x+2}$$

Cover-up for $B$: multiply by $(x-1)^2$, set $x=1$: $B = \frac{4}{3}$

Cover-up for $C$: multiply by $(x+2)$, set $x=-2$: $C = \frac{1}{9}$

Compare $x^2$ coefficients (or set $x=0$) to find $A = -\frac{1}{9}$:
$$\int\left(\frac{-1/9}{x-1} + \frac{4/3}{(x-1)^2} + \frac{1/9}{x+2}\right)dx = -\frac{1}{9}\ln|x-1| - \frac{4}{3(x-1)} + \frac{1}{9}\ln|x+2| + C$$

---

#### 5. Case 3 — Irreducible Quadratic Factors

**Recognition:** $ax^2 + bx + c$ is irreducible over $\mathbb{R}$ when the discriminant $b^2 - 4ac < 0$.
*Examples:* $x^2 + 1$, $x^2 + 4$, $x^2 + 2x + 5$, $2x^2 + x + 3$.

**Form:** Each distinct irreducible quadratic factor $(ax^2+bx+c)$ contributes:
$$\frac{Ax + B}{ax^2+bx+c}$$

**Key integrals arising from Case 3:**
$$\int \frac{dx}{x^2+a^2} = \frac{1}{a}\arctan\!\left(\frac{x}{a}\right) + C$$
$$\int \frac{x\,dx}{x^2+a^2} = \frac{1}{2}\ln(x^2+a^2) + C$$

**Example:** $\displaystyle\int \frac{2x+3}{(x-1)(x^2+4)}\,dx$

$$\frac{2x+3}{(x-1)(x^2+4)} = \frac{A}{x-1} + \frac{Bx+C}{x^2+4}$$

$x=1$: $A = 5/5 = 1$. Expanding and comparing: $B = -1$, $C = -1$.

$$\int\!\left(\frac{1}{x-1} + \frac{-x-1}{x^2+4}\right)dx = \ln|x-1| - \frac{1}{2}\ln(x^2+4) - \frac{1}{2}\arctan\!\frac{x}{2} + C$$

---

#### 6. Case 4 — Repeated Irreducible Quadratic Factors

**Form:** If $(x^2+bx+c)^m$ appears in $Q(x)$:
$$\frac{A_1 x+B_1}{x^2+bx+c} + \frac{A_2 x+B_2}{(x^2+bx+c)^2} + \cdots + \frac{A_m x+B_m}{(x^2+bx+c)^m}$$

**Engineering relevance:** This case appears when a Laplace denominator has complex double poles — e.g., $\mathcal{L}\{t\sin(\omega t)\}$ involves $1/(s^2+\omega^2)^2$.

---

#### 7. General Algorithm for Partial Fraction Decomposition

**Complete procedure:**
1. If improper → perform polynomial long division first.
2. Fully factor $Q(x)$ over $\mathbb{R}$.
3. Write the partial fraction template based on the factor types.
4. Multiply both sides by $Q(x)$.
5. Find constants by: (a) cover-up method for linear factors, (b) comparing coefficients or substituting convenient values of $x$ for remaining constants.
6. Integrate each term using the standard results.

---

#### 8. Completing the Square — Motivation

**Problem:** The quadratic $x^2 + 4x + 8$ is irreducible (discriminant $= 16 - 32 < 0$) but does not match the form $x^2 + a^2$. We cannot directly use $\int dx/(x^2+a^2) = \frac{1}{a}\arctan(x/a)$.

**Solution:** Rewrite $x^2 + 4x + 8$ as $(x+2)^2 + 4$ — now it matches $(u^2+a^2)$ with $u = x+2$, $a = 2$.

---

#### 9. Completing the Square — The Method

**For $ax^2 + bx + c$:**

$$ax^2 + bx + c = a\!\left(x + \frac{b}{2a}\right)^2 + \left(c - \frac{b^2}{4a}\right)$$

**Steps:**
1. Factor out $a$ from the quadratic terms.
2. Inside the parenthesis, add and subtract $\left(\frac{b}{2a}\right)^2$.
3. Identify the perfect square and the constant remainder.

**Examples:**
| Original | Completed form |
|----------|---------------|
| $x^2 + 6x + 10$ | $(x+3)^2 + 1$ |
| $x^2 - 4x + 7$ | $(x-2)^2 + 3$ |
| $2x^2 + 4x + 6$ | $2(x+1)^2 + 4$ |
| $-x^2 + 2x + 3$ | $-(x-1)^2 + 4$ |

---

#### 10. Completing the Square — Applied to Integration

**Standard results after completing the square** (with $u = x + p$, $a^2 = q$):

$$\int \frac{dx}{(x+p)^2 + a^2} = \frac{1}{a}\arctan\!\frac{x+p}{a} + C$$

$$\int \frac{(x+p)\,dx}{(x+p)^2+a^2} = \frac{1}{2}\ln\!\left[(x+p)^2+a^2\right] + C$$

**Example 1:** $\displaystyle\int \frac{dx}{x^2+4x+8}$

Complete: $x^2+4x+8 = (x+2)^2+4$
$$\int\frac{dx}{(x+2)^2+4} = \frac{1}{2}\arctan\!\frac{x+2}{2} + C$$

**Example 2:** $\displaystyle\int \frac{2x+3}{x^2+4x+8}\,dx$

Split numerator: $2x+3 = 2(x+2) - 1$:
$$\int\frac{2(x+2)}{(x+2)^2+4}\,dx - \int\frac{dx}{(x+2)^2+4} = \ln\!\left[(x+2)^2+4\right] - \frac{1}{2}\arctan\!\frac{x+2}{2} + C$$

---

#### 11. Connection to Inverse Laplace Transforms (Forward Link to Week 14)

The same completing-the-square technique is used when computing inverse Laplace transforms of second-order systems with complex poles.

**Preview example:** Find $\mathcal{L}^{-1}\!\left\{\dfrac{1}{s^2+2s+5}\right\}$.

Complete the square in $s$: $s^2+2s+5 = (s+1)^2+4$

Use the Laplace pair $\mathcal{L}\{e^{-at}\sin(\omega t)\} = \dfrac{\omega}{(s+a)^2+\omega^2}$:
$$\mathcal{L}^{-1}\!\left\{\frac{1}{(s+1)^2+4}\right\} = \frac{1}{2}\,e^{-t}\sin(2t)$$

**Another preview:** $\mathcal{L}^{-1}\!\left\{\dfrac{s+1}{(s+1)^2+4}\right\} = e^{-t}\cos(2t)$

These examples show exactly why completing the square matters — it is not an abstract algebraic exercise, but a concrete computational tool for ODE solutions.

---

#### 12. Integrating Rational Functions — Complete Worked Example

**Integrate:** $\displaystyle\int \frac{x^3 - x + 1}{x^2 + x - 2}\,dx$

**Step 1 — Long division** (degree 3 > degree 2, so improper):
$$x^3 - x + 1 \div (x^2+x-2) = x - 1 + \frac{2x-1}{x^2+x-2}$$

**Step 2 — Factor denominator:** $x^2+x-2 = (x+2)(x-1)$

**Step 3 — Partial fractions on proper part:**
$$\frac{2x-1}{(x+2)(x-1)} = \frac{A}{x+2} + \frac{B}{x-1}$$
$A = \frac{2(-2)-1}{-2-1} = \frac{-5}{-3} = \frac{5}{3}$, $B = \frac{2(1)-1}{1+2} = \frac{1}{3}$

**Step 4 — Integrate:**
$$\int\!\left(x - 1 + \frac{5/3}{x+2} + \frac{1/3}{x-1}\right)dx = \frac{x^2}{2} - x + \frac{5}{3}\ln|x+2| + \frac{1}{3}\ln|x-1| + C$$

---

#### 13. Summary — Lecture 2

**Partial Fraction Cases:**

| Factor type in $Q(x)$ | Partial fraction form |
|-----------------------|----------------------|
| $(x-r)$ | $\dfrac{A}{x-r}$ |
| $(x-r)^m$ | $\dfrac{A_1}{x-r} + \cdots + \dfrac{A_m}{(x-r)^m}$ |
| $(x^2+bx+c)$, $\Delta<0$ | $\dfrac{Ax+B}{x^2+bx+c}$ |
| $(x^2+bx+c)^m$, $\Delta<0$ | $\sum_{k=1}^m \dfrac{A_k x+B_k}{(x^2+bx+c)^k}$ |

**Completing the square:** $ax^2+bx+c = a(x+p)^2+q$ where $p = b/2a$, $q = c - b^2/4a$.

**The connection:** Both techniques will appear again in Week 14 in the form of computing $\mathcal{L}^{-1}\{F(s)\}$ for rational $F$.

---

## Lecture 3: Trigonometric Substitution, Improper Integrals, and the Gamma Function

### Introduction

This lecture covers three topics that extend integration to situations the previous lectures cannot handle:

**Trigonometric substitution** resolves integrals involving square roots like $\sqrt{a^2-x^2}$, $\sqrt{a^2+x^2}$, and $\sqrt{x^2-a^2}$ — forms that arise constantly in geometry, mechanics, and electrostatics.

**Improper integrals** extend integration to unbounded intervals or integrands with singularities. They are essential for defining the Laplace transform ($\int_0^\infty e^{-st}f(t)\,dt$) and for probability distributions in engineering statistics.

**The Gamma function** generalizes the factorial to non-integer arguments and appears throughout engineering mathematics — in Bessel functions, probability distributions, and the Laplace transform of $t^n$.

---

### Knowledge Points

---

#### 1. Trigonometric Substitution — Motivation

**Problem:** $\displaystyle\int\sqrt{4 - x^2}\,dx$

Neither u-substitution nor IBP works cleanly. The difficulty is the square root of a difference involving $x^2$.

**Key insight:** If $x = 2\sin\theta$, then $4 - x^2 = 4 - 4\sin^2\theta = 4\cos^2\theta$, and $\sqrt{4-x^2} = 2\cos\theta$ — the square root disappears! The Pythagorean identities of trigonometry are precisely designed to eliminate these square roots.

**General principle:** Three radical forms each suggest one substitution, based on a right triangle.

---

#### 2. Pattern 1 — $\sqrt{a^2 - x^2}$: Substitution $x = a\sin\theta$

**Setup:** $x = a\sin\theta$, $dx = a\cos\theta\,d\theta$, $\theta \in [-\pi/2, \pi/2]$

$$\sqrt{a^2 - x^2} = \sqrt{a^2 - a^2\sin^2\theta} = a\cos\theta \quad (\cos\theta \geq 0 \text{ on } [-\pi/2,\pi/2])$$

**Reference triangle:**
- Hypotenuse $a$, opposite side $x$, adjacent side $\sqrt{a^2-x^2}$
- $\sin\theta = x/a$, $\cos\theta = \sqrt{a^2-x^2}/a$, $\tan\theta = x/\sqrt{a^2-x^2}$

**Example:** $\displaystyle\int\sqrt{4-x^2}\,dx$, $x = 2\sin\theta$:
$$\int 2\cos\theta \cdot 2\cos\theta\,d\theta = 4\int\cos^2\theta\,d\theta = 4\cdot\frac{\theta + \sin\theta\cos\theta}{2} + C$$
$$= 2\theta + 2\sin\theta\cos\theta + C = 2\arcsin\frac{x}{2} + \frac{x\sqrt{4-x^2}}{2} + C$$

*(Geometric interpretation: this is exactly the formula for the area of a circular sector plus triangle.)*

---

#### 3. Pattern 1 — Second Example

**Example:** $\displaystyle\int \frac{x^2}{\sqrt{9-x^2}}\,dx$, $x = 3\sin\theta$:

$$\int \frac{9\sin^2\theta}{3\cos\theta}\cdot 3\cos\theta\,d\theta = 9\int\sin^2\theta\,d\theta = \frac{9}{2}(\theta - \sin\theta\cos\theta) + C$$
$$= \frac{9}{2}\arcsin\frac{x}{3} - \frac{x\sqrt{9-x^2}}{2} + C$$

---

#### 4. Pattern 2 — $\sqrt{a^2 + x^2}$: Substitution $x = a\tan\theta$

**Setup:** $x = a\tan\theta$, $dx = a\sec^2\theta\,d\theta$, $\theta \in (-\pi/2, \pi/2)$

$$\sqrt{a^2 + x^2} = \sqrt{a^2 + a^2\tan^2\theta} = a\sec\theta \quad (\sec\theta > 0)$$

**Reference triangle:**
- $\tan\theta = x/a$, $\sec\theta = \sqrt{a^2+x^2}/a$

**Example:** $\displaystyle\int\frac{dx}{\sqrt{x^2+1}}$, $x = \tan\theta$:
$$\int\frac{\sec^2\theta}{\sec\theta}\,d\theta = \int\sec\theta\,d\theta = \ln|\sec\theta + \tan\theta| + C = \ln\!\left|x + \sqrt{x^2+1}\right| + C$$

*(Note: this equals $\sinh^{-1}(x) + C$ — connecting to Week 1's inverse hyperbolic derivatives!)*

**Example:** $\displaystyle\int\frac{dx}{(x^2+4)^{3/2}}$, $x = 2\tan\theta$:
$$\int\frac{2\sec^2\theta}{8\sec^3\theta}\,d\theta = \frac{1}{4}\int\cos\theta\,d\theta = \frac{\sin\theta}{4} + C = \frac{x}{4\sqrt{x^2+4}} + C$$

---

#### 5. Pattern 3 — $\sqrt{x^2 - a^2}$: Substitution $x = a\sec\theta$

**Setup:** $x = a\sec\theta$, $dx = a\sec\theta\tan\theta\,d\theta$, $\theta \in [0, \pi/2) \cup (\pi/2, \pi]$

$$\sqrt{x^2 - a^2} = a\tan\theta \quad (\tan\theta \geq 0 \text{ in first quadrant})$$

**Reference triangle:**
- $\sec\theta = x/a$, $\tan\theta = \sqrt{x^2-a^2}/a$

**Example:** $\displaystyle\int\frac{\sqrt{x^2-9}}{x}\,dx$, $x = 3\sec\theta$:
$$\int\frac{3\tan\theta}{3\sec\theta}\cdot 3\sec\theta\tan\theta\,d\theta = 3\int\tan^2\theta\,d\theta = 3(\tan\theta - \theta) + C = \sqrt{x^2-9} - 3\text{arcsec}\frac{x}{3} + C$$

---

#### 6. Trig Substitution Combined with Completing the Square

**When the quadratic is $ax^2 + bx + c$:** First complete the square to get $(x+p)^2 \pm q^2$, then substitute $u = x+p$ and apply the appropriate trig substitution.

**Example:** $\displaystyle\int\frac{dx}{\sqrt{-x^2+4x-3}}$

Complete the square: $-x^2+4x-3 = -(x^2-4x+3) = -((x-2)^2-1) = 1-(x-2)^2$

Let $u = x-2$: $\displaystyle\int\frac{du}{\sqrt{1-u^2}}$. This is Pattern 1 with $a=1$:
$$= \arcsin(u) + C = \arcsin(x-2) + C$$

---

#### 7. Summary of Trigonometric Substitution Patterns

| Radical form | Substitution | Identity used |
|-------------|--------------|--------------|
| $\sqrt{a^2-x^2}$ | $x = a\sin\theta$ | $1-\sin^2\theta = \cos^2\theta$ |
| $\sqrt{a^2+x^2}$ | $x = a\tan\theta$ | $1+\tan^2\theta = \sec^2\theta$ |
| $\sqrt{x^2-a^2}$ | $x = a\sec\theta$ | $\sec^2\theta-1 = \tan^2\theta$ |

**After integrating:** Use the reference triangle to convert all trig expressions back to $x$.

---

#### 8. Improper Integrals — Motivation

**The problem:** The definite integral $\int_a^b f(x)\,dx$ requires a *bounded* interval $[a,b]$ and a *bounded* function $f$. In engineering, we frequently need to integrate:
- Over an infinite range: $\int_0^\infty e^{-st}f(t)\,dt$ (Laplace transform — Week 14)
- Near a singularity: $\int_0^1 \frac{1}{\sqrt{x}}\,dx$ (integrand → ∞ as $x \to 0$)

**Definition:** These are called **improper integrals** and are evaluated using limits.

---

#### 9. Type I — Infinite Limits

**Definition:**
$$\int_a^\infty f(x)\,dx = \lim_{b\to\infty}\int_a^b f(x)\,dx$$
$$\int_{-\infty}^b f(x)\,dx = \lim_{a\to-\infty}\int_a^b f(x)\,dx$$
$$\int_{-\infty}^\infty f(x)\,dx = \int_{-\infty}^c f(x)\,dx + \int_c^\infty f(x)\,dx \quad \text{(split at any } c\text{)}$$

The integral **converges** if the limit exists and is finite; otherwise it **diverges**.

**Example 1 (converges):** $\displaystyle\int_1^\infty \frac{1}{x^2}\,dx = \lim_{b\to\infty}\Big[-\frac{1}{x}\Big]_1^b = \lim_{b\to\infty}\!\left(-\frac{1}{b}+1\right) = 1$

**Example 2 (diverges):** $\displaystyle\int_1^\infty \frac{1}{x}\,dx = \lim_{b\to\infty}[\ln b - \ln 1] = \infty$

---

#### 10. The p-Test for Type I Integrals

**Theorem:**
$$\int_1^\infty \frac{1}{x^p}\,dx \begin{cases} \text{converges} & \text{if } p > 1 \\ \text{diverges} & \text{if } p \leq 1 \end{cases}$$

**Proof:** For $p \neq 1$: $\displaystyle\int_1^b x^{-p}\,dx = \frac{x^{-p+1}}{1-p}\Big|_1^b = \frac{b^{1-p}-1}{1-p}$. As $b\to\infty$: if $p>1$, $b^{1-p}\to 0$ → converges to $\frac{1}{p-1}$; if $p<1$, diverges.

**Practical significance:** This test quickly determines convergence for many engineering integrals without computing the limit explicitly.

---

#### 11. Comparison Test for Improper Integrals

**Theorem:** If $0 \leq f(x) \leq g(x)$ for all $x \geq a$, then:
- If $\int_a^\infty g(x)\,dx$ converges → $\int_a^\infty f(x)\,dx$ converges.
- If $\int_a^\infty f(x)\,dx$ diverges → $\int_a^\infty g(x)\,dx$ diverges.

**Example:** Does $\displaystyle\int_1^\infty \frac{\sin^2 x}{x^2}\,dx$ converge?

Since $0 \leq \sin^2 x \leq 1$: $\frac{\sin^2 x}{x^2} \leq \frac{1}{x^2}$, and $\int_1^\infty x^{-2}\,dx$ converges (p=2>1). Therefore the integral converges.

---

#### 12. Type II — Discontinuous Integrands

**Setup:** $f$ has a singularity (vertical asymptote) at some point in $[a,b]$.

**Case: singularity at left endpoint $a$:**
$$\int_a^b f(x)\,dx = \lim_{\varepsilon\to 0^+}\int_{a+\varepsilon}^b f(x)\,dx$$

**Case: singularity at right endpoint $b$:**
$$\int_a^b f(x)\,dx = \lim_{\varepsilon\to 0^+}\int_a^{b-\varepsilon} f(x)\,dx$$

**Case: singularity at interior point $c \in (a,b)$:**
$$\int_a^b f(x)\,dx = \int_a^c f(x)\,dx + \int_c^b f(x)\,dx$$
*(split into two Type II integrals — BOTH must converge)*

---

#### 13. Type II — Examples

**Example 1 (converges):** $\displaystyle\int_0^1 \frac{1}{\sqrt{x}}\,dx$

$$= \lim_{\varepsilon\to 0^+}\int_\varepsilon^1 x^{-1/2}\,dx = \lim_{\varepsilon\to 0^+}\Big[2\sqrt{x}\Big]_\varepsilon^1 = \lim_{\varepsilon\to 0^+}(2 - 2\sqrt{\varepsilon}) = 2$$

**Example 2 (diverges):** $\displaystyle\int_0^1 \frac{1}{x}\,dx$

$$= \lim_{\varepsilon\to 0^+}[\ln x]_\varepsilon^1 = \lim_{\varepsilon\to 0^+}(0 - \ln\varepsilon) = +\infty$$

**The p-test for Type II (singularity at 0):**
$$\int_0^1 \frac{dx}{x^p} \begin{cases} \text{converges} & \text{if } p < 1 \\ \text{diverges} & \text{if } p \geq 1 \end{cases}$$
*(Note: opposite condition from Type I!)*

---

#### 14. The Gamma Function — Definition

**Definition:**
$$\Gamma(x) = \int_0^\infty t^{x-1}e^{-t}\,dt, \quad x > 0$$

This is a Type I improper integral (infinite upper limit) with a Type II singularity at $t=0$ for $x < 1$. It converges for all $x > 0$.

**Why define it?** The Gamma function extends the factorial to non-integer and even complex arguments. In engineering, it appears in:
- Laplace transforms of $t^n$ (for non-integer $n$)
- Bessel functions (Week 13)
- Probability distributions (Chi-squared, Student's t, F-distributions)
- Signal processing and fractional calculus

---

#### 15. Gamma Function — Key Properties

**Recurrence relation (the fundamental property):**
$$\Gamma(x+1) = x\,\Gamma(x)$$

**Proof:** Integrate by parts with $u = t^x$, $dv = e^{-t}dt$:
$$\Gamma(x+1) = \Big[-t^x e^{-t}\Big]_0^\infty + x\int_0^\infty t^{x-1}e^{-t}\,dt = 0 + x\,\Gamma(x)$$

**Connection to factorials:** $\Gamma(1) = \int_0^\infty e^{-t}\,dt = 1$, and by recurrence:
$$\Gamma(n+1) = n! \quad \text{for } n = 0,1,2,\ldots$$

**Special value:** $\Gamma(1/2) = \sqrt{\pi}$ (proved via Gaussian integral)

From recurrence: $\Gamma(3/2) = \frac{1}{2}\Gamma(1/2) = \frac{\sqrt{\pi}}{2}$, $\Gamma(5/2) = \frac{3\sqrt{\pi}}{4}$, etc.

**Laplace transform connection (forward link to Week 14):**
$$\mathcal{L}\{t^n\} = \frac{\Gamma(n+1)}{s^{n+1}} = \frac{n!}{s^{n+1}} \quad \text{for integer } n$$
$$\mathcal{L}\{t^{1/2}\} = \frac{\Gamma(3/2)}{s^{3/2}} = \frac{\sqrt{\pi}}{2s^{3/2}}$$

---

#### 16. Summary — Lecture 3

**Trigonometric substitution at a glance:**

| You see | You use | $\sqrt{\cdot}$ becomes |
|---------|---------|----------------------|
| $\sqrt{a^2-x^2}$ | $x=a\sin\theta$ | $a\cos\theta$ |
| $\sqrt{a^2+x^2}$ | $x=a\tan\theta$ | $a\sec\theta$ |
| $\sqrt{x^2-a^2}$ | $x=a\sec\theta$ | $a\tan\theta$ |

**Improper integrals convergence summary:**

| Type | Converges when |
|------|---------------|
| $\int_1^\infty x^{-p}\,dx$ | $p > 1$ |
| $\int_0^1 x^{-p}\,dx$ | $p < 1$ |

**Gamma function essentials:**
$$\Gamma(x+1) = x\,\Gamma(x), \quad \Gamma(n+1) = n!, \quad \Gamma(1/2) = \sqrt{\pi}$$

---

## Practice Session

**Theme:** Volumes of Revolution; Arc Length; comprehensive integration review.

### Practice Problems

**Set A — Volumes of Revolution**

1. Find the volume of the solid obtained by rotating the region bounded by $y = \sqrt{x}$, $y = 0$, $x = 4$ about the x-axis. *(Disk method)*
2. Find the volume when $y = x^2$ and $y = x$ (first quadrant) is rotated about the y-axis. *(Shell method)*
3. Find the volume when $y = e^x$, $y = 0$, $x = 0$, $x = 1$ is rotated about $y = -1$. *(Washer method)*
4. Verify that a sphere of radius $r$ has volume $\frac{4}{3}\pi r^3$ using the disk method applied to $y = \sqrt{r^2 - x^2}$.

**Set B — Arc Length**

5. Find the arc length of $y = \frac{2}{3}x^{3/2}$ from $x = 0$ to $x = 3$.
6. Find the arc length of $y = \ln(\cos x)$ from $x = 0$ to $x = \pi/4$. *(Hint: the integrand simplifies to $\sec x$.)*
7. Find the arc length of the parametric curve $x = t^2$, $y = t^3$ from $t = 0$ to $t = 1$.

**Set C — Integration Techniques (Mixed)**

8. $\displaystyle\int \frac{3x^2 - 2}{(x-1)(x^2+1)}\,dx$ *(partial fractions, Cases 1 and 3)*
9. $\displaystyle\int \frac{dx}{x^2+6x+13}$ *(completing the square)*
10. $\displaystyle\int \frac{x+2}{(x+1)^2+4}\,dx$ *(completing the square, split numerator)*
11. $\displaystyle\int \frac{\sqrt{x^2-4}}{x}\,dx$ *(trig substitution, Pattern 3)*
12. $\displaystyle\int_0^\infty xe^{-x^2}\,dx$ *(improper + u-substitution)*
13. Determine whether $\displaystyle\int_0^\infty \frac{x}{1+x^3}\,dx$ converges or diverges. *(Comparison test)*
14. Compute $\displaystyle\int_0^\infty t^4 e^{-t}\,dt$ using the Gamma function.
