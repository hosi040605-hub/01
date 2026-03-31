# Week 5 — Linear First-Order ODEs, Autonomous Equations & Applications

**Course:** Engineering Mathematics 1
**Part:** II — First-Order Ordinary Differential Equations
**Kreyszig Sections:** §1.5, §1.7

---

## Lecture 1: Linear First-Order ODEs and Bernoulli Equations

### Introduction

In Week 4 we solved separable and exact ODEs. A large and important class that is neither separable nor exact in general is the **linear first-order ODE**. Its systematic solution method is the **integrating factor**: multiply both sides by a cleverly chosen function $\mu(x)$ so that the left side becomes an exact derivative. This lecture also covers the **Bernoulli equation** — an important nonlinear ODE that can be *transformed* into a linear equation by substitution, with the **logistic equation** as its most important application.

---

### Knowledge Points

---

#### 1. Standard Form of a Linear First-Order ODE

**Definition:** A **linear first-order ODE** in **standard form** is:
$$y' + p(x)\,y = r(x)$$
where $p(x)$ and $r(x)$ are given continuous functions.

**Key features:**
- $y$ and $y'$ appear to the **first power only** (no $y^2$, $yy'$, $\sin y$, etc.).
- $p$, $r$ may be arbitrary functions of $x$.
- $r(x) = 0$: **homogeneous**. $r(x) \neq 0$: **non-homogeneous**.

**Converting to standard form:** Divide through by the coefficient of $y'$.

**Example:** $xy' + 3y = \cos x$. Divide by $x$ ($x \neq 0$): $y' + \frac{3}{x}y = \frac{\cos x}{x}$.
Here $p(x) = 3/x$, $r(x) = (\cos x)/x$.

---

#### 2. The Homogeneous Linear ODE

**Equation:** $y' + p(x)y = 0$.

This is **separable**: $dy/y = -p(x)\,dx$. Integrating:
$$\ln|y| = -\int p(x)\,dx + C_1 \implies y_h = Ce^{-\int p(x)\,dx}.$$

**Properties:**
- Single-parameter family of curves.
- $y = 0$ is always a solution (trivial solution).
- All non-trivial solutions are scalar multiples of $e^{-\int p\,dx}$.

**Example:** $y' + 2xy = 0$. Then $y_h = Ce^{-x^2}$.

**Role of $y_h$:** $y_h$ encodes the **transient** (decaying) behaviour; it is the "free" part of the full solution.

---

#### 3. Derivation of the Integrating Factor

**Goal:** Solve $y' + p(x)y = r(x)$.

**Idea:** Multiply both sides by $\mu(x)$ (to be determined):
$$\mu y' + \mu p y = \mu r.$$

We want the left side to equal $\frac{d}{dx}[\mu y] = \mu y' + \mu' y$. This requires $\mu' = \mu p(x)$:
$$\frac{d\mu}{\mu} = p(x)\,dx \implies \mu(x) = e^{\int p(x)\,dx}.$$

With this $\mu$:
$$\frac{d}{dx}[\mu y] = \mu r \implies \mu y = \int \mu r\,dx + C \implies \boxed{y = \frac{1}{\mu}\!\left(\int \mu r\,dx + C\right).}$$

**Connection to Week 4:** Same IF idea from Lec 3 (differential form $(py-r)\,dx+dy=0$, $(M_y-N_x)/N = p(x)$).

---

#### 4. The Integrating Factor Method — Algorithm

**Given:** $y' + p(x)y = r(x)$, $y(x_0) = y_0$.

1. Compute $\mu(x) = e^{\int p(x)\,dx}$ (any antiderivative — the constant cancels).
2. Rewrite as $(\mu y)' = \mu(x)\,r(x)$.
3. Integrate: $\mu(x)\,y = \displaystyle\int \mu(x)\,r(x)\,dx + C$.
4. Divide by $\mu(x)$: $y = \dfrac{1}{\mu(x)}\!\left(\displaystyle\int\mu r\,dx + C\right)$.
5. Apply IC to determine $C$.

**Note:** If $r(x) = 0$, step 3 gives $\mu y = C$, recovering $y_h = Ce^{-\int p\,dx}$. The general solution is always $y = y_h + y_p$ (transient + steady-state).

---

#### 5. Worked Example 1 — Variable Coefficients

**Solve:** $y' + \dfrac{1}{x}y = x^2$, $y(1) = 2$ (for $x > 0$).

$p = 1/x$, $r = x^2$. $\mu = e^{\int (1/x)\,dx} = e^{\ln x} = x$.

$(xy)' = x \cdot x^2 = x^3$. Integrate: $xy = x^4/4 + C$. Divide: $y = x^3/4 + C/x$.

Apply IC: $y(1) = 1/4 + C = 2 \Rightarrow C = 7/4$.

**Solution:** $y = \dfrac{x^3}{4} + \dfrac{7}{4x}$.

**Notes:**
- IF $\mu = x$ is a polynomial — no exponential needed.
- $p = 1/x$ is discontinuous at $x = 0$: solution is valid on $(0,\infty)$ only.

---

#### 6. Worked Example 2 — Trigonometric Forcing

**Solve:** $y' - y = \sin x$.

$p = -1$, $r = \sin x$. $\mu = e^{-x}$.

$(e^{-x}y)' = e^{-x}\sin x$. Integrate by parts: $\int e^{-x}\sin x\,dx = -\dfrac{e^{-x}}{2}(\sin x + \cos x) + C$.

**Solution:** $y = -\dfrac{1}{2}(\sin x + \cos x) + Ce^{x}$.

**Interpretation:**
- $y_p = -\frac{1}{2}(\sin x + \cos x)$: oscillates at the forcing frequency.
- $y_h = Ce^{x}$: **unstable** transient (grows for $C \neq 0$).

---

#### 7. Singular Points and Interval of Validity

The IF formula is valid only where $p(x)$ and $r(x)$ are **continuous**.

**Theorem (Existence and Uniqueness for Linear ODEs):** If $p$ and $r$ are continuous on an open interval $I \ni x_0$, then the IVP $y' + py = r$, $y(x_0) = y_0$ has a **unique solution on all of $I$**.

*Key difference from nonlinear ODEs:* For linear ODEs the solution exists on the *entire* interval of continuity — no finite blow-up.

**Practical rule:** Before solving, identify all singular points of $p$ and $r$. The solution interval is the maximal subinterval around $x_0$ containing no singularities.

---

#### 8. Newton's Law of Cooling — Linear ODE Perspective

Newton's Cooling: $T' = -k(T - T_{\rm env})$. Rewrite: $T' + kT = kT_{\rm env}$.

$p = k$, $r = kT_{\rm env}$ (constant). $\mu = e^{kt}$.

$(e^{kt}T)' = kT_{\rm env}e^{kt} \implies T = T_{\rm env} + Ae^{-kt}$.

Apply $T(0) = T_0$: $A = T_0 - T_{\rm env}$.
$$T(t) = T_{\rm env} + (T_0 - T_{\rm env})\,e^{-kt}.$$

**Same result as the Week 4 separable method** — confirming both approaches. The linear ODE approach is more powerful for **time-varying** $T_{\rm env}(t)$: just replace the constant $r = kT_{\rm env}$ by $k T_{\rm env}(t)$ and integrate.

---

#### 9. The Bernoulli Equation — Definition and Substitution

**Definition:** A **Bernoulli equation** is a first-order ODE of the form:
$$y' + p(x)y = r(x)y^n, \qquad n \in \mathbb{R},\ n \neq 0, 1.$$

- $n = 0$: reduces to linear $y' + py = r$ (already solved).
- $n = 1$: reduces to separable $y' + (p-r)y = 0$.
- All other $n$: **nonlinear** — requires the Bernoulli substitution.

**Examples:**
- $y' - y = -y^2$ ($n = 2$, logistic type).
- $y' + y = xy^3$ ($n = 3$).
- $y' - \frac{1}{2}y = \frac{3}{2}y^{1/3}$ ($n = 1/3$).

**Key idea:** Divide both sides by $y^n$: $y^{-n}y' + p(x)y^{1-n} = r(x)$.

Set $v = y^{1-n}$: $v' = (1-n)y^{-n}y'$, so $y^{-n}y' = v'/(1-n)$.

**Theorem (Bernoulli Substitution):** $v = y^{1-n}$ transforms $y' + py = ry^n$ into the **linear** ODE:
$$v' + (1-n)\,p(x)\,v = (1-n)\,r(x).$$
Solve for $v$ by IF: $\mu = e^{(1-n)\int p\,dx}$. Back-substitute $v = y^{1-n}$ to recover $y$.
**Check:** $y = 0$ is a singular solution, lost when dividing by $y^n$.

---

#### 10. Bernoulli Example 1 — $n = 2$

**Solve:** $y' - y = -y^2$, $y(0) = 2$.

Divide by $y^2$: $y^{-2}y' - y^{-1} = -1$.
Let $v = y^{-1}$, $v' = -y^{-2}y'$: $-v' - v = -1$, i.e., $v' + v = 1$.
Linear ODE, $p=1$, $r=1$, $\mu = e^x$.
$(e^x v)' = e^x \Rightarrow v = 1 + Ae^{-x}$.
Back-substitute $v = 1/y$: $y = \dfrac{1}{1 + Ae^{-x}}$.
Apply $y(0) = 2$: $A = -1/2$.

**Solution:** $y = \dfrac{2}{2 - e^{-x}}$. (Singular: $y = 0$, not this IC.)

---

#### 11. Bernoulli Example 2 — $n = 3$

**Solve:** $y' + \dfrac{1}{x}y = xy^3$ ($x > 0$, $n = 3$).

Divide by $y^3$: $y^{-3}y' + x^{-1}y^{-2} = x$.
$v = y^{-2}$, $v' = -2y^{-3}y'$: $-\frac{1}{2}v' + x^{-1}v = x \Rightarrow v' - \frac{2}{x}v = -2x$.
$p = -2/x$, $\mu = x^{-2}$.
$(x^{-2}v)' = -2x^{-1} \Rightarrow v = x^2(A - 2\ln x)$.

Back-substitute: **General solution:** $y^2 = \dfrac{1}{x^2(A - 2\ln x)}$.

---

#### 12. The Logistic Equation — A Bernoulli Application

**Model:** Population with carrying capacity $K$:
$$\frac{dP}{dt} = rP\!\left(1 - \frac{P}{K}\right) = rP - \frac{r}{K}P^2, \quad P(0) = P_0.$$

This is **Bernoulli with $n=2$**: $P' - rP = -\dfrac{r}{K}P^2$.

Apply substitution $v = P^{-1}$, solve $v' + rv = r/K$ by IF ($\mu = e^{rt}$), back-substitute:
$$\boxed{P(t) = \frac{K}{1 + \left(\dfrac{K-P_0}{P_0}\right)e^{-rt}}}$$

**Key features:**
- **S-shaped** for $P_0 < K$; $P(t) \to K$ as $t \to \infty$.
- Inflection at $P = K/2$: maximum growth rate.
- $P = K$ stable equilibrium; $P = 0$ unstable.

**Applications:** Population biology, epidemic spread, market saturation.

---

#### 13. Common Traps and Reduction to Standard Form

**Trap 1 — Wrong form; divide first:**
$xy' = y + x^2$ becomes $y' - \frac{1}{x}y = x$ (linear, $p = -1/x$).

**Trap 2 — Reversed roles ($x$ as unknown):**
$(1+y^2)\frac{dx}{dy} = \arctan y - x$. Rewrite: $\frac{dx}{dy} + \frac{x}{1+y^2} = \frac{\arctan y}{1+y^2}$.
Linear ODE in $x(y)$ — apply IF with $y$ as the independent variable.

**Trap 3 — Bernoulli disguised:**
Always check whether $r(x)y^n$ appears *before* applying the IF method. If $y^n$ is present with $n \neq 0, 1$, use the Bernoulli substitution.

**Practical tip:** Check separable → exact → linear → Bernoulli (in that order) before resorting to numerics.

---

#### 14. Summary — Lecture 1

| Concept | Formula / Rule |
|---------|---------------|
| Standard form | $y' + p(x)y = r(x)$ |
| Integrating factor | $\mu(x) = e^{\int p(x)\,dx}$ |
| General solution | $y = \frac{1}{\mu}\!\left(\int\mu r\,dx + C\right) = y_h + y_p$ |
| Homogeneous solution | $y_h = Ce^{-\int p\,dx}$ (transient) |
| Interval of validity | All of $I$ where $p$, $r$ continuous |
| Bernoulli | $y'+py = ry^n$; $v = y^{1-n}$ → linear |
| Logistic | $P'=rP(1-P/K)$; Bernoulli $n=2$; $P \to K$ |

---

## Lecture 2: Existence, Uniqueness, and Autonomous Equations

### Introduction

This lecture addresses the foundational questions: *Does a solution always exist? Is it unique?* The answers, given by the **Picard–Lindelöf Theorem**, are essential for trusting our computed solutions. We then develop the powerful qualitative theory of **autonomous ODEs** $y' = f(y)$ — equations in which the independent variable does not appear explicitly. Using the **phase line** and stability analysis, we can determine the long-term behaviour of solutions without solving the ODE analytically.

---

### Knowledge Points

---

#### 1. Picard–Lindelöf Theorem

**Theorem:** Suppose $f(x,y)$ is continuous on a rectangle $R: |x-x_0|\leq a,\; |y-y_0|\leq b$, and satisfies the **Lipschitz condition** in $y$:
$$|f(x,y_1) - f(x,y_2)| \leq L\,|y_1 - y_2|$$
for some constant $L > 0$ and all $(x,y_1),(x,y_2) \in R$.

Then the IVP $y' = f(x,y)$, $y(x_0) = y_0$ has a **unique solution** $y(x)$ on some interval $|x-x_0| \leq h$.

**Sufficient condition for Lipschitz:** If $\partial f/\partial y$ is continuous and bounded on $R$, then $f$ is Lipschitz with $L = \max_R |\partial f/\partial y|$.

**Physical meaning:** The IVP is **well-posed** — a unique future is determined by the present state (mathematical foundation of classical determinism).

---

#### 2. The Lipschitz Condition — Intuition and Failure

**Geometric meaning:** The Lipschitz condition bounds how fast $f$ can change in the $y$-direction, preventing direction-field segments from becoming infinitely steep — which would allow solution curves to merge or cross.

**Proof of uniqueness via Lipschitz:** If $y_1$ and $y_2$ both solve the IVP, then $u = y_1 - y_2$ satisfies $|u'| = |f(x,y_1)-f(x,y_2)| \leq L|u|$. By Gronwall's inequality: $|u(x)| \leq |u(x_0)|e^{L|x-x_0|} = 0$. Hence $y_1 = y_2$.

**When Lipschitz fails:** $f(x,y) = y^{2/3}$. At $y = 0$: $\partial f/\partial y = \frac{2}{3}y^{-1/3} \to \infty$ — not Lipschitz. The IVP $y' = y^{2/3}$, $y(0) = 0$ has two solutions: $y \equiv 0$ and $y = \left(\frac{x}{3}\right)^3$ for $x \geq 0$. Uniqueness fails!

---

#### 3. Interval of Existence

**Nonlinear ODEs:** Solution may exist only on a finite interval, even with smooth $f$.

**Example (finite-time blow-up):** $y' = y^2$, $y(0) = 1$. Solution: $y = 1/(1-x)$ blows up at $x = 1$. Picard–Lindelöf guarantees a local solution, but cannot predict finite-time blow-up.

**Theorem (Global Existence for Linear ODEs):** If $p(x)$ and $r(x)$ are continuous on $I = (a,b)$ with $x_0 \in I$, the IVP $y' + py = r$, $y(x_0) = y_0$ has a unique solution on **all of $I$** — no blow-up possible for linear equations.

**Physical significance:** Blow-up in finite time corresponds to a physical singularity (e.g., a resistanceless circuit, a population model ignoring all limiting factors).

---

#### 4. Autonomous First-Order ODEs

**Definition:** $y' = f(y)$ — the right-hand side depends on $y$ **only**, not explicitly on $x$ (or $t$).

**Key property:** If $y(x)$ is a solution, so is $y(x+c)$ for any constant $c$ (time-shift symmetry). The direction field has the same slope at every $x$ for fixed $y$.

**Examples:**
- $y' = ky$ — exponential growth/decay; autonomous.
- $P' = rP(1-P/K)$ — logistic; autonomous.
- $y' = y^2 - 1$ — depends only on $y$; autonomous.
- $y' = xy$ — $x$ appears; **not** autonomous.

**Direction field consequence:** All slope marks at height $y = y_0$ have the same slope $f(y_0)$ — the field repeats in vertical strips.

---

#### 5. Equilibrium Points

**Definition:** $y(x) = y^*$ is an **equilibrium** of $y' = f(y)$ if and only if $f(y^*) = 0$. It is a constant solution — a horizontal line in the $xy$-plane.

**Finding equilibria:** Solve $f(y) = 0$ for $y$.

**Example:** $y' = y^2 - 1 = (y-1)(y+1)$. Equilibria: $y^* = 1$ and $y^* = -1$.

**Geometric meaning:**
- Equilibria separate the real line into intervals of positive or negative $f$.
- Non-equilibrium solutions can never cross an equilibrium (uniqueness theorem).

---

#### 6. The Phase Line

**Definition:** The **phase line** of $y' = f(y)$ is a one-dimensional diagram of the state space (the $y$-axis), encoding:
- **Equilibria:** points $y^*$ where $f(y^*) = 0$ (zero velocity; constant solution).
- **Flow arrows:** $\uparrow$ on intervals where $f(y) > 0$; $\downarrow$ where $f(y) < 0$.

**Construction:** (1) Solve $f(y^*) = 0$. (2) Test sign of $f$ on each sub-interval. (3) Draw arrows.

**Reading:** Follow arrows from $y_0$ to find $\lim_{x\to\infty}y(x)$.

**Example:** $y' = y^2 - 1$.
- $y < -1$: $f > 0$ ↑ (toward $-1$).
- $-1 < y < 1$: $f < 0$ ↓ (toward $-1$).
- $y > 1$: $f > 0$ ↑ (away from $1$).
- $y^* = -1$: arrows converge → **stable**.
- $y^* = 1$: arrows diverge → **unstable**.

---

#### 7. Stability Classification

**Definitions:**
- **Asymptotically stable (sink):** arrows on both sides point *toward* $y^*$; every nearby solution → $y^*$ as $x \to +\infty$.
- **Unstable (source):** arrows on both sides point *away* from $y^*$; nearby solutions diverge.
- **Semi-stable:** arrows toward from one side, away from the other.

**Example (semi-stable):** $y' = -y^2$. $y^* = 0$: $f(y) = -y^2 < 0$ for all $y \neq 0$.
$y > 0$: $\downarrow$ (toward 0). $y < 0$: $\downarrow$ (away from 0).
$y = 0$ is **semi-stable**: solutions from above converge; solutions from below diverge to $-\infty$.

---

#### 8. Stability via the Derivative Criterion

**Theorem (Derivative Criterion):** Let $y^*$ be an equilibrium of $y' = f(y)$, $f$ differentiable at $y^*$.
- $f'(y^*) < 0$ → $y^*$ is **asymptotically stable**.
- $f'(y^*) > 0$ → $y^*$ is **unstable**.
- $f'(y^*) = 0$ → **inconclusive** (use phase line).

**Derivation (linearisation):** Write $y = y^* + u$ (small perturbation): $u' = f(y^*+u) \approx f'(y^*)u$. Solution: $u(x) = u_0 e^{f'(y^*)x}$. Sign of $f'(y^*)$ determines decay or growth.

**Example:** $y' = y^2-1$, $f'(y) = 2y$.
- $y^*=-1$: $f'(-1) = -2 < 0$ → **stable**.
- $y^*=1$: $f'(1) = 2 > 0$ → **unstable**.

---

#### 9. Logistic Equation — Phase Line Analysis

Logistic equation: $P' = rP(1-P/K)$, $r, K > 0$.

**Equilibria:** $f(P) = rP(1-P/K) = 0 \Rightarrow P^* = 0$ and $P^* = K$.

**Derivative criterion:** $f'(P) = r(1-2P/K)$.
- $f'(0) = r > 0$ → $P^* = 0$ **unstable**.
- $f'(K) = -r < 0$ → $P^* = K$ **asymptotically stable**.

**Phase line:**
- $0 < P < K$: $f > 0$ ↑ (growing toward $K$).
- $P > K$: $f < 0$ ↓ (decreasing toward $K$).

**Conclusion:** For any $P_0 > 0$: $P(t) \to K$ as $t \to \infty$. The phase line gives the result *instantly, without solving the ODE*.

**Inflection** at $P = K/2$: where $f'(P) = 0$, i.e., where growth rate is fastest.

---

#### 10. Logistic with Constant Harvesting

**Model:** Start from $P' = rP(1-P/K)$. Remove individuals at constant rate $H > 0$:
$$P' = rP\!\left(1-\frac{P}{K}\right) - H.$$

With $r=1$, $K=4$: $f(P) = P - P^2/4 - H$. Equilibria: $P^2/4 - P + H = 0 \Rightarrow P^* = 2 \pm 2\sqrt{1-H}$.

**Three regimes:**
- $H < 1$ (below MSY $= rK/4 = 1$): two equilibria $P_-^* < P_+^*$. $P_+^*$ stable, $P_-^*$ unstable. Any $P_0 > P_-^*$ stabilises at $P_+^*$; any $P_0 < P_-^*$ → extinction.
- $H = 1$ (at MSY): single semi-stable equilibrium $P^* = 2$; extinction risk for $P_0 < 2$.
- $H > 1$ (above MSY): no real equilibria; $f(P) < 0$ for all $P$ → **population collapses**.

At $H=1$: the two equilibria collide and annihilate — the system transitions from sustainable to collapse.

---

#### 11. Basins of Attraction

**Definition:** The **basin of attraction** of a stable equilibrium $y^*$ is the set of initial conditions $y_0$ for which $\lim_{x\to\infty}y(x) = y^*$. In 1D: the basin is the open interval between the two nearest unstable equilibria.

**Logistic with harvesting** ($H = 3/4$, $r=1$, $K=4$): $P_\pm^* = 2 \pm 2\sqrt{1-3/4} = 2 \pm 1$, so $P_-^* = 1$, $P_+^* = 3$.
- Basin of $P_+^* = (1, +\infty)$.
- Basin of extinction $= (-\infty, 1)$.

**Engineering significance:**
- The basin of attraction defines the **safe operating region**.
- $P_-^*$ is the **tipping point** — cross it and the system collapses.
- Designing large basins around desired equilibria is a core goal of control engineering.

---

#### 12. Graphical Analysis Toolkit

For $y' = f(y)$, graph $f$ as a function of $y$ to read off everything:

| Feature of $f(y)$ graph | Information about $y(x)$ |
|-------------------------|--------------------------|
| Zeros of $f$ | Equilibria |
| Sign of $f$ | Direction of flow ($+$ = increase, $-$ = decrease) |
| Maxima/minima of $f$ | Fastest increase/decrease of $y$ |
| Sign of $f'$ at equilibrium | Stability ($f'<0$: stable, $f'>0$: unstable) |
| $f'(y)=0$ (with $f \neq 0$) | Inflection of solution curve |

**Second derivative:** Since $y'' = \frac{d}{dx}[f(y)] = f'(y)\cdot y' = f'(y)f(y)$:
- $f'(y)f(y) > 0$: solution curve is **concave up**.
- $f'(y)f(y) < 0$: solution curve is **concave down**.
- Logistic inflection at $P = K/2$: $f'(K/2) = 0$ with $f(K/2) \neq 0$.

---

#### 13. Autonomous ODEs — Unified View

| Equation | Equilibria | Stability |
|----------|-----------|-----------|
| $y' = ky$ | $y^*=0$ | Stable if $k<0$; unstable if $k>0$ |
| $P' = rP(1-P/K)$ | $0$, $K$ | $0$ unstable; $K$ stable |
| $T' = -k(T-T_e)$ | $T^*=T_e$ | Stable ($k>0$) |
| $v' = g-(b/m)v$ | $v^*=mg/b$ | Globally stable |
| $P' = rP(1-P/K)-H$ | 0, 1, or 2 | Varies |

---

#### 14. Summary — Lecture 2

| Concept | Key Statement |
|---------|--------------|
| Picard–Lindelöf | Continuous $f$, Lipschitz in $y$ → unique local solution |
| Lipschitz condition | $|f(x,y_1)-f(x,y_2)| \leq L|y_1-y_2|$ |
| Linear ODE uniqueness | Solution on **all** of continuity interval of $p$, $r$ |
| General solution | $y = y_h + y_p = Ce^{-\int p\,dx} + y_p$ |
| Autonomous ODE | $y'=f(y)$: independent variable absent |
| Phase line | Signs of $f(y)$ → flow arrows |
| Derivative criterion | $f'(y^*)<0$: stable; $f'(y^*)>0$: unstable |
| Basin of attraction | Initial conditions → $y^*$ as $x\to\infty$ |

**Supplementary — Picard Iteration (not required for exams):**
The Picard–Lindelöf proof is constructive: it builds the solution as the limit of successive approximations. Starting from $\phi_0(x) = y_0$:
$$\phi_{n+1}(x) = y_0 + \int_{x_0}^{x} f\!\bigl(t,\phi_n(t)\bigr)\,dt.$$
**Example:** $y' = y$, $y(0)=1$: $\phi_0=1$, $\phi_1=1+x$, $\phi_2=1+x+x^2/2$, $\phi_3=1+x+x^2/2+x^3/6$, $\ldots$ — partial sums of $e^x$. ✓

---

## Lecture 3: Modeling — RL and RC Circuits, Falling Body

### Introduction

This lecture applies the linear ODE techniques of Week 5 to three fundamental engineering models: the **RL circuit**, the **RC circuit**, and the **falling body** (with linear and quadratic drag). Together these illustrate how the same mathematical structure — a first-order linear ODE with a single stable equilibrium — governs vastly different physical systems.

---

### Knowledge Points

---

#### 1. RL Circuit — Physical Model and ODE

**Kirchhoff's Voltage Law:** $V_R + V_L = E(t)$, i.e., $Ri + L\dfrac{di}{dt} = E(t)$.

**Standard form** (divide by $L$):
$$\frac{di}{dt} + \frac{R}{L}\,i = \frac{E(t)}{L}.$$

Linear first-order ODE with $p = R/L$ and $r(t) = E(t)/L$.

**Circuit elements:**
- Resistor $R$ ($\Omega$): voltage drop $V_R = Ri$.
- Inductor $L$ (H): voltage drop $V_L = L\,di/dt$.
- EMF source $E(t)$ (V): driving voltage.

**Key parameter:** Time constant $\tau = L/R$ (seconds). Larger $L$ → slower response; larger $R$ → faster decay.

---

#### 2. RL Circuit — Solution

Integrating factor: $\mu = e^{(R/L)t}$.

**Constant EMF** $E(t) = E_0$, $i(0) = i_0$:
$$\boxed{i(t) = \frac{E_0}{R} + \!\left(i_0 - \frac{E_0}{R}\right)e^{-t/\tau}}, \qquad \tau = \frac{L}{R}.$$

**Switch-on** ($i_0 = 0$): $i(t) = \dfrac{E_0}{R}\!\left(1 - e^{-t/\tau}\right)$.

**Switch-off** ($E_0 = 0$): $i(t) = i_0\,e^{-t/\tau}$ (stored energy discharges).

**Decomposition:** $i(t) = i_p + i_h$:
- **Steady-state:** $i_p = E_0/R$ — Ohm's Law; inductor acts as short circuit at DC.
- **Transient:** $i_h = (i_0 - E_0/R)e^{-t/\tau}$ — exponential decay.

**Rule of thumb:** At $t = \tau$, transient decays to $e^{-1} \approx 37\%$. At $t = 5\tau$, transient $< 1\%$ — circuit essentially at steady state.

**Worked example:** $R=100\,\Omega$, $L=0.5\,\rm H$, $E_0=50\,\rm V$, $i(0)=0$.
$\tau = L/R = 5\,\rm ms$. $i_\infty = E_0/R = 0.5\,\rm A$.
$i(t) = 0.5(1 - e^{-200t})$ A. At $t = 5\tau = 25\,\rm ms$: $i \approx 0.497\,\rm A$ (99.3% of steady state).

**Phase line view:** Equilibrium $i^* = E_0/R$; $f'(i) = -R/L < 0$ → globally stable.

---

#### 3. RC Circuit — Physical Model

**Circuit elements:**
- Resistor $R$ ($\Omega$): voltage drop $V_R = Ri$.
- Capacitor $C_0$ (F): voltage drop $V_C = Q/C_0$, where $Q(t)$ (C) is the charge stored on the capacitor.
- Since current $i = dQ/dt$, substituting eliminates $i$ and gives an ODE in $Q$.
- Voltage source $V(t)$ (V): driving voltage.

**Kirchhoff's Voltage Law:** $V_R + V_C = V(t)$, i.e., $Ri + \dfrac{Q}{C_0} = V(t)$. Substitute $i = dQ/dt$:
$$Q' + \frac{1}{RC_0}\,Q = \frac{V(t)}{R}.$$

Linear first-order ODE with $p = 1/(RC_0)$ and $\mu = e^{t/(RC_0)}$.

**Key parameter:** Time constant $\tau = RC_0$ (seconds). Larger $C_0$ → slower charging; larger $R$ → slower charging.

---

#### 3b. RC Circuit — Solution

**Constant voltage $V$, $Q(0) = Q_0$:**
$$Q(t) = C_0 V + (Q_0 - C_0 V)\,e^{-t/\tau}, \qquad \tau = RC_0.$$

**Switch-on** ($Q_0 = 0$): $Q(t) = C_0 V\!\left(1 - e^{-t/\tau}\right).$

**Switch-off** ($V = 0$): $Q(t) = Q_0\,e^{-t/\tau}$ (capacitor discharges).

**Decomposition** $Q = Q_p + Q_h$:
- **Steady state:** $Q_p = C_0 V$ (capacitor fully charged to $V$).
- **Transient:** $Q_h = (Q_0 - C_0 V)e^{-t/\tau}$ — exponential decay.
- At $t = \tau$: transient at $e^{-1} \approx 37\%$; at $t = 5\tau$: $< 1\%$.

**Phase line view:** Equilibrium $Q^* = C_0 V$; $f'(Q) = -1/(RC_0) < 0$ → globally stable.

---

#### 4. RC vs. RL — Structural Comparison

| Feature | RL Circuit | RC Circuit |
|---------|-----------|-----------|
| State variable | Current $i(t)$ | Charge $Q(t)$ |
| Energy storage | Inductor ($\frac{1}{2}Li^2$) | Capacitor ($\frac{1}{2}Q^2/C_0$) |
| ODE | $i' + \frac{R}{L}i = \frac{E_0}{L}$ | $Q' + \frac{1}{RC_0}Q = \frac{V}{R}$ |
| Steady state | $i^* = E_0/R$ (Ohm's Law) | $Q^* = C_0 V$ (capacitor charged) |
| Time constant | $\tau = L/R$ | $\tau = RC_0$ |
| Switch-on | $i = i^*(1-e^{-t/\tau})$ | $Q = C_0V(1-e^{-t/\tau})$ |

**Same mathematical structure:** Both solve $y' + \frac{1}{\tau}y = \frac{y^*}{\tau}$ with different physical interpretations.

---

#### 5. Falling Body — Linear Drag

**Newton's Second Law:** $m\,dv/dt = mg - F_{\rm drag}(v)$ (downward positive).

**Linear drag** $F_{\rm drag} = bv$ (Stokes/viscous drag, valid at low speed):
$$v' + \frac{b}{m}\,v = g.$$

Linear first-order ODE with $p = b/m$, $r = g$.

**Solution with $v(0) = 0$:** $\mu = e^{(b/m)t}$, giving:
$$\boxed{v(t) = \frac{mg}{b}\!\left(1 - e^{-(b/m)t}\right) = v_T\!\left(1 - e^{-t/\tau}\right)}, \quad v_T = \frac{mg}{b},\quad \tau = \frac{m}{b}.$$

Short-time check ($t \ll \tau$): $v(t) \approx gt$, so $x(t) \approx \frac{1}{2}gt^2$ — free fall. ✓

---

#### 6. Terminal Velocity — Equilibrium Analysis

**Autonomous form:** $v' = g - (b/m)v = f(v)$.

**Terminal Velocity Theorem:** Equilibrium: $f(v^*) = 0 \Rightarrow v^* = mg/b =: v_T$.
Stability: $f'(v) = -b/m < 0$ for all $v$ → $v_T$ is **globally asymptotically stable**.
Every initial velocity (even $v_0 > v_T$) converges to $v_T$.

**Phase line:** Single equilibrium $v_T$; arrows up for $v < v_T$ (accelerating), down for $v > v_T$ (decelerating).

**Typical values:**

| Object | $v_T$ |
|--------|-------|
| Skydiver (spread-eagle) | $\approx 55\,\rm m/s$ |
| Skydiver (head-down) | $\approx 90\,\rm m/s$ |
| Baseball | $\approx 42\,\rm m/s$ |
| Raindrop (1 mm) | $\approx 4\,\rm m/s$ |

---

#### 7. Quadratic Drag Model

**High-speed regime:** $F_{\rm drag} = cv^2$ (Newton/pressure drag, valid for large objects):
$$v' = g - \frac{c}{m}v^2 = g\!\left(1 - \frac{v^2}{v_T^2}\right), \qquad v_T = \sqrt{\frac{mg}{c}}.$$

This is **separable**: $\int\frac{dv}{1-v^2/v_T^2} = g\,dt$. Using partial fractions:
$$v(t) = v_T\tanh\!\left(\frac{g}{v_T}\,t\right).$$

**Note:** $\tanh$ (Week 1!) appears naturally. As $t\to\infty$: $\tanh\to 1$, so $v\to v_T$.

**When to use which drag:**
- **Linear** ($bv$): slow flow, small objects (raindrops, bacteria). Exact linear ODE.
- **Quadratic** ($cv^2$): fast flow, larger objects (skydivers, cars). Separable ODE.

---

#### 8. Worked Example — Parachutist Problem

**Two-phase fall:** $m = 80\,\rm kg$, linear drag.

**Phase 1** (before parachute, $b = 15.6\,\rm kg/s$):
$v_T = mg/b \approx 50.3\,\rm m/s$, $\tau = m/b \approx 5.13\,\rm s$.
$v_1(t) = 50.3(1-e^{-t/5.13})$.
At $t_p = 10\,\rm s$: $v_1(10) \approx 43.1\,\rm m/s$.

**Phase 2** (parachute open, $b_p = 160\,\rm kg/s$):
$v_{T,p} = mg/b_p = 4.9\,\rm m/s$, $\tau_p = 0.5\,\rm s$.
$v_2(t) = 4.9 + 38.2\,e^{-2(t-t_p)}$.
After $5\tau_p = 2.5\,\rm s$: $v \approx 4.9\,\rm m/s$ — safe landing speed.

**Key lesson:** The *same* ODE method (linear IF) applies to both phases, with different parameters. Initial condition of Phase 2 is the final state of Phase 1.

---

#### 9. Drag Model Comparison

| Feature | Linear drag $F=bv$ | Quadratic drag $F=cv^2$ |
|---------|-------------------|------------------------|
| ODE type | Linear (IF method) | Separable |
| Solution | $v_T(1-e^{-t/\tau})$ | $v_T\tanh(gt/v_T)$ |
| Terminal velocity | $v_T = mg/b$ | $v_T = \sqrt{mg/c}$ |
| Approach shape | Exponential | Hyperbolic tangent |
| Valid regime | Low Re (small/slow) | High Re (large/fast) |
| Week 1 connection | — | $\tanh$ from hyperbolic functions |

---

#### 10. RL Circuit vs. Falling Body — Structural Analogy

| System | ODE | Equilibrium | Time constant |
|--------|-----|------------|--------------|
| RL circuit (const. $E_0$) | $i' + \frac{R}{L}i = \frac{E_0}{L}$ | $i^* = E_0/R$ | $\tau = L/R$ |
| Falling body (linear drag) | $v' + \frac{b}{m}v = g$ | $v^* = mg/b$ | $\tau = m/b$ |

**Mathematical correspondence:** $i \leftrightarrow v$, $R/L \leftrightarrow b/m$, $E_0/L \leftrightarrow g$, $E_0/R \leftrightarrow mg/b$.

**Mechanical–Electrical Analogy:** The same first-order linear ODE $y' + \frac{1}{\tau}y = \frac{y^*}{\tau}$ governs both systems. This structural analogy extends to RLC circuits and mass-spring systems (Week 10).

---

#### 11. Review — First-Order ODE Models (Linear, Weeks 4–5)

| Model | ODE (standard form) | Method | Equilibrium / Solution |
|-------|---------------------|--------|----------------------|
| Exponential | $y' = ky$ | Separable | $y^*=0$; $y=Ce^{kt}$ |
| Newton's cooling | $T' + kT = kT_e$ | Linear (IF) | $T^*=T_e$ (globally stable) |
| RC circuit | $Q' + \frac{1}{RC}Q = \frac{V}{R}$ | Linear (IF) | $Q^*=CV$; $\tau=RC$ |
| RL circuit | $i' + \frac{R}{L}i = \frac{E_0}{L}$ | Linear (IF) | $i^*=E_0/R$; $\tau=L/R$ |
| Mixing (tank) | $Q' + \frac{r}{V}Q = r c_{\rm in}$ | Linear (IF) | $Q^*=c_{\rm in}V$ (stable) |
| Falling (linear) | $v' + \frac{b}{m}v = g$ | Linear (IF) | $v^*=mg/b$; $\tau=m/b$ |

**Unifying structure:** $y' + \frac{1}{\tau}y = \frac{y^*}{\tau}$ $\Rightarrow$ $y(t) = y^* + (y_0-y^*)e^{-t/\tau}$. One stable equilibrium $y^*$; time constant $\tau$ sets the speed of approach.

---

#### 12. Review — First-Order ODE Models (Nonlinear & Autonomous, Week 5)

| Model | ODE | Method | Equilibria / Long-term |
|-------|-----|--------|----------------------|
| Logistic growth | $P' = rP\!\left(1-\frac{P}{K}\right)$ | Bernoulli | $P^*=0$ (unstable); $P^*=K$ (stable); $P\to K$ |
| Logistic + harvest | $P' = rP\!\left(1-\frac{P}{K}\right)-H$ | Autonomous | $P_\pm^*=2\pm2\sqrt{1-H}$; bifurcation at $H=1$ |
| Falling (quadratic) | $v' = g - \frac{c}{m}v^2$ | Separable | $v^*=\sqrt{mg/c}$; $v=v^*\tanh\!\left(\frac{g}{v^*}t\right)$ |

**Key contrasts with linear models:**
- Multiple equilibria possible; stability depends on phase line analysis.
- Parameters (e.g. $H$) can cause qualitative changes — **bifurcations**.
- Solutions may not exist for all time.

---

#### 13. Complete First-Order ODE Method Selection Guide

| ODE form | Method |
|----------|--------|
| $y' = g(x)h(y)$ | **Separable** (Week 4) |
| $M_y = N_x$ | **Exact** (Week 4) |
| $y' + p(x)y = r(x)$ | **Linear — integrating factor** (Week 5) |
| $y' + p(x)y = r(x)y^n$ | **Bernoulli** → linear (Week 5) |
| $y' = f(y)$ (no $x$) | **Autonomous — phase line** (Week 5) |
| None of the above | **Numerical** (Euler / RK4) |

---

#### 14. Summary — Lecture 3

| System / Concept | Key Formula |
|-----------------|------------|
| RL circuit ODE | $i' + (R/L)i = E_0/L$ |
| RL solution (switch-on) | $i = (E_0/R)(1 - e^{-t/\tau})$, $\tau = L/R$ |
| Falling body (linear drag) | $v' + (b/m)v = g$ |
| Terminal velocity | $v_T = mg/b$; globally stable equilibrium |
| Velocity solution | $v = v_T(1 - e^{-t/\tau})$, $\tau = m/b$ |
| Falling body (quad. drag) | $v = v_T\tanh(gt/v_T)$, $v_T = \sqrt{mg/c}$ |
| $5\tau$ rule | System at $>99\%$ steady state after $5\tau$ |
| Structural analogy | RL $\leftrightarrow$ falling body: same ODE form |

---

## Practice Problems

1. Solve the linear IVP $y' + 2xy = 4x$, $y(0) = 3$.

2. Solve $y' - y = e^{2x}$ and write the solution as $y_h + y_p$. Here $y_h$ is called the homogeneous solution, which is the solution to the homogeneous equation $y' - y = 0$, and $y_p$ is called the particular solution, which is the solution to the non-homogeneous equation $y' - y = e^{2x}$.

3. Solve the Bernoulli equation $y' + y = y^3$.

4. Solve $xy' + y = y^2\ln x$ ($x > 0$). *(Hint: Bernoulli with $n = 2$.)*

5. For $y' = (y-1)(y-3)$: (a) find all equilibria; (b) classify each as stable/unstable using the derivative criterion; (c) sketch the phase line and phase portrait; (d) determine $\lim_{x\to\infty}y(x)$ for $y(0) = 2$.

6. For the autonomous ODE $y' = y^2 - 4$: (a) find the basins of attraction of all stable equilibria; (b) solve explicitly and verify your phase-line prediction.

7. An RL circuit has $R = 4\,\Omega$, $L = 2\,\text{H}$, and $E = 12\,\text{V}$ (constant). The switch closes at $t = 0$ with $i(0) = 0$. Find $i(t)$ and the time constant $\tau$. When does $i$ reach $95\%$ of its steady-state value?

8. An RC circuit has $R = 10^4\,\Omega$, $C = 10^{-4}\,\text{F}$, and $E = 100\,\text{V}$. Find the charge $q(t)$ if $q(0) = 0$, and compute the steady-state charge.

9. A 70 kg skydiver falls from rest. With linear drag $b = 14\,\text{kg/s}$ and $g = 9.8\,\text{m/s}^2$: (a) find $v(t)$; (b) find the terminal velocity; (c) find the time to reach $90\%$ of terminal velocity.

10. Verify the existence and uniqueness of $y' = \sqrt{|y|}$, $y(0) = 0$. Does $y \equiv 0$ satisfy the IVP? Is the solution unique? Explain why Picard–Lindelöf does not guarantee uniqueness here.
