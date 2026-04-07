# Week 6 — Second-Order Linear ODEs: Structure, Complex Roots, and Euler–Cauchy

**Course:** Engineering Mathematics 1
**Part:** III — Second-Order Ordinary Differential Equations
**Kreyszig Sections:** §2.1, §2.2, §2.5, §2.6

---

## Lecture 1: Structure of Second-Order ODEs and Reduction of Order

### Introduction

Second-order linear ODEs are the central objects of engineering mathematics. They govern mechanical oscillators, RLC circuits, beam deflection, heat conduction, and quantum mechanics. Understanding their **structure** — before attempting any solution method — is the key to working confidently with this entire class of equations.

This lecture establishes the theoretical framework: existence/uniqueness of solutions, the superposition principle, the Wronskian as a tool for detecting linear independence, and the **reduction of order** method that extracts a second solution from a known first one.

**Why it matters:**
- Every physical second-order system (spring-mass, RLC, beam) has two free constants (energy stored in two "state variables"). The theory tells us there are exactly two linearly independent solutions.
- Reduction of order is both a practical tool and the conceptual foundation for Variation of Parameters (Week 7).

---

### Knowledge Points

---

#### 1. Standard Form and Existence/Uniqueness

**Standard form** of the second-order linear ODE:
$$y'' + p(x)\,y' + q(x)\,y = r(x).$$

- $p(x)$, $q(x)$: coefficient functions (may be variable)
- $r(x)$: forcing function (right-hand side)
- **Homogeneous** if $r(x) = 0$; **non-homogeneous** if $r(x) \neq 0$

**Existence and Uniqueness Theorem (2nd order):** If $p$, $q$, and $r$ are continuous on an open interval $I$ containing $x_0$, then the IVP
$$y'' + py' + qy = r, \quad y(x_0) = k_0,\; y'(x_0) = k_1$$
has a **unique solution** on all of $I$.

**Implications:**
- Two initial conditions are needed (position and velocity in mechanics).
- Solutions cannot cross — uniqueness eliminates ambiguity.
- The solution exists on the full continuity interval (no finite-time blowup for linear equations).

---

#### 2. Superposition Principle

**Theorem (Superposition for Homogeneous):** If $y_1$ and $y_2$ are solutions of the homogeneous equation $y'' + py' + qy = 0$, then so is any linear combination $c_1 y_1 + c_2 y_2$ for constants $c_1, c_2 \in \mathbb{R}$.

**Proof sketch:** Linearity of differentiation. $L[c_1 y_1 + c_2 y_2] = c_1 L[y_1] + c_2 L[y_2] = 0 + 0 = 0$.

**General solution:** $y_h = c_1 y_1 + c_2 y_2$, where $\{y_1, y_2\}$ is a **fundamental set** — two linearly independent solutions. The two constants $c_1, c_2$ are determined by two ICs.

**Key fact:** The homogeneous equation has a **2-dimensional** solution space. Any two linearly independent solutions span it completely.

---

#### 3. Linear Independence and the Wronskian

**Definition:** Two functions $y_1$, $y_2$ are **linearly dependent** on $I$ if one is a constant multiple of the other: $y_1 = cy_2$ for all $x \in I$. Otherwise they are **linearly independent**.

**Wronskian:** The Wronskian of $y_1$, $y_2$ is the $2\times 2$ determinant
$$W[y_1, y_2](x) = \begin{vmatrix} y_1 & y_2 \\ y_1' & y_2' \end{vmatrix} = y_1 y_2' - y_1' y_2.$$

**Theorem:** If $y_1$, $y_2$ are solutions of $y'' + py' + qy = 0$ on $I$, then either:
- $W(x) = 0$ for **all** $x \in I$ (dependent), or
- $W(x) \neq 0$ for **all** $x \in I$ (independent, i.e., a fundamental set).

**Diagnostic rule for solutions:** $\{y_1, y_2\}$ is a fundamental set $\iff$ $W \neq 0$ at any one point $x_0 \in I$.

**Example:** $y_1 = e^x$, $y_2 = e^{2x}$, equation $y'' - 3y' + 2y = 0$.
$$W = e^x \cdot 2e^{2x} - e^x \cdot e^{2x} = 2e^{3x} - e^{3x} = e^{3x} \neq 0.$$
Confirmed fundamental set.

**Non-example:** $y_1 = x^2$, $y_2 = 3x^2$. $W = x^2(6x) - 2x(3x^2) = 6x^3 - 6x^3 = 0$. Linearly dependent.

---

#### 4. IVP Solution Procedure

For $y'' + py' + qy = 0$ with ICs $y(x_0) = k_0$, $y'(x_0) = k_1$:

1. Find fundamental set $\{y_1, y_2\}$.
2. Write $y = c_1 y_1 + c_2 y_2$.
3. Apply ICs: solve the $2 \times 2$ linear system for $c_1$, $c_2$.

**Example:** Solve $y'' - 3y' + 2y = 0$, $y(0) = 1$, $y'(0) = 0$.
- Characteristic roots (Lecture 2): $\lambda = 1, 2$. General solution: $y = c_1 e^x + c_2 e^{2x}$.
- $y(0) = c_1 + c_2 = 1$; $y'(0) = c_1 + 2c_2 = 0$.
- Solving: $c_2 = -1$, $c_1 = 2$.
- **Solution:** $y = 2e^x - e^{2x}$.

---

#### 5. Reduction of Order

**Setup:** Given one known solution $y_1 \neq 0$ of $y'' + py' + qy = 0$, find a second linearly independent solution $y_2$.

**Ansatz:** $y_2 = v(x)\,y_1(x)$, where $v(x)$ is unknown.

**Derivation:** Compute $y_2'$, $y_2''$ and substitute into the ODE. The $v$-term vanishes (since $y_1$ solves the ODE), leaving a first-order ODE in $v'$. Setting $w = v'$:
$$y_1 w' + (2y_1' + py_1)w = 0 \quad \Longrightarrow \quad \frac{w'}{w} = -\frac{2y_1'}{y_1} - p.$$

**Integration formula:**
$$v'(x) = \frac{e^{-\int p\,dx}}{y_1^2(x)}, \qquad y_2 = y_1 \int \frac{e^{-\int p\,dx}}{y_1^2}\,dx.$$

**Why $W \neq 0$:** $W[y_1, y_2] = y_1^2 v' = e^{-\int p\,dx} \neq 0$, confirming $y_2$ is indeed independent of $y_1$.

---

#### 6. Worked Examples for Reduction of Order

**Example 1 — Repeated root (const.-coeff.):** $y'' - 2y' + y = 0$, $y_1 = e^x$.
- Standard form: $p = -2$, $q = 1$.
- $v'(x) = \frac{e^{-\int(-2)\,dx}}{(e^x)^2} = \frac{e^{2x}}{e^{2x}} = 1$.
- $v = x$; $y_2 = x e^x$.
- Verify: $y_2'' - 2y_2' + y_2 = (2e^x+xe^x) - 2(e^x+xe^x) + xe^x = 0$. ✓
- **General solution:** $y = (c_1 + c_2 x)e^x$. *(The repeated-root formula $xe^{\lambda x}$ re-derived in Lec 3.)*

**Example 2 — Euler–Cauchy double root:** $x^2 y'' - 3xy' + 4y = 0$, $y_1 = x^2$.
- Standard form: $p(x) = -3/x$.
- $v' = \frac{e^{-\int(-3/x)\,dx}}{(x^2)^2} = \frac{e^{3\ln x}}{x^4} = \frac{x^3}{x^4} = \frac{1}{x}$.
- $v = \ln x$; $y_2 = x^2 \ln x$.
- Verify: $y_2' = x(2\ln x+1)$, $y_2'' = 2\ln x + 3$; substituting gives $0$. ✓
- **General solution:** $y = x^2(c_1 + c_2\ln x)$.

**Example 3 — Variable-coefficient equation:** $x^2 y'' - x(x+2)y' + (x+2)y = 0$, $y_1 = x$.
- Verify $y_1$: $0 - x(x+2) + (x+2)x = 0$. ✓
- Standard form: $p(x) = -(x+2)/x = -1 - 2/x$.
- $\int p\,dx = -x - 2\ln x$, so $e^{-\int p\,dx} = e^{x+2\ln x} = x^2 e^x$.
- $v' = x^2 e^x/x^2 = e^x$; $v = e^x$; $y_2 = xe^x$.
- **General solution:** $y = x(c_1 + c_2\,e^x)$. *(Requires the full method; $y_2 = xe^x$ cannot be guessed.)*

---

#### 7. Summary Table — Reduction of Order

| Step | Action |
|------|--------|
| Start | Know $y_1 \neq 0$ solves homogeneous ODE |
| Ansatz | $y_2 = v(x)\,y_1(x)$ |
| Reduce | Substitute → first-order ODE in $w = v'$ |
| Solve | $v' = e^{-\int p\,dx}/y_1^2$ |
| Final | $y_2 = y_1 \int v'\,dx$; check $W \neq 0$ |

---

## Lecture 2: Complex Numbers and the Characteristic Equation

### Introduction

The characteristic equation of a constant-coefficient second-order ODE is quadratic, and its roots may be complex. This lecture develops the complex number toolkit — Euler's formula, polar form, complex exponentials — and applies it to solve the ODE for all three root types (real distinct, complex, repeated). The physics of overdamped vs. underdamped systems emerges naturally from the algebra.

**Why complex numbers matter:**
- Oscillatory behavior (springs, circuits, waves) corresponds to complex characteristic roots.
- Euler's formula $e^{i\theta} = \cos\theta + i\sin\theta$ is the bridge from complex exponentials to real sinusoids.
- All signal processing (Fourier, Laplace) rests on this algebraic foundation.

---

### Knowledge Points

---

#### 1. Complex Number Arithmetic

A **complex number** has the form $z = a + bi$ where $a = \mathrm{Re}(z)$, $b = \mathrm{Im}(z)$, $i = \sqrt{-1}$.

**Operations:**
- **Addition:** $(a+bi) + (c+di) = (a+c) + (b+d)i$
- **Multiplication:** $(a+bi)(c+di) = (ac-bd) + (ad+bc)i$
- **Conjugate:** $\bar{z} = a - bi$; $|z|^2 = z\bar{z} = a^2 + b^2$
- **Division:** $\frac{z}{w} = \frac{z\bar{w}}{|w|^2}$
- **Modulus:** $|z| = \sqrt{a^2 + b^2}$ (distance from origin)

**Polar form:** $z = r e^{i\theta}$ where $r = |z|$, $\theta = \arg(z) = \arctan(b/a)$.

Multiplication in polar form: $|z_1||z_2|e^{i(\theta_1+\theta_2)}$ — multiply magnitudes, add angles.

---

#### 2. Euler's Formula

**Euler's formula:**
$$e^{i\theta} = \cos\theta + i\sin\theta.$$

**Derivation via Taylor series:**
$$e^{i\theta} = \sum_{n=0}^\infty \frac{(i\theta)^n}{n!} = \underbrace{1 - \frac{\theta^2}{2!} + \frac{\theta^4}{4!} - \cdots}_{\cos\theta} + i\underbrace{\left(\theta - \frac{\theta^3}{3!} + \frac{\theta^5}{5!} - \cdots\right)}_{\sin\theta}.$$

The Taylor series of $e^{i\theta}$ naturally splits into the real series for $\cos\theta$ and the imaginary series for $\sin\theta$.

**Special values:** $e^{i\pi} = -1$ (Euler's identity); $e^{i\pi/2} = i$; $e^{-i\theta} = \cos\theta - i\sin\theta$.

**Recovering real functions:**
$$\cos\theta = \frac{e^{i\theta} + e^{-i\theta}}{2}, \qquad \sin\theta = \frac{e^{i\theta} - e^{-i\theta}}{2i}.$$

---

#### 3. Complex Exponential for ODEs

For complex $\lambda = \alpha + i\beta$:
$$e^{\lambda x} = e^{(\alpha+i\beta)x} = e^{\alpha x}(\cos\beta x + i\sin\beta x).$$

**Linearity principle:** If the ODE $y'' + py' + qy = 0$ has real coefficients and $\tilde{y} = e^{(\alpha+i\beta)x}$ is a complex solution, then both its real and imaginary parts are real solutions:
$$y_1 = \mathrm{Re}(\tilde{y}) = e^{\alpha x}\cos\beta x, \qquad y_2 = \mathrm{Im}(\tilde{y}) = e^{\alpha x}\sin\beta x.$$

This is the fundamental reason why complex roots yield cosine/sine solutions.

---

#### 4. The Characteristic Equation

For the constant-coefficient homogeneous ODE
$$ay'' + by' + cy = 0,$$
substituting the trial $y = e^{\lambda x}$ gives $e^{\lambda x}(a\lambda^2 + b\lambda + c) = 0$, so:

$$\boxed{a\lambda^2 + b\lambda + c = 0}$$

This is the **characteristic equation** (also called auxiliary equation). Its two roots $\lambda_{1,2}$ determine the two independent solutions.

**Quadratic formula:** $\lambda = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$.

**Discriminant:** $\Delta = b^2 - 4ac$.

---

#### 5. Case 1 — Real Distinct Roots ($\Delta > 0$)

Roots $\lambda_1 \neq \lambda_2$, both real.

**General solution:**
$$y = c_1 e^{\lambda_1 x} + c_2 e^{\lambda_2 x}.$$

**Physical interpretation (spring-mass with damping $by' + cy = 0$):**
- Both roots negative ($\lambda_1 < \lambda_2 < 0$): **overdamped** — solution decays to zero without oscillation, two distinct exponential rates.
- One positive, one negative: unstable (energy source).
- Both positive: unstable growth.

**Example:** $y'' - 5y' + 6y = 0$.
$$\lambda^2 - 5\lambda + 6 = (\lambda-2)(\lambda-3) = 0 \;\Rightarrow\; \lambda_1 = 2,\; \lambda_2 = 3.$$
$$y = c_1 e^{2x} + c_2 e^{3x}.$$

**Example (overdamped spring-mass):** $m=1$, $c=5$, $k=4$ $\Rightarrow$ $y''+5y'+4y=0$. Discriminant $25-16=9>0$.
$$\lambda^2 + 5\lambda + 4 = (\lambda+1)(\lambda+4) = 0 \;\Rightarrow\; \lambda = -1, -4.$$
$$y = c_1 e^{-t} + c_2 e^{-4t} \to 0.$$
Fast mode $e^{-4t}$ gone in $\approx 0.25$ s; slow mode $e^{-t}$ in $\approx 1$ s. **No oscillation.**

---

#### 6. Case 2 — Complex Conjugate Roots ($\Delta < 0$)

Roots $\lambda = \alpha \pm i\beta$ where $\alpha = -b/(2a)$, $\beta = \sqrt{4ac-b^2}/(2a) > 0$.

**General solution (real form):**
$$\boxed{y = e^{\alpha x}(c_1\cos\beta x + c_2\sin\beta x).}$$

**Derivation:** Complex solutions $e^{(\alpha+i\beta)x}$ and $e^{(\alpha-i\beta)x}$; take real and imaginary parts; $y_1 = e^{\alpha x}\cos\beta x$, $y_2 = e^{\alpha x}\sin\beta x$.

**Physical interpretation:**
- $\alpha < 0$: **underdamped oscillation** — decaying sinusoid (transient response in RLC circuits, damped spring).
- $\alpha = 0$: **undamped oscillation** (pure sinusoid, $e^{0} = 1$).
- $\alpha > 0$: growing oscillation (unstable).

**$\alpha = 0$ case:** Roots $\pm i\beta$; solution $y = c_1\cos\beta x + c_2\sin\beta x$. Natural frequency $\omega_0 = \beta$.

**Amplitude-phase form:** $y = R\cos(\beta x - \varphi)$ where $R = \sqrt{c_1^2 + c_2^2}$, $\tan\varphi = c_2/c_1$.

---

#### 7. Worked Examples — Complex Roots

**Example 1 (complex roots, $\alpha > 0$):** $y'' - 2y' + 5y = 0$.
$$\lambda^2 - 2\lambda + 5 = 0 \;\Rightarrow\; \lambda = 1 \pm 2i \;\Rightarrow\; \alpha = 1,\; \beta = 2.$$
$$y = e^{x}(c_1\cos 2x + c_2\sin 2x).$$
Growing oscillations ($\alpha > 0$) — physically unstable system.

**Example 2 — IVP (underdamped, $\alpha < 0$):** $y'' + 2y' + 10y = 0$, $y(0) = 0$, $y'(0) = 3$.
$$\lambda = \frac{-2 \pm \sqrt{4-40}}{2} = -1 \pm 3i \;\Rightarrow\; \alpha = -1,\; \beta = 3.$$
$$y = e^{-x}(c_1\cos 3x + c_2\sin 3x).$$
$y(0) = c_1 = 0$; $y'(0) = -c_1 + 3c_2 = 3 \Rightarrow c_2 = 1$.
**Solution:** $y = e^{-x}\sin 3x$.

**Example 3 (underdamped RLC circuit):** $L=1$ H, $R=2\,\Omega$, $C=1/5$ F $\Rightarrow$ $q''+2q'+5q=0$.
Check: $R^2 = 4 < 4L/C = 20$ (underdamped).
Roots $\lambda = -1\pm 2i$ ($\alpha=-1$, $\beta=2$):
$$q(t) = e^{-t}(A\cos 2t + B\sin 2t).$$
Charge oscillates at 2 rad/s with exponentially decaying amplitude. Applications: camera flash discharge; radio tuner (LC resonance).

---

#### 8. Summary of Cases 1 and 2

| Discriminant | Roots | Solution Form | Physics |
|---|---|---|---|
| $\Delta > 0$ | $\lambda_1 \neq \lambda_2$ real | $c_1 e^{\lambda_1 x} + c_2 e^{\lambda_2 x}$ | Overdamped (if $\lambda < 0$) |
| $\Delta < 0$ | $\alpha \pm i\beta$ | $e^{\alpha x}(c_1\cos\beta x + c_2\sin\beta x)$ | Underdamped oscillation |

---

## Lecture 3: Repeated Roots, Euler–Cauchy, and the Wronskian

### Introduction

Two topics complete the second-order homogeneous theory: the **repeated root** case (critical damping in physics), and the **Euler–Cauchy equation** — the canonical variable-coefficient ODE that appears in cylindrical and spherical coordinate problems. Abel's theorem then provides an elegant shortcut for computing Wronskians.

---

### Knowledge Points

---

#### 1. Case 3 — Repeated Root ($\Delta = 0$)

When $\Delta = b^2 - 4ac = 0$, the characteristic equation has one double root:
$$\lambda = -\frac{b}{2a}.$$

The trial $y_1 = e^{\lambda x}$ gives one solution. We need a second. Reduction of order gives:
$$v' = \frac{e^{-\int p\,dx}}{y_1^2} = \frac{e^{-(-b/a)x}}{e^{2\lambda x}} = \frac{e^{(b/a)x}}{e^{2(-b/2a)x}} = 1.$$
So $v = x$ and:
$$y_2 = x e^{\lambda x}.$$

**General solution (repeated root):**
$$\boxed{y = (c_1 + c_2 x)\,e^{\lambda x}.}$$

**Physical meaning — critical damping:** For a spring-mass-damper $my'' + cy' + ky = 0$ with $c^2 = 4mk$ (balance between damping and restoring force):
- The system returns to equilibrium as fast as possible without oscillating.
- The response $(c_1 + c_2 t)e^{-t}$ decays faster than underdamped (no oscillation) and faster than overdamped (single exponential, but with polynomial factor).

**Example:** $y'' + 4y' + 4y = 0$.
$$\lambda^2 + 4\lambda + 4 = (\lambda+2)^2 = 0 \;\Rightarrow\; \lambda = -2.$$
$$y = (c_1 + c_2 x)e^{-2x}.$$

---

#### 2. Complete Three-Case Summary

| Case | Condition | Roots | General Solution |
|---|---|---|---|
| **1** | $\Delta = b^2-4ac > 0$ | $\lambda_1, \lambda_2$ real, distinct | $c_1 e^{\lambda_1 x} + c_2 e^{\lambda_2 x}$ |
| **2** | $\Delta < 0$ | $\alpha \pm i\beta$ complex | $e^{\alpha x}(c_1\cos\beta x + c_2\sin\beta x)$ |
| **3** | $\Delta = 0$ | $\lambda$ repeated | $(c_1 + c_2 x)e^{\lambda x}$ |

**Engineering analogy:**
- Case 1 (overdamped): heavy oil dashpot — slow return, no oscillation.
- Case 2 (underdamped): light spring — oscillates before settling.
- Case 3 (critically damped): optimal shock absorber — fastest non-oscillatory return.

---

#### 3. Euler–Cauchy Equation

**Standard form:**
$$x^2 y'' + axy' + by = 0, \qquad x > 0.$$

Named after Euler and Cauchy; also called the **equidimensional equation**.

**Scale invariance:** If $y(x)$ is a solution, so is $y(cx)$ for any constant $c > 0$. This means power functions $y = x^m$ are natural trial solutions.

**Characteristic equation:** Substitute $y = x^m$:
$$m(m-1) + am + b = 0 \qquad \Longrightarrow \qquad m^2 + (a-1)m + b = 0.$$

**Connection to polar coordinates:** The Laplace equation $\nabla^2 u = 0$ in polar form separates into an Euler–Cauchy equation in $r$, explaining why the equation appears in electrostatics, fluid flow, and heat transfer.

---

#### 4. Three Cases for Euler–Cauchy

Let $\Delta = (a-1)^2 - 4b$.

**Case 1 — Distinct real roots** $m_1 \neq m_2$:
$$y = c_1 x^{m_1} + c_2 x^{m_2}.$$

**Case 2 — Complex roots** $m = \mu \pm i\nu$:
Since $x^{m} = x^{\mu+i\nu} = x^\mu \cdot x^{i\nu} = x^\mu e^{i\nu\ln x}$, using Euler's formula:
$$y = x^\mu \bigl(c_1\cos(\nu\ln x) + c_2\sin(\nu\ln x)\bigr).$$

**Case 3 — Repeated root** $m_1 = m_2 = m$:
Reduction of order gives $y_2 = x^m \ln x$:
$$y = (c_1 + c_2\ln x)\,x^m.$$

---

#### 5. Euler–Cauchy Worked Examples

**Example 1 (distinct real roots):** $x^2 y'' - 2xy' - 4y = 0$.
$$m^2 + (-2-1)m + (-4) = m^2 - 3m - 4 = (m-4)(m+1) = 0 \;\Rightarrow\; m_1 = 4,\; m_2 = -1.$$
$$y = c_1 x^4 + c_2 x^{-1}.$$

**Example 2 (complex roots):** $x^2 y'' + xy' + y = 0$.
$$m(m-1) + m + 1 = m^2 + 1 = 0 \;\Rightarrow\; m = \pm i \;\Rightarrow\; \mu = 0,\; \nu = 1.$$
$$y = c_1\cos(\ln x) + c_2\sin(\ln x).$$

**Example 3 (IVP, repeated root):** $x^2 y'' - 3xy' + 4y = 0$, $y(1) = 2$, $y'(1) = 0$.
$$m^2 - 4m + 4 = (m-2)^2 = 0 \;\Rightarrow\; m = 2.$$
General: $y = x^2(c_1 + c_2\ln x)$; $y' = x(2c_1 + c_2(2\ln x+1))$.
Apply ICs: $y(1) = c_1 = 2$; $y'(1) = 2c_1 + c_2 = 0 \Rightarrow c_2 = -4$.
**Solution:** $y = x^2(2 - 4\ln x)$.

---

#### 6. Structural Analogy: Constant-Coefficient vs. Euler–Cauchy

| Feature | Const.-Coeff. $ay''+by'+cy=0$ | Euler–Cauchy $x^2y''+axy'+by=0$ |
|---|---|---|
| Trial function | $e^{\lambda x}$ | $x^m$ |
| Char. equation | $a\lambda^2+b\lambda+c=0$ | $m^2+(a-1)m+b=0$ |
| Distinct real | $c_1e^{\lambda_1 x}+c_2e^{\lambda_2 x}$ | $c_1x^{m_1}+c_2x^{m_2}$ |
| Complex $\alpha\pm i\beta$ / $\mu\pm i\nu$ | $e^{\alpha x}(c_1\cos\beta x + c_2\sin\beta x)$ | $x^\mu(c_1\cos(\nu\ln x)+c_2\sin(\nu\ln x))$ |
| Repeated root | $(c_1+c_2 x)e^{\lambda x}$ | $(c_1+c_2\ln x)x^m$ |
| Domain issue | $x \in \mathbb{R}$ | $x > 0$ (singularity at $x=0$) |

The substitution $x = e^t$ (so $t = \ln x$) transforms Euler–Cauchy into a constant-coefficient ODE.

---

#### 7. Wronskian — Definition and Properties

**Definition:** For solutions $y_1$, $y_2$ of $y'' + py' + qy = 0$:
$$W[y_1, y_2](x) = \begin{vmatrix} y_1 & y_2 \\ y_1' & y_2' \end{vmatrix} = y_1 y_2' - y_1' y_2.$$

**All-or-nothing property:** $W$ is either identically zero (linearly dependent) or never zero (linearly independent) on the interval. There is no "sometimes zero" case for ODE solutions.

**Proof:** $W' = y_1 y_2'' - y_1'' y_2 = -p(y_1 y_2' - y_1' y_2) = -pW$, so $W' + pW = 0$ — a first-order linear ODE for $W$.

**Warning:** The all-or-nothing property holds **only for ODE solutions**. For arbitrary functions, $W = 0$ everywhere does not imply linear dependence. Counterexample: $f(x) = x^2$, $g(x) = x|x|$ on $\mathbb{R}$ have $W = 0$ everywhere but are not proportional.

---

#### 8. Abel's Theorem

**Theorem (Abel, 1826):** The Wronskian of two solutions of $y'' + p(x)y' + q(x)y = 0$ satisfies:
$$W(x) = W(x_0)\,e^{-\int_{x_0}^x p(t)\,dt}.$$

**Consequences:**
- $W(x) \neq 0$ for all $x$ if $W(x_0) \neq 0$ at any one point $x_0$.
- $W(x) = 0$ everywhere if $W(x_0) = 0$ at any one point.
- **Shortcut:** Compute $W$ at one convenient point $x_0$ to classify independence.
- For constant coefficients ($p = $ const.): $W(x) = W(0)e^{-px}$.

**Application 1:** $y'' + (\sin x)y' + xy = 0$, given $W(\pi/2) = 1$:
$$W(x) = e^{-\int_{\pi/2}^x \sin t\,dt} = e^{\cos x - \cos(\pi/2)} = e^{\cos x}.$$

**Application 2:** $y'' + (2/x)y' + y = 0$ ($x > 0$, $p = 2/x$), given $W(1) = 3$:
$$W(x) = 3\,e^{-\int_1^x (2/t)\,dt} = 3\,e^{-2\ln x} = \frac{3}{x^2} \neq 0 \text{ for all } x>0.$$
Any pair with $W(1) \neq 0$ is a fundamental set.

**Practical use in VoP (Week 7):** Abel's theorem lets us compute $W(x)$ without explicitly computing the determinant — just evaluate at $x_0$ and multiply by $e^{-\int p\,dt}$.

---

#### 9. Summary Table — Week 6

| Concept | Formula / Statement |
|---|---|
| Standard form | $y'' + p(x)y' + q(x)y = r(x)$ |
| Existence/uniqueness | Unique solution on full continuity interval |
| Superposition | $c_1y_1 + c_2y_2$ solves homogeneous |
| Wronskian | $W = y_1y_2' - y_1'y_2$ |
| Fund. set criterion | $W \neq 0 \iff$ linearly independent |
| Reduction of order | $y_2 = y_1\int e^{-\int p\,dx}/y_1^2\,dx$ |
| Char. eq. Case 1 | $\Delta > 0$: $c_1e^{\lambda_1 x}+c_2e^{\lambda_2 x}$ |
| Char. eq. Case 2 | $\Delta < 0$: $e^{\alpha x}(c_1\cos\beta x+c_2\sin\beta x)$ |
| Char. eq. Case 3 | $\Delta = 0$: $(c_1+c_2x)e^{\lambda x}$ |
| Euler–Cauchy trial | $y = x^m$; char. eq. $m^2+(a-1)m+b=0$ |
| E–C Case 3 | $(c_1+c_2\ln x)x^m$ |
| Abel's theorem | $W(x) = W(x_0)e^{-\int_{x_0}^x p\,dt}$ |
| Physics mapping | Overdamped / Critically damped / Underdamped |

---

## Cross-References

- **Week 5 Lec 1** (Linear first-order ODEs): integrating factor structure prepares for operator notation.
- **Week 7 Lec 1** (Undetermined Coefficients): uses characteristic roots from this week's theory.
- **Week 7 Lec 2** (Variation of Parameters): uses the Wronskian and reduction-of-order ideas.
- **Week 7 Lec 3** (Higher-order ODEs): extends all three characteristic root cases to degree $n$.

---

## Practice Problems

1. Find the general solution of $y'' + 6y' + 9y = 0$ and identify the physical damping case.
2. Find $y_2$ by reduction of order: $y'' - 2y' + y = 0$, given $y_1 = e^x$.
3. Solve $x^2 y'' + xy' - 4y = 0$ ($x > 0$) using the Euler–Cauchy method.
4. Apply Abel's theorem to $y'' + (\cos x)y' + y = 0$: if $W(\pi) = 2$, find $W(0)$.
5. Solve the IVP: $y'' + 4y = 0$, $y(0) = 3$, $y'(0) = -2$.
6. For $x^2y'' - xy' + 5y = 0$, find the general solution and verify the Wronskian is nonzero.
