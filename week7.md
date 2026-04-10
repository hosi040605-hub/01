# Week 7 — Non-Homogeneous Second-Order ODEs and Higher-Order Linear ODEs

**Course:** Engineering Mathematics 1
**Part:** III — Second-Order Ordinary Differential Equations (Non-Homogeneous); Higher-Order
**Kreyszig Sections:** §2.7, §2.10; §3.1–3.3

---

## Lecture 1: Method of Undetermined Coefficients

### Introduction

Having solved the homogeneous equation $y_h$, we now tackle non-homogeneous second-order ODEs $y'' + py' + qy = r(x)$. The **Method of Undetermined Coefficients (UC)** is the fastest approach when $r(x)$ belongs to a specific family — polynomials, exponentials, and sinusoids. The key insight is that these functions are **closed under differentiation**, so a trial of the same form will survive substitution and allow coefficient matching.

**Why UC matters in engineering:**
- Forced mechanical oscillations ($r = F_0\cos\omega t$), driven RLC circuits, and polynomial loading on beams — all fall squarely in the UC family.
- The modification rule captures **resonance** — the physically critical situation where forcing matches the natural frequency.

---

### Knowledge Points

---

#### 1. General Solution Structure for Non-Homogeneous ODEs

**Theorem:** The general solution of $y'' + p(x)y' + q(x)y = r(x)$ is:
$$y = y_h + y_p = c_1 y_1 + c_2 y_2 + y_p,$$
where $\{y_1, y_2\}$ is a fundamental set for the homogeneous equation and $y_p$ is **any** particular solution of the full equation.

**Physical decomposition:**
- $y_h = c_1 y_1 + c_2 y_2$: **transient response** — decays if $\mathrm{Re}(\lambda) < 0$.
- $y_p$: **forced/steady-state response** — driven by $r(x)$, persists as long as $r$ acts.

**Proof sketch:** Any solution $Y$ satisfies $(Y - y_p)'' + p(Y - y_p)' + q(Y - y_p) = r - r = 0$, so $Y - y_p = c_1 y_1 + c_2 y_2$, i.e., $Y = y_h + y_p$. $\checkmark$

**Caution:** Apply ICs to the **full** solution $y = y_h + y_p$, not to $y_h$ alone.

---

#### 2. The UC Family and Trial Functions

**Scope:** The UC method works when $r(x)$ belongs to the **UC family**: polynomials, exponentials, $\cos$/$\sin$, and their products and sums. These are closed under differentiation — substituting the trial always produces the same family.

| $r(x)$ | Trial $y_p$ |
|---|---|
| Constant $A$ | $K$ |
| $P_n(x)$ (degree $n$) | $K_n x^n + \cdots + K_0$ |
| $e^{\alpha x}$ | $K e^{\alpha x}$ |
| $\cos\beta x$ or $\sin\beta x$ | $A\cos\beta x + B\sin\beta x$ |
| $e^{\alpha x}\cos\beta x$ or $e^{\alpha x}\sin\beta x$ | $e^{\alpha x}(A\cos\beta x + B\sin\beta x)$ |
| $P_n(x)\,e^{\alpha x}$ | $(K_n x^n + \cdots + K_0)e^{\alpha x}$ |

**Key rules:**
1. Always include **both** $\cos\beta x$ and $\sin\beta x$ in the trial for sinusoidal forcing.
2. If $r = r_1 + r_2$: find $y_{p1}$, $y_{p2}$ separately and add (superposition).

---

#### 3. Superposition for Right-Hand Sides

**Theorem:** If $y_{p1}$ solves $L[y] = r_1(x)$ and $y_{p2}$ solves $L[y] = r_2(x)$, then $y_p = y_{p1} + y_{p2}$ solves $L[y] = r_1(x) + r_2(x)$.

**Strategy:** Split $r(x) = r_1 + r_2 + \cdots$ into pieces, find each $y_{pk}$ individually, then add.

---

#### 4. Worked Examples

**Example 1 — Polynomial forcing:** Solve $y'' - 3y' + 2y = 4x^2$.
- Homogeneous: $(\lambda-1)(\lambda-2)=0 \Rightarrow y_h = c_1 e^x + c_2 e^{2x}$.
- Trial: $y_p = Ax^2 + Bx + C$; $y_p' = 2Ax+B$; $y_p'' = 2A$.
- Substitute: $2A - 3(2Ax+B) + 2(Ax^2+Bx+C) = 4x^2$.
- Match: $x^2$: $A=2$; $x^1$: $-6A+2B=0 \Rightarrow B=6$; $x^0$: $2A-3B+2C=0 \Rightarrow C=7$.
- **Solution:** $y = c_1 e^x + c_2 e^{2x} + 2x^2 + 6x + 7$.

**Example 2 — Exponential forcing:** Solve $y'' - y' - 2y = 3e^{4x}$.
- $y_h = c_1 e^{2x} + c_2 e^{-x}$.
- Trial: $y_p = Ke^{4x}$; $(16K - 4K - 2K)e^{4x} = 3e^{4x} \Rightarrow 10K = 3 \Rightarrow K = 3/10$.
- **Solution:** $y = c_1 e^{2x} + c_2 e^{-x} + \frac{3}{10}e^{4x}$.

**Example 3 — Sinusoidal forcing:** Solve $y'' + 4y = 8\cos 3x$.
- $\lambda = \pm 2i \Rightarrow y_h = c_1\cos 2x + c_2\sin 2x$.
- Trial: $y_p = A\cos 3x + B\sin 3x$; $y_p'' = -9A\cos 3x - 9B\sin 3x$.
- $(-9A+4A)\cos 3x + (-9B+4B)\sin 3x = 8\cos 3x$: $A = -8/5$, $B = 0$.
- **Solution:** $y = c_1\cos 2x + c_2\sin 2x - \frac{8}{5}\cos 3x$.
- (Forcing frequency $\neq$ natural frequency; no resonance.)

**Example 4 — Superposition:** Solve $y'' - y = e^x + \sin 2x$.
- $y_h = c_1 e^x + c_2 e^{-x}$.
- **Part 1** ($r_1 = e^x$): $\alpha = 1$ is a simple root $\Rightarrow$ multiply trial by $x$.
  Try $y_{p1} = Axe^x$: $y_{p1}'' - y_{p1} = 2Ae^x = e^x \Rightarrow A = 1/2$. $y_{p1} = \frac{1}{2}xe^x$.
- **Part 2** ($r_2 = \sin 2x$): Trial $A\cos 2x + B\sin 2x$; $(-4A - A)\cos 2x + (-4B - B)\sin 2x = \sin 2x$: $A = 0$, $B = -1/5$. $y_{p2} = -\frac{1}{5}\sin 2x$.
- **Solution:** $y = c_1 e^x + c_2 e^{-x} + \frac{1}{2}xe^x - \frac{1}{5}\sin 2x$.

---

#### 5. The Modification Rule — When the Trial Is in $y_h$

**The problem:** If the natural trial $y_p^{(0)}$ is a solution of the homogeneous equation (or a linear combination), substituting it gives $0 = r(x)$ — a contradiction.

**Engineering meaning:** The forcing frequency matches the system's natural frequency — **resonance**. The response grows without bound.

**Modification Rule:** If the natural trial satisfies the homogeneous equation with multiplicity $s$ (the corresponding characteristic root has multiplicity $s$), multiply the trial by $x^s$.
- $\lambda = \alpha$ simple and $r = e^{\alpha x}$: try $y_p = Axe^{\alpha x}$.
- $\lambda = \alpha$ double and $r = e^{\alpha x}$: try $y_p = Ax^2 e^{\alpha x}$.
- $\lambda = \pm i\beta$ simple and $r = \cos\beta x$: try $y_p = x(A\cos\beta x + B\sin\beta x)$.

**Example — Exponential resonance:** $y'' - 2y' + y = e^x$.
- $(\lambda-1)^2 = 0 \Rightarrow \lambda = 1$ (double). $y_h = (c_1 + c_2 x)e^x$.
- Natural trial $e^x$ is in $y_h$ with multiplicity 2: try $y_p = Ax^2 e^x$.
- Substituting: $y_p'' - 2y_p' + y_p = 2Ae^x = e^x \Rightarrow A = 1/2$.
- **Solution:** $y = (c_1 + c_2 x)e^x + \frac{x^2}{2}e^x$.

**Example — Sinusoidal resonance (undamped):** $y'' + \omega_0^2 y = F_0\cos\omega_0 x$.
- Roots $\pm i\omega_0$ (simple): try $y_p = x(A\cos\omega_0 x + B\sin\omega_0 x)$.
- After substituting: $B = F_0/(2\omega_0)$, $A = 0$, so
$$y_p = \frac{F_0}{2\omega_0}\,x\sin\omega_0 x.$$
- The factor $x$ causes amplitude to grow **linearly without bound** — resonance.

---

#### 6. UC Summary Table

| Concept | Key Formula / Rule |
|---|---|
| General solution | $y = y_h + y_p = c_1y_1 + c_2y_2 + y_p$ |
| Trial: polynomial | $r = P_n(x) \to y_p = Q_n(x)$ (same degree) |
| Trial: exponential | $r = e^{\alpha x} \to y_p = Ke^{\alpha x}$ |
| Trial: sinusoidal | $r = \cos\beta x$ or $\sin\beta x \to A\cos\beta x + B\sin\beta x$ |
| Superposition | $r = r_1 + r_2 \to y_p = y_{p1} + y_{p2}$ |
| Modification rule | Trial in $y_h$ with mult. $s$: multiply by $x^s$ |
| Resonance formula | $y_p = \frac{F_0}{2\omega_0}x\sin\omega_0 x$ (undamped) |
| Scope | UC family: poly $\times$ exp $\times$ trig only |

---

## Lecture 2: Variation of Parameters

### Introduction

The UC method fails when $r(x)$ lies outside the UC family — $\sec x$, $\ln x$, $e^x/x^2$, or any function that does not belong to a finite-dimensional subspace closed under differentiation. **Variation of Parameters (VoP)**, invented by Lagrange, handles **any** continuous $r(x)$ and works for variable-coefficient equations too. The price: two integrals, which may require numerical evaluation.

**Key idea (Lagrange):** Replace the constants $c_1$, $c_2$ in $y_h = c_1 y_1 + c_2 y_2$ with unknown functions $u_1(x)$, $u_2(x)$:
$$y_p = u_1(x)\,y_1(x) + u_2(x)\,y_2(x).$$

---

### Knowledge Points

---

#### 1. When UC Fails

The UC method requires $r(x)$ to belong to the UC family (poly $\times$ exp $\times$ trig). Many engineering forcing functions lie outside this family:
- $r(x) = \sec x = 1/\cos x$ — no finite trial function.
- $r(x) = 1/x$, $\ln x$ — appear in Euler–Cauchy problems.
- $r(x) = e^x/x^2$ — rational factor blocks UC.

VoP handles any continuous $r(x)$, and works for variable-coefficient equations too.

---

#### 2. Derivation — Lagrange's Condition

**Differentiate the ansatz:** $y_p' = u_1'y_1 + u_1 y_1' + u_2'y_2 + u_2 y_2'$.

**Impose Lagrange's condition** (simplifies algebra):
$$u_1'y_1 + u_2'y_2 = 0. \tag{L}$$
Then $y_p' = u_1 y_1' + u_2 y_2'$.

**Differentiate again:** $y_p'' = u_1'y_1' + u_1 y_1'' + u_2'y_2' + u_2 y_2''$.

**Substitute into $y_p'' + py_p' + qy_p = r$:** The terms $u_i(y_i'' + py_i' + qy_i) = 0$ vanish (since $y_i$ solves the homogeneous equation), leaving:
$$u_1'y_1' + u_2'y_2' = r. \tag{R}$$

**The $2\times 2$ system** from (L) and (R):
$$\begin{pmatrix}y_1 & y_2 \\ y_1' & y_2'\end{pmatrix} \begin{pmatrix}u_1' \\ u_2'\end{pmatrix} = \begin{pmatrix}0 \\ r\end{pmatrix}.$$
Coefficient determinant $= W = y_1 y_2' - y_1' y_2 \neq 0$.

---

#### 3. VoP Formulas

**Solve by Cramer's Rule:**
$$u_1' = \frac{-y_2 r}{W}, \qquad u_2' = \frac{y_1 r}{W}.$$

**Integrate:**
$$u_1 = -\int\frac{y_2(x)\,r(x)}{W(x)}\,dx, \qquad u_2 = \int\frac{y_1(x)\,r(x)}{W(x)}\,dx.$$

**VoP Particular Solution:**
$$\boxed{y_p = -y_1\int\frac{y_2 r}{W}\,dx + y_2\int\frac{y_1 r}{W}\,dx.}$$

**Notes:**
- No constants of integration needed in $u_1$, $u_2$ — any antiderivative gives a valid $y_p$.
- $W \neq 0$ is guaranteed since $\{y_1, y_2\}$ is a fundamental set.
- **Abel's shortcut:** $W(x) = W(x_0)e^{-\int_{x_0}^x p\,dt}$ — avoids direct Wronskian computation.

---

#### 4. Worked Examples

**Example 1 — Exponential Forcing (Compare UC and VoP):** Solve $y'' - 3y' + 2y = e^{3x}$.
- $y_1 = e^x$, $y_2 = e^{2x}$; $W = e^x \cdot 2e^{2x} - e^x \cdot e^{2x} = e^{3x}$.
- VoP: $u_1' = -e^{2x} \cdot e^{3x}/e^{3x} = -e^{2x} \Rightarrow u_1 = -e^{2x}/2$.
- $u_2' = e^x \cdot e^{3x}/e^{3x} = e^x \Rightarrow u_2 = e^x$.
- $y_p = e^x(-e^{2x}/2) + e^{2x}(e^x) = -e^{3x}/2 + e^{3x} = e^{3x}/2$.
- **UC check:** $\alpha=3$ not a root; trial $Ke^{3x}$: $(9-9+2)K = 1 \Rightarrow K = 1/2$. $\checkmark$

**Example 2 — Outside the UC Family: $\sec x$:** Solve $y'' + y = \sec x$ ($-\pi/2 < x < \pi/2$).
- $\lambda = \pm i$: $y_1 = \cos x$, $y_2 = \sin x$, $W = 1$.
- $u_1' = -\sin x \cdot \sec x = -\tan x \Rightarrow u_1 = \ln|\cos x|$.
- $u_2' = \cos x \cdot \sec x = 1 \Rightarrow u_2 = x$.
$$y_p = \cos x \cdot \ln|\cos x| + x\sin x.$$
- **General solution:** $y = c_1\cos x + c_2\sin x + \cos x\ln|\cos x| + x\sin x$.
- **Why UC fails:** $\sec x = 1/\cos x$ is not in any finite-dimensional subspace closed under differentiation.

**Example 3 — Euler–Cauchy with VoP:** Solve $x^2 y'' - 3xy' + 3y = x^4\ln x$ ($x > 0$).
- Homogeneous (Euler–Cauchy): $m^2 - 4m + 3 = (m-1)(m-3) = 0 \Rightarrow y_1 = x$, $y_2 = x^3$.
- **Standard form** (divide by $x^2$): $r(x) = x^2\ln x$.
- $W = x \cdot 3x^2 - 1 \cdot x^3 = 2x^3$.
- $u_1' = -x^3 \cdot x^2\ln x/(2x^3) = -x^2\ln x/2$:
  $u_1 = -\frac{1}{2}\left[\frac{x^3}{3}\ln x - \frac{x^3}{9}\right] = -\frac{x^3\ln x}{6} + \frac{x^3}{18}$.
- $u_2' = x \cdot x^2\ln x/(2x^3) = \ln x/2$: $u_2 = (x\ln x - x)/2$.
- **Particular solution:**
$$y_p = \frac{x^4\ln x}{3} - \frac{4x^4}{9}.$$

---

#### 5. Green's Function Interpretation

Using definite integrals in VoP gives the **Green's function** (impulse response) formulation:
$$y_p(x) = \int_{x_0}^x G(x,t)\,r(t)\,dt, \qquad G(x,t) = \frac{y_1(t)y_2(x) - y_1(x)y_2(t)}{W(t)}.$$

$G(x,t)$ is the response at $x$ to an impulse at $t$ — the foundation of the **impulse response** approach in control engineering (Weeks 14–15).

**Full IVP procedure with VoP:**
1. Find $y_h = c_1 y_1 + c_2 y_2$.
2. Apply VoP to find $y_p$ (use indefinite integrals, drop constants).
3. Write $y = c_1 y_1 + c_2 y_2 + y_p$.
4. Apply ICs $y(x_0) = k_0$, $y'(x_0) = k_1$ to determine $c_1$, $c_2$.

**Caution:** ICs are applied to the **full** solution $y_h + y_p$, not $y_h$ alone.

---

#### 6. UC vs. VoP Comparison

| Feature | Undetermined Coefficients | Variation of Parameters |
|---|---|---|
| Scope of $r(x)$ | UC family only | Any continuous $r(x)$ |
| Computation | Algebraic (match coefficients) | Integration (may be hard) |
| Needs $y_h$? | Roots only (modification check) | Yes (full fundamental set) |
| Variable coefficients? | No | Yes |
| Modification rule? | Sometimes | Never |
| Best for | Const.-coeff. UC forcing | General; variable-coeff. |

**Practical rule:** Use UC when applicable (faster). Fall back to VoP for forcing outside the UC family or variable-coefficient ODEs.

---

#### 7. VoP Summary Table

| Concept | Key Formula |
|---|---|
| VoP ansatz | $y_p = u_1(x)y_1 + u_2(x)y_2$ |
| Lagrange's condition | $u_1'y_1 + u_2'y_2 = 0$ |
| ODE condition | $u_1'y_1' + u_2'y_2' = r$ |
| $u_1'$, $u_2'$ | $u_1' = -y_2 r/W$, $u_2' = y_1 r/W$ |
| VoP formula | $y_p = -y_1\int(y_2 r/W)\,dx + y_2\int(y_1 r/W)\,dx$ |
| Abel's shortcut | $W(x) = W(x_0)e^{-\int_{x_0}^x p\,dt}$ |
| Green's function | $y_p(x) = \int_{x_0}^x G(x,t)r(t)\,dt$ |
| Scope | Any continuous $r(x)$; any equation with known $y_h$ |

---

## Lecture 3: Higher-Order Linear ODEs

### Introduction

The theory of second-order linear ODEs extends cleanly to order $n$. The structure — characteristic polynomial, fundamental set, UC, VoP — all generalize with the same logic. This lecture establishes the $n$-th order theory and works through key engineering applications, including the **Euler–Bernoulli beam equation** (4th order).

---

### Knowledge Points

---

#### 1. Structure of Order-$n$ ODEs

**Standard form:**
$$y^{(n)} + p_{n-1}(x)\,y^{(n-1)} + \cdots + p_1(x)\,y' + p_0(x)\,y = r(x).$$

**Existence and Uniqueness:** If all $p_k$ and $r$ are continuous on $I \ni x_0$, the IVP with $n$ conditions
$$y(x_0) = k_0,\; y'(x_0) = k_1,\; \ldots,\; y^{(n-1)}(x_0) = k_{n-1}$$
has a **unique solution** on all of $I$.

**Solution space:** The homogeneous equation has an **$n$-dimensional** solution space. A fundamental set $\{y_1, \ldots, y_n\}$ has $W[y_1, \ldots, y_n] \neq 0$.

**General solution:** $y = y_h + y_p = c_1 y_1 + \cdots + c_n y_n + y_p$.

**Engineering examples:**
- Beam deflection: $EI\,y^{(4)} = q(x)$ — 4th order, 4 constants, 4 BCs.
- Higher-order electrical filter: transfer function poles of multiplicity $> 2$.
- Characteristic polynomial of order $n$ = denominator in Laplace analysis.

---

#### 2. Characteristic Polynomial and Root Contributions

**Constant-coefficient case:** Trial $y = e^{\lambda x}$ gives $P(\lambda) = a_n\lambda^n + \cdots + a_0 = 0$ (degree $n$, $n$ roots).

**Contribution of each root type:**

**Real root $\lambda = a$ of multiplicity $k$:**
$$e^{ax},\; xe^{ax},\; x^2 e^{ax},\; \ldots,\; x^{k-1}e^{ax}. \quad (k \text{ solutions})$$

**Complex pair $\lambda = \alpha \pm i\beta$ of multiplicity $k$:**
$$x^j e^{\alpha x}\cos\beta x \;\text{ and }\; x^j e^{\alpha x}\sin\beta x, \quad j = 0, 1, \ldots, k-1. \quad (2k \text{ solutions})$$

**Total:** Every root of multiplicity $k$ contributes $k$ linearly independent solutions, summing to exactly $n$ solutions.

---

#### 3. Worked Examples — Higher-Order

**Example 1 — Fourth-order ODE:** Solve $y^{(4)} - y = 0$.
$$\lambda^4 - 1 = (\lambda^2-1)(\lambda^2+1) = (\lambda-1)(\lambda+1)(\lambda-i)(\lambda+i) = 0.$$
Roots: $\lambda = 1,\; -1,\; \pm i$.
$$y = c_1 e^x + c_2 e^{-x} + c_3\cos x + c_4\sin x.$$
Equivalently: $c_1\cosh x + c_2\sinh x + c_3\cos x + c_4\sin x$.

**Example 2 — Triple root:** Solve $y''' - 3y'' + 3y' - y = 0$.
$$\lambda^3 - 3\lambda^2 + 3\lambda - 1 = (\lambda-1)^3 = 0.$$
Triple root $\lambda = 1$:
$$y = (c_1 + c_2 x + c_3 x^2)e^x.$$

**Example 3 — Repeated complex roots:** Solve $y^{(4)} + 8y'' + 16y = 0$.
$$\lambda^4 + 8\lambda^2 + 16 = (\lambda^2+4)^2 = 0.$$
Roots $\lambda = \pm 2i$, each of multiplicity 2 ($\alpha = 0$, $\beta = 2$). Four solutions: $\cos 2x$, $\sin 2x$, $x\cos 2x$, $x\sin 2x$:
$$y = (c_1 + c_3 x)\cos 2x + (c_2 + c_4 x)\sin 2x.$$

---

#### 4. Non-Homogeneous Higher-Order ODEs

**Structure unchanged:** $y = y_h + y_p$; apply ICs to full solution.

**UC:** Same trial families as second order; same modification rule (multiply by $x^s$ if trial lies in $y_h$ with multiplicity $s$).

**Example — UC for 3rd order:** Solve $y''' - y'' = 3e^{2x}$.
- $\lambda^3 - \lambda^2 = \lambda^2(\lambda-1) = 0$: $\lambda = 0$ (double), $\lambda = 1$.
- $y_h = c_1 + c_2 x + c_3 e^x$.
- UC trial: $r = 3e^{2x}$, $\alpha = 2$ not a root $\Rightarrow y_p = Ae^{2x}$.
- $(8A - 4A)e^{2x} = 3e^{2x} \Rightarrow 4A = 3 \Rightarrow A = 3/4$.
- **Solution:** $y = c_1 + c_2 x + c_3 e^x + \frac{3}{4}e^{2x}$.

**Modification example:** $y''' - y'' = 3x + 2$.
- $y_h = c_1 + c_2 x + c_3 e^x$.
- Natural trial $Ax + B$ is in $y_h$ ($\lambda = 0$ double, $s = 2$).
- Modified trial: $(Ax + B)x^2 = Ax^3 + Bx^2$.

---

#### 5. IVP for Higher-Order ODEs

**Procedure:** $n$ initial conditions at $x_0$ determine the $n$ constants $c_1, \ldots, c_n$.

**Example:** Solve $y''' - y'' = 3e^{2x}$, $y(0) = 0$, $y'(0) = 0$, $y''(0) = 0$.
- From above: $y_h = c_1 + c_2 x + c_3 e^x$, $y_p = \frac{3}{4}e^{2x}$.
- Full solution: $y = c_1 + c_2 x + c_3 e^x + \frac{3}{4}e^{2x}$.
- $y' = c_2 + c_3 e^x + \frac{3}{2}e^{2x}$; $y'' = c_3 e^x + 3e^{2x}$.
- Apply ICs at $x = 0$:
  - $y(0) = c_1 + c_3 + 3/4 = 0 \Rightarrow c_1 + c_3 = -3/4$.
  - $y'(0) = c_2 + c_3 + 3/2 = 0 \Rightarrow c_2 + c_3 = -3/2$.
  - $y''(0) = c_3 + 3 = 0 \Rightarrow c_3 = -3$.
- Back-substitute: $c_1 = 9/4$, $c_2 = 3/2$.
- **Solution:** $y = \frac{9}{4} + \frac{3}{2}x - 3e^x + \frac{3}{4}e^{2x}$.

---

#### 6. Beam Deflection — A 4th-Order Application

**Euler–Bernoulli Beam Equation:**
$$EI\,\frac{d^4 y}{dx^4} = q(x),$$
where $y(x)$ = deflection, $E$ = Young's modulus, $I$ = second moment of area, $q(x)$ = distributed load (N/m).

**Homogeneous solution** ($q = 0$): $\lambda^4 = 0$ — quadruple root $\lambda = 0$.
$$y_h = c_1 + c_2 x + c_3 x^2 + c_4 x^3.$$
Cubic polynomial deflection — consistent with zero-bending unloaded beam.

**Boundary conditions (BCs):** Specified at **both** ends (not just $x = 0$).

Simply supported beam ($0 \leq x \leq L$):
$$y(0) = 0,\; y''(0) = 0,\; y(L) = 0,\; y''(L) = 0.$$

**Engineering significance:** Structural analysis of beams, bridges, and plates. The same 4th-order ODE governs all classical beam theories.

---

#### 7. Summary — Higher-Order Linear ODEs

| Concept | Extension to Order $n$ |
|---|---|
| Characteristic polynomial | Degree $n$; $n$ roots (with multiplicity) |
| Real root mult. $k$ | $e^{ax}, xe^{ax}, \ldots, x^{k-1}e^{ax}$ ($k$ solutions) |
| Complex pair mult. $k$ | $x^j e^{\alpha x}\cos\beta x$ and $x^j e^{\alpha x}\sin\beta x$, $j=0,\ldots,k-1$ |
| General solution | $y = c_1y_1 + \cdots + c_ny_n + y_p$ |
| IVP | $n$ conditions $y(x_0)=k_0, \ldots, y^{(n-1)}(x_0)=k_{n-1}$ |
| UC | Same trial families; modification rule unchanged |
| VoP | $n\times n$ system; complex for $n \geq 3$ |
| Beam equation | $y^{(4)} = q/EI$; 4th order; BCs at two endpoints |

---

## Cross-References

- **Week 6 Lec 1** (Reduction of Order): provides the foundation for VoP derivation.
- **Week 6 Lec 2/3** (Characteristic equation, 3 cases): the homogeneous solutions $y_h$ required by both UC and VoP.
- **Weeks 14–15** (Laplace Transform): Green's functions appear as transfer functions; UC and VoP solutions reappear in frequency domain.

---

## Practice Problems

1. Solve $y'' + 2y' + y = e^{-x}$ using UC (watch for resonance).
2. Solve $y'' + y = \tan x$ using VoP ($-\pi/2 < x < \pi/2$). Hint: $\int \sec x\,dx = \ln|\sec x + \tan x|$.
3. Solve $y^{(4)} - 16y = 0$. Identify all four characteristic roots and write the general solution.
4. Solve $y''' - y'' = x^2$. Check whether modification is needed.
5. Apply VoP to $y'' - y = e^x / (1 + e^x)$.
6. A uniform beam of length $L$ is clamped at both ends with uniform load $q_0$. Set up the BVP: $EI\,y^{(4)} = q_0$ with BCs $y(0) = y'(0) = y(L) = y'(L) = 0$. Find $y(x)$.
