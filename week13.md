# Week 13 — Special Functions: Legendre, Frobenius, and Bessel

**Course:** Engineering Mathematics 1
**Part:** IV — Sequences, Series & Power Series Solutions
**Kreyszig Sections:** §5.2, 5.3, 5.4, 5.5

> **Capping Part IV:** The power series machinery of Weeks 11–12 is deployed on its primary targets: variable-coefficient ODEs whose solutions cannot be expressed in elementary functions. **Legendre's equation** (from Laplace's equation in spherical coordinates) produces polynomial solutions forming an orthogonal basis on $[-1,1]$. The **Frobenius method** extends power series to regular singular points via a fractional-power ansatz $y = x^r \sum a_n x^n$. **Bessel's equation** (from wave and heat problems in cylindrical geometry) produces the Bessel functions $J_\nu(x)$, derived here by the Frobenius method in full detail.
>
> **Note on scope:** Legendre polynomials are developed completely (recurrence, Rodrigues, Bonnet, orthogonality with proof, Legendre series). The Frobenius method is covered systematically with three cases and one worked example per case. Bessel functions are derived by the 10-step Frobenius procedure; half-integer orders are computed exactly.

---

## Lecture 1: Legendre's Equation and Legendre Polynomials (§5.2)

### Introduction

**Legendre's equation** arises when the Laplace equation $\nabla^2 u = 0$ is solved in spherical coordinates $(r, \theta, \phi)$ using separation of variables. After separating the angular $\theta$-dependence (substituting $x = \cos\theta \in [-1, 1]$), the $\Theta$-equation becomes:
$$(1-x^2)\Theta'' - 2x\Theta' + \lambda\,\Theta = 0.$$
For a solution bounded on $[-1, 1]$, one needs $\lambda = n(n+1)$, giving **Legendre's equation**. The power series method at $x_0 = 0$ produces a remarkable result: one of the two series solutions **terminates**, giving a polynomial. These are the **Legendre polynomials** $P_n(x)$, which form a complete orthogonal basis on $[-1, 1]$.

**Why it matters in engineering:**
- Gravitational and electrostatic potential theory in spherical domains (satellite orbits, antenna patterns).
- Heat conduction in spherical objects.
- Quantum mechanics: spherical harmonics (eigenstates of angular momentum) are built from Legendre polynomials.

---

### Knowledge Points

---

#### 1. Legendre's Equation — Setup and Singular Points

**Equation:**
$$(1-x^2)y'' - 2xy' + n(n+1)\,y = 0, \quad n = 0, 1, 2, \ldots \tag{L}$$

**Standard form:** $y'' - \dfrac{2x}{1-x^2}y' + \dfrac{n(n+1)}{1-x^2}y = 0$.

$P(x) = -2x/(1-x^2)$, $Q(x) = n(n+1)/(1-x^2)$: analytic for $|x| < 1$, **singular at $x = \pm 1$** (zeros of the leading coefficient $1-x^2$).

Both $x = \pm 1$ are regular singular points (checked: $(x \mp 1)P$ and $(x \mp 1)^2 Q$ remain analytic). So $x_0 = 0$ is an ordinary point, and the power series method gives solutions convergent for $|x| < 1$.

**Equivalent self-adjoint form:**
$$(1-x^2)y'' - 2xy' + n(n+1)y = \frac{d}{dx}\!\left[(1-x^2)y'\right] + n(n+1)y = 0.$$

This Sturm–Liouville form is the key to orthogonality.

**Normalization convention:** $P_n(1) = 1$ for all $n$. Physical motivation: in the potential expansion $u = \sum(A_n r^n + B_n r^{-(n+1)})P_n(\cos\theta)$, the value at the north pole ($\theta = 0$, $x = 1$) is $P_n(1) = 1$ — clean and natural.

---

#### 2. Power Series Recurrence and Termination

**Substitute** $y = \sum_{k=0}^\infty c_k x^k$ into (L). After re-indexing the $y''$ term and collecting the coefficient of $x^k$:
$$(k+2)(k+1)c_{k+2} + \bigl[n(n+1) - k(k-1) - 2k\bigr]c_k = 0.$$

The bracket simplifies: $n(n+1) - k(k-1) - 2k = n(n+1) - k(k+1) = (n-k)(n+k+1)$.

**Recurrence:**
$$c_{k+2} = -\frac{(n-k)(n+k+1)}{(k+2)(k+1)}\,c_k. \tag{L-rec}$$

$c_0$ and $c_1$ are free parameters.

**Termination:** When $k = n$ (and $n$ is a non-negative integer), $(n-k) = 0$ and $c_{n+2} = 0$. The recurrence then gives $c_{n+4} = c_{n+6} = \cdots = 0$. The series **terminates** at degree $n$ — a polynomial!

- If $n$ is even: the even series (from $c_0$) terminates; set $c_1 = 0$ and discard the divergent odd series.
- If $n$ is odd: the odd series (from $c_1$) terminates; set $c_0 = 0$ and discard the even series.

**Why discard the infinite series?** It converges only for $|x| < 1$ and diverges at $x = \pm 1$, making it physically inadmissible for the sphere problem.

---

#### 3. Legendre Polynomials $P_0$–$P_4$ and Their Properties

Applying (L-rec) with the normalization $P_n(1) = 1$:

$$P_0(x) = 1.$$
$$P_1(x) = x.$$
$$P_2(x) = \tfrac{1}{2}(3x^2 - 1).$$
$$P_3(x) = \tfrac{1}{2}(5x^3 - 3x).$$
$$P_4(x) = \tfrac{1}{8}(35x^4 - 30x^2 + 3).$$

**Quick checks:** $P_2(1) = \tfrac{1}{2}(3-1) = 1$ ✓; $P_3(1) = \tfrac{1}{2}(5-3) = 1$ ✓.

**Parity:** $P_n(-x) = (-1)^n P_n(x)$ — even/odd depending on $n$.

**Values at endpoints:** $P_n(1) = 1$, $P_n(-1) = (-1)^n$ for all $n$.

**Example — deriving $P_2$:** Take $n = 2$, $c_1 = 0$. From (L-rec) with $k=0$:
$$c_2 = -\frac{(2)(3)}{2 \cdot 1}c_0 = -3c_0.$$
Normalize: $P_2(1) = c_0 + c_2 = c_0 - 3c_0 = -2c_0 = 1 \Rightarrow c_0 = -1/2$.
$P_2(x) = -\frac{1}{2} + \frac{3}{2}x^2 = \frac{1}{2}(3x^2 - 1)$ ✓

---

#### 4. Rodrigues' Formula

The Legendre polynomials have a compact closed form:
$$P_n(x) = \frac{1}{2^n\,n!}\,\frac{d^n}{dx^n}\!\left[(x^2-1)^n\right].$$

**Verification for $n=2$:** $(x^2-1)^2 = x^4 - 2x^2 + 1$.
$$\frac{d^2}{dx^2}(x^4-2x^2+1) = 12x^2 - 4.$$
$$\frac{1}{4 \cdot 2}(12x^2-4) = \frac{12x^2-4}{8} = \frac{3x^2-1}{2} = P_2(x). \checkmark$$

**Closed-form expansion from Rodrigues:** Using the binomial theorem $(x^2-1)^n = \sum_j \binom{n}{j}(-1)^{n-j}x^{2j}$ and differentiating $n$ times term by term:

$$P_n(x) = \sum_{m=0}^{\lfloor n/2\rfloor}(-1)^m\, \frac{(2n-2m)!}{2^n\,m!\,(n-m)!\,(n-2m)!}\,x^{n-2m}.$$

Verify $n=2$: $m=0$ gives $\tfrac{4!}{4 \cdot 1 \cdot 2 \cdot 2}x^2 = \tfrac{3}{2}x^2$; $m=1$ gives $-\tfrac{2!}{4 \cdot 1 \cdot 1 \cdot 1} = -\tfrac{1}{2}$. So $P_2 = \tfrac{1}{2}(3x^2-1)$ ✓

Rodrigues' formula shows $P_n$ is a polynomial of degree exactly $n$, and directly proves normalization $P_n(1)=1$ and the parity property.

---

#### 5. Bonnet's Recurrence

The Legendre polynomials satisfy a recurrence between consecutive polynomials:
$$(n+1)P_{n+1}(x) = (2n+1)\,x\,P_n(x) - n\,P_{n-1}(x).$$

This allows $P_{n+1}$ to be computed from $P_n$ and $P_{n-1}$ without returning to the ODE.

**Verification ($n=1$):**
$$2P_2 = 3xP_1 - P_0 \iff 2 \cdot \tfrac{1}{2}(3x^2-1) = 3x \cdot x - 1 \iff 3x^2-1 = 3x^2-1. \checkmark$$

**Using Bonnet to get $P_4$ from $P_2, P_3$ ($n=3$):**
$$4P_4 = 7x P_3 - 3P_2 = 7x \cdot \tfrac{1}{2}(5x^3-3x) - 3 \cdot \tfrac{1}{2}(3x^2-1) = \tfrac{35x^4-21x^2}{2} - \tfrac{9x^2-3}{2} = \tfrac{35x^4-30x^2+3}{2}.$$
So $P_4 = \tfrac{1}{8}(35x^4-30x^2+3)$ ✓

| Formula | Purpose |
|---------|---------|
| Rodrigues | Closed-form definition; proves degree, parity, normalization |
| Bonnet | Efficient computation of $P_{n+1}$ from previous two |

---

#### 6. Orthogonality — Proof

**Theorem:**
$$\int_{-1}^1 P_m(x)\,P_n(x)\,dx = \frac{2}{2n+1}\,\delta_{mn}.$$

**Proof for $m \neq n$ (WLOG $m < n$).** Apply Rodrigues to $P_n$:
$$\int_{-1}^1 P_m P_n\,dx = \frac{1}{2^n n!}\int_{-1}^1 P_m(x)\,\frac{d^n}{dx^n}(x^2-1)^n\,dx.$$

Integrate by parts $n$ times. Each step produces a boundary term of the form:
$$\left[\frac{d^{k-1}P_m}{dx^{k-1}} \cdot \frac{d^{n-k}}{dx^{n-k}}(x^2-1)^n\right]_{x=-1}^{x=1}, \quad k=1,\ldots,n.$$

All boundary terms vanish: $(x^2-1)^n = (x-1)^n(x+1)^n$ has a zero of order $n$ at each of $x = \pm 1$, so every derivative up to order $n-1$ still vanishes there. After $n$ integrations by parts:
$$\int_{-1}^1 P_m P_n\,dx = \frac{(-1)^n}{2^n n!}\int_{-1}^1 \frac{d^n P_m}{dx^n} \cdot (x^2-1)^n\,dx.$$

Since $P_m$ has degree $m < n$, its $n$-th derivative is zero. Therefore $\int_{-1}^1 P_m P_n\,dx = 0$. $\square$

**Proof that $\|P_n\|^2 = 2/(2n+1)$.** The same IBP with $m = n$ gives:
$$\|P_n\|^2 = \frac{(-1)^n}{2^n n!} \cdot \frac{(2n)!}{2^n n!} \cdot (-1)^n \cdot I_n,$$
where $I_n = \int_{-1}^1 (1-x^2)^n\,dx$. One IBP gives the reduction $I_n = \frac{2n}{2n+1}I_{n-1}$, $I_0 = 2$, so $I_n = \dfrac{2^{2n+1}(n!)^2}{(2n+1)!}$. Substituting:
$$\|P_n\|^2 = \frac{(2n)! \cdot 2}{(2n+1)!} = \frac{2}{2n+1}. \quad \square$$

---

#### 7. Legendre Series and Example

**Expansion:** Any $f \in L^2[-1,1]$ expands as:
$$f(x) = \sum_{n=0}^\infty a_n\,P_n(x), \qquad a_n = \frac{2n+1}{2}\int_{-1}^1 f(x)\,P_n(x)\,dx.$$

**Derivation:** Multiply both sides by $P_m$ and integrate; orthogonality kills all terms except $m = n$: $\int_{-1}^1 f P_m\,dx = a_m \cdot \dfrac{2}{2m+1}$.

**Example:** Expand $f(x) = x^2$ in Legendre series.

Since $x^2$ is an even degree-2 polynomial, only $a_0$ and $a_2$ are nonzero (odd terms vanish by parity):

$a_0 = \dfrac{1}{2}\int_{-1}^1 x^2\,dx = \dfrac{1}{2} \cdot \dfrac{2}{3} = \dfrac{1}{3}$.

$a_2 = \dfrac{5}{2}\int_{-1}^1 x^2 \cdot \dfrac{3x^2-1}{2}\,dx = \dfrac{5}{4}\!\left[3 \cdot \dfrac{2}{5} - \dfrac{2}{3}\right] = \dfrac{5}{4} \cdot \dfrac{8}{15} = \dfrac{2}{3}$.

$$x^2 = \tfrac{1}{3}P_0(x) + \tfrac{2}{3}P_2(x). \checkmark$$

Verify: $\tfrac{1}{3} \cdot 1 + \tfrac{2}{3} \cdot \tfrac{3x^2-1}{2} = \tfrac{1}{3} + x^2 - \tfrac{1}{3} = x^2$ ✓

---

#### 8. Summary — Lecture 1

| Concept | Key Formula |
|---------|------------|
| Legendre's equation | $(1-x^2)y'' - 2xy' + n(n+1)y = 0$ |
| Recurrence | $c_{k+2} = -\dfrac{(n-k)(n+k+1)}{(k+2)(k+1)}c_k$ |
| Termination | For integer $n$: series terminates at degree $n$ |
| $P_0$–$P_3$ | $1,\ x,\ \tfrac{1}{2}(3x^2-1),\ \tfrac{1}{2}(5x^3-3x)$ |
| Normalization | $P_n(1) = 1$ |
| Rodrigues | $P_n = \dfrac{1}{2^n n!}\dfrac{d^n}{dx^n}(x^2-1)^n$ |
| Bonnet | $(n+1)P_{n+1} = (2n+1)xP_n - nP_{n-1}$ |
| Orthogonality | $\int_{-1}^1 P_m P_n\,dx = \dfrac{2}{2n+1}\delta_{mn}$ |
| Series coefficients | $a_n = \dfrac{2n+1}{2}\int_{-1}^1 f\,P_n\,dx$ |

---

## Lecture 2: The Frobenius Method (§5.3)

### Introduction

The power series method $y = \sum c_n x^n$ works only at **ordinary points**. As soon as the leading coefficient of the ODE vanishes at a point, dividing to get standard form is impossible there — the power series existence theorem breaks down.

Yet physical ODEs frequently have singular points. Bessel's equation has $x = 0$ as a singular point; Legendre's equation has $x = \pm 1$. To handle these, **Frobenius** extended the power series ansatz to allow a fractional-power prefactor $x^r$.

**The key insight:** at a *regular* singular point, the ODE is "mildly singular" — the coefficients $xp(x)$ and $x^2q(x)$ remain analytic. This is just enough regularity to guarantee a Frobenius series solution.

---

### Knowledge Points

---

#### 1. Why Plain Power Series Fails

**Example:** try $y = \sum c_n x^n$ in $2xy'' + y' + xy = 0$ (singular at $x = 0$):

$2xy'' = \sum_{n=2}^\infty 2n(n-1)c_n x^{n-1} = \sum_{n=1}^\infty 2n(n+1)c_{n+1}x^n$ (after re-index).

The $n=0$ coefficient of $2xy''$ is zero — the equation forces $c_1 = 0$ from the $y'$ term but produces no constraint on $c_0$ from $2xy''$. The plain series exists but **misses a whole family of solutions** (those behaving like $x^{1/2}$, which cannot be represented by a plain power series).

**The remedy:** allow the ansatz $y = x^r \sum_{n=0}^\infty a_n x^n$ with $a_0 \neq 0$, where $r$ is a real number to be determined.

---

#### 2. Regular vs. Irregular Singular Points

Write the ODE in standard form: $y'' + p(x)y' + q(x)y = 0$.

**Definition:** $x_0$ is a **singular point** if $p$ or $q$ is not analytic at $x_0$. It is a **regular** singular point if
$$(x-x_0)\,p(x) \quad\text{and}\quad (x-x_0)^2\,q(x)$$
are both analytic at $x_0$. Otherwise it is an **irregular** singular point.

Equivalently, $b_0 = \lim_{x\to x_0}(x-x_0)p(x)$ and $c_0 = \lim_{x\to x_0}(x-x_0)^2 q(x)$ are both finite.

| ODE | $p(x)$ | $q(x)$ | $(x-x_0)p$, $(x-x_0)^2q$ | Type |
|-----|--------|--------|--------------------------|------|
| $x^2y''+xy'+(x^2-\nu^2)y=0$ | $1/x$ | $1-\nu^2/x^2$ | $1,\;x^2-\nu^2$ | Regular |
| $(1-x^2)y''-2xy'+n(n+1)y=0$ | $-2x/(1-x^2)$ | $n(n+1)/(1-x^2)$ | analytic at $\pm1$ | Regular |
| $x^3y''+y=0$ | $0$ | $1/x^3$ | $x^2q = 1/x$: not analytic | **Irregular** |

**Key fact:** The Frobenius method works only at regular singular points. Irregular singular points require asymptotic expansions (beyond scope).

---

#### 3. Standard Frobenius Form and the Indicial Equation

At a regular singular point $x_0 = 0$, write the ODE as:
$$x^2y'' + x\,b(x)\,y' + c(x)\,y = 0,$$
where $b(x) = \sum_{n=0}^\infty b_n x^n$ and $c(x) = \sum_{n=0}^\infty c_n x^n$ are analytic at $x_0 = 0$. (Here $b_0 = \lim_{x\to 0}xp(x)$ and $c_0 = \lim_{x\to 0}x^2 q(x)$.)

**Frobenius ansatz:** $y = x^r \sum_{n=0}^\infty a_n x^n = \sum_{n=0}^\infty a_n x^{n+r}$, $a_0 \neq 0$.

Substituting and collecting the coefficient of $x^{n+r}$, with $F(s) = s(s-1) + b_0 s + c_0$:
$$F(n+r)\,a_n = -\sum_{k=0}^{n-1}\bigl[b_{n-k}(k+r) + c_{n-k}\bigr]\,a_k, \quad n = 0, 1, 2, \ldots$$

For $n = 0$: the right-hand side is empty, so $F(r)\,a_0 = 0$. Since $a_0 \neq 0$:

**Indicial equation:**
$$F(r) = r(r-1) + b_0\,r + c_0 = 0.$$

The two roots $r_1 \geq r_2$ (by real part) are the **indicial roots**.

For $n \geq 1$: if $F(n+r) \neq 0$, then $a_n$ is determined uniquely from $a_0, \ldots, a_{n-1}$.

**Warning:** If $r_1 - r_2 = N \in \mathbb{Z}^+$, then $F(N+r_2) = F(r_1) = 0$. At step $n = N$ for $r_2$, the left-hand side vanishes but the right-hand side may not — the recurrence breaks down and forces a $\ln x$ term into $y_2$.

---

#### 4. Three Cases for the Two Solutions

Let $r_1, r_2$ be the indicial roots with $\operatorname{Re}(r_1) \geq \operatorname{Re}(r_2)$.

| Case | Condition | Two linearly independent solutions |
|------|-----------|-----------------------------------|
| I | $r_1 - r_2 \notin \mathbb{Z}$ | $y_1 = x^{r_1}\sum a_n x^n$, $\quad y_2 = x^{r_2}\sum b_n x^n$ |
| II | $r_1 = r_2$ | $y_1 = x^{r_1}\sum a_n x^n$, $\quad y_2 = y_1 \ln x + x^{r_1}\sum b_n x^n$ |
| III | $r_1 - r_2 = N \in \mathbb{Z}^+$ | $y_1 = x^{r_1}\sum a_n x^n$, $\quad y_2 = c\,y_1 \ln x + x^{r_2}\sum b_n x^n$ |

- **Case I:** Both indicial roots yield Frobenius series directly.
- **Case II:** The second solution always has a $\ln x$ term.
- **Case III:** $c$ may or may not be zero. If the right-hand side at step $n = N$ is non-zero, then $c \neq 0$ (log unavoidable). If zero, the pure Frobenius series from $r_2$ works.
- In all cases, $y_1$ is obtained from $r_1$; both series converge for $0 < x < R$ where $R$ is the distance from $x_0$ to the next singular point.

---

#### 5. Case I Example: $2xy'' + y' + xy = 0$

**Standard Frobenius form:** multiply by $x$: $2x^2y'' + xy' + x^2y = 0$, so $b(x) = \tfrac{1}{2}$ (constant), $c(x) = \tfrac{x^2}{2}$.

$b_0 = \tfrac{1}{2}$, $c_0 = 0$, and the only non-zero higher coefficient is $c_2 = \tfrac{1}{2}$.

**Indicial equation:** $F(r) = r(r-1) + \tfrac{1}{2}r = r^2 - \tfrac{1}{2}r = r(r - \tfrac{1}{2}) = 0$.

Roots: $r_1 = \tfrac{1}{2}$, $r_2 = 0$. Difference $\tfrac{1}{2} \notin \mathbb{Z}$ — **Case I**.

**Recurrence:** Since $b_k = 0$ for $k \geq 1$ and $c_k = 0$ for $k \neq 2$:
$$F(n+r)\,a_n = -c_2\,a_{n-2} = -\tfrac{1}{2}\,a_{n-2} \quad (n \geq 2), \qquad a_1 = 0.$$
$$a_n = \frac{-a_{n-2}}{(n+r)(2n+2r-1)}.$$

All odd-index coefficients vanish. **Solution 1 from $r_1 = \tfrac{1}{2}$:**
$$a_2 = -\frac{a_0}{2 \cdot 5} = -\frac{a_0}{10}, \quad a_4 = \frac{a_0}{360}, \quad a_6 = -\frac{a_0}{28080}, \ldots$$
$$y_1 = a_0\,x^{1/2}\!\left(1 - \frac{x^2}{10} + \frac{x^4}{360} - \cdots\right).$$

**Solution 2 from $r_2 = 0$:**
$$a_2 = -\frac{a_0}{2 \cdot 3} = -\frac{a_0}{6}, \quad a_4 = \frac{a_0}{168}, \quad a_6 = -\frac{a_0}{11088}, \ldots$$
$$y_2 = a_0\!\left(1 - \frac{x^2}{6} + \frac{x^4}{168} - \cdots\right).$$

Both series converge for all $x > 0$ (Ratio Test). General solution: $y = Ay_1 + By_2$.

---

#### 6. Case II Example: $x^2y'' - xy' + y = 0$

**Standard form:** $b(x) = -1$, $c(x) = 1$ (both constant).

$b_0 = -1$, $c_0 = 1$.

**Indicial equation:** $F(r) = r(r-1) + (-1)r + 1 = r^2 - 2r + 1 = (r-1)^2 = 0$.

Double root: $r_1 = r_2 = 1$ — **Case II**.

**Recurrence for $r = 1$:** Since $b_n = c_n = 0$ for $n \geq 1$:
$$F(n+1)\,a_n = 0, \quad F(n+1) = n^2. \quad \Rightarrow \quad a_n = 0 \text{ for } n \geq 1.$$

The Frobenius series terminates: $y_1 = a_0\,x$.

By Case II, $y_2 = y_1 \ln x + x \sum b_n x^n$. **Direct verification** that $y_2 = x \ln x$ works:
$$y_2' = \ln x + 1, \quad y_2'' = \frac{1}{x}.$$
$$x^2 \cdot \frac{1}{x} - x(\ln x + 1) + x\ln x = x - x\ln x - x + x\ln x = 0. \checkmark$$

**General solution:** $y = (A + B\ln x)\,x$, $x > 0$.

**Remark:** This is Euler–Cauchy with double characteristic root $r = 1$. The Case II formula $y_2 = y_1 \ln x$ recovers the standard Euler–Cauchy result automatically.

---

#### 7. Case III Example: $x^2y'' + xy' + (x-1)y = 0$

**Standard form:** $b(x) = 1$, $c(x) = x - 1$.

$b_0 = 1$, $c_0 = -1$. The only non-zero higher coefficient is $c_1 = 1$.

**Indicial equation:** $F(r) = r(r-1) + r - 1 = r^2 - 1 = (r-1)(r+1) = 0$.

Roots: $r_1 = 1$, $r_2 = -1$. $N = r_1 - r_2 = 2 \in \mathbb{Z}^+$ — **Case III**.

**Solution 1 from $r_1 = 1$:** $F(n+1) = (n+1)^2 - 1 = n(n+2)$.
$$n(n+2)\,a_n = -a_{n-1} \quad (n \geq 1).$$
$$a_1 = -\frac{a_0}{3}, \quad a_2 = \frac{a_0}{24}, \quad a_3 = -\frac{a_0}{360}, \ldots$$
$$y_1 = a_0\,x\!\left(1 - \frac{x}{3} + \frac{x^2}{24} - \frac{x^3}{360} + \cdots\right).$$

**Attempt Frobenius from $r_2 = -1$:** $F(n-1) = n(n-2)$.
- $n = 1$: $1 \cdot (-1)\,b_1 = -b_0 \Rightarrow b_1 = b_0$.
- $n = 2$: $2 \cdot 0 \cdot b_2 = -b_1 = -b_0$. **Contradiction** since $b_0 \neq 0$.

The recurrence breaks down at $n = N = 2$: $F(1) = 0$ but the right-hand side $\neq 0$. A logarithmic term is **unavoidable**:
$$y_2 = c\,y_1 \ln x + x^{-1}\sum_{n=0}^\infty d_n x^n.$$
The constants $c$ and $d_n$ are determined by substituting $y_2$ and matching coefficients.

---

#### 8. Summary — Lecture 2

| Step | Action |
|------|--------|
| 1 | Write ODE as $x^2y'' + xb(x)y' + c(x)y = 0$; check $b$, $c$ analytic at $x_0$ |
| 2 | Read off $b_0 = b(0)$, $c_0 = c(0)$; form indicial equation $r(r-1) + b_0 r + c_0 = 0$ |
| 3 | Solve for $r_1 \geq r_2$; determine Case I, II, or III |
| 4 | Substitute $y = \sum a_n x^{n+r}$; derive recurrence from coefficient of $x^{n+r}$ |
| 5 | Solve recurrence for $r_1$ $\Rightarrow$ $y_1$ |
| 6 | Case I: repeat for $r_2$ $\Rightarrow$ $y_2$; Case II/III: use $y_2 = cy_1\ln x + x^{r_2}\sum b_n x^n$ |
| 7 | State radius of convergence; write $y = Ay_1 + By_2$ |

---

## Lecture 3: Bessel's Equation and Bessel Functions (§5.4, 5.5)

### Introduction

**Bessel's equation** arises when the wave equation, heat equation, or Laplace equation is solved in **cylindrical coordinates** $(r, \theta, z)$. Separation of variables in the radial direction produces:
$$x^2 y'' + xy' + (x^2 - \nu^2)y = 0, \quad \nu \geq 0.$$

Unlike Legendre's equation, $x = 0$ is a **regular singular point** of Bessel's equation — the power series method does not directly apply. The Frobenius method (from Lecture 2) applies and produces $J_\nu(x)$ in 10 steps.

**Why it matters in engineering:**
- Vibrating circular membranes (drum heads): natural frequencies are zeros of $J_0$, $J_1$, etc.
- Heat conduction in a cylinder: solutions involve $J_0$.
- Electromagnetic waveguides: TE$_{mn}$ modes in circular waveguides use zeros of $J_n'$.

---

### Knowledge Points

---

#### 1. Bessel's Equation — Regular Singular Point and Indicial Equation

**Equation of order $\nu$:**
$$x^2y'' + xy' + (x^2 - \nu^2)y = 0, \quad x > 0. \tag{B}$$

**Standard form** (divide by $x^2$): $p(x) = 1/x$, $q(x) = 1 - \nu^2/x^2$.

**Classify $x = 0$:**
$$p_0 = \lim_{x\to0} x \cdot \frac{1}{x} = 1, \qquad q_0 = \lim_{x\to0} x^2 \cdot \frac{x^2 - \nu^2}{x^2} = -\nu^2.$$
Both limits are finite: $x = 0$ is a **regular** singular point. The Frobenius method applies.

**Indicial equation:** $r(r-1) + p_0 r + q_0 = r(r-1) + r - \nu^2 = r^2 - \nu^2 = 0$, giving:
$$r = \pm\nu.$$

The larger root $r_1 = +\nu$ gives the first (better-behaved) solution $J_\nu(x)$.

---

#### 2. Steps 1–4: Frobenius Ansatz and Setting Up the Recurrence

**Step 1 — Ansatz with $r = \nu$:**
$$y = x^\nu \sum_{n=0}^\infty c_n x^n = \sum_{n=0}^\infty c_n x^{n+\nu}, \quad c_0 \neq 0.$$

**Step 2 — Substituting $y'$, $y''$:**
$$x^2y'' = \sum_{n=0}^\infty (n+\nu)(n+\nu-1)\,c_n\,x^{n+\nu}, \quad xy' = \sum_{n=0}^\infty (n+\nu)\,c_n\,x^{n+\nu}.$$
Combining: $x^2y'' + xy' = \sum (n+\nu)^2 c_n x^{n+\nu}$ (since $(n+\nu)(n+\nu-1)+(n+\nu) = (n+\nu)^2$).

Bessel's equation becomes:
$$\sum_{n=0}^\infty (n+\nu)^2 c_n x^{n+\nu} - \nu^2 \sum_{n=0}^\infty c_n x^{n+\nu} + \sum_{n=0}^\infty c_n x^{n+\nu+2} = 0.$$

**Step 3 — Simplify and align:**
$$[(n+\nu)^2 - \nu^2]c_n = n(n+2\nu)\,c_n.$$

Re-index the last sum $n \to n-2$: $\sum_{n=0}^\infty c_n x^{n+\nu+2} = \sum_{n=2}^\infty c_{n-2} x^{n+\nu}$.

$$\sum_{n=0}^\infty n(n+2\nu)\,c_n x^{n+\nu} + \sum_{n=2}^\infty c_{n-2} x^{n+\nu} = 0.$$

**Step 4 — Recurrence by cases:**
- $n=0$: $0 = 0$ — $c_0$ is a free parameter.
- $n=1$: $1 \cdot (1+2\nu)\,c_1 = 0$. Since $\nu \geq 0$, we must have $c_1 = 0$. Then $c_3 = c_5 = \cdots = 0$ (all odd-index coefficients vanish).
- $n \geq 2$: $n(n+2\nu)\,c_n + c_{n-2} = 0$, so $c_n = -\dfrac{c_{n-2}}{n(n+2\nu)}$.

Setting $n = 2m$:
$$c_{2m} = -\frac{c_{2m-2}}{4m(m+\nu)}, \quad m = 1, 2, 3, \ldots$$

---

#### 3. Steps 5–6: Gamma Function

**Step 5 — Definition and properties:**

$$\Gamma(s) = \int_0^\infty t^{s-1} e^{-t}\,dt, \quad s > 0.$$

**Functional equation** (IBP): $\Gamma(s+1) = s\,\Gamma(s)$.

Base value: $\Gamma(1) = 1$. For positive integers: $\Gamma(n) = (n-1)!$.

**Step 6 — Key product identity:**
$$(1+\nu)(2+\nu)\cdots(m+\nu) = \frac{\Gamma(m+\nu+1)}{\Gamma(\nu+1)}.$$

**Proof:** Apply the functional equation repeatedly starting from $\Gamma(\nu+1)$:
$\Gamma(m+\nu+1) = (m+\nu)(m-1+\nu)\cdots(1+\nu)\,\Gamma(\nu+1)$. Divide both sides by $\Gamma(\nu+1)$. $\square$

This identity holds for any $\nu \geq 0$, not just integers — what makes the Bessel function formula work for all orders.

---

#### 4. Steps 7–8: Telescoping and Normalization

**Step 7 — Telescoping the recurrence:**
$$c_2 = -\frac{c_0}{4 \cdot 1 \cdot (1+\nu)}, \quad c_4 = \frac{c_0}{4^2 \cdot 1 \cdot 2 \cdot (1+\nu)(2+\nu)}, \quad \ldots$$

General pattern:
$$c_{2m} = \frac{(-1)^m\,c_0}{4^m \cdot m! \cdot (1+\nu)(2+\nu)\cdots(m+\nu)} = \frac{(-1)^m\,c_0\,\Gamma(\nu+1)}{4^m \cdot m! \cdot \Gamma(m+\nu+1)}.$$

**Step 8 — Standard normalization:**
$$c_0 = \frac{1}{2^\nu\,\Gamma(\nu+1)}.$$

Then $c_0\,\Gamma(\nu+1) = 1/2^\nu$, and:
$$c_{2m} = \frac{(-1)^m}{m!\,\Gamma(m+\nu+1)} \cdot \frac{1}{2^{2m+\nu}} = \frac{(-1)^m}{m!\,\Gamma(m+\nu+1)}\left(\frac{1}{2}\right)^{2m+\nu}.$$

This gives the compact form $c_{2m}\,x^{2m+\nu} = \dfrac{(-1)^m}{m!\,\Gamma(m+\nu+1)}\!\left(\dfrac{x}{2}\right)^{\!2m+\nu}$.

---

#### 5. Steps 9–10: The Bessel Function $J_\nu$ and Integer Orders

**Step 9 — Final formula:**

$$J_\nu(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m!\,\Gamma(m+\nu+1)}\!\left(\frac{x}{2}\right)^{\!2m+\nu}, \quad x > 0, \quad \nu \geq 0.$$

**Convergence** (Ratio Test): consecutive term ratio $\to x^2/[4(m+1)(m+\nu+1)] \to 0$ as $m \to \infty$. So $J_\nu(x)$ converges for all $x > 0$.

**Behaviour near $x = 0$:** Leading term $c_0 x^\nu = x^\nu/(2^\nu\Gamma(\nu+1))$. For $\nu > 0$: $J_\nu(0) = 0$; for $\nu = 0$: $J_0(0) = 1$.

**Step 10 — Integer order $\nu = n$:** $\Gamma(m+n+1) = (m+n)!$, so:
$$J_n(x) = \sum_{m=0}^\infty \frac{(-1)^m}{m!\,(m+n)!}\!\left(\frac{x}{2}\right)^{\!2m+n}.$$

**Explicit first terms:**
$$J_0(x) = 1 - \frac{x^2}{4} + \frac{x^4}{64} - \frac{x^6}{2304} + \cdots$$
$$J_1(x) = \frac{x}{2} - \frac{x^3}{16} + \frac{x^5}{384} - \cdots$$
$$J_2(x) = \frac{x^2}{8} - \frac{x^4}{96} + \frac{x^6}{3072} - \cdots$$

Each $J_n(x)$ starts like $x^n$ near $x=0$, grows to a maximum, then oscillates with **decreasing amplitude** as $x \to \infty$ (like a damped cosine). Large-$x$ asymptotics:
$$J_\nu(x) \approx \sqrt{\frac{2}{\pi x}}\cos\!\left(x - \frac{\nu\pi}{2} - \frac{\pi}{4}\right), \quad x \to \infty.$$

---

#### 6. Linear Dependence for Integer Order and Recurrences

**For non-integer $\nu$:** roots $r_1 = \nu$, $r_2 = -\nu$ differ by a non-integer (Case I). $J_\nu$ and $J_{-\nu}$ are linearly independent.

**For integer $\nu = n$:** $r_1 - r_2 = 2n \in \mathbb{Z}^+$ (Case III). Using the convention $1/\Gamma(k) = 0$ for $k = 0, -1, -2, \ldots$, direct computation gives:
$$J_{-n}(x) = (-1)^n J_n(x).$$

**Proof:** In the series for $J_{-\nu}$, replace $\nu \to n$ and shift $m \to m+n$; terms with $m < n$ vanish because $\Gamma(m-n+1)$ has a pole. Relabelling $k = m-n$ gives $(-1)^n J_n(x)$. $\square$

So $J_{-n}$ is NOT a second independent solution when $n$ is an integer.

**Three-term recurrence** (useful for computation):
$$J_{\nu+1}(x) = \frac{2\nu}{x}J_\nu(x) - J_{\nu-1}(x).$$

Example: $J_2 = \tfrac{2}{x}J_1 - J_0$. At $x = 1$: $J_2(1) \approx 2(0.4401) - 0.7652 = 0.1150$ (table: 0.1149) ✓

**Derivative identities:**
$$\frac{d}{dx}\bigl[x^\nu J_\nu(x)\bigr] = x^\nu J_{\nu-1}(x), \qquad \frac{d}{dx}\bigl[x^{-\nu}J_\nu(x)\bigr] = -x^{-\nu}J_{\nu+1}(x).$$

Combining: $J_\nu'(x) = \tfrac{1}{2}\bigl[J_{\nu-1}(x) - J_{\nu+1}(x)\bigr]$.

**Special case $\nu = 0$:** $J_0'(x) = -J_1(x)$.

**Integration formulas:**
$$\int x^\nu J_{\nu-1}(x)\,dx = x^\nu J_\nu(x) + C, \qquad \int x^{-\nu}J_{\nu+1}(x)\,dx = -x^{-\nu}J_\nu(x) + C.$$

---

#### 7. Half-Integer Bessel Functions

For half-integer orders $\nu = \tfrac{1}{2}, \tfrac{3}{2}, \ldots$, Bessel functions reduce to **elementary functions**. These arise in separating the spherical wave/heat equation (order $\nu = \ell + \tfrac{1}{2}$, $\ell = 0, 1, 2, \ldots$).

**Key Gamma value:** $\Gamma\!\left(\tfrac{1}{2}\right) = \sqrt{\pi}$.

Proof: substitute $t = u^2$ in $\Gamma(\tfrac{1}{2}) = \int_0^\infty t^{-1/2}e^{-t}dt$ to get the Gaussian integral $2\int_0^\infty e^{-u^2}du = \sqrt{\pi}$.

Building up from $\Gamma(\tfrac{1}{2})$:

| $m$ | $\Gamma(m+\tfrac{3}{2})$ |
|-----|------------------------|
| 0 | $\Gamma(\tfrac{3}{2}) = \tfrac{1}{2}\sqrt{\pi}$ |
| 1 | $\Gamma(\tfrac{5}{2}) = \tfrac{3}{4}\sqrt{\pi}$ |
| 2 | $\Gamma(\tfrac{7}{2}) = \tfrac{15}{8}\sqrt{\pi}$ |
| 3 | $\Gamma(\tfrac{9}{2}) = \tfrac{105}{16}\sqrt{\pi}$ |

General formula: $\Gamma(m+\tfrac{3}{2}) = \dfrac{(2m+1)!}{4^m\,m! \cdot 2}\,\sqrt{\pi}$.

**Deriving $J_{1/2}$:** Substitute $\nu = \tfrac{1}{2}$ into the series. Using $m!\,\Gamma(m+\tfrac{3}{2}) = \dfrac{(2m+1)!}{4^m \cdot 2}\sqrt{\pi}$:
$$J_{1/2}(x) = \frac{\sqrt{2}}{\sqrt{\pi}}\,x^{1/2}\sum_{m=0}^\infty \frac{(-1)^m x^{2m}}{(2m+1)!} = \frac{\sqrt{2}}{\sqrt{\pi}}\,x^{1/2} \cdot \frac{\sin x}{x}.$$

$$\boxed{J_{1/2}(x) = \sqrt{\frac{2}{\pi x}}\,\sin x.}$$

**Deriving $J_{-1/2}$:** Similarly, using $m!\,\Gamma(m+\tfrac{1}{2}) = \dfrac{(2m)!}{4^m}\sqrt{\pi}$:
$$J_{-1/2}(x) = \frac{\sqrt{2}}{\sqrt{\pi}}\,x^{-1/2}\sum_{m=0}^\infty \frac{(-1)^m x^{2m}}{(2m)!} = \sqrt{\frac{2}{\pi x}}\cos x.$$

$$\boxed{J_{-1/2}(x) = \sqrt{\frac{2}{\pi x}}\,\cos x.}$$

Since $\nu = -\tfrac{1}{2}$ is non-integer, $J_{-1/2}$ and $J_{1/2}$ are linearly independent (Case I).

**Deriving $J_{3/2}$ via recurrence:** Set $\nu = \tfrac{1}{2}$ in $J_{\nu+1} = \tfrac{2\nu}{x}J_\nu - J_{\nu-1}$:
$$J_{3/2}(x) = \frac{1}{x}J_{1/2}(x) - J_{-1/2}(x) = \sqrt{\frac{2}{\pi x}}\!\left(\frac{\sin x}{x} - \cos x\right).$$

| Order | Closed form |
|-------|------------|
| $J_{1/2}$ | $\sqrt{2/\pi x}\,\sin x$ |
| $J_{-1/2}$ | $\sqrt{2/\pi x}\,\cos x$ |
| $J_{3/2}$ | $\sqrt{2/\pi x}\!\left(\dfrac{\sin x}{x} - \cos x\right)$ |

Each $J_{n+1/2}$ involves only $\sin x$, $\cos x$, and powers of $1/x$ — these are the **spherical Bessel functions** of physics.

---

#### 8. Bessel Functions of the Second Kind — $Y_\nu$ (§5.5)

For integer order $n$, $J_{-n} = (-1)^n J_n$ is not independent, so we need another solution.

**Definition:**
$$Y_\nu(x) = \frac{\cos(\nu\pi)\,J_\nu(x) - J_{-\nu}(x)}{\sin(\nu\pi)}.$$
For integer $n$: $Y_n(x) = \lim_{\nu \to n} Y_\nu(x)$ (L'Hôpital-type limit).

**Key properties:**
- $Y_\nu(x) \to -\infty$ as $x \to 0^+$ (logarithmic singularity; contains $\ln x$ term).
- $J_\nu$ and $Y_\nu$ are always linearly independent for any $\nu \geq 0$.
- Large-$x$: $Y_\nu(x) \approx \sqrt{2/(\pi x)}\sin(x - \nu\pi/2 - \pi/4)$ — oscillatory with decaying amplitude.

**General solution of Bessel's equation:**
$$y = A\,J_\nu(x) + B\,Y_\nu(x).$$

**Physical rule:** If the domain includes $x = 0$: set $B = 0$ (regularity). $Y_\nu$ is retained only when the origin is excluded (e.g., an annular region $0 < a \leq r \leq b$).

---

#### 9. Engineering Applications

**Zeros of $J_0$ and $J_1$** (needed for boundary conditions):

| $m$ | $j_{0m}$ | $j_{1m}$ |
|-----|----------|----------|
| 1 | 2.405 | 3.832 |
| 2 | 5.520 | 7.016 |
| 3 | 8.654 | 10.173 |

**Vibrating circular membrane:** $u_{tt} = c^2\nabla^2 u$ in polar, $u(a, \theta, t) = 0$. Natural frequencies: $\omega_{nm} = c\,j_{nm}/a$ where $j_{nm}$ is the $m$-th zero of $J_n$.

**Heat conduction in a cylinder:** $T_t = \alpha\nabla^2 T$, $T(R, t) = 0$.
$$T(r,t) = \sum_k c_k\,J_0\!\left(\frac{j_{0k}}{R}r\right)e^{-\alpha j_{0k}^2 t/R^2}.$$

**Electromagnetic waveguide (circular):** TM modes: $E_z \propto J_n(k_{nm}r)\cos n\theta$ with cutoff $k_{nm} = j_{nm}/a$. TE modes: zeros of $J_n'$ determine cutoff.

---

#### 10. Summary — Lecture 3

| Concept | Key Formula / Fact |
|---------|--------------------|
| Bessel's equation | $x^2y'' + xy' + (x^2-\nu^2)y = 0$ |
| Singular point | $x = 0$ is regular singular; Frobenius applies |
| Indicial equation | $r^2 - \nu^2 = 0$, so $r = \pm\nu$ |
| $J_\nu$ series | $\sum_{m=0}^\infty \dfrac{(-1)^m}{m!\,\Gamma(m+\nu+1)}\!\left(\dfrac{x}{2}\right)^{2m+\nu}$ |
| $J_0$ near origin | $J_0(0) = 1$; $J_n(0) = 0$ ($n \geq 1$) |
| Integer order | $J_{-n} = (-1)^n J_n$ (not independent) |
| Recurrence | $J_{\nu+1} = \tfrac{2\nu}{x}J_\nu - J_{\nu-1}$ |
| Derivative | $J_0' = -J_1$ |
| $J_{1/2}$, $J_{-1/2}$ | $\sqrt{2/\pi x}\sin x$, $\sqrt{2/\pi x}\cos x$ |
| $Y_\nu$ | $\to -\infty$ at origin; keep only if origin excluded |
| Drum frequencies | $\omega_n = c\,j_{0n}/a$ |

**The big picture:**

| Geometry | ODE | Special functions |
|----------|-----|------------------|
| Cartesian | constant-coefficient | sines, cosines, exponentials |
| Spherical | Legendre | $P_n(\cos\theta)$ |
| Cylindrical | Bessel | $J_\nu(kr)$, $Y_\nu(kr)$ |

Each arises from Laplace's (or wave/heat) equation in the appropriate coordinate system. The Frobenius method is the unified derivation tool.

---

## Practice Session

**Theme:** Legendre polynomials; Frobenius method; Bessel function recognition and derivation.

---

### Practice Problems

**Set A — Legendre Polynomials**

1. (a) Derive $P_3(x)$ using the recurrence (L-rec) with $n = 3$, $c_0 = 0$, $c_1 = 1$, and normalise so $P_3(1) = 1$.
   (b) Verify using Rodrigues' formula: compute $\tfrac{1}{48}\tfrac{d^3}{dx^3}(x^2-1)^3$.
   (c) Verify using Bonnet's formula: $3P_3 = 5x\,P_2 - 2P_1$.

2. Verify the orthogonality relations:
   (a) $\displaystyle\int_{-1}^1 P_1(x)\,P_3(x)\,dx = 0$.
   (b) $\displaystyle\int_{-1}^1 [P_1(x)]^2\,dx = \dfrac{2}{3}$ (i.e., $\|P_1\|^2 = 2/(2\cdot1+1)$).
   (c) $\displaystyle\int_{-1}^1 [P_2(x)]^2\,dx = \dfrac{2}{5}$.

3. Expand $f(x) = x^3$ in a Legendre series.
   (a) Use symmetry to argue $a_0 = a_2 = 0$.
   (b) Compute $a_1$ and $a_3$.
   (c) Verify: $x^3 = a_1 P_1 + a_3 P_3$.

4. Expand $f(x) = x^2 + 1$ in a Legendre series (exact finite sum). Verify directly.

**Set B — Frobenius Method**

5. Apply the Frobenius method to $4xy'' + 2y' + y = 0$.
   (a) Write in standard Frobenius form; identify $b_0$, $c_0$.
   (b) Solve the indicial equation; determine which case applies.
   (c) Find the first three non-zero terms of each independent solution.

6. Apply the Frobenius method to $x^2y'' + x(x-1)y' + y = 0$.
   (a) Compute $b_0$, $c_0$ and solve the indicial equation.
   (b) Determine which case applies.
   (c) Find the first three terms of $y_1$ from the larger indicial root.

7. For the Euler–Cauchy equation $x^2y'' + 5xy' + 4y = 0$:
   (a) Apply the Frobenius method with the indicial equation.
   (b) Identify the case (double root, distinct roots, or integer difference).
   (c) Write the general solution. Verify that it matches the Euler–Cauchy formula from Week 6.

8. Consider $2xy'' + (1-2x)y' - y = 0$.
   (a) Classify the singular point $x = 0$ as regular or irregular.
   (b) Find the indicial roots and determine the Frobenius case.
   (c) Write the recurrence and compute the first three non-zero terms of $y_1$.

**Set C — Bessel Functions**

9. For $J_0(x) = \displaystyle\sum_{m=0}^\infty \dfrac{(-1)^m}{(m!)^2}\!\left(\dfrac{x}{2}\right)^{\!2m}$:
   (a) Verify that $J_0$ satisfies Bessel's equation of order 0: substitute the first three terms into $xy'' + y' + xy = 0$.
   (b) Compute $J_0(0)$ and $J_0'(0)$.
   (c) Use the series to estimate $J_0(1)$ to four decimal places (use three terms).

10. Using the Frobenius derivation, verify the recurrence $c_{2m} = -c_{2m-2}/[4m(m+1)]$ for $J_1$ ($\nu=1$), and write out the first three non-zero terms explicitly.

11. A circular drum of radius $a = 0.4$ m has wave speed $c = 250$ m/s.
    (a) Find the first three natural frequencies $f_n = \omega_n/(2\pi)$ in Hz for the $m = 0$ (axially symmetric) mode, using zeros of $J_0$.
    (b) Find the fundamental frequency of the first azimuthal mode ($m = 1$) using the first zero of $J_1$.
    (c) Which mode has the lower fundamental frequency?

12. Identify each ODE as Bessel's equation of some order $\nu$ (possibly after substitution), state $\nu$, and write the general solution:
    (a) $x^2y'' + xy' + (x^2 - 9)y = 0$
    (b) $xy'' + y' + 4xy = 0$ *(substitute $t = 2\sqrt{x}$)*
    (c) $x^2y'' + xy' + 4x^6 y = 0$ *(substitute $t = x^3/3$)*
    (d) Show that $y'' + y = 0$ is equivalent to a Bessel equation of order $\tfrac{1}{2}$ via $y = u/\sqrt{x}$, $t = x$.
