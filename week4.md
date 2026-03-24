# Week 4 — Motivation, Basic Concepts, Separable Equations & Exact Equations

**Course:** Engineering Mathematics 1
**Part:** II — First-Order Ordinary Differential Equations
**Kreyszig Sections:** §1.1–1.4, §1.7

**Bridging lecture:** Lecture 1 explicitly connects Part I (calculus) to Part II (ODEs), answering "Why do engineers need differential equations?" before introducing any formalism.

---

## Lecture 1: What Is an ODE? Motivation, Concepts, and Direction Fields

### Introduction

So far in this course, calculus has been a tool for analysing *known* functions. In engineering, the situation is almost always reversed: the function is **unknown**, and what we know is a **relationship between the function and its derivatives**. Such a relationship is an **ordinary differential equation (ODE)**.

---

### Knowledge Points

---

#### 1. What Is a Model?

**Definition:** A **model** is a mathematical representation of a real-world system that captures its *essential* behaviour — **not** an exact copy of reality. An exact copy would be too complex to analyse.

**Modeling** is the full process:
$$\text{Formulate} \;\to\; \text{Solve} \;\to\; \text{Interpret} \;\to\; \text{Validate / Refine}$$

**Why not an exact copy?**
- A perfect description of nature requires tracking every molecule — impossible in practice.
- A good model keeps only the variables that *govern* the behaviour of interest.
- Example: $\frac{dN}{dt} = -\lambda N$ captures radioactive decay with one parameter $\lambda$, ignoring quantum-level details irrelevant to bulk decay.

**Running example:** A mixing tank — salt $Q(t)$ in a tank fed by brine, drained at the same rate. The ODE model is $\frac{dQ}{dt} = r_{\rm in} - \frac{rQ}{V}$, solution $Q(t) = Q_\infty + Ce^{-t/\tau}$.

---

#### 2. From Calculus to Differential Equations

**The key shift:** In calculus, we differentiate a *known* function to find its rate of change. In ODEs, we are *given* the rate of change and must recover the function.

**Simplest example:** $y'(x) = 2x$ — integrating gives $y = x^2 + C$.

**More fundamental:** $y'(x) = ky(x)$ — the rate of change is proportional to the current value. Solution: $y = Ce^{kx}$.

**Physical realisations of $y' = ky$:**
- Exponential population growth ($k > 0$)
- Radioactive decay ($k < 0$)
- Continuous compound interest ($k = r$)
- Charging/discharging of a capacitor

All are the same ODE with solution $y = Ce^{kx}$ — different contexts, unified mathematics.

---

#### 3. Definition of an ODE and Its Order

**Definition:** An **ordinary differential equation (ODE)** of **order $n$** is an equation involving an unknown function $y(x)$ and its derivatives up to order $n$:
$$F\bigl(x,\, y,\, y',\, y'',\, \ldots,\, y^{(n)}\bigr) = 0.$$

"Ordinary" distinguishes these from *partial* differential equations (PDEs), which involve partial derivatives with respect to multiple variables.

**Examples by order:**

| Order | Example ODE | Physical context |
|-------|-------------|-----------------|
| 1st | $y' = ky$ | Exponential growth/decay |
| 1st | $y' + p(x)y = r(x)$ | General linear 1st-order |
| 2nd | $y'' + 4y = 0$ | Undamped oscillator |
| 2nd | $my'' + cy' + ky = F(t)$ | Damped forced oscillator |
| 3rd | $y''' - y' + xy = \sin x$ | Beam deflection |

---

#### 4. Linearity

**Definition:** An ODE is **linear** if it can be written as:
$$a_n(x)y^{(n)} + a_{n-1}(x)y^{(n-1)} + \cdots + a_1(x)y' + a_0(x)y = r(x).$$

$y$ and all its derivatives appear to the **first power** only, with coefficients depending only on $x$. If $r(x) = 0$: **homogeneous**. Otherwise: **non-homogeneous**.

**Nonlinear examples:**
- $y' = y^2$ — $y$ squared.
- $yy' = 1$ — product of $y$ and $y'$.
- $y'' + \sin y = 0$ — pendulum; $\sin y$ is nonlinear.
- $(y')^3 + y = x$ — $y'$ cubed.

**Why linearity matters:** Linear ODEs obey the superposition principle and have a complete, systematic solution theory. Nonlinear ODEs often require numerical methods.

---

#### 5. Solutions and Verification

**Definition:** $y = \phi(x)$ is a **solution** of the ODE on an interval $I$ if $\phi$ is $n$ times differentiable on $I$ and substituting $\phi$ into the ODE gives a true identity for all $x \in I$.

- **General solution:** Contains $n$ arbitrary constants — a family of curves.
- **Particular solution:** One member of the family (constants fixed by conditions).
- **Singular solutions:** Solutions not obtainable from the general solution (arise in nonlinear ODEs).

**Verification procedure:**
1. Differentiate $\phi$ as needed.
2. Substitute $\phi$ and its derivatives into the ODE.
3. Confirm the equation reduces to an identity.

**Example 1:** Verify $y = Ce^{2x}$ solves $y' = 2y$: $y' = 2Ce^{2x} = 2y$. ✓

**Example 2:** Verify $y = x^2 + 3x$ solves $y'' = 2$: $y' = 2x+3$, $y'' = 2$. ✓

---

#### 6. Initial Value Problems and Boundary Value Problems

**Definition (IVP):** An ODE together with **initial conditions** at a single point $x_0$:
$$y' = f(x,y), \quad y(x_0) = y_0 \quad (\text{or higher order: also } y'(x_0)=y_1, \ldots)$$

Physical meaning: ODE = law of evolution; initial condition = state at the starting instant.

**Example:** $y' = -2y$, $y(0) = 5$. General solution: $y = Ce^{-2x}$. Apply IC: $C = 5$. Particular solution: $y = 5e^{-2x}$.

**Boundary Value Problem (BVP):** Conditions at *two different* points. Example: $y'' + y = 0$, $y(0)=0$, $y(\pi/2)=1$. BVPs arise in beam deflection and temperature distribution in rods; they require different solution methods from IVPs.

---

#### 7. Existence and Uniqueness — Picard–Lindelöf Theorem

**Question:** Does an IVP always have a solution? Is it unique?

**Theorem (Picard–Lindelöf, conceptual statement):** If $f(x,y)$ is **continuous** and $\partial f/\partial y$ is **continuous** in a rectangle around $(x_0,y_0)$, then the IVP
$$y' = f(x,y), \quad y(x_0) = y_0$$
has a **unique solution** in some open interval containing $x_0$.

**Physical significance:** The theorem guarantees that a physical problem is *well-posed* — a unique future is determined by the present state. This is the mathematical foundation of determinism in classical mechanics.

**When uniqueness fails:**
- $y' = y^{2/3}$, $y(0) = 0$: $\partial f/\partial y = \frac{2}{3}y^{-1/3}$ is **not continuous** at $y=0$ — theorem fails. Two solutions exist: $y \equiv 0$ and $y = \left(\frac{x}{3}\right)^3$.
- Finite-time blow-up: $y' = y^2$, $y(0) = 1$ → $y = 1/(1-x)$ exists only on $(-\infty, 1)$, despite smooth initial data. **Lesson:** the theorem guarantees a solution *near* $x_0$, not necessarily on the whole real line.

---

#### 8. Direction Fields

**Definition:** The ODE $y' = f(x,y)$ assigns a **slope** $f(x,y)$ to each point $(x,y)$. Drawing a short line segment of that slope at each grid point gives the **direction field** (slope field).

**Key property:** Every solution curve is *tangent* to the field at every point — it *flows along* the field.

**Construction:**
1. Choose a grid of points $(x_i, y_j)$.
2. Compute $m = f(x_i, y_j)$ at each.
3. Draw a short segment of slope $m$ at that point.

**Example — $y' = y$:**
- $y = 0$: slopes are all zero → horizontal equilibrium line.
- $y > 0$: positive slopes; curves rise steeply for large $y$.
- $y < 0$: negative slopes; curves fall steeply for large $|y|$.
Solutions $y = Ce^x$ are consistent with this picture.

**MATLAB code for direction fields** (example: $y' = 1 - y$):
```matlab
[x, y] = meshgrid(-2:0.3:4, -1:0.3:3);
dydx = 1 - y;              % f(x,y)
L    = sqrt(1 + dydx.^2);  % normalise

figure
quiver(x, y, 1./L, dydx./L, 0.5, 'Color', [0.2 0.4 0.8])
xlabel('x'),  ylabel('y')
title("Direction field:  y' = 1 - y")
hold on

% overlay particular solutions
xp = linspace(-2, 4, 200);
plot(xp, 1 + 2*exp(-xp), 'r', 'LineWidth', 2)
plot(xp, 1 - 0.5*exp(-xp), 'g', 'LineWidth', 2)
yline(1, 'k--', 'LineWidth', 1.5)
```

**What to observe:**
- Equilibrium $y=1$: horizontal arrows along dashed line.
- Red ($y_0 > 1$): decreases toward $y=1$.
- Green ($y_0 < 1$): increases toward $y=1$.

**Equilibrium solutions:** If $f(x,y_0) = 0$ for all $x$, then $y = y_0$ is a **constant solution** — a horizontal line where all slopes are zero.

**Stability from the direction field:**
- If nearby solutions above $y_0$ slope downward and below $y_0$ slope upward → **stable equilibrium**.
- If nearby solutions diverge away from $y_0$ → **unstable equilibrium**.

---

#### 9. Three Fundamental Engineering Models

All three are first-order ODEs sharing the same structure: *exponential approach to equilibrium with time constant $\tau$*.

**Model 1 — Radioactive decay:**
$$\frac{dN}{dt} = -\lambda N,\quad N(0)=N_0 \;\Rightarrow\; N(t) = N_0 e^{-\lambda t},\quad t_{1/2} = \frac{\ln 2}{\lambda}.$$

**Model 2 — RL circuit** (Kirchhoff: $LI' + RI = V$, constant $V$, $I_0=0$):
$$I(t) = \frac{V}{R}\!\left(1 - e^{-Rt/L}\right), \qquad \tau = \frac{L}{R}.$$

**Model 3 — Newton's law of cooling:**
$$\frac{dT}{dt} = -k(T - T_{\rm env}) \;\Rightarrow\; T(t) = T_{\rm env} + (T_0 - T_{\rm env})\,e^{-kt}, \quad \tau = \frac{1}{k}.$$

Weeks 4–5 will solve all three systematically using linear ODE methods.

---

#### 10. Summary — Lecture 1

| Concept | Key Formula / Rule |
|---------|--------------------|
| ODE order | Highest derivative present |
| Linear ODE | Coefficients $a_k(x)$ on $y,y',\ldots$; $y$ to first power |
| General solution | Contains $n$ arbitrary constants (order $n$) |
| IVP | ODE $+$ $n$ conditions at a single point $x_0$ |
| BVP | ODE $+$ conditions at two different points |
| Picard–Lindelöf | Continuous $f$ and $\partial f/\partial y$ → unique local solution |
| Direction field | Slope $f(x,y)$ at grid points; solutions flow along it |
| Equilibrium | $y_0$ with $f(x,y_0)=0$; stable if nearby solutions converge |

---

## Lecture 2: Separable ODEs and Euler's Method

### Introduction

The first ODE solution technique is **separation of variables**: if the ODE factors into a product $g(x)h(y)$, then all $y$-terms and all $x$-terms can be moved to opposite sides and integrated independently. Despite its simplicity, separable ODEs cover an enormous class of models.

After separation, we introduce **Euler's Method** — the simplest numerical algorithm for ODEs and the conceptual foundation of all numerical ODE solvers.

---

### Knowledge Points

---

#### 1. Separable ODEs — Definition and Identification

**Definition:** A first-order ODE is **separable** if it can be written as:
$$\frac{dy}{dx} = g(x)\,h(y).$$

**Identification:** Try to factor $f(x,y)$ into $g(x)\cdot h(y)$.

**Separable examples:**
- $y' = 3x^2 y$: $g = 3x^2$, $h = y$.
- $y' = (1+y^2)\cos x$: $g = \cos x$, $h = 1+y^2$.
- $y' = e^{x+y} = e^x e^y$: $g = e^x$, $h = e^y$.

**Non-separable example:** $y' = x + y$ — cannot be factored as $g(x)h(y)$.

---

#### 2. The Method of Separation of Variables

**Procedure:**
1. Write $dy/dx = g(x)h(y)$.
2. Separate: $\dfrac{dy}{h(y)} = g(x)\,dx$.
3. Integrate both sides: $\displaystyle\int\frac{dy}{h(y)} = \int g(x)\,dx + C$.
4. Solve for $y$ (explicit if possible; implicit otherwise).
5. Apply initial condition to fix $C$.

**Caveat on singular solutions:** Dividing by $h(y)$ loses equilibrium solutions $h(y) = 0$. Always check these separately.

**Example:** $y' = 3x^2 y$, $y(0) = 2$.
Separate: $dy/y = 3x^2\,dx$. Integrate: $\ln|y| = x^3 + C_1$. Exponentiate: $y = Ae^{x^3}$.
Apply IC: $A = 2$. **Solution:** $y = 2e^{x^3}$.
(Singular solution $y=0$ satisfies the ODE but not the IC here.)

---

#### 3. Exponential Growth and Radioactive Decay

**Model:** $dy/dt = ky$, $y(0) = y_0$ → $y(t) = y_0 e^{kt}$.
- $k > 0$: exponential growth.
- $k < 0$: exponential decay. **Half-life:** $t_{1/2} = \ln 2/|k|$.

**Radiocarbon Dating:** $^{14}$C half-life $\approx 5730$ yr: $k = -\ln2/5730 \approx -1.21\times10^{-4}$ yr$^{-1}$.
A sample retaining 60% of original $^{14}$C: $0.6 = e^{kt} \Rightarrow t = \frac{\ln 0.6}{k} \approx 4222$ years.

**Newton's Law of Cooling (separable form):** $\frac{dT}{dt} = -k(T - T_{\rm env})$.
Let $u = T - T_{\rm env}$: $du/dt = -ku \Rightarrow u = u_0 e^{-kt}$, so
$$T(t) = T_{\rm env} + (T_0 - T_{\rm env})\,e^{-kt}.$$

---

#### 4. Implicit Solutions

Sometimes $\int dy/h(y)$ cannot be inverted to give $y$ explicitly, leaving an **implicit solution** $H(y) = G(x) + C$.

**Example:** $y' = x/y$, $y(0) = 3$.
Separate: $y\,dy = x\,dx$. Integrate: $y^2/2 = x^2/2 + C$.
Apply IC: $9/2 = C$. **Implicit solution:** $y^2 - x^2 = 9$. (Upper branch: $y = \sqrt{x^2+9}$.)
The family $y^2 - x^2 = K$ is a family of hyperbolas.

**When to keep the implicit form:**
- Solving for $y$ would require choosing branches (multi-valuedness).
- The implicit relation completely defines the solution set.
- Numerical evaluation is still straightforward from the implicit form.

---

#### 5. Mixing Problems

**Setup:** Tank holds $V$ L of solution. Concentration $c_{\rm in}$ flows in at rate $r_{\rm in}$ L/min; mixed solution drains at $r_{\rm out}$ L/min. Let $Q(t)$ = amount of solute (kg).

**Key principle:** Conservation of mass:
$$\frac{dQ}{dt} = \underbrace{\text{rate in}}_{\rm kg/min} - \underbrace{\text{rate out}}_{\rm kg/min}$$

- **Rate in:** $r_{\rm in}\,[\rm L/min] \times c_{\rm in}\,[\rm kg/L]$
- **Rate out:** $r_{\rm out}\,[\rm L/min] \times \dfrac{Q(t)}{V(t)}\,[\rm kg/L]$

**ODE:**
$$\boxed{\frac{dQ}{dt} = r_{\rm in}\,c_{\rm in} - r_{\rm out}\,\frac{Q(t)}{V(t)}}$$

Volume: $V(t) = V_0 + (r_{\rm in} - r_{\rm out})\,t$. Constant volume if $r_{\rm in} = r_{\rm out}$.

**Constant-volume case** ($r_{\rm in} = r_{\rm out} = r$, $c_{\rm in} = 0$):
$$\frac{dQ}{dt} = -\frac{r}{V}Q \implies Q(t) = Q_0\,e^{-rt/V}.$$

**Example:** 100 L tank, $Q_0 = 5$ kg salt; pure water in at 5 L/min.
$Q(t) = 5e^{-t/20}$ kg. Concentration $= Q/V = 0.05\,e^{-t/20}$ kg/L.
Time to halve salt: $t = 20\ln 2 \approx 13.9$ min.

**Other applications:** Drug clearance (pharmacokinetics), pollutant washout from a lake, salt in process tanks.

---

#### 6. The Logistic Equation

**Model:** Population with carrying capacity $K$:
$$\frac{dP}{dt} = rP\!\left(1 - \frac{P}{K}\right), \quad P(0) = P_0.$$

Separable: $\dfrac{dP}{P(1-P/K)} = r\,dt$.

**Partial fractions:** $\dfrac{1}{P(1-P/K)} = \dfrac{1}{P} + \dfrac{1/K}{1-P/K}$.

**Solution:**
$$\boxed{P(t) = \frac{K}{1 + \left(\frac{K}{P_0}-1\right)e^{-rt}}}$$

**Key features:**
- **S-shaped (sigmoidal)** growth for $P_0 < K$: slow start → rapid growth → levelling off at $K$.
- $P = K$: **stable** equilibrium. $P = 0$: **unstable** equilibrium.
- **Inflection point** at $P = K/2$: maximum growth rate.
- As $t\to\infty$: $P(t)\to K$ regardless of $P_0 > 0$.

**Applications:** Population biology, epidemic spread, market saturation, fishery management.

---

#### 7. Further Separable ODE Examples

**Example 1:** $y' = \dfrac{xy}{1+x^2}$, $y(0) = 2$.
Separate: $\frac{dy}{y} = \frac{x\,dx}{1+x^2}$. Integrate: $\ln|y| = \frac{1}{2}\ln(1+x^2) + C_1$.
Exponentiate: $y = A\sqrt{1+x^2}$. IC: $A=2$. **Solution:** $y = 2\sqrt{1+x^2}$.

**Example 2:** $y' = (1+y^2)e^x$, $y(0) = 0$.
Separate: $\frac{dy}{1+y^2} = e^x\,dx$. Integrate: $\arctan y = e^x + C$.
IC: $\arctan 0 = e^0 + C \Rightarrow C = -1$. **Solution:** $y = \tan(e^x - 1)$.
*(Blows up when $e^x - 1 = \pi/2$, i.e., $x = \ln(1+\pi/2) \approx 0.89$ — Picard–Lindelöf guarantees only local existence.)*

**Example 3 — Chemical Decomposition:** A substance decomposes proportional to the amount present. 80% remains after 2 hr. When does 50% remain?
Model: $dA/dt = kA$, $A(0)=A_0 \Rightarrow A(t)=A_0 e^{kt}$.
Find $k$: $0.8 = e^{2k} \Rightarrow k = \frac{\ln 0.8}{2} \approx -0.1116$ hr$^{-1}$.
Find $t$: $0.5 = e^{kt} \Rightarrow t = \frac{\ln 0.5}{k} = \frac{2\ln 0.5}{\ln 0.8} \approx 6.21$ hr.

**Example 4 — Newton's Cooling with Data:** Body cools from $100°$C to $60°$C in 10 min; room at $20°$C. Find $T$ at $t = 20$ min.
$T(t) = 20 + 80\,e^{kt}$. $T(10)=60$: $40 = 80\,e^{10k} \Rightarrow e^{10k} = \frac{1}{2} \Rightarrow k = -\frac{\ln 2}{10}$.
$T(20) = 20 + 80\,e^{-2\ln 2} = 20 + 80\cdot\frac{1}{4} = \mathbf{40°C}$.

---

#### 8. Euler's Method — Motivation and Algorithm

**Problem:** Approximate $y(x)$ from $y' = f(x,y)$, $y(x_0)=y_0$ at a sequence of points.

**Geometric idea:** At $(x_0, y_0)$ the direction field gives slope $f(x_0,y_0)$; step $h$ along this tangent: $y_1 \approx y_0 + h\cdot f(x_0,y_0)$. Repeat.

**Algorithm:** For $n = 0, 1, 2, \ldots$:
$$x_{n+1} = x_n + h, \qquad y_{n+1} = y_n + h\cdot f(x_n, y_n).$$

**Example:** $y' = y$, $y(0) = 1$, $h = 0.1$ (exact $y = e^x$):

| $n$ | $x_n$ | $y_n$ (Euler) | $e^{x_n}$ |
|-----|--------|--------------|-----------|
| 0 | 0.0 | 1.0000 | 1.0000 |
| 1 | 0.1 | 1.1000 | 1.1052 |
| 2 | 0.2 | 1.2100 | 1.2214 |
| 3 | 0.3 | 1.3310 | 1.3499 |

**Local truncation error (LTE):** By Taylor's theorem: $y(x_{n+1}) = y(x_n) + hy'(x_n) + \frac{h^2}{2}y''(\xi)$.
Euler keeps only the first two terms: LTE $= \frac{h^2}{2}y''(\xi) = O(h^2)$.

**Global error:** Over $N = (b-a)/h$ steps: global error $= O(h)$. Euler is a **first-order method** — halving $h$ halves the global error.

**Stiff equations:** When solutions have very different timescales, Euler requires tiny $h$ for stability. Example: Substance A decays in 0.001 s (fast), substance B in 100 s (slow) — both in the same ODE. Euler must use $h < 0.001$ s to track A, even after A has vanished. **Fix:** use a stiff solver — `ode15s` (MATLAB) or `method='Radau'` (Python).

---

#### 9. Higher-Order Methods — Overview

More accurate methods average *multiple* slopes per step:

| Method | Slopes / step | Global error | Use |
|--------|---------------|-------------|-----|
| Euler | 1 | $O(h)$ | Teaching; simple baseline |
| Heun (Impr. Euler) | 2 | $O(h^2)$ | Predictor–corrector pair |
| RK4 | 4 | $O(h^4)$ | Workhorse in practice |
| `ode45`/`solve_ivp` | adaptive | $O(h^5)$ | Software standard |

You do **not** need to memorise the Heun or RK4 formulas — software handles them. Understanding *Euler* is enough to grasp the concept of **order**, **step size**, and **accumulated error** that underlies all these methods.

---

#### 10. Solving ODEs with MATLAB and Python

**MATLAB — `ode45`** (Runge–Kutta 4(5) with automatic step-size control):
```matlab
% Scalar ODE: y' = -y + cos(t), y(0) = 0, t in [0, 10]
f = @(t, y)  -y + cos(t);
[t, y] = ode45(f, [0 10], 0);
plot(t, y), xlabel('t'), ylabel('y')

% 2nd-order ODE: y'' + y = 0, y(0)=1, y'(0)=0
% Reduce: u1 = y, u2 = y'
f = @(t, u)  [u(2); -u(1)];
[t, u] = ode45(f, [0 10], [1; 0]);
plot(t, u(:,1))  % y(t)

% Stiff equations: replace ode45 with ode15s
```

**Python — `scipy.integrate.solve_ivp`** (RK45 by default):
```python
import numpy as np
from scipy.integrate import solve_ivp
import matplotlib.pyplot as plt

# Scalar ODE: y' = -y + cos(t), y(0) = 0
f = lambda t, y: [-y[0] + np.cos(t)]
sol = solve_ivp(f, [0, 10], [0])
plt.plot(sol.t, sol.y[0])

# 2nd-order ODE: y'' + y = 0, y(0)=1, y'(0)=0
f = lambda t, u: [u[1], -u[0]]
sol = solve_ivp(f, [0, 10], [1, 0])
plt.plot(sol.t, sol.y[0])  # y(t)

# Stiff equations: add method='Radau' or method='BDF'
```

---

#### 11. Summary — Lecture 2

| Concept | Formula / Rule |
|---------|----------------|
| Separable ODE | $dy/dx = g(x)h(y)$ → $\int dy/h(y) = \int g(x)\,dx + C$ |
| Singular solutions | Check $h(y)=0$ separately (lost by division) |
| Exponential model | $y' = ky$ → $y = y_0 e^{kx}$; $t_{1/2} = \ln2/|k|$ |
| Logistic model | $P' = rP(1-P/K)$; S-shaped; $P\to K$ as $t\to\infty$ |
| Euler step | $y_{n+1} = y_n + hf(x_n,y_n)$; global error $O(h)$ |
| Higher-order | Heun $O(h^2)$, RK4 $O(h^4)$ — formulas handled by software |
| MATLAB | `ode45(f, tspan, y0)` |
| Python | `solve_ivp(f, [t0,tf], y0)` |

---

## Lecture 3: Exact Differential Equations and Integrating Factors

### Introduction

Separation of variables handles only a special class of ODEs. The next major class is **exact equations**: ODEs of the form $M\,dx + N\,dy = 0$ where the left side equals the total differential $dF$ of some function $F(x,y)$. The solution is then simply $F(x,y) = C$. When the equation is not exact, an **integrating factor** $\mu(x,y)$ converts it to one that is exact.

---

### Knowledge Points

---

#### 1. Total Differential and Exact Equations

**Recall:** For $F(x,y)$, the total differential is $dF = F_x\,dx + F_y\,dy$.

**Definition:** $M(x,y)\,dx + N(x,y)\,dy = 0$ is **exact** on a region $R$ if there exists $F(x,y)$ with:
$$F_x = M, \qquad F_y = N.$$
Then $M\,dx+N\,dy = dF = 0$, so the **general solution** is $F(x,y) = C$ (level curves of the potential $F$).

**Example:** $(2xy)\,dx + (x^2+3y^2)\,dy = 0$.
Try $F_x = 2xy$: $F = x^2 y + g(y)$.
$F_y = x^2 + g'(y) = x^2 + 3y^2 \Rightarrow g'(y) = 3y^2 \Rightarrow g = y^3$.
**General solution:** $x^2 y + y^3 = C$.

---

#### 2. The Exactness Test

**Theorem:** On a simply-connected region, $M\,dx + N\,dy = 0$ is exact **if and only if**:
$$\frac{\partial M}{\partial y} = \frac{\partial N}{\partial x}.$$

**Proof sketch:** If $F$ exists with $F_x = M$, $F_y = N$, then by Clairaut's theorem: $M_y = F_{xy} = F_{yx} = N_x$.

**Examples:**
- $(3x^2y+2)\,dx + (x^3-5)\,dy = 0$: $M_y = 3x^2$, $N_x = 3x^2$ ✓. **Exact.**
- $(2x+y)\,dx + (x+3y)\,dy = 0$: $M_y = 1$, $N_x = 1$ ✓. **Exact.**
- $(x+y^2)\,dx + (x^2+y)\,dy = 0$: $M_y = 2y$, $N_x = 2x$. ✗. **Not exact.**

---

#### 3. Solving an Exact ODE — Algorithm

1. Verify $M_y = N_x$.
2. Integrate $M$ with respect to $x$: $F = \displaystyle\int M\,dx + g(y)$.
3. Differentiate $F$ w.r.t. $y$ and set equal to $N$: $F_y = N$.
4. Solve for $g'(y)$ — it must depend only on $y$.
5. Integrate to find $g(y)$.
6. Write general solution $F(x,y) = C$.

**Example:** $(y\cos x + 2xe^y)\,dx + (\sin x + x^2 e^y - 1)\,dy = 0$.
Check: $M_y = \cos x + 2xe^y = N_x$ ✓.
$F = \int(y\cos x + 2xe^y)\,dx = y\sin x + x^2 e^y + g(y)$.
$F_y = \sin x + x^2 e^y + g'(y) = \sin x + x^2 e^y - 1 \Rightarrow g'(y) = -1 \Rightarrow g = -y$.
**General solution:** $y\sin x + x^2 e^y - y = C$.

---

#### 4. Non-Exact Equations and Integrating Factors

**Idea:** If $M_y \neq N_x$, multiply through by $\mu(x,y)$ to make $(\mu M)_y = (\mu N)_x$.

**Measure of non-exactness:** $\varepsilon = M_y - N_x$ (the "exactness defect"). The goal: choose $\mu$ so that after multiplying, $\varepsilon$ becomes zero.

The condition on $\mu$ is a PDE — harder than the original ODE. We look for special cases.

---

#### 5. Integrating Factor $\mu = \mu(x)$

**Assumption:** $\mu$ depends only on $x$. Exactness requires:
$$\frac{\mu'}{\mu} = \frac{M_y - N_x}{N} \eqqcolon P(x).$$

**Condition:** $(M_y - N_x)/N$ must depend only on $x$.

**Theorem:** If $P(x) = \dfrac{M_y - N_x}{N}$ depends only on $x$, then
$$\mu(x) = e^{\int P(x)\,dx}.$$

**Worked example:** $(y^2 + e^{-x})\,dx + 2y\,dy = 0$.
$M = y^2 + e^{-x}$, $N = 2y$. $M_y = 2y$, $N_x = 0$. Not exact.
Test $\mu(x)$: $\frac{M_y - N_x}{N} = \frac{2y}{2y} = 1$ — depends only on $x$. ✓
$\mu(x) = e^{\int 1\,dx} = e^x$.
Multiply: $(y^2 e^x + 1)\,dx + 2ye^x\,dy = 0$. Check: $(\mu M)_y = 2ye^x = (\mu N)_x$. ✓
Solve: $F = y^2 e^x + x + g(y)$; $F_y = 2ye^x + g'(y) = 2ye^x \Rightarrow g'(y) = 0$.
**General solution:** $\boxed{y^2 e^x + x = C}$.

---

#### 6. Integrating Factor $\mu = \mu(y)$

**Assumption:** $\mu$ depends only on $y$. The exactness condition gives:
$$\frac{\mu'}{\mu} = \frac{N_x - M_y}{M} \eqqcolon Q(y).$$

**Condition:** $(N_x - M_y)/M$ must depend only on $y$.

**Theorem:** If $Q(y) = \dfrac{N_x - M_y}{M}$ depends only on $y$, then
$$\mu(y) = e^{\int Q(y)\,dy}.$$

**Example:** $(2xy)\,dx + (y^2 - x^2)\,dy = 0$.
$M_y = 2x$, $N_x = -2x$. $(M_y-N_x)/N = 4x/(y^2-x^2)$ — depends on $y$ too. Try $\mu(y)$:
$(N_x-M_y)/M = (-2x-2x)/(2xy) = -2/y$ — depends only on $y$! ✓
$\mu = e^{\int -2/y\,dy} = y^{-2}$. Multiply: $(2x/y)\,dx + (1-x^2/y^2)\,dy = 0$.
Check: $M_y = -2x/y^2 = N_x$ ✓. **Solution:** $F = x^2/y + y = C$.

**Summary of IF strategy:**

| Check | If yes | $\mu$ |
|-------|--------|-------|
| $(M_y-N_x)/N = P(x)$ | ✓ | $e^{\int P\,dx}$ |
| $(N_x-M_y)/M = Q(y)$ | ✓ | $e^{\int Q\,dy}$ |

---

#### 7. Connection to First-Order Linear ODEs

The linear ODE $y' + p(x)y = r(x)$ in differential form:
$$(py - r)\,dx + dy = 0, \qquad M = py-r,\; N = 1.$$
$M_y = p(x)$, $N_x = 0$ → $(M_y - N_x)/N = p(x)$ — depends only on $x$. ✓

Integrating factor: $\mu(x) = e^{\int p(x)\,dx}$.

**This is exactly the integrating factor used in Week 5 for linear ODEs.** The exact-equation method and the standard linear method are the same in this case.

---

#### 8. Worked Example — Full Solution with IVP

**Solve:** $(e^x\sin y - 2y\sin x)\,dx + (e^x\cos y + 2\cos x)\,dy = 0$, $y(0) = \pi/2$.

**Step 1 — Check exactness:**
$M_y = e^x\cos y - 2\sin x$, $N_x = e^x\cos y - 2\sin x$ ✓.

**Step 2 — Find $F$:**
$F = \int M\,dx = e^x\sin y + 2y\cos x + g(y)$.
$F_y = e^x\cos y + 2\cos x + g'(y) = e^x\cos y + 2\cos x \Rightarrow g'(y) = 0 \Rightarrow g = \text{const}$.

General solution: $e^x\sin y + 2y\cos x = C$.

**Step 3 — Apply IC** $y(0) = \pi/2$:
$e^0\sin(\pi/2) + 2(\pi/2)\cos 0 = 1 + \pi = C$.

**Particular solution:** $e^x\sin y + 2y\cos x = 1+\pi$.

---

#### 9. Common Errors and Pitfalls

1. **Skip the exactness check.** Always verify $M_y = N_x$ *before* applying the method.
2. **Sign errors in $g'(y)$.** After computing $\int M\,dx$, differentiate the *entire* result w.r.t. $y$ — including $y$-terms from the $x$-integration.
3. **Confuse $M\,dx+N\,dy=0$ with $y'=f(x,y)$.** They are equivalent ($y' = -M/N$), but the differential form makes exactness transparent.
4. **Forget to re-verify after multiplying by IF.** Always recheck $(\mu M)_y = (\mu N)_x$ before proceeding.
5. **Lose singular solutions.** If $M = 0$ somewhere, solutions at that locus may be lost when dividing by $M$ to compute $Q(y)$.

---

#### 10. Exercises with hints

**Problem 1:** $(2y + x)\,dx + x\,dy = 0$
*Hint:* $M_y - N_x = 2 - 1 = 1$. $\frac{M_y - N_x}{N} = \frac{1}{x}$ (only $x$) $\Rightarrow \mu = x$.
After multiplying by $\mu$: find $F$ such that $F_x = \mu M$, $F_y = \mu N$, and write $F(x,y) = C$.

**Problem 2:** $(3xy + y^2)\,dx + (x^2 + xy)\,dy = 0$
*Hint:* Factor $N = x(x+y)$. Show $\frac{M_y - N_x}{N} = \frac{1}{x}$ $\Rightarrow \mu = x$.
After multiplying: the solution has the form $x^3 y + \frac{1}{2}x^2 y^2 = C$.

**Problem 3:** $(y + xy^2)\,dx - x\,dy = 0$
*Hint:* Factor $M = y(1+xy)$. $\frac{N_x - M_y}{M} = \frac{-2}{y}$ (only $y$) $\Rightarrow \mu = y^{-2}$.
After multiplying by $y^{-2}$: the equation becomes exact. Find $F$ and write $F(x,y) = C$.

**Problem 4:** $(y^3 + y)\,dx - 2x\,dy = 0$
*Hint:* Factor $M = y(y^2+1)$. Show $\frac{N_x - M_y}{M} = \frac{-3}{y}$ $\Rightarrow \mu = y^{-3}$.
After multiplying: $\mu M = 1 + y^{-2}$. Find $F = x\!\left(1 + \frac{1}{y^2}\right)$.
**Solution:** $x\!\left(1 + \frac{1}{y^2}\right) = C$.

---

#### 11. Method Selection Guide — First-Order ODEs

After Weeks 4–5, five methods will be available. Check in this order (lowest complexity first):

| Check | Method |
|-------|--------|
| $y' = g(x)h(y)$? | **Separable** (Lec 2 this week) |
| $M_y = N_x$? | **Exact** (Lec 3 this week) |
| $y' + p(x)y = r(x)$? | **Linear** (Week 5) |
| Bernoulli: $y' + py = ry^n$? | **Bernoulli** → linear (Week 5) |
| None of the above | **Numerical** (Euler / RK4) |

**Tip:** Separable is lowest complexity (one integration each side); exact requires no rearrangement beyond finding $F$; linear methods come next in Week 5.

---

#### 12. Summary — Lecture 3

| Concept | Key Formula |
|---------|------------|
| Exact ODE | $M_y = N_x$ → $\exists\,F$: $dF = M\,dx+N\,dy$; solution $F = C$ |
| Exactness test | $\partial M/\partial y = \partial N/\partial x$ (necessary & sufficient on simply-connected domain) |
| Finding $F$ | Integrate $M$ in $x$; fix $g(y)$ via $F_y = N$ |
| IF $\mu(x)$ | $P(x) = (M_y-N_x)/N$ only in $x$ $\Rightarrow$ $\mu = e^{\int P\,dx}$ |
| IF $\mu(y)$ | $Q(y) = (N_x-M_y)/M$ only in $y$ $\Rightarrow$ $\mu = e^{\int Q\,dy}$ |
| Link to Week 5 | Linear $y'+py=r$ has $\mu = e^{\int p\,dx}$ (same formula) |
| Selection order | Separable → Exact → Linear → Numerical |

---

## Practice Problems

1. Classify each ODE by order, linearity, and autonomy: (a) $y'' + 3y' - y = e^x$; (b) $yy' = x$; (c) $y' = y^2 - x$; (d) $y^{(4)} + y = 0$.

2. Verify that $y = Ce^{-2x} + \tfrac{1}{2}$ is a general solution of $y' + 2y = 1$. Find the particular solution satisfying $y(0) = 3$.

3. Solve the separable ODE $\frac{dy}{dx} = \frac{x^2}{1-y^2}$. Check whether any singular solutions are lost.

4. A radioactive substance decays so that its half-life is 8 days. If 100 g are present initially, find the amount remaining after 20 days.

5. Use Euler's method with step $h = 0.1$ to approximate $y(0.3)$ for $y' = x + y$, $y(0) = 1$. Compare with the exact solution $y = -x - 1 + 2e^x$.

6. Solve the logistic IVP $P' = 2P(1 - P/5)$, $P(0) = 1$. Find the time at which $P = 4$.

7. Test exactness and solve: $(2xy + y^2)\,dx + (x^2 + 2xy)\,dy = 0$.

8. Find an integrating factor $\mu(x)$ and solve: $(y^2)\,dx + (2xy + e^y)\,dy = 0$.

9. Solve $(y + xy^2)\,dx - x\,dy = 0$ using an integrating factor $\mu(y)$.

10. For the mixing problem: a tank holds 100 L of pure water. Brine with 0.5 kg/L enters at 4 L/min and the well-mixed solution drains at 4 L/min. Set up and solve the ODE for salt $Q(t)$. Find the limiting salt content.
