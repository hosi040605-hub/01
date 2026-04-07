# Week 8 — Midterm Examination

**Course:** Engineering Mathematics 1
**Coverage:** Weeks 1–7 — Part I (Calculus), Part II (First-Order ODEs), and Part III (Second-Order and Higher-Order ODEs)
**Kreyszig Sections:** §1.1–1.4, §1.5, §1.7; §2.1, §2.2, §2.5, §2.6, §2.7, §2.10; §3.1–3.3

> **Structure of Week 8:** Lecture 1 and Lecture 2 are pre-exam review sessions organised by part. The Midterm Examination occupies the Lecture 3 slot. The Practice Session is used for exam return, grade appeal, and a brief preview of Week 9.
>
> **Note:** §2.4 (Free Oscillations modelling) is covered in Week 10 and is **not** on the Midterm.

---

## Pre-Exam Review 1 — Part I (Weeks 1–3) and Part II (Weeks 4–5)

### Introduction

This review lecture consolidates the key formulas, methods, and conceptual connections from the first seven weeks of the course. It focuses on the ideas most likely to appear on the Midterm and on the connections between Parts I and II that students are expected to draw on fluently.

**Part I (Weeks 1–3):** Differentiation and integration tools. These are not directly tested for their own sake on the Midterm, but are required at every step of the ODE solution methods in Parts II and III. Weak calculation skills in Part I produce errors in Part II and III solutions.

**Part II (Weeks 4–5):** Five first-order ODE methods. The Midterm will test method identification (which method applies?), execution (carrying out the method without errors), and physical interpretation (what does the solution mean?).

---

### Knowledge Points

---

#### 1. Part I Review — Differentiation (Week 1)

**Fundamental rules:**

| Rule | Formula |
|------|---------|
| Power | $(x^n)' = nx^{n-1}$ |
| Product | $(uv)' = u'v + uv'$ |
| Quotient | $(u/v)' = (u'v - uv')/v^2$ |
| Chain | $(f(g(x)))' = f'(g(x))\cdot g'(x)$ |
| Exponential | $(e^x)' = e^x$; $(a^x)' = a^x\ln a$ |
| Logarithm | $(\ln x)' = 1/x$; $(\log_a x)' = 1/(x\ln a)$ |
| Trigonometric | $(\sin x)' = \cos x$; $(\cos x)' = -\sin x$; $(\tan x)' = \sec^2 x$ |
| Inverse trig and Inverse hyperbolic | $(\arctan x)' = 1/(1+x^2)$; $(\arcsin x)' = 1/\sqrt{1-x^2}$; $(\arccos x)' = -1/\sqrt{1-x^2}$; $(\sinh^{-1} x)' = 1/\sqrt{1+x^2}$; $(\cosh^{-1} x)' = 1/\sqrt{x^2-1}$ |

**Hyperbolic functions (Week 1, Lecture 2):**
$$\sinh x = \frac{e^x - e^{-x}}{2}, \quad \cosh x = \frac{e^x + e^{-x}}{2}, \quad \tanh x = \frac{\sinh x}{\cosh x}.$$
Identity: $\cosh^2 x - \sinh^2 x = 1$ (sign differs from trig!).
Derivatives: $(\sinh x)' = \cosh x$; $(\cosh x)' = \sinh x$; $(\tanh x)' = \text{sech}^2 x$.

**Reappearance:** Hyperbolic functions arise as solutions of $y'' - \omega^2 y = 0$ (characteristic roots $\pm\omega$): $y = A\cosh\omega x + B\sinh\omega x$ — used in Week 6 and Week 10. The function $\tanh$ appears in the quadratic-drag falling body solution (Week 5).

---

#### 2. Part I Review — Integration Techniques (Week 2)

**Fundamental Theorem of Calculus:**
$$\int_a^b f(x)\,dx = F(b) - F(a), \quad F'(x) = f(x).$$

**Integration techniques and when to use each:**

| Technique | When to apply | Key step |
|-----------|--------------|---------|
| u-substitution | Composite functions | Set $u = g(x)$; $du = g'(x)dx$ |
| Integration by Parts | Products (LIATE order) | $\int u\,dv = uv - \int v\,du$ |
| Partial Fractions | Rational functions | Factor denominator; decompose |
| Completing the square | Quadratic denominator | $(ax^2+bx+c) \to a(x+p)^2+q$ |
| Trig substitution | $\sqrt{a^2-x^2}$, $\sqrt{a^2+x^2}$, $\sqrt{x^2-a^2}$ | $x = a\sin\theta$, $a\tan\theta$, $a\sec\theta$ |

**Improper integrals (Week 2, Lecture 1):**
$$\int_a^\infty f(x)\,dx = \lim_{R\to\infty}\int_a^R f(x)\,dx.$$
Converges if the limit is finite. Key examples: $\int_1^\infty x^{-p}dx$ converges iff $p > 1$.

**Reappearance:** These integrals appear directly in every ODE solution method: $\int p\,dx$ for integrating factors, $\int \mu r\,dx$ for linear ODEs, $\int dy/h(y)$ for separable equations. Partial fractions are used in VoP integrals (Week 7). Completing the square will appear centrally in inverse Laplace transforms (Weeks 14–15).

---

#### 3. Part I Review — Partial Fractions and Completing the Square (Week 2)

**Partial fractions — method review:**

Decompose $r(x)/q(x)$ (degree $r <$ degree $q$) by factoring $q(x)$:
- Linear factor $(x-a)$: contributes $A/(x-a)$.
- Repeated linear $(x-a)^k$: contributes $A_1/(x-a) + \cdots + A_k/(x-a)^k$.
- Irreducible quadratic $(x^2+bx+c)$: contributes $(Bx+C)/(x^2+bx+c)$.

**Example:**
$$\frac{5x+3}{(x-1)(x^2+1)} = \frac{A}{x-1} + \frac{Bx+C}{x^2+1}.$$
Multiply through: $5x+3 = A(x^2+1) + (Bx+C)(x-1)$.
Set $x=1$: $8 = 2A \Rightarrow A=4$. Comparing $x^2$: $0 = A+B \Rightarrow B=-4$. Comparing $x^0$: $3=A-C \Rightarrow C=1$.

**Completing the square:**
$$ax^2 + bx + c = a\!\left[\left(x + \frac{b}{2a}\right)^2 + \frac{c}{a} - \frac{b^2}{4a^2}\right].$$

This converts integrals of the form $\int dx/(ax^2+bx+c)$ to standard arctangent or logarithm forms.

**Reappearance:** Partial fractions appear in solving the logistic equation (Week 4/5) and will reappear centrally in inverse Laplace transforms (Weeks 14–15). Completing the square appears in Laplace transform inversions with complex roots.

---

#### 4. Part II Review — First-Order ODE Methods: Overview (Weeks 4–5)

**Master method selection guide:**

```
Step 1: Is F(x,y) = g(x)·h(y)?          → Separable. Separate and integrate.
         ↓ NO

Step 2: Does x not appear in F?          → Autonomous. Phase line + separable.
         ↓ NO

Step 3: Linear form y' + p(x)y = r(x)?  → Integrating Factor method.
         ↓ NO

Step 4: Bernoulli: y' + p(x)y = r(x)yⁿ? → v = y^(1-n) substitution.
         ↓ NO

Step 5: M dx + N dy = 0, Mᵧ = Nₓ?      → Exact. Find potential F(x,y).
         ↓ NO

Step 6: (Mᵧ-Nₓ)/N = P(x) only?         → μ(x) = e^(∫P dx). Multiply; exact.
        (Nₓ-Mᵧ)/M = Q(y) only?          → μ(y) = e^(∫Q dy). Multiply; exact.
         ↓ NONE

Step 7: Numerical (Euler/Heun/RK4) or special substitution.
```

**Priority note:** Steps are roughly in order of computational simplicity (separable is easiest; numerical is a last resort), but some ODEs satisfy multiple criteria. When in doubt, try separable first.

---

#### 5. Part II Review — Separable and Exact ODEs (Week 4)

**Separable ODEs** $y' = g(x)h(y)$:
$$\int\frac{dy}{h(y)} = \int g(x)\,dx + C.$$
Always check for singular solutions $h(y) = 0$ that were lost by division.

**Key examples:**
- Exponential: $y' = ky \Rightarrow y = Ce^{kx}$.
- Radiocarbon dating: $dN/dt = -\lambda N$, half-life $t_{1/2} = \ln 2/\lambda$.
- Newton's Cooling: $T' = -k(T-T_e) \Rightarrow T = T_e + (T_0-T_e)e^{-kt}$.

**Exact ODEs** $M\,dx + N\,dy = 0$ with $M_y = N_x$:
$$F(x,y) = C, \quad F_x = M,\; F_y = N.$$
**Algorithm:** Integrate $M$ in $x$ to get $F = \int M\,dx + g(y)$. Differentiate in $y$ and match $N$ to find $g'(y)$.

**Integrating factors** (if not exact): If $(M_y - N_x)/N = P(x)$ depends only on $x$: $\mu = e^{\int P\,dx}$.

---

#### 6. Part II Review — Linear First-Order ODEs (Week 5)

**Standard form:** $y' + p(x)y = r(x)$.

**Solution:**
$$\mu(x) = e^{\int p\,dx}, \qquad y = \frac{1}{\mu(x)}\left(\int\mu(x)r(x)\,dx + C\right).$$

**Structure:** $y = y_h + y_p = Ce^{-\int p\,dx} + y_p$.

**Key examples:**
- Constant $p$, $r$: $y' + ky = A \Rightarrow y = A/k + Ce^{-kx}$.
- RC circuit: $Q' + Q/(RC) = V/R \Rightarrow Q = CV + (Q_0-CV)e^{-t/(RC)}$, $\tau = RC$.

**Existence and Uniqueness (linear):** If $p$, $r$ are continuous on $I \ni x_0$, the IVP has a unique solution on **all** of $I$ — not just locally. This is stronger than Picard–Lindelöf.

---

#### 7. Part II Review — Bernoulli Equations and Logistic Growth (Week 5)

**Bernoulli equation:** $y' + p(x)y = r(x)y^n$ ($n \neq 0, 1$).

**Substitution:** $v = y^{1-n}$. Then $v' + (1-n)p(x)v = (1-n)r(x)$ — linear in $v$.

**The logistic equation** ($n = 2$, $p = -r$, $r(x) = r/K$):
$$P' = rP\left(1-\frac{P}{K}\right), \quad P(t) = \frac{K}{1+\!\left(\frac{K-P_0}{P_0}\right)e^{-rt}}.$$
- $P = 0$: unstable equilibrium. $P = K$: stable equilibrium.
- Inflection at $P = K/2$ (fastest growth).
- Maximum sustainable yield: $H_{\rm MSY} = rK/4$ at $P = K/2$.

**Picard–Lindelöf Theorem:** IVP $y' = f(x,y)$, $y(x_0) = y_0$ has a unique local solution if $f$ and $\partial f/\partial y$ are continuous near $(x_0,y_0)$. When $\partial f/\partial y$ is unbounded, uniqueness can fail (e.g., $y' = y^{2/3}$, $y(0) = 0$ has infinitely many solutions).

---

#### 8. Part II Review — Autonomous Equations and Phase Line (Week 5)

**Autonomous ODE:** $y' = f(y)$ — no explicit $x$ (or $t$). The direction field repeats in vertical strips.

**Phase line construction:**
1. Find equilibria: solve $f(y^*) = 0$.
2. Determine sign of $f(y)$ between equilibria.
3. Draw arrows up ($\uparrow$) where $f > 0$, down ($\downarrow$) where $f < 0$.

**Stability classification:**
- **Stable (sink):** arrows converge to $y^*$ from both sides; $f'(y^*) < 0$.
- **Unstable (source):** arrows diverge from $y^*$; $f'(y^*) > 0$.
- **Semi-stable:** arrows toward from one side only.

**Derivative criterion:** $f'(y^*) < 0 \Rightarrow$ stable; $f'(y^*) > 0 \Rightarrow$ unstable; $f'(y^*) = 0 \Rightarrow$ inconclusive.

**Basins of attraction:** In 1D, the basin of a stable equilibrium $y^*$ is the open interval between the two nearest unstable equilibria.

---

#### 9. Part II Review — Modeling: RL Circuits and Falling Body (Week 5)

**RL circuit** (Kirchhoff's voltage law):
$$i' + \frac{R}{L}i = \frac{E(t)}{L}, \qquad \tau = \frac{L}{R}.$$
Constant $E_0$: $i(t) = E_0/R + (i_0 - E_0/R)e^{-t/\tau}$.
- Steady state: $i_p = E_0/R$. Transient: decays with time constant $\tau = L/R$.

**Falling body — linear drag:**
$$v' + \frac{b}{m}v = g, \quad v_T = \frac{mg}{b},\quad \tau = \frac{m}{b}.$$
$v(t) = v_T(1 - e^{-t/\tau})$. Terminal velocity $v_T$ is the unique stable equilibrium.

**Falling body — quadratic drag:**
$$v' = g - \frac{c}{m}v^2, \quad v_T = \sqrt{\frac{mg}{c}}.$$
$v(t) = v_T\tanh(gt/v_T)$. (Separable; solution involves $\tanh$ from Week 1.)

**Structural analogy:**

| RL circuit | Falling body (linear drag) |
|------------|--------------------------|
| $i' + (R/L)i = E/L$ | $v' + (b/m)v = g$ |
| $\tau = L/R$ | $\tau = m/b$ |
| $i_\infty = E/R$ | $v_\infty = mg/b$ |

Both share the same mathematical structure: first-order linear ODE with a unique globally stable equilibrium.

---

#### 10. Part II Review — Euler's Method and Numerical Approximation (Week 4)

**Euler's method** for $y' = f(x,y)$, $y(x_0) = y_0$, step size $h$:
$$x_{n+1} = x_n + h, \qquad y_{n+1} = y_n + h\,f(x_n, y_n).$$
Global error: $O(h)$ — first-order method.

**Heun's method (Improved Euler):**
$$\tilde{y}_{n+1} = y_n + h\,f(x_n, y_n) \quad\text{(predictor)},$$
$$y_{n+1} = y_n + \frac{h}{2}\bigl[f(x_n,y_n) + f(x_{n+1},\tilde{y}_{n+1})\bigr] \quad\text{(corrector)}.$$
Global error: $O(h^2)$ — second-order method.

---

#### 11. Common Exam Errors — Part I and Part II

**Integration errors:**
- Forgetting the constant of integration (fatal in IVP problems).
- Sign errors when integrating $\int e^{-px}\,dx = -e^{-px}/p + C$ (missing the negative).
- Partial fraction coefficients computed incorrectly (use cover-up method for linear factors).

**ODE method errors:**
- Applying the linear IF method to a Bernoulli equation without the substitution (gives wrong answer).
- Not checking for singular solutions $h(y) = 0$ in separable equations.
- In exact equations: integrating $M$ with respect to $x$ but forgetting to include an arbitrary function $g(y)$ (not a constant) in $F$.
- In the IF method: computing $\int p\,dx$ as $p\,x$ even when $p = p(x)$ is variable.

**Phase line errors:**
- Confusing the sign convention: $f(y) > 0$ means $y$ **increases** (arrow up), not $f$ increases.
- Semi-stable equilibria misclassified as stable or unstable — always draw arrows on **both** sides.

---

#### 12. Summary — Review 1

| Topic | Core formula / test |
|-------|---------------------|
| Separable ODE | $\int dy/h(y) = \int g(x)\,dx$ |
| Exact ODE | $M_y = N_x \Rightarrow F(x,y) = C$ |
| IF for non-exact | $(M_y-N_x)/N = P(x) \Rightarrow \mu = e^{\int P\,dx}$ |
| Linear ODE | $\mu = e^{\int p\,dx}$; $y = (\int\mu r\,dx + C)/\mu$ |
| Bernoulli | $v = y^{1-n}$; reduces to linear |
| Logistic | $P = K/(1+Ae^{-rt})$; inflection at $K/2$ |
| Autonomous | Phase line; $f'(y^*)<0$ stable; $f'(y^*)>0$ unstable |
| RL circuit | $\tau = L/R$; $i_\infty = E_0/R$ |
| Falling body | $v_T = mg/b$ (linear); $v_T = \sqrt{mg/c}$ (quadratic) |

---

## Pre-Exam Review 2 — Part III: Second-Order and Higher-Order ODEs (Weeks 6–7)

### Introduction

This lecture reviews the Week 6 and Week 7 content (second-order and higher-order ODEs) and then turns to exam strategy. The Midterm covers the **full** Part III content from Weeks 6–7 — including homogeneous equations (characteristic equation, Euler–Cauchy, Abel's theorem) and non-homogeneous methods (UC and VoP), plus higher-order ODEs.

**Key question for each ODE:** What is the equation type, and which method applies? For the Midterm, this is the critical first step.

---

### Knowledge Points

---

#### 1. Part III Review — Structure of Second-Order Homogeneous ODEs (Week 6)

**Standard form:**
$$y'' + p(x)y' + q(x)y = 0. \tag{H}$$

**General solution:** $y = c_1 y_1 + c_2 y_2$ where $\{y_1, y_2\}$ is any **fundamental set** ($W[y_1,y_2] \neq 0$).

**Superposition:** Any linear combination of solutions is a solution (homogeneous case only).

**IVP:** Two initial conditions $y(x_0) = k_0$, $y'(x_0) = k_1$ uniquely determine $c_1, c_2$.

**Key difference from first-order:** Two constants, two conditions, two linearly independent solutions. The solution space is 2-dimensional.

---

#### 2. Part III Review — Constant-Coefficient Equations and the Characteristic Equation (Week 6)

**Equation:** $ay'' + by' + cy = 0$.

**Trial:** $y = e^{\lambda x}$ → **characteristic equation:** $a\lambda^2 + b\lambda + c = 0$.

**Three cases:**

| Case | Discriminant $\Delta = b^2-4ac$ | Roots | General solution |
|------|-------------------------------|-------|-----------------|
| 1 | $\Delta > 0$ | $\lambda_1 \neq \lambda_2$ (real) | $c_1e^{\lambda_1 x} + c_2e^{\lambda_2 x}$ |
| 2 | $\Delta < 0$ | $\lambda = \alpha \pm i\beta$ | $e^{\alpha x}(c_1\cos\beta x + c_2\sin\beta x)$ |
| 3 | $\Delta = 0$ | $\lambda = -b/(2a)$ (double) | $(c_1 + c_2 x)e^{\lambda x}$ |

**Where:** $\alpha = -b/(2a)$, $\beta = \sqrt{|\Delta|}/(2a)$.

**Physical meaning for $my'' + cy' + ky = 0$:**
- $\Delta > 0$ (overdamped): exponential decay, no oscillation.
- $\Delta < 0$ (underdamped): decaying oscillation (if $\alpha < 0$); growing (if $\alpha > 0$).
- $\Delta = 0$ (critically damped): fastest decay without oscillation.

---

#### 3. Part III Review — Complex Numbers and Euler's Formula (Week 6)

**Complex arithmetic essentials:**
- $z = a + bi$, $|z| = \sqrt{a^2+b^2}$, $\bar{z} = a-bi$, $z\bar{z} = |z|^2$.
- $(a+bi)(c+di) = (ac-bd) + (ad+bc)i$ (remember: $i^2 = -1$).
- $\dfrac{a+bi}{c+di} = \dfrac{(a+bi)(c-di)}{c^2+d^2}$ (conjugate trick).

**Euler's Formula:**
$$e^{i\theta} = \cos\theta + i\sin\theta.$$

**Polar form:** $z = re^{i\theta}$, $r = |z|$, $\theta = \arg z$.

**For ODEs:** Complex roots $\lambda = \alpha \pm i\beta$ give real solutions $e^{\alpha x}\cos\beta x$ and $e^{\alpha x}\sin\beta x$ via:
$$e^{(\alpha\pm i\beta)x} = e^{\alpha x}(\cos\beta x \pm i\sin\beta x).$$

---

#### 4. Part III Review — Euler–Cauchy Equation (Week 6)

**Equation:** $x^2 y'' + axy' + by = 0$ ($x > 0$).

**Trial:** $y = x^m$ → **auxiliary equation:** $m^2 + (a-1)m + b = 0$.

**Three cases** (same structure as constant-coefficient):

| Case | Roots | General solution |
|------|-------|----|
| Real distinct $m_1 \neq m_2$ | — | $c_1 x^{m_1} + c_2 x^{m_2}$ |
| Complex $m = \mu \pm i\nu$ | — | $x^\mu\bigl(c_1\cos(\nu\ln x) + c_2\sin(\nu\ln x)\bigr)$ |
| Repeated $m$ | — | $x^m(c_1 + c_2\ln x)$ |

**Quick identification:** Euler–Cauchy has the pattern $x^2 y''$, $xy'$, $y$ — powers of $x$ match derivative orders. **Auxiliary equation:** $m^2+(a-1)m+b=0$ (not $m^2+am+b=0$!).

---

#### 5. Part III Review — Wronskian and Abel's Theorem (Week 6)

**Wronskian:**
$$W[y_1, y_2](x) = y_1 y_2' - y_1' y_2 = \begin{vmatrix}y_1 & y_2 \\ y_1' & y_2'\end{vmatrix}.$$

**For ODE solutions:** $W \neq 0$ on $I$ iff $\{y_1, y_2\}$ is a fundamental set (all-or-nothing theorem). This holds **only for ODE solutions** — arbitrary functions with $W = 0$ everywhere are not necessarily linearly dependent.

**Abel's Theorem:** For $y'' + p(x)y' + q(x)y = 0$:
$$W(x) = W(x_0)\,e^{-\int_{x_0}^x p(t)\,dt}.$$

**Practical use:** Compute $W$ once (e.g., at $x = 0$ or $x = 1$) and use Abel's formula to determine $W(x)$ everywhere; or verify a proposed fundamental set without integrating. Also used in VoP (Week 7) to compute $W$ without direct Wronskian evaluation.

**Applications:**
- $y'' + (\sin x)y' + xy = 0$, $W(\pi/2) = 1$: $W(x) = e^{\cos x}$.
- $y'' + (2/x)y' + y = 0$ ($x > 0$), $W(1) = 3$: $W(x) = 3/x^2$.

---

#### 6. Part III Review — Reduction of Order (Week 6)

**Given:** One solution $y_1$. **Ansatz:** $y_2 = v(x)y_1$.

**Outcome:** After substitution, the $v$-coefficient vanishes (because $y_1$ satisfies the ODE), leaving a first-order ODE for $w = v'$:
$$y_1 w' + (2y_1' + py_1)w = 0.$$

**Result:**
$$v'(x) = \frac{e^{-\int p\,dx}}{y_1^2(x)}, \qquad y_2 = y_1 \int \frac{e^{-\int p\,dx}}{y_1^2}\,dx.$$

**Key use case:** Derives $y_2 = xe^{\lambda x}$ for the double-root case ($y_1 = e^{\lambda x}$, $v' = 1$, $v = x$). Also derives $y_2 = x^m\ln x$ for Euler–Cauchy double root.

---

#### 7. Part III Review — General Solution Structure for Non-Homogeneous ODEs (Week 7)

**Theorem:** The general solution of $y'' + p(x)y' + q(x)y = r(x)$ is:
$$y = y_h + y_p = c_1 y_1 + c_2 y_2 + y_p,$$
where $\{y_1, y_2\}$ is a fundamental set for the homogeneous equation and $y_p$ is **any** particular solution.

**Physical decomposition:**
- $y_h = c_1 y_1 + c_2 y_2$: **transient response** — decays if $\mathrm{Re}(\lambda) < 0$.
- $y_p$: **forced/steady-state response** — driven by $r(x)$.

**Caution:** Apply ICs to the **full** solution $y = y_h + y_p$, not to $y_h$ alone.

---

#### 8. Part III Review — Undetermined Coefficients (Week 7)

**Scope:** Works when $r(x)$ belongs to the **UC family**: polynomials, exponentials, $\cos$/$\sin$, and their products/sums.

**Trial function table:**

| $r(x)$ | Trial $y_p$ |
|--------|------------|
| Constant $A$ | $K$ |
| $P_n(x)$ (degree $n$) | $K_n x^n + \cdots + K_0$ |
| $e^{\alpha x}$ | $Ke^{\alpha x}$ |
| $\cos\beta x$ or $\sin\beta x$ | $A\cos\beta x + B\sin\beta x$ |
| $e^{\alpha x}\cos\beta x$ or $e^{\alpha x}\sin\beta x$ | $e^{\alpha x}(A\cos\beta x + B\sin\beta x)$ |
| $P_n(x)e^{\alpha x}$ | $(K_nx^n+\cdots+K_0)e^{\alpha x}$ |

**Modification rule:** If the trial overlaps with $y_h$ (the corresponding characteristic root has multiplicity $s$), multiply the trial by $x^s$.

**Resonance formula** (undamped, $r = F_0\cos\omega_0 x$, roots $\pm i\omega_0$):
$$y_p = \frac{F_0}{2\omega_0}\,x\sin\omega_0 x.$$
The factor $x$ causes amplitude to grow **linearly without bound**.

**Superposition:** If $r = r_1 + r_2$, find $y_{p1}$, $y_{p2}$ separately; $y_p = y_{p1} + y_{p2}$.

---

#### 9. Part III Review — Variation of Parameters (Week 7)

**When UC fails:** $r(x)$ outside the UC family ($\sec x$, $\ln x$, $e^x/x^2$, variable-coefficient ODE).

**Ansatz:** $y_p = u_1(x)y_1 + u_2(x)y_2$.

**Lagrange's condition:** $u_1'y_1 + u_2'y_2 = 0$. Combined with the ODE condition $u_1'y_1' + u_2'y_2' = r$, solved by Cramer's rule:
$$u_1' = \frac{-y_2 r}{W}, \qquad u_2' = \frac{y_1 r}{W}.$$

**VoP particular solution:**
$$\boxed{y_p = -y_1\int\frac{y_2 r}{W}\,dx + y_2\int\frac{y_1 r}{W}\,dx.}$$

**Abel's shortcut:** Use $W(x) = W(x_0)e^{-\int_{x_0}^x p\,dt}$ to compute $W$ without direct evaluation.

**Green's function interpretation:**
$$y_p(x) = \int_{x_0}^x G(x,t)\,r(t)\,dt, \qquad G(x,t) = \frac{y_1(t)y_2(x) - y_1(x)y_2(t)}{W(t)}.$$

**UC vs. VoP:**

| Feature | UC | VoP |
|---------|-----|-----|
| Scope | UC family only | Any continuous $r(x)$ |
| Computation | Algebraic | Integration |
| Variable coefficients? | No | Yes |
| Modification rule? | Sometimes | Never |

**Practical rule:** Use UC when applicable (faster). Use VoP for forcing outside the UC family or variable-coefficient ODEs.

---

#### 10. Part III Review — Higher-Order Linear ODEs (Week 7)

**Structure:** $n$-th order has $n$-dimensional solution space. IVP requires $n$ conditions.

**Root contributions (constant-coefficient):**

| Root type | Multiplicity $k$ | Contribution to $y_h$ |
|----------|-----------------|----------------------|
| Real $\lambda = a$ | $k$ | $e^{ax},\,xe^{ax},\,\ldots,\,x^{k-1}e^{ax}$ |
| Complex $\alpha\pm i\beta$ | $k$ | $x^j e^{\alpha x}\cos\beta x$ and $x^j e^{\alpha x}\sin\beta x$, $j=0,\ldots,k-1$ |

**Examples:**
- $y^{(4)} - y = 0$: roots $1, -1, \pm i$ → $y = c_1e^x + c_2e^{-x} + c_3\cos x + c_4\sin x$.
- $(\lambda-1)^3 = 0$: triple root → $y = (c_1+c_2x+c_3x^2)e^x$.
- $(\lambda^2+4)^2 = 0$: repeated complex $\pm 2i$ (mult. 2) → $y = (c_1+c_3x)\cos2x + (c_2+c_4x)\sin2x$.

**Euler–Bernoulli beam equation** ($y^{(4)} = q/EI$): quadruple root $\lambda=0$ gives $y_h = c_1+c_2x+c_3x^2+c_4x^3$. Four boundary conditions at two endpoints.

---

#### 11. Cross-Week Connections — Tools from Part I in Parts II and III

**Why Part I matters for the Midterm:**

| Part I tool (Week) | Where it appears in Parts II–III |
|--------------------|----------------------------------|
| $\int e^{ax}dx = e^{ax}/a$ (Wk 2) | IF method, characteristic equation solutions |
| Integration by parts (Wk 2) | $\int e^{ax}\cos bx\,dx$, $\int xe^{ax}\,dx$ in IF method and VoP |
| Partial fractions (Wk 2) | Separating $1/(P(K-P))$ for logistic equation; VoP integrals |
| $\int dx/(x^2+a^2) = \arctan(x/a)/a$ (Wk 2) | Inverse trig in separable ODEs; char. eq. with complex roots |
| $\tanh$ derivative (Wk 1) | Quadratic-drag falling body solution (Week 5) |
| Taylor series / $e^{i\theta}$ (Wk 2, 3) | Euler's Formula derivation; complex roots (Week 6) |
| Polar coordinates $re^{i\theta}$ (Wk 3) | Formalized as $z = re^{i\theta}$ in Week 6 |

---

#### 12. Exam Strategy — Method Identification

**On the exam, for every ODE problem:**

**Step 1 — Read the equation carefully.** Write it in the form $y' = f(x,y)$ or $M\,dx + N\,dy = 0$.

**Step 2 — Determine the order.** First-order: Part II methods. Second-order or higher: Part III methods.

**Step 3 — For first-order, run the decision tree:**
1. Does $f(x,y)$ factor as $g(x) \cdot h(y)$? → Separable.
2. No explicit $x$? → Autonomous (phase line).
3. Linear ($y, y'$ only to first power)? → IF method.
4. Looks almost linear but has $y^n$? → Bernoulli.
5. In $M\,dx + N\,dy$ form, $M_y = N_x$? → Exact.
6. Exactness defect $(M_y - N_x)/N$ is a function of $x$ only? → $\mu(x)$.

**Step 4 — For second-order constant-coefficient:**
1. Homogeneous? Compute characteristic equation; identify $\Delta$; apply Case 1, 2, or 3.
2. Non-homogeneous? Is $r(x)$ in the UC family? → UC. Otherwise → VoP.
3. Apply ICs to the **full** solution $y_h + y_p$.

**Step 5 — For Euler–Cauchy:**
1. Recognise pattern $x^2 y''$, $xy'$, $y$.
2. Compute auxiliary equation $m^2 + (a-1)m + b = 0$.
3. Apply same three cases as constant-coefficient; $e^{\lambda x} \to x^m$, $xe^{\lambda x} \to x^m\ln x$.

---

#### 13. Exam Strategy — Checking Your Work

**For IVP problems:** After finding $y(x)$, substitute back into the ODE and check both initial conditions. This takes 30–60 seconds and catches most errors.

**For complex-root problems:** Always verify: $\alpha = -b/(2a)$, $\beta = \sqrt{4ac-b^2}/(2a)$. Compute $\beta$ explicitly — errors here cascade through the entire solution.

**For Euler–Cauchy:** Always write $x^2y'' + axy' + by = 0$ in standard (EC) form first, then write down $m^2 + (a-1)m + b = 0$. Don't mix up with the characteristic equation $\lambda^2 + a\lambda + b = 0$.

**For UC:** Before writing the trial, check whether the trial overlaps with $y_h$. If it does, multiply by $x$ (or $x^2$ for double root) — missing this gives a system with no solution.

**For VoP:** Always put the ODE in **standard form** (coefficient of $y''$ = 1) before identifying $r(x)$.

---

#### 14. Common Exam Errors — Part III

**Characteristic equation errors:**
- Computing $\Delta = b^2 - 4ac$ incorrectly (sign errors when $b$ or $c$ is negative).
- For Case 2, computing $\beta$ as $\sqrt{b^2-4ac}$ instead of $\sqrt{4ac-b^2}$ (forgetting $\Delta < 0$).
- For Case 3, writing $(c_1 + c_2 x)e^{\lambda x}$ — correct — but then computing $y'$ incorrectly (product rule applied to $c_1 + c_2 x$ and $e^{\lambda x}$).

**Euler–Cauchy errors:**
- Writing the auxiliary equation as $m^2 + am + b = 0$ instead of $m^2 + (a-1)m + b = 0$.
- Forgetting $\ln x$ in the repeated-root solution: writing $x^m + cx^m$ instead of $x^m(c_1 + c_2\ln x)$.
- For complex roots: writing $\cos(\nu x)$ instead of $\cos(\nu \ln x)$.

**Wronskian errors:**
- Computing $W = y_1 y_2 - y_1' y_2'$ (product, not cross-derivative).

**Non-homogeneous errors:**
- Applying ICs to $y_h$ alone, then adding $y_p$ — ICs must be applied to the full solution $y_h + y_p$.
- Forgetting the modification rule in UC.
- In VoP: using the original (non-standard) form of the ODE instead of dividing by the coefficient of $y''$.

---

#### 15. Summary — Review 2

| Topic | Key exam checkpoints |
|-------|---------------------|
| 2nd-order structure | 2 constants, IVP needs $y(x_0)$ and $y'(x_0)$ |
| Characteristic equation | $a\lambda^2+b\lambda+c=0$; 3 cases by sign of $\Delta$ |
| Complex roots | $\alpha = -b/(2a)$, $\beta = \sqrt{4ac-b^2}/(2a)$; use Euler's formula |
| Case 3 (double root) | $y = (c_1+c_2x)e^{\lambda x}$; derived via Reduction of Order |
| Euler–Cauchy | Auxiliary eq. $m^2+(a-1)m+b=0$; $e^{\lambda x} \to x^m$; $xe^{\lambda x} \to x^m\ln x$ |
| Wronskian | $W = y_1y_2'-y_1'y_2$; Abel's Theorem: $W(x) = W(x_0)e^{-\int p\,dt}$ |
| Reduction of Order | $y_2 = vy_1$; $v' = e^{-\int p\,dx}/y_1^2$ |
| Non-homogeneous | $y = y_h + y_p$; ICs applied to full solution |
| UC method | UC family; modification rule; resonance: $y_p = (F_0/2\omega_0)x\sin\omega_0 x$ |
| VoP | $u_1' = -y_2r/W$; $u_2' = y_1r/W$; any continuous $r(x)$ |
| Higher-order | Real root mult $k$: $x^j e^{ax}$; complex pair mult $k$: $x^j e^{\alpha x}\cos\beta x$, $x^j e^{\alpha x}\sin\beta x$ |

---

## Midterm Examination

### Format and Coverage

**Coverage:** Weeks 1–7 (Parts I, II, and Part III §2.1, §2.2, §2.5, §2.6, §2.7, §2.10; §3.1–3.3).

> **Not included in Midterm:** §2.4 (Free Oscillations modelling) is covered in Week 10 and is explicitly excluded.

**Duration:** 120 minutes.

**Format:** Closed-book. A **formula sheet** is provided by the instructor, containing:
- Standard derivative table (power, exp/log, trig, hyperbolic, inverse trig).
- Standard integral table (basic antiderivatives and standard forms).
- No ODE solution formulas — those are derived from the methods.

**Calculators:** Not permitted.

---

### Problem Distribution (Typical)

| Area | Expected problems |
|------|------------------|
| Part I — Integration technique | 1–2 (IBP, partial fractions, trig substitution, or completing the square) |
| Part II — Separable or exact ODE | 1–2 |
| Part II — Linear first-order ODE | 1 |
| Part II — Bernoulli equation | 0–1 |
| Part II — Autonomous ODE and phase line | 1 |
| Part II — Application problem | 1 (mixing tank, Newton's cooling, RL circuit, or population dynamics) |
| Part III — 2nd-order homogeneous ODE (all root cases) | 2–3 |
| Part III — Euler–Cauchy equation | 1 |
| Part III — Wronskian / Reduction of Order | 0–1 |
| Part III — Non-homogeneous ODE (UC or VoP) | 1–2 |

---

### Sample Midterm Problems

The following problems illustrate the level and style expected. They are not the actual exam.

**Problem 1 (Integration — Partial Fractions):** Evaluate $\displaystyle\int \frac{3x+5}{(x-1)(x^2+4)}\,dx$.

**Problem 2 (Integration — Integration by Parts):** Evaluate $\displaystyle\int x^2 e^{-x}\,dx$.

**Problem 3 (Separable ODE):** Solve the IVP $y' = \dfrac{x^2}{1-y^2}$, $y(0) = 0$.

**Problem 4 (Exact ODE):** Solve $(3x^2y + 2xy^2)\,dx + (x^3 + 2x^2y)\,dy = 0$.

**Problem 5 (Linear First-Order ODE):** Solve $y' + \dfrac{2}{x}y = \cos x$, $y(\pi) = 0$ ($x > 0$).

**Problem 6 (Bernoulli Equation):** Solve $y' - y = xy^3$.

**Problem 7 (Phase Line):** For $y' = y^3 - 4y$: find all equilibria, construct the phase line, classify stability of each equilibrium, and describe the long-term behaviour for $y(0) = 1.5$.

**Problem 8 (Application — Mixing Tank):** A 100-L tank initially contains 20 kg of salt dissolved in water. Brine of concentration 0.3 kg/L enters at 4 L/min; the well-mixed solution drains at 4 L/min. Find $Q(t)$ and determine how long until the salt content reaches 25 kg.

**Problem 9 (Application — Logistic Growth):** Solve $P' = 0.3P(1-P/800)$, $P(0) = 100$. Find the time when $P = 400$.

**Problem 10 (Second-Order ODE — Complex Roots):** Solve the IVP $y'' - 4y' + 13y = 0$, $y(0) = 1$, $y'(0) = 2$.

**Problem 11 (Second-Order ODE — Repeated Root):** Solve the IVP $y'' - 6y' + 9y = 0$, $y(0) = 2$, $y'(0) = 1$.

**Problem 12 (Second-Order ODE — Real Distinct Roots):** Solve $y'' - y = 0$, $y(0) = 3$, $y'(0) = 1$. Express the answer in terms of $\cosh x$ and $\sinh x$.

**Problem 13 (Euler–Cauchy):** Solve $x^2y'' + 2xy' - 6y = 0$ ($x > 0$) with $y(1) = 0$, $y'(1) = 1$.

**Problem 14 (Wronskian):** Given that $y_1 = e^{2x}$ is a solution of $y'' - 5y' + 6y = 0$, use Reduction of Order to find a second independent solution $y_2$ and verify $W[y_1, y_2] \neq 0$.

**Problem 15 (Non-Homogeneous — UC):** Solve $y'' + 2y' + y = e^{-x}$. (Check the modification rule.)

**Problem 16 (Non-Homogeneous — VoP):** Solve $y'' + y = \sec x$ ($-\pi/2 < x < \pi/2$).

**Problem 17 (Higher-Order):** Solve $y^{(4)} - 16y = 0$.

---

## No Practice Session: Grade Return and Preview

### Purpose

The grade return and grade appeal session:
1. **Grade return and review:** Examine returned scripts. Understand where points were lost and why.
2. **Grade appeal:** Minor grading issues are addressed immediately according to the appeal procedure below.

---

### Grade Appeal Procedure

**Scope:** Appeals are limited to **arithmetic and transcription errors** — cases where the grader marked an answer wrong that is in fact correct, or added marks incorrectly.

**Process:**
1. Visit the instructor's office hours.
2. Review your answers carefully with the instructor.
3. If an error is found, it will be corrected immediately.

**Not in scope for appeal:** Partial credit allocation, interpretation of the problem, or method choice — these are at the instructor's discretion.

---

### Quick Reference — All Five First-Order ODE Methods

| Method | Form | Algorithm | Key formula |
|--------|------|-----------|-------------|
| Separable | $y' = g(x)h(y)$ | Separate; integrate | $\int dy/h(y) = \int g\,dx$ |
| Autonomous | $y' = f(y)$ | Phase line | $f'(y^*)<0$ → stable |
| Linear IF | $y'+py=r$ | Multiply by $\mu$ | $\mu = e^{\int p\,dx}$ |
| Bernoulli | $y'+py=ry^n$ | $v=y^{1-n}$ | Linear in $v$ |
| Exact | $M_y=N_x$ | Find potential $F$ | $F(x,y)=C$ |

### Quick Reference — Second-Order Homogeneous Methods (Week 6)

| Method | Equation | Algorithm | Key formula |
|--------|---------|-----------|-------------|
| Char. eq. (Case 1) | $ay''+by'+cy=0$, $\Delta>0$ | Roots $\lambda_1\neq\lambda_2$ | $c_1e^{\lambda_1 x}+c_2e^{\lambda_2 x}$ |
| Char. eq. (Case 2) | $\Delta<0$ | Roots $\alpha\pm i\beta$ | $e^{\alpha x}(c_1\cos\beta x+c_2\sin\beta x)$ |
| Char. eq. (Case 3) | $\Delta=0$ | Double root $\lambda$ | $(c_1+c_2x)e^{\lambda x}$ |
| Euler–Cauchy | $x^2y''+axy'+by=0$ | Auxiliary $m^2+(a-1)m+b=0$ | Same 3 cases; $e^{\lambda x}\to x^m$ |
| Reduction of Order | Any (H) with $y_1$ known | $y_2=vy_1$; $v'=e^{-\int p}/y_1^2$ | $y_2=y_1\int v'\,dx$ |
| Wronskian | Fundamental set test | $W=y_1y_2'-y_1'y_2$ | Abel: $W(x)=W(x_0)e^{-\int p\,dt}$ |

### Quick Reference — Non-Homogeneous and Higher-Order Methods (Week 7)

| Method | Scope | Key formula |
|--------|-------|-------------|
| General solution | Any | $y = y_h + y_p$; ICs on full solution |
| UC — standard trial | $r\in$ UC family | Match coefficients |
| UC — modification rule | Trial overlaps $y_h$ (mult. $s$) | Multiply trial by $x^s$ |
| UC — resonance | $r=F_0\cos\omega_0 x$, roots $\pm i\omega_0$ | $y_p = (F_0/2\omega_0)x\sin\omega_0 x$ |
| VoP | Any continuous $r(x)$ | $u_1'=-y_2r/W$; $u_2'=y_1r/W$ |
| Higher-order | Order $n$ | Real root mult $k$: $x^j e^{ax}$; complex pair mult $k$: $x^j e^{\alpha x}\{\cos,\sin\}\beta x$ |
| Beam equation | $EI\,y^{(4)}=q(x)$ | 4th-order; BCs at two endpoints |
