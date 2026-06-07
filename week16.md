# Week 16 — Final Examination

**Course:** Engineering Mathematics 1
**Coverage:** Weeks 9–15 (Part III applications, Systems of ODEs, Series, Laplace Transforms)
**Format:** Closed-book; formula sheet provided
**Duration:** 120 minutes
**Weight:** 40% of final grade

> **No new material this week.** Week 16 is the Final Examination. This document is the complete exam preparation reference: a corrected coverage map, a self-contained formula sheet, topic-by-topic review notes with common pitfalls, and a full set of sample examination problems.
>
> **Not on the Final:** Parts I and II (Weeks 1–3 calculus, Weeks 4–5 first-order ODEs) and Part III theory (Weeks 6–7 characteristic equation, UC method, VoP) were tested on the Midterm (Week 8) and are **not** re-examined. The final begins with the *applications* of second-order ODEs (Week 9) and continues through Laplace Transforms (Week 15).

---

## Exam Coverage and Weighting Guide

### Topics Covered (Weeks 9–15)

| Week | Topic | Kreyszig | Expected weight |
|------|-------|----------|----------------|
| 9 | Free/forced oscillations, RLC circuits; 2×2 matrices & eigenvalues | §2.4, 2.8, 2.9; §4.0 | Medium |
| 10 | Systems of ODEs; eigenvalue method; phase plane | §4.1–4.3 | **High** |
| 11 | Sequences; convergence tests; power series (IOC) | §11 (supp.) | Medium |
| 12 | Taylor series; remainder; power series ODE method | §11 (supp.) | Medium |
| 13 | Legendre polynomials; Frobenius method; Bessel functions | §5.2–5.5 | Low–Medium |
| 14 | Laplace: definition, table, shifting, IVP pipeline | §6.1–6.2 | **High** |
| 15 | Step/delta forcing; convolution; impulse response | §6.3–6.5 | **High** |

### What the Formula Sheet Will Include

Provided by the instructor during the exam:
- Standard Laplace transform table (complete pairs including shifts)
- Legendre polynomials $P_0$–$P_3$
- Standard derivative and integral table

**What you must know without the sheet:**
- Mass-spring ODE and damping regime classification ($\zeta$ formula)
- RLC analogy correspondence
- Eigenvalue algorithm for 2×2 matrices and phase-plane classification rules
- Power series re-indexing procedure and recurrence setup
- Laplace transform of $y'$ and $y''$ including IC terms
- Both shifting theorems and the sifting property of $\delta$
- Convolution integral definition

---

## Formula Reference Sheet

### Part III — Second-Order ODE Applications (Week 9)

**Mass-spring ODE:** $m\ddot{y} + c\dot{y} + ky = r(t)$. Natural frequency $\omega_0 = \sqrt{k/m}$.

| $\zeta = c/(2\sqrt{mk})$ | Regime | $y_h$ form |
|--------------------------|--------|------------|
| $\zeta = 0$ | Undamped | $R\cos(\omega_0 t - \delta)$ |
| $0 < \zeta < 1$ | Underdamped | $Re^{-\alpha t}\cos(\omega_d t - \delta)$ |
| $\zeta = 1$ | Critically damped | $(c_1+c_2 t)e^{-\alpha t}$ |
| $\zeta > 1$ | Overdamped | $c_1 e^{\lambda_1 t}+c_2 e^{\lambda_2 t}$ |

where $\alpha = c/(2m)$, $\omega_d = \sqrt{\omega_0^2-\alpha^2}$.

**Resonance** ($c=0$, $\omega = \omega_0$): $y_p = \dfrac{F_0}{2m\omega_0}\,t\sin\omega_0 t$ (grows without bound).

**Steady-state amplitude** ($c > 0$, forcing $F_0\cos\omega t$):
$$C(\omega) = \frac{F_0}{\sqrt{(k-m\omega^2)^2+c^2\omega^2}}, \qquad M = \frac{1}{\sqrt{(1-r^2)^2+(2\zeta r)^2}}, \quad r = \omega/\omega_0.$$

**Resonance peak** (for $\zeta < 1/\sqrt{2}$): $\omega_\text{res} = \omega_0\sqrt{1-2\zeta^2}$, $M_{\max} = \dfrac{1}{2\zeta\sqrt{1-\zeta^2}}$.

**Q-factor:** $Q = 1/(2\zeta) = \sqrt{mk}/c$.

**RLC analogy:** $m \leftrightarrow L$, $c \leftrightarrow R$, $k \leftrightarrow 1/C$, $\omega_0 = 1/\sqrt{LC}$, $Z = \sqrt{R^2+(L\omega-1/(C\omega))^2}$.

---

### Systems of ODEs — Eigenvalue Method (Week 10)

**Homogeneous system:** $\mathbf{y}' = \mathbf{A}\mathbf{y}$. Ansatz $\mathbf{y} = \mathbf{v}e^{\lambda t}$ $\Rightarrow$ eigenvalue problem $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$.

**Characteristic equation:** $\det(\mathbf{A}-\lambda\mathbf{I}) = \lambda^2 - (\text{tr}\,\mathbf{A})\lambda + \det\mathbf{A} = 0$.

| Eigenvalue type | General solution |
|-----------------|-----------------|
| Real distinct $\lambda_1 \neq \lambda_2$ | $\mathbf{y} = c_1\mathbf{v}^{(1)}e^{\lambda_1 t} + c_2\mathbf{v}^{(2)}e^{\lambda_2 t}$ |
| Complex $\lambda = \alpha \pm i\beta$ | $\mathbf{y} = e^{\alpha t}[c_1(\mathbf{a}\cos\beta t - \mathbf{b}\sin\beta t) + c_2(\mathbf{a}\sin\beta t + \mathbf{b}\cos\beta t)]$ |
| Repeated $\lambda$ (defective) | $\mathbf{y} = c_1\mathbf{v}e^{\lambda t} + c_2(\mathbf{v}t + \mathbf{u})e^{\lambda t}$, $(\mathbf{A}-\lambda\mathbf{I})\mathbf{u}=\mathbf{v}$ |
| Repeated $\lambda$ (complete) | $\mathbf{y} = (c_1\mathbf{v}^{(1)}+c_2\mathbf{v}^{(2)})e^{\lambda t}$ |

**Phase-plane classification** (using $p = \text{tr}\,\mathbf{A}$, $q = \det\mathbf{A}$, $D = p^2-4q$):

| Condition | Critical point | Stability |
|-----------|---------------|-----------|
| $q < 0$ | Saddle | Unstable |
| $q > 0$, $D > 0$, $p < 0$ | Stable node | Asymptotically stable |
| $q > 0$, $D > 0$, $p > 0$ | Unstable node | Unstable |
| $q > 0$, $D = 0$, $p < 0$ | Stable improper node | Asymptotically stable |
| $q > 0$, $D = 0$, $p > 0$ | Unstable improper node | Unstable |
| $q > 0$, $D < 0$, $p < 0$ | Stable spiral | Asymptotically stable |
| $q > 0$, $D < 0$, $p > 0$ | Unstable spiral | Unstable |
| $q > 0$, $p = 0$ | Center | Stable (not asymptot.) |

**Nonhomogeneous system:** $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}(t)$. General solution: $\mathbf{y} = \mathbf{y}_h + \mathbf{y}_p$.

---

### Part IV — Series and Power Series Methods (Weeks 11–13)

**Convergence tests:**

| Test | Criterion | Best for |
|------|-----------|---------|
| Ratio | $L=\lim|a_{n+1}/a_n|$; conv. if $L<1$, div. if $L>1$ | Factorials, exponentials |
| Root | $L=\lim|a_n|^{1/n}$; conv. if $L<1$, div. if $L>1$ | $n$-th powers |
| Integral | $\int_1^\infty f(x)\,dx$ conv. $\iff \sum a_n$ conv. | Decreasing, integrable |
| AST | $a_n \to 0$ decreasingly $\Rightarrow$ converges | Alternating series |
| LCT | $\lim a_n/b_n = L > 0$ $\Rightarrow$ same behaviour | Rational-looking terms |

**Power series:** $\sum c_n(x-x_0)^n$. Radius $R = \lim|c_n/c_{n+1}|$. Check endpoints separately.

**Taylor/Maclaurin:**
$$f(x) = \sum_{n=0}^\infty \frac{f^{(n)}(x_0)}{n!}(x-x_0)^n, \qquad |R_N(x)| \leq \frac{M}{(N+1)!}|x-x_0|^{N+1}.$$

**Standard series:**
$$e^x = \sum_{n=0}^\infty\frac{x^n}{n!},\quad \sin x = \sum_{n=0}^\infty\frac{(-1)^n x^{2n+1}}{(2n+1)!},\quad \cos x = \sum_{n=0}^\infty\frac{(-1)^n x^{2n}}{(2n)!},$$
$$\frac{1}{1-x} = \sum_{n=0}^\infty x^n \;(|x|<1),\quad \ln(1+x) = \sum_{n=1}^\infty\frac{(-1)^{n-1}}{n}x^n,\quad \arctan x = \sum_{n=0}^\infty\frac{(-1)^n}{2n+1}x^{2n+1}.$$

**Power series ODE method:** Assume $y=\sum c_n x^n$; re-index $y''=\sum_{n=0}^\infty(n+2)(n+1)c_{n+2}x^n$; collect like powers of $x$; equate coefficients to zero $\Rightarrow$ recurrence relation.

**Legendre polynomials** $(1-x^2)y''-2xy'+n(n+1)y=0$:
$$P_0=1,\quad P_1=x,\quad P_2=\tfrac{1}{2}(3x^2-1),\quad P_3=\tfrac{1}{2}(5x^3-3x).$$
Orthogonality: $\displaystyle\int_{-1}^1 P_m P_n\,dx = \dfrac{2}{2n+1}\delta_{mn}$.
Legendre series: $f(x) = \sum a_n P_n(x)$, $a_n = \dfrac{2n+1}{2}\displaystyle\int_{-1}^1 f(x)P_n(x)\,dx$.

**Frobenius method** (regular singular point): $y = x^r\sum_{n=0}^\infty a_n x^n$, $a_0 \neq 0$. Indicial equation from the $n=0$ coefficient. Three cases for roots $r_1, r_2$ ($r_1 \geq r_2$): (1) $r_1-r_2 \notin \mathbb{Z}$: two Frobenius series; (2) $r_1 = r_2$: second solution has $\ln x$ term; (3) $r_1-r_2 \in \mathbb{Z}^+$: second solution may have $\ln x$ term.

**Bessel equation:** $x^2y''+xy'+(x^2-\nu^2)y=0$. Solutions $J_\nu(x)$ (finite at $0$) and $Y_\nu(x)$ (singular at $0$). $J_0(0)=1$, $J_n(0)=0$ for $n \geq 1$, $J_0'(x)=-J_1(x)$.

---

### Part V — Laplace Transforms (Weeks 14–15)

**Definition:** $\mathcal{L}\{f(t)\} = F(s) = \displaystyle\int_0^\infty e^{-st}f(t)\,dt$.

**Standard table:**

| $f(t)$ | $F(s)$ | | $f(t)$ | $F(s)$ |
|--------|--------|-|--------|--------|
| $1$ | $1/s$ | | $e^{at}$ | $1/(s-a)$ |
| $t^n$ | $n!/s^{n+1}$ | | $t^n e^{at}$ | $n!/(s-a)^{n+1}$ |
| $\sin\omega t$ | $\omega/(s^2+\omega^2)$ | | $e^{at}\sin\omega t$ | $\omega/((s-a)^2+\omega^2)$ |
| $\cos\omega t$ | $s/(s^2+\omega^2)$ | | $e^{at}\cos\omega t$ | $(s-a)/((s-a)^2+\omega^2)$ |
| $\sinh at$ | $a/(s^2-a^2)$ | | $u(t-a)$ | $e^{-as}/s$ |
| $\cosh at$ | $s/(s^2-a^2)$ | | $\delta(t-a)$ | $e^{-as}$ |

**Transform of derivatives:**
$$\mathcal{L}\{y'\} = sY-y(0), \qquad \mathcal{L}\{y''\} = s^2Y - sy(0) - y'(0).$$

**1st Shifting Theorem ($s$-shift):** $\mathcal{L}\{e^{at}f(t)\} = F(s-a)$.

**2nd Shifting Theorem ($t$-shift):** $\mathcal{L}\{u(t-a)f(t-a)\} = e^{-as}F(s)$.

**Sifting property:** $\mathcal{L}\{\delta(t-a)\} = e^{-as}$; $\displaystyle\int_0^\infty f(t)\delta(t-a)\,dt = f(a)$.

**Convolution:** $(f*g)(t) = \displaystyle\int_0^t f(\tau)g(t-\tau)\,d\tau$; $\mathcal{L}\{f*g\} = F(s)G(s)$.

**IVP pipeline:** Transform $\to$ Solve $Y(s)$ $\to$ PFD / complete the square $\to$ Apply shifting theorems $\to$ Invert.

**Partial fractions:**
$$\frac{P(s)}{(s-a)(s-b)} = \frac{A}{s-a}+\frac{B}{s-b}, \quad \frac{P(s)}{(s-a)^2} = \frac{A}{s-a}+\frac{B}{(s-a)^2}, \quad \frac{P(s)}{(s-a)^2+\omega^2} = \frac{As+B}{(s-a)^2+\omega^2}.$$

**Completing the square:** $s^2+bs+c = \left(s+\dfrac{b}{2}\right)^2+c-\dfrac{b^2}{4}$.

---

## Topic-by-Topic Review Notes

### Week 9 — Oscillations and 2×2 Matrix Foundations

**Free oscillations ($m\ddot{y}+c\dot{y}+ky=0$) — checklist:**
1. Compute $\alpha = c/(2m)$, $\omega_0 = \sqrt{k/m}$, $\zeta = c/(2\sqrt{mk})$ (or check discriminant $\Delta = c^2-4mk$).
2. Identify regime: $\Delta < 0$ (underdamped), $\Delta = 0$ (critically damped), $\Delta > 0$ (overdamped).
3. Write $y_h$; apply ICs.

**Forced oscillations ($c=0$) — key cases:**
- $\omega \neq \omega_0$: trial $y_p = A\cos\omega t$, giving $A = F_0/m(\omega_0^2-\omega^2)$.
- $\omega = \omega_0$ (resonance): trial $y_p = t(A\cos\omega_0 t+B\sin\omega_0 t)$, giving the $t\sin\omega_0 t$ factor.
- $\omega \approx \omega_0$: beat formula with amplitude pulsation at rate $|\omega_0-\omega|$.

**RLC circuits:** Replace $m \to L$, $c \to R$, $k \to 1/C$ in every formula. $\omega_0 = 1/\sqrt{LC}$.

**2×2 eigenvalue problem — row equation method:**
1. Characteristic equation $\lambda^2 - (\text{tr}\,\mathbf{A})\lambda + \det\mathbf{A} = 0 \Rightarrow \lambda_1, \lambda_2$.
2. For each $\lambda_k$: form $\mathbf{B} = \mathbf{A}-\lambda_k\mathbf{I}$, pick any nonzero row, solve $b_{11}v_1+b_{12}v_2=0$.
3. Eigenvectors determined up to scalar; choose convenient representative.

**Most common mistakes — Week 9:**
- Writing $\omega_0 = \sqrt{LC}$ instead of $\omega_0 = 1/\sqrt{LC}$ for the RLC circuit.
- In pure resonance: writing $y_p = A\cos\omega_0 t + B\sin\omega_0 t$ (which is in $y_h$) rather than using the modification rule.
- Confusing $\omega_0$ (natural frequency) with $\omega_d = \omega_0\sqrt{1-\zeta^2}$ (damped frequency).

---

### Week 10 — Systems of ODEs and Phase Plane

**Eigenvalue method — three cases:**

**Case 1: Distinct real eigenvalues** $\lambda_1 \neq \lambda_2$
$$\mathbf{y}(t) = c_1\mathbf{v}^{(1)}e^{\lambda_1 t} + c_2\mathbf{v}^{(2)}e^{\lambda_2 t}.$$
Phase plane: node (both negative $\to$ stable, both positive $\to$ unstable) or saddle (opposite signs $\to$ always unstable).

**Case 2: Complex eigenvalues** $\lambda = \alpha \pm i\beta$

Complex eigenvector for $\lambda = \alpha+i\beta$: $\mathbf{v} = \mathbf{a}+i\mathbf{b}$. Real general solution:
$$\mathbf{y}(t) = e^{\alpha t}\bigl[c_1(\mathbf{a}\cos\beta t - \mathbf{b}\sin\beta t) + c_2(\mathbf{a}\sin\beta t + \mathbf{b}\cos\beta t)\bigr].$$
Phase plane: spiral ($\alpha \neq 0$) or center ($\alpha = 0$).

**Case 3: Repeated eigenvalue** $\lambda$ (defective, one eigenvector only)

Find generalised eigenvector $\mathbf{u}$ from $(\mathbf{A}-\lambda\mathbf{I})\mathbf{u} = \mathbf{v}$:
$$\mathbf{y}(t) = c_1\mathbf{v}e^{\lambda t} + c_2(\mathbf{v}t + \mathbf{u})e^{\lambda t}.$$
Phase plane: improper (degenerate) node.

**Phase-plane quick diagnostics** (no computation needed):
- $\det\mathbf{A} < 0$: saddle (always unstable).
- $\det\mathbf{A} > 0$, $\text{tr}\,\mathbf{A} = 0$: center (neutrally stable).
- $\det\mathbf{A} > 0$, $\text{tr}\,\mathbf{A} < 0$: stable (spiral or node).
- $\det\mathbf{A} > 0$, $\text{tr}\,\mathbf{A} > 0$: unstable (spiral or node).

**Linearisation at a critical point** $(x_0, y_0)$ of $x'=f(x,y)$, $y'=g(x,y)$:
Jacobian $\mathbf{A} = \begin{pmatrix}f_x & f_y \\ g_x & g_y\end{pmatrix}$ evaluated at $(x_0,y_0)$. Classify the linearised system; the nonlinear system has the same type (except at border cases: center vs. spiral).

**Most common mistakes — Week 10:**
- Case 2: Extracting $\mathbf{a}$ and $\mathbf{b}$ from the complex eigenvector $\mathbf{v} = \mathbf{a}+i\mathbf{b}$ and then writing $c_1 e^{\alpha t}\mathbf{a}\cos\beta t + c_2 e^{\alpha t}\mathbf{b}\sin\beta t$ (missing the cross terms). The correct form has both $\mathbf{a}$ and $\mathbf{b}$ in each part.
- Case 3: Trying to find two eigenvectors instead of one eigenvector and one generalised eigenvector.
- Forgetting the extra $\mathbf{v}t$ term in the Case 3 second solution.
- Applying ICs to the wrong function (applying before combining $c_1$, $c_2$).

---

### Week 11 — Convergence Tests and Power Series

**Quick decision tree:**
- Terms have $n!$ or $n^n$ → Ratio Test.
- Terms are $n$-th powers → Root Test.
- Decreasing, positive, integrable function → Integral Test.
- Alternating series → AST (then check absolute convergence separately).
- Looks like $p(n)/q(n)$ (rational in $n$) → LCT with $p$-series $\sum 1/n^k$.

**Interval of convergence (IOC) procedure:**
1. Apply Ratio Test to get $R = \lim|c_n/c_{n+1}|$ (or $1/\lim|c_{n+1}/c_n|$).
2. IOC interior: $(x_0-R,\; x_0+R)$.
3. **Test both endpoints** $x_0 \pm R$ separately (Ratio Test gives $L=1$ there; use AST, $p$-series, etc.).

**Most common mistakes — Week 11:**
- Concluding convergence or divergence when the Ratio/Root Test gives $L=1$. It is **inconclusive**.
- IOC: forgetting to check endpoints, or including/excluding the wrong endpoint.
- AST: invoking it on a non-alternating or non-decreasing series.
- Reporting "absolutely convergent" from the AST alone — AST gives only conditional convergence.

---

### Week 12 — Taylor Series and Power Series ODE Method

**Taylor series limits** (know these):
$$\lim_{x\to 0}\frac{\sin x - x}{x^3} = -\frac{1}{6}, \quad \lim_{x\to 0}\frac{1-\cos x}{x^2} = \frac{1}{2}, \quad \lim_{x\to 0}\frac{e^x-1-x}{x^2} = \frac{1}{2}.$$

**Power series ODE method — standard procedure:**
1. Substitute $y = \sum_{n=0}^\infty c_n x^n$ into the ODE.
2. Re-index $y'' = \sum_{n=0}^\infty (n+2)(n+1)c_{n+2}x^n$ (shift index by 2 when writing $y''$).
3. Collect all terms as a single power series in $x^n$.
4. Set the coefficient of each $x^n$ to zero → recurrence relation for $c_{n+2}$ (or $c_{n+k}$) in terms of earlier $c_j$.
5. $c_0$ and $c_1$ are free parameters (two linearly independent solutions); the recurrence generates all higher coefficients.
6. Write the two independent solutions (even-power series with $c_0$, odd-power series with $c_1$), or identify the terminating series (polynomial) if one exists.

**Most common mistakes — Week 12:**
- Re-indexing $y''$ incorrectly. After re-indexing, $y'' = \sum_{n=0}^\infty(n+2)(n+1)c_{n+2}x^n$ — the *running* index is $n$, not $n+2$.
- Forgetting to handle the $n=0$ and $n=1$ equations separately before the main recurrence starts.
- Evaluating limits by substituting only the leading term without cancelling correctly.

---

### Week 13 — Legendre, Frobenius, and Bessel

**Legendre series** — what to know:
- $P_0=1$, $P_1=x$, $P_2=\tfrac{1}{2}(3x^2-1)$, $P_3=\tfrac{1}{2}(5x^3-3x)$ (memorize or derive from Rodrigues).
- Orthogonality: $\int_{-1}^1 P_m P_n\,dx = \tfrac{2}{2n+1}\delta_{mn}$.
- Coefficient: $a_n = \tfrac{2n+1}{2}\int_{-1}^1 f P_n\,dx$ (the $\tfrac{2n+1}{2}$ factor is essential).

**Frobenius method** — what to know:
- Identify a **regular singular point** $x_0$: $p(x) = (x-x_0)P(x)$ and $q(x) = (x-x_0)^2 Q(x)$ with $P,Q$ analytic at $x_0$.
- Indicial equation from $n=0$ term: $r(r-1)+P_0 r + Q_0 = 0$ (where $P_0 = \lim_{x\to x_0}(x-x_0)p$, $Q_0 = \lim_{x\to x_0}(x-x_0)^2 q$).
- Three cases for roots $r_1 \geq r_2$: (1) $r_1-r_2 \notin \mathbb{Z}$: two Frobenius series; (2) $r_1=r_2$: need $\ln$ for second solution; (3) $r_1-r_2 \in \mathbb{Z}^+$: second solution from $r_2$ (may or may not need $\ln$).

**Bessel** — what to know:
- Recognise the equation $x^2y''+xy'+(x^2-\nu^2)y=0$.
- $J_0(0)=1$, $J_n(0)=0$ for $n \geq 1$.
- $J_0'(x) = -J_1(x)$.
- $Y_\nu$ is singular at $x=0$: discard when seeking bounded solutions at the origin.

**Most common mistakes — Week 13:**
- Legendre coefficients: forgetting the $\frac{2n+1}{2}$ factor.
- Orthogonality: writing $\int_{-1}^1 P_m P_n = \delta_{mn}$ (missing the $\frac{2}{2n+1}$).
- Frobenius: using the regular power series method ($r=0$ only) when the equation has a singular point.
- Bessel: writing $J_0'=-J_0$ instead of $J_0'=-J_1$.

---

### Weeks 14–15 — Laplace Transforms

**IVP pipeline — five steps:**
1. Take $\mathcal{L}$ of both sides: $\mathcal{L}\{y''\} = s^2Y-sy(0)-y'(0)$; $\mathcal{L}\{y'\}=sY-y(0)$.
2. Collect all $Y(s)$ terms on one side; solve for $Y(s)$.
3. Decompose $Y(s)$ by partial fractions (linear, repeated, or irreducible quadratic factors).
4. Complete the square for terms like $s^2+bs+c$; apply the 1st Shifting Theorem.
5. For terms with $e^{-as}$: factor out $e^{-as}$, find $\mathcal{L}^{-1}$ of the remaining $G(s)$, then apply the 2nd Shifting Theorem: result is $u(t-a)\,g(t-a)$.

**Both shifting theorems — side by side:**

| Theorem | Forward | Inverse |
|---------|---------|---------|
| 1st (s-shift) | $e^{at}f(t) \xrightarrow{\mathcal{L}} F(s-a)$ | $F(s-a) \xrightarrow{\mathcal{L}^{-1}} e^{at}f(t)$ |
| 2nd (t-shift) | $u(t-a)f(t-a) \xrightarrow{\mathcal{L}} e^{-as}F(s)$ | $e^{-as}F(s) \xrightarrow{\mathcal{L}^{-1}} u(t-a)f(t-a)$ |

**Delta forcing** $y'' + py' + qy = \delta(t-a)$: the delta contributes $e^{-as}$ to $R(s) = \mathcal{L}\{r(t)\}$.

**Convolution** $(f*g)(t) = \int_0^t f(\tau)g(t-\tau)\,d\tau$: useful for inverting a product $F(s)G(s)$ when PFD is awkward.

**Impulse response** $h(t) = \mathcal{L}^{-1}\{H(s)\}$ where $H(s)=1/Q(s)$: the system's response to $\delta(t)$ with zero ICs. Response to any input $r(t)$: $y_p(t) = (h*r)(t)$.

**Most common mistakes — Weeks 14–15:**
- $\mathcal{L}\{y''\}$: omitting the $y'(0)$ term; writing $s^2Y - y(0)$ instead of $s^2Y - sy(0) - y'(0)$.
- Before applying the 1st Shifting Theorem: failing to complete the square ($s^2+4s+13 = (s+2)^2+9$).
- 2nd Shifting Theorem (inverse): writing $u(t-a)\,g(t)$ instead of $u(t-a)\,g(t-a)$ — $t$ must be replaced by $t-a$.
- Confusing the two theorems: 1st is triggered by $e^{at}$ in $f(t)$ or shifted $s$; 2nd is triggered by $e^{-as}$ multiplying $F(s)$ or $u(t-a)$ in $f(t)$.
- Treating $\delta(t-a)$ like a regular function; use the sifting property directly.

---

## Sample Final Examination Problems

The following problems illustrate the level and style expected. They cover all seven weeks in proportion to their expected exam weight. These are **not** the actual exam.

---

### Section A — Oscillations and Matrix Foundations (Week 9)

**Problem A1 (Free oscillations):** A mass-spring system satisfies $2\ddot{y} + 8\dot{y} + 8y = 0$, $y(0) = 1$, $\dot{y}(0) = 0$.

(a) Classify the system (overdamped / critically damped / underdamped) and find $\zeta$.

(b) Solve the IVP.

(c) Find $\lim_{t\to\infty} y(t)$.

---

**Problem A2 (Forced oscillations):** Solve $\ddot{y} + 25y = 5\cos 5t$, $y(0) = 0$, $\dot{y}(0) = 1$.

(a) Explain why the standard trial $y_p = A\cos 5t$ fails.

(b) Apply the modification rule and find $y_p$.

(c) Write the general solution and describe the long-term behaviour.

---

**Problem A3 (Eigenvalues):** For $\mathbf{A} = \begin{pmatrix}5 & -2 \\ 4 & -1\end{pmatrix}$:

(a) Find all eigenvalues and eigenvectors.

(b) Using the phase-plane classification table, identify the type of critical point and its stability.

---

### Section B — Systems of ODEs and Phase Plane (Week 10)

**Problem B1 (Distinct real eigenvalues):** Solve the IVP:
$$\mathbf{y}' = \begin{pmatrix}3 & 1 \\ 1 & 3\end{pmatrix}\mathbf{y}, \qquad \mathbf{y}(0) = \begin{pmatrix}2 \\ 0\end{pmatrix}.$$

(a) Find the eigenvalues and eigenvectors.

(b) Write the general solution.

(c) Apply the initial condition and give the solution $\mathbf{y}(t)$.

---

**Problem B2 (Complex eigenvalues):** Solve:
$$\mathbf{y}' = \begin{pmatrix}1 & -5 \\ 1 & -1\end{pmatrix}\mathbf{y}.$$

(a) Find the eigenvalues $\lambda = \alpha \pm i\beta$ and the complex eigenvector for $\lambda = \alpha + i\beta$.

(b) Extract $\mathbf{a} = \text{Re}(\mathbf{v})$ and $\mathbf{b} = \text{Im}(\mathbf{v})$, and write the real general solution.

(c) Classify the critical point and determine its stability.

---

**Problem B3 (Repeated eigenvalue):** Find the general solution of:
$$\mathbf{y}' = \begin{pmatrix}-3 & 1 \\ 0 & -3\end{pmatrix}\mathbf{y}.$$

(a) Show that $\lambda = -3$ is a repeated eigenvalue with only one eigenvector.

(b) Find the generalised eigenvector $\mathbf{u}$ satisfying $(\mathbf{A}+3\mathbf{I})\mathbf{u} = \mathbf{v}$.

(c) Write the general solution and classify the critical point.

---

**Problem B4 (Phase-plane classification — no calculation):** For each matrix below, use only $p = \text{tr}\,\mathbf{A}$ and $q = \det\mathbf{A}$ to classify the critical point of $\mathbf{y}' = \mathbf{A}\mathbf{y}$ and state its stability:

(a) $\mathbf{A} = \begin{pmatrix}2 & -5 \\ 1 & -2\end{pmatrix}$ $\qquad$ (b) $\mathbf{A} = \begin{pmatrix}-1 & 3 \\ -3 & -1\end{pmatrix}$ $\qquad$ (c) $\mathbf{A} = \begin{pmatrix}2 & 1 \\ 3 & 4\end{pmatrix}$

---

### Section C — Convergence and Series (Week 11)

**Problem C1 (Convergence tests):** Determine whether each series converges absolutely, converges conditionally, or diverges:

(a) $\displaystyle\sum_{n=1}^\infty \frac{3^n}{n!\,n}$

(b) $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n}{\sqrt{n}}$

(c) $\displaystyle\sum_{n=1}^\infty \frac{n^2+1}{2n^3-1}$

---

**Problem C2 (Interval of convergence):** Find the radius and interval of convergence of $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n(x+2)^n}{n \cdot 4^n}$, including analysis of both endpoints.

---

### Section D — Taylor Series and Power Series ODE Method (Week 12)

**Problem D1 (Taylor series limit):** Evaluate without L'Hôpital's rule:
$$\lim_{x\to 0}\frac{e^{2x} - 1 - 2x - 2x^2}{x^3}.$$

---

**Problem D2 (Power series ODE):** Apply the power series method to $y'' - xy' - y = 0$ centred at $x_0 = 0$.

(a) Substitute $y = \sum_{n=0}^\infty c_n x^n$ and derive the recurrence relation.

(b) Write the two linearly independent series solutions (even and odd), giving the first three nonzero terms of each.

---

### Section E — Legendre and Bessel (Week 13)

**Problem E1 (Legendre series):** Expand $f(x) = x^2 + 2x - 1$ as a finite Legendre series $f(x) = \sum_{n=0}^N a_n P_n(x)$. Determine all non-zero coefficients.

---

**Problem E2 (Frobenius / recognition):** Consider $x^2 y'' + x\,y' + (x^2 - \tfrac{1}{4})y = 0$.

(a) Show that $x = 0$ is a regular singular point and find the indicial equation.

(b) Identify the equation as a Bessel equation and state the order $\nu$.

(c) Write the general solution in terms of Bessel functions, noting which solution is bounded at $x = 0$.

---

### Section F — Laplace Transforms (Weeks 14–15)

**Problem F1 (Inverse Laplace):** Find $\mathcal{L}^{-1}$ of each:

(a) $\dfrac{2s+3}{s^2+2s+5}$

(b) $\dfrac{s+1}{s^2(s-2)}$

---

**Problem F2 (IVP by Laplace):** Solve $y'' + 4y' + 4y = 4e^{-2t}$, $y(0) = 0$, $y'(0) = 1$, using the Laplace transform.

---

**Problem F3 (IVP with step forcing):** Solve $y'' + 9y = 18\,u(t-\pi)$, $y(0) = 0$, $y'(0) = 0$.

(a) Take the Laplace transform and solve for $Y(s)$.

(b) Invert using the 2nd Shifting Theorem.

(c) Write $y(t)$ as a piecewise function (for $0 \leq t < \pi$ and for $t \geq \pi$).

---

**Problem F4 (Delta forcing):** Solve $y'' + 2y' + 2y = \delta(t-\pi)$, $y(0) = 1$, $y'(0) = 0$.

(a) Transform and solve for $Y(s)$.

(b) Write $Y(s) = Y_{\text{IC}}(s) + Y_{\text{forcing}}(s)$ and invert each part.

(c) Describe the effect of the delta impulse at $t = \pi$ on the oscillation.

---

**Problem F5 (Convolution):** Use convolution to find $\mathcal{L}^{-1}\!\left\{\dfrac{1}{s(s^2+4)}\right\}$.

Verify your answer by partial fractions.

---

## Final Examination Information

| Item | Detail |
|------|--------|
| Date | To be announced |
| Location | To be announced |
| Duration | 120 minutes |
| Format | Closed-book; formula sheet provided by instructor |
| Calculators | Not permitted |
| Coverage | Weeks 9–15 only |
| Grade appeal | Opens immediately after exams are returned |

**Good luck!**
