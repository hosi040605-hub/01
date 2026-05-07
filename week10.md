# Week 10 — Systems of ODEs and the Phase Plane

**Course:** Engineering Mathematics 1
**Part:** IV — Systems of Ordinary Differential Equations
**Kreyszig Sections:** §4.1, 4.2, 4.3

> **Building on Week 9:** The 2D matrix algebra and eigenvalue method reviewed in Week 9 (§4.0) are now put to work. Systems of first-order ODEs arise naturally from multi-degree-of-freedom engineering models (coupled oscillators, mixing tanks, electrical networks) and from the reduction of higher-order ODEs. The **eigenvalue method** solves constant-coefficient systems directly, and the **phase plane** gives a complete geometric picture of solution behaviour without computing explicit formulas.

---

## Lecture 1: Systems of ODEs as Engineering Models (§4.1)

### Introduction

A single second-order ODE describes one degree of freedom. Real engineering systems — two coupled masses, a multi-tank process, a network of electrical loops — involve several interacting quantities and require a **system** of ODEs. This lecture shows how such models arise, how any higher-order ODE converts into a first-order system, and how to write the result in compact matrix form $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}(t)$.

**Why it matters in engineering:**
- Multi-DOF vibration problems (buildings, aircraft, rotating machinery) are inherently systems.
- State-space representation — the matrix form of a first-order system — is the foundation of modern control engineering.
- Numerical ODE solvers (MATLAB's `ode45`, etc.) accept only first-order systems; converting higher-order problems is a prerequisite for computation.

---

### Knowledge Points

---

#### 1. Linear Systems of First-Order ODEs — Definition

A **linear system of $n$ first-order ODEs** in matrix form:
$$\mathbf{y}' = \mathbf{A}(t)\mathbf{y} + \mathbf{g}(t), \qquad \mathbf{y} = \mathbf{y}(t) = \begin{pmatrix}y_1(t) \\ \vdots \\ y_n(t)\end{pmatrix}, \quad \mathbf{A}(t) = [a_{ij}(t)]_{n\times n}, \quad \mathbf{g}(t) = \begin{pmatrix}g_1(t) \\ \vdots \\ g_n(t)\end{pmatrix}.$$

**Homogeneous linear system:** $\mathbf{y}' = \mathbf{A}(t)\mathbf{y}$ (i.e., $\mathbf{g} = \mathbf{0}$).

**Constant-coefficient homogeneous system:** $\mathbf{y}' = \mathbf{A}\mathbf{y}$ with $\mathbf{A}$ constant — the main object of §4.3.

**Existence and uniqueness:** If $\mathbf{A}(t)$ and $\mathbf{g}(t)$ are continuous on an open interval $I$ containing $t_0$, the IVP $\mathbf{y}' = \mathbf{A}(t)\mathbf{y} + \mathbf{g}(t)$, $\mathbf{y}(t_0) = \mathbf{y}_0$ has a **unique solution** on all of $I$.

---

#### 2. Converting Higher-Order ODEs to First-Order Systems

**Standard reduction:** The $n$-th order ODE $y^{(n)} = f(t, y, y', \ldots, y^{(n-1)})$ becomes a first-order system by setting:
$$y_1 = y, \quad y_2 = y', \quad y_3 = y'', \quad \ldots, \quad y_n = y^{(n-1)}.$$

Then $y_1' = y_2$, $\ldots$, $y_{n-1}' = y_n$, $y_n' = f(t, y_1, \ldots, y_n)$.

**Example — second-order ODE:** Convert $y'' + py' + qy = r(t)$ to matrix form.

Let $y_1 = y$, $y_2 = y'$:
$$\begin{pmatrix}y_1' \\ y_2'\end{pmatrix} = \underbrace{\begin{pmatrix}0 & 1 \\ -q & -p\end{pmatrix}}_{\text{companion matrix}}\begin{pmatrix}y_1 \\ y_2\end{pmatrix} + \begin{pmatrix}0 \\ r(t)\end{pmatrix}.$$

**Key observation:** The characteristic equation of the companion matrix,
$$\det\begin{pmatrix}-\lambda & 1 \\ -q & -p-\lambda\end{pmatrix} = \lambda^2 + p\lambda + q = 0,$$
is exactly the characteristic equation of the original ODE. The eigenvalue method for systems is the direct generalisation of the characteristic equation method from Week 6.

---

#### 3. Coupled Spring Systems (§4.1)

**Physical setup:** Two masses $m_1$, $m_2$ connected in series by springs with constants $k_1$ (wall to $m_1$), $k_2$ (between masses), $k_3$ ($m_2$ to wall).

**Equations of motion** (Newton's second law for each mass):
$$m_1\ddot{y}_1 = -k_1 y_1 + k_2(y_2 - y_1) = -(k_1+k_2)y_1 + k_2 y_2,$$
$$m_2\ddot{y}_2 = -k_2(y_2 - y_1) - k_3 y_2 = k_2 y_1 - (k_2+k_3)y_2.$$

In matrix form (second-order system):
$$\begin{pmatrix}\ddot{y}_1 \\ \ddot{y}_2\end{pmatrix} = \frac{1}{m}\begin{pmatrix}-(k_1+k_2) & k_2 \\ k_2 & -(k_2+k_3)\end{pmatrix}\begin{pmatrix}y_1 \\ y_2\end{pmatrix}$$
(assuming $m_1 = m_2 = m$).

**First-order system:** Introduce $\mathbf{x} = (y_1, \dot{y}_1, y_2, \dot{y}_2)^T$ — a 4×4 system.

**Normal modes:** The eigenvalues of the coefficient matrix give $\lambda = -\omega^2$, so $\omega$ are the **normal mode frequencies**. Each eigenvector describes the shape of one mode of vibration.

**Special case** $m = 1$, $k_1 = k_3 = 1$, $k_2 = 2$:
$$\mathbf{K} = \begin{pmatrix}-3 & 2 \\ 2 & -3\end{pmatrix}.$$
Eigenvalues: $\lambda_1 = -1$, $\lambda_2 = -5$ → natural frequencies $\omega_1 = 1$, $\omega_2 = \sqrt{5}$.

In-phase mode ($\omega_1 = 1$): $\mathbf{v}^{(1)} = \begin{pmatrix}1 \\ 1\end{pmatrix}$ — both masses move together.

Out-of-phase mode ($\omega_2 = \sqrt{5}$): $\mathbf{v}^{(2)} = \begin{pmatrix}1 \\ -1\end{pmatrix}$ — masses move in opposite directions.

---

#### 4. Mixing Tank Models (§4.1)

**Two-tank problem:** Tank 1 (volume $V_1$) and Tank 2 (volume $V_2$) exchange fluid. Let $y_1(t)$, $y_2(t)$ be the amounts of solute.

Conservation of mass (balance of inflow minus outflow for each tank):
$$y_1' = -\frac{r_{12}}{V_1}y_1 + \frac{r_{21}}{V_2}y_2 + \text{external input}_1,$$
$$y_2' = \frac{r_{12}}{V_1}y_1 - \left(\frac{r_{21}+r_{\text{out}}}{V_2}\right)y_2.$$

This is a 2×2 linear system $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}$ with constant coefficients.

**General principle:** Any multi-compartment model with linear transfer rates (pharmacokinetics, ecology, economics) yields a linear system of ODEs. The eigenvalues determine the timescales of the mixing process.

---

#### 5. Worked Example — Electric Network (§4.1, Fig. 79)

**Circuit:** Two-mesh network (switch closes at $t = 0$). Left mesh: EMF $E = 12$ V, inductor $L = 1$ H. Right mesh: capacitor $C = 0.25$ F, resistor $R_2 = 6\ \Omega$. Shared branch (middle): resistor $R_1 = 4\ \Omega$.

**Variables:** $I_1(t)$ = left mesh current, $I_2(t)$ = right mesh current. Initial conditions: $I_1(0) = I_2(0) = 0$ (inductor and capacitor both start with no energy stored).

**Step 1 — KVL for Mesh 1** (left loop, clockwise):
$$L\dot{I}_1 + R_1(I_1 - I_2) = E \implies \dot{I}_1 = -4I_1 + 4I_2 + 12. \tag{1}$$

**Step 2 — KVL for Mesh 2** (right loop, clockwise). The charge on the capacitor is $Q$, with $\dot{Q} = I_2$:
$$R_1(I_2 - I_1) + \frac{Q}{C} + R_2 I_2 = 0 \implies -4I_1 + 10I_2 + 4Q = 0. \tag{2}$$

Equation (2) is an algebraic constraint involving the integral $Q = \int I_2\,dt$. **Differentiating** (2) with respect to $t$ (and using $\dot{Q} = I_2$):
$$-4\dot{I}_1 + 10\dot{I}_2 + 4I_2 = 0 \implies 10\dot{I}_2 = 4\dot{I}_1 - 4I_2.$$

Substituting (1):
$$10\dot{I}_2 = 4(-4I_1 + 4I_2 + 12) - 4I_2 = -16I_1 + 12I_2 + 48,$$
$$\dot{I}_2 = -\tfrac{8}{5}I_1 + \tfrac{6}{5}I_2 + \tfrac{24}{5}. \tag{3}$$

**Step 3 — Matrix form.** With $\mathbf{y}(t) = \begin{pmatrix}I_1(t) \\ I_2(t)\end{pmatrix}$:
$$\mathbf{y}' = \begin{pmatrix}-4 & 4 \\[4pt] -\tfrac{8}{5} & \tfrac{6}{5}\end{pmatrix}\mathbf{y} + \begin{pmatrix}12 \\[4pt] \tfrac{24}{5}\end{pmatrix}, \qquad \mathbf{y}(0) = \begin{pmatrix}0 \\ 0\end{pmatrix}.$$

**Steady-state check:** Setting $\mathbf{y}' = \mathbf{0}$ gives $I_1^* = 3$ A and $I_2^* = 0$ A. This is physically correct: at DC steady state the capacitor is fully charged ($U_C = Q/C = 12$ V $= E$), no current flows in the right mesh, and the left mesh current is $I_1 = E/R_1 = 12/4 = 3$ A.

---

#### 6. Worked Example — Converting a Scalar ODE

**Problem:** Convert $y'' - 3y' + 2y = 0$ to a first-order system and write the matrix.

Setting $y_1 = y$, $y_2 = y'$:
$$\begin{pmatrix}y_1' \\ y_2'\end{pmatrix} = \begin{pmatrix}0 & 1 \\ -2 & 3\end{pmatrix}\begin{pmatrix}y_1 \\ y_2\end{pmatrix}.$$

Eigenvalues: $\lambda^2 - 3\lambda + 2 = (\lambda-1)(\lambda-2) = 0$ → $\lambda_1 = 1$, $\lambda_2 = 2$.

These match the roots of the characteristic equation $r^2 - 3r + 2 = 0$ from the original scalar ODE — confirming the equivalence.

---

#### 7. Summary — Lecture 1

| Model | System form | Key structure |
|-------|-------------|---------------|
| $n$-th order ODE | $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}$ (companion matrix) | Eigenvalues = characteristic roots |
| Two coupled masses | $4\times4$ system | Eigenvalues give normal frequencies |
| Two-tank mixing | $2\times2$ system | Eigenvalues give mixing timescales |
| Two-mesh RL-RC network | $2\times2$ system | Differentiate KVL to eliminate capacitor integral |

---

## Lecture 2: Basic Theory of Linear Systems (§4.2)

### Introduction

The theory of linear systems $\mathbf{y}' = \mathbf{A}(t)\mathbf{y}$ is the direct generalisation of the theory for a single $n$-th order linear ODE. Every concept from Weeks 6–7 — superposition, Wronskian, general solution structure, Abel's theorem — carries over to systems, now expressed in matrix-vector language. This theoretical foundation justifies the eigenvalue solution method of Lecture 3.

---

### Knowledge Points

---

#### 1. Superposition Principle

**Theorem:** If $\mathbf{y}^{(1)}, \ldots, \mathbf{y}^{(n)}$ are solutions of the homogeneous system $\mathbf{y}' = \mathbf{A}(t)\mathbf{y}$, then
$$\mathbf{y} = c_1\mathbf{y}^{(1)} + \cdots + c_n\mathbf{y}^{(n)}$$
is also a solution for any constants $c_1, \ldots, c_n$.

**Proof:** Each $(\mathbf{y}^{(k)})' = \mathbf{A}\mathbf{y}^{(k)}$, so $\mathbf{y}' = \sum c_k(\mathbf{y}^{(k)})' = \mathbf{A}\sum c_k\mathbf{y}^{(k)} = \mathbf{A}\mathbf{y}$. $\square$

---

#### 2. Linear Independence and the Wronskian

**Definition:** Solution vectors $\mathbf{y}^{(1)}, \ldots, \mathbf{y}^{(n)}$ are **linearly independent** if $\sum c_k\mathbf{y}^{(k)}(t) = \mathbf{0}$ for all $t$ implies $c_1 = \cdots = c_n = 0$.

**Wronskian:** The determinant of the **fundamental matrix** $\mathbf{Y}(t) = [\mathbf{y}^{(1)} \; \cdots \; \mathbf{y}^{(n)}]$:
$$W(t) = \det\mathbf{Y}(t).$$

**Theorem:** The solutions are linearly independent on $I$ if and only if $W(t) \neq 0$ for all $t \in I$.

For 2×2: $W(t) = \det\begin{pmatrix}y_1^{(1)} & y_1^{(2)} \\ y_2^{(1)} & y_2^{(2)}\end{pmatrix} = y_1^{(1)}y_2^{(2)} - y_1^{(2)}y_2^{(1)}$.

---

#### 3. Fundamental System and General Solution

**Fundamental system:** A set of $n$ linearly independent solutions $\{\mathbf{y}^{(1)}, \ldots, \mathbf{y}^{(n)}\}$.

**General solution of the homogeneous system:**
$$\mathbf{y}_h = c_1\mathbf{y}^{(1)} + \cdots + c_n\mathbf{y}^{(n)}.$$

**General solution of the nonhomogeneous system** $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}$:
$$\mathbf{y} = \mathbf{y}_h + \mathbf{y}_p,$$
exactly as in the scalar theory (Weeks 6–7).

---

#### 4. Abel's Formula for Systems

For $\mathbf{y}' = \mathbf{A}(t)\mathbf{y}$, the Wronskian satisfies:
$$W(t) = W(t_0)\exp\!\left(\int_{t_0}^t \text{tr}\,\mathbf{A}(s)\,ds\right).$$

**Consequence:** $W(t)$ is either identically zero or never zero — no intermediate behaviour possible.

**For constant-coefficient systems:** $\text{tr}\,\mathbf{A} = \lambda_1 + \lambda_2$ (sum of eigenvalues), so:
$$W(t) = W(0)\,e^{(\text{tr}\,\mathbf{A})\,t}.$$

**Connection to Week 6:** Abel's theorem for the scalar equation $y'' + p(t)y' + q(t)y = 0$ gives $W = W(t_0)e^{-\int p\,dt}$. For the companion matrix, $\text{tr}\,\mathbf{A} = -p$, so the two formulas agree.

---

#### 5. Worked Example — Verifying a Fundamental System

**Problem:** Verify that $\mathbf{y}^{(1)} = \begin{pmatrix}e^t \\ e^t\end{pmatrix}$ and $\mathbf{y}^{(2)} = \begin{pmatrix}e^{-t} \\ -e^{-t}\end{pmatrix}$ form a fundamental system for $\mathbf{y}' = \begin{pmatrix}0 & 1 \\ 1 & 0\end{pmatrix}\mathbf{y}$.

**Step 1 — Check solutions:**
$(\mathbf{y}^{(1)})' = \begin{pmatrix}e^t \\ e^t\end{pmatrix}$ and $\mathbf{A}\mathbf{y}^{(1)} = \begin{pmatrix}e^t \\ e^t\end{pmatrix}$. ✓

$(\mathbf{y}^{(2)})' = \begin{pmatrix}-e^{-t} \\ e^{-t}\end{pmatrix}$ and $\mathbf{A}\mathbf{y}^{(2)} = \begin{pmatrix}-e^{-t} \\ e^{-t}\end{pmatrix}$. ✓

**Step 2 — Wronskian:**
$$W(t) = \det\begin{pmatrix}e^t & e^{-t} \\ e^t & -e^{-t}\end{pmatrix} = -1 - 1 = -2 \neq 0.$$

Linearly independent ✓. General solution: $\mathbf{y} = c_1\begin{pmatrix}1 \\ 1\end{pmatrix}e^t + c_2\begin{pmatrix}1 \\ -1\end{pmatrix}e^{-t}$.

**Abel's formula check:** $\text{tr}\,\mathbf{A} = 0$, so $W(t) = W(0)e^0 = -2$. ✓ (constant Wronskian).

---

#### 6. Analogy Table — Scalar ODE vs. System

| Concept | Scalar ODE ($n$-th order) | Linear system ($n\times n$) |
|---------|--------------------------|----------------------------|
| Superposition | $y = \sum c_k y_k$ | $\mathbf{y} = \sum c_k\mathbf{y}^{(k)}$ |
| Wronskian | $\det[y_k^{(j-1)}]$ | $\det[\mathbf{y}^{(1)}\cdots\mathbf{y}^{(n)}]$ |
| Abel's formula | $W = W_0 e^{-\int p\,dt}$ | $W = W_0 e^{\int\text{tr}\,\mathbf{A}\,dt}$ |
| General solution | $y_h + y_p$ | $\mathbf{y}_h + \mathbf{y}_p$ |

---

#### 7. Summary — Lecture 2

The three pillars of linear system theory:

1. **Superposition:** Linear combinations of solutions are solutions.
2. **Wronskian test:** $W \neq 0$ iff solutions are linearly independent (fundamental system).
3. **Abel's formula:** $W(t) = W(0)e^{(\text{tr}\,\mathbf{A})t}$ — sign of $W$ never changes.

These justify seeking $n$ linearly independent solutions and forming the general solution as their linear combination.

---

## Lecture 3: Constant-Coefficient Systems and the Phase Plane (§4.3)

### Introduction

For the constant-coefficient system $\mathbf{y}' = \mathbf{A}\mathbf{y}$, the **eigenvalue method** produces the general solution directly. The ansatz $\mathbf{y} = \mathbf{v}e^{\lambda t}$ reduces the ODE problem to the algebraic eigenvalue problem $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$, solved using the tools of Week 9 Lecture 3.

The **phase plane** provides a complementary geometric picture: instead of computing explicit formulas, we classify the qualitative behaviour of all solutions simultaneously by examining trajectories in the $(y_1, y_2)$-plane. The phase portrait is determined entirely by the eigenvalues of $\mathbf{A}$.

---

### Knowledge Points

---

#### 1. The Eigenvalue Method

**Ansatz:** Assume $\mathbf{y}(t) = \mathbf{v}e^{\lambda t}$ with $\mathbf{v} \neq \mathbf{0}$.

Substituting into $\mathbf{y}' = \mathbf{A}\mathbf{y}$: $\lambda\mathbf{v}e^{\lambda t} = \mathbf{A}\mathbf{v}e^{\lambda t}$, so $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$.

**Algorithm (for a 2×2 system):**
1. Solve $\det(\mathbf{A} - \lambda\mathbf{I}) = 0$ for eigenvalues $\lambda_1, \lambda_2$.
2. For each $\lambda_k$, solve $(\mathbf{A} - \lambda_k\mathbf{I})\mathbf{v} = \mathbf{0}$ for eigenvector $\mathbf{v}^{(k)}$.
3. Form solution vectors $\mathbf{y}^{(k)} = \mathbf{v}^{(k)}e^{\lambda_k t}$.
4. **General solution** (when $\lambda_1 \neq \lambda_2$): $\mathbf{y} = c_1\mathbf{v}^{(1)}e^{\lambda_1 t} + c_2\mathbf{v}^{(2)}e^{\lambda_2 t}$.

---

#### 2. Case 1 — Two Distinct Real Eigenvalues

**Conditions:** $\lambda_1, \lambda_2 \in \mathbb{R}$, $\lambda_1 \neq \lambda_2$.

**General solution:** $\mathbf{y}(t) = c_1\mathbf{v}^{(1)}e^{\lambda_1 t} + c_2\mathbf{v}^{(2)}e^{\lambda_2 t}$.

**Phase plane classification:**
- **Stable node** ($\lambda_1 < \lambda_2 < 0$): all trajectories approach origin as $t \to \infty$; asymptotically stable.
- **Unstable node** ($0 < \lambda_1 < \lambda_2$): all trajectories diverge from origin.
- **Saddle point** ($\lambda_1 < 0 < \lambda_2$): trajectories approach origin along $\mathbf{v}^{(1)}$ (stable manifold), diverge along $\mathbf{v}^{(2)}$ (unstable manifold); always unstable.

**Worked Example:**
$$\mathbf{A} = \begin{pmatrix}-3 & 1 \\ 1 & -3\end{pmatrix}.$$
Characteristic equation: $(\lambda+3)^2 - 1 = \lambda^2 + 6\lambda + 8 = (\lambda+2)(\lambda+4) = 0$.
$\lambda_1 = -2$, $\lambda_2 = -4$.

$\lambda_1 = -2$: $\mathbf{v}^{(1)} = \begin{pmatrix}1 \\ 1\end{pmatrix}$. \quad $\lambda_2 = -4$: $\mathbf{v}^{(2)} = \begin{pmatrix}1 \\ -1\end{pmatrix}$.

$$\mathbf{y}(t) = c_1\begin{pmatrix}1 \\ 1\end{pmatrix}e^{-2t} + c_2\begin{pmatrix}1 \\ -1\end{pmatrix}e^{-4t}.$$

**Classification:** Stable node (both eigenvalues negative). For large $t$, trajectories are tangent to $\mathbf{v}^{(1)}$ (slower decay dominates).

---

#### 3. Case 2 — Complex Conjugate Eigenvalues

**Conditions:** $\lambda_{1,2} = \alpha \pm i\beta$, $\beta \neq 0$.

**Real-valued solutions:** If $\mathbf{v} = \mathbf{a} + i\mathbf{b}$ is the eigenvector for $\lambda = \alpha + i\beta$, take real and imaginary parts of $\mathbf{v}e^{\lambda t}$:
$$\mathbf{y}^{(1)} = e^{\alpha t}(\mathbf{a}\cos\beta t - \mathbf{b}\sin\beta t), \qquad \mathbf{y}^{(2)} = e^{\alpha t}(\mathbf{a}\sin\beta t + \mathbf{b}\cos\beta t).$$

**General solution:**
$$\mathbf{y}(t) = e^{\alpha t}\bigl[c_1(\mathbf{a}\cos\beta t - \mathbf{b}\sin\beta t) + c_2(\mathbf{a}\sin\beta t + \mathbf{b}\cos\beta t)\bigr].$$

**Phase plane classification:**
- **Stable spiral** ($\alpha < 0$): trajectories spiral inward; asymptotically stable.
- **Unstable spiral** ($\alpha > 0$): trajectories spiral outward.
- **Center** ($\alpha = 0$): closed ellipses — neutral (not asymptotically) stable.

**Worked Example:**
$$\mathbf{A} = \begin{pmatrix}-1 & -2 \\ 2 & -1\end{pmatrix}.$$
$\lambda^2 + 2\lambda + 5 = 0 \Rightarrow \lambda = -1 \pm 2i$. Here $\alpha = -1 < 0$, $\beta = 2$ → **stable spiral**.

Eigenvector for $\lambda = -1+2i$: $\begin{pmatrix}-2i & -2 \\ 2 & -2i\end{pmatrix}\mathbf{v} = \mathbf{0}$ → $\mathbf{v} = \begin{pmatrix}1 \\ -i\end{pmatrix} = \begin{pmatrix}1 \\ 0\end{pmatrix} + i\begin{pmatrix}0 \\ -1\end{pmatrix}$.

$\mathbf{a} = \begin{pmatrix}1 \\ 0\end{pmatrix}$, $\mathbf{b} = \begin{pmatrix}0 \\ -1\end{pmatrix}$.

$$\mathbf{y}(t) = e^{-t}\!\left[c_1\begin{pmatrix}\cos 2t \\ \sin 2t\end{pmatrix} + c_2\begin{pmatrix}\sin 2t \\ -\cos 2t\end{pmatrix}\right].$$

---

#### 4. Case 3 — Repeated Eigenvalue

**Conditions:** $\lambda_1 = \lambda_2 = \lambda$ (double eigenvalue).

**Sub-case A — Two independent eigenvectors** (occurs only when $\mathbf{A} = \lambda\mathbf{I}$):
$$\mathbf{y}(t) = (c_1\mathbf{v}^{(1)} + c_2\mathbf{v}^{(2)})e^{\lambda t}. \quad \text{(star node)}$$

**Sub-case B — Only one eigenvector** (defective matrix, the generic case):

Find a **generalised eigenvector** $\mathbf{u}$ satisfying $(\mathbf{A} - \lambda\mathbf{I})\mathbf{u} = \mathbf{v}$. The second solution is:
$$\mathbf{y}^{(2)}(t) = (\mathbf{v}t + \mathbf{u})e^{\lambda t}.$$

**General solution:**
$$\mathbf{y}(t) = c_1\mathbf{v}e^{\lambda t} + c_2(\mathbf{v}t + \mathbf{u})e^{\lambda t}.$$

**Phase plane:** **Improper node** — trajectories approach (or diverge from) origin with a definite tangential direction.

**Connection to Week 6:** For a 2nd-order scalar ODE with repeated root, $(c_1 + c_2 t)e^{\lambda t}$ is recovered when $\mathbf{v}$ and $\mathbf{u}$ reduce to scalars.

---

#### 5. Phase Plane — Critical Point Classification

The **phase plane** for $\mathbf{y}' = \mathbf{A}\mathbf{y}$ is the $(y_1, y_2)$-plane. Each solution traces a **trajectory**. The origin is the only **critical point** (equilibrium) when $\det\mathbf{A} \neq 0$.

**Stability definitions:**
- **Asymptotically stable:** $\mathbf{y}(t) \to \mathbf{0}$ as $t \to \infty$ for all nearby initial conditions.
- **Stable (not asymptotically):** nearby trajectories stay near the origin but do not converge to it.
- **Unstable:** nearby trajectories move away from the origin.

**Five types of critical points (Kreyszig classification):**

**1. Improper Node** — two distinct real eigenvalues of the same sign ($\lambda_1 \neq \lambda_2$, both positive or both negative). Trajectories approach (stable, $\lambda_i < 0$) or leave (unstable, $\lambda_i > 0$) the origin tangentially in the direction of the eigenvector corresponding to the smaller $|\lambda|$.

Also applies when the eigenvalue is repeated but the matrix is **defective** (only one eigenvector): the second solution contains the factor $te^{\lambda t}$, and trajectories are tangent to the single eigenvector direction.

**2. Proper Node (Star Node)** — repeated eigenvalue $\lambda_1 = \lambda_2 = \lambda$ with **two** linearly independent eigenvectors (occurs only when $\mathbf{A} = \lambda\mathbf{I}$). Every direction is an eigenvector direction; all trajectories are straight lines through the origin. Stable if $\lambda < 0$, unstable if $\lambda > 0$.

**3. Saddle Point** — two real eigenvalues of opposite signs ($\lambda_1 < 0 < \lambda_2$). Some trajectories approach the origin (along the stable eigenvector direction), others diverge (along the unstable eigenvector direction). Always **unstable**.

**4. Center** — purely imaginary eigenvalues $\lambda = \pm i\beta$ ($\beta \neq 0$, i.e., $\alpha = 0$). Trajectories are closed ellipses around the origin — perpetual oscillation with no amplitude change. **Stable** but not asymptotically stable.

**5. Spiral Point** — complex eigenvalues $\lambda = \alpha \pm i\beta$ with $\alpha \neq 0$, $\beta \neq 0$. Trajectories spiral inward (stable, $\alpha < 0$) or outward (unstable, $\alpha > 0$).

---

#### 6. Complete Phase Portrait Classification Table

| Eigenvalues | Type | Stability |
|------------|------|-----------|
| $\lambda_1, \lambda_2$ real, same sign, distinct | Improper node | Stable ($\lambda_i < 0$) / Unstable ($\lambda_i > 0$) |
| $\lambda_1 = \lambda_2$, defective (one eigenvector) | Improper node | Stable ($\lambda < 0$) / Unstable ($\lambda > 0$) |
| $\lambda_1 = \lambda_2 = \lambda$, $\mathbf{A} = \lambda\mathbf{I}$ (two eigenvectors) | Proper node (star node) | Stable ($\lambda < 0$) / Unstable ($\lambda > 0$) |
| $\lambda_1 < 0 < \lambda_2$ (real, opposite signs) | Saddle point | Always unstable |
| $\lambda = \pm i\beta$, $\alpha = 0$ | Center | Stable (not asymptotically) |
| $\lambda = \alpha \pm i\beta$, $\alpha \neq 0$ | Spiral point | Stable ($\alpha < 0$) / Unstable ($\alpha > 0$) |

**Quick classification using $p = \text{tr}\,\mathbf{A}$ and $q = \det\mathbf{A}$, $D = p^2 - 4q$:**

| $q$ | $p$ | $D$ | Type |
|-----|-----|-----|------|
| $< 0$ | any | $> 0$ | Saddle point |
| $> 0$ | $\neq 0$ | $> 0$ | Improper node |
| $> 0$ | $\neq 0$ | $= 0$ | Improper node (defective) or proper node |
| $> 0$ | $\neq 0$ | $< 0$ | Spiral point |
| $> 0$ | $= 0$ | $< 0$ | Center |

---

#### 7. Worked Examples — One per Classification Type

**Example A — Stable Improper Node** (distinct real eigenvalues, $\lambda_1 < \lambda_2 < 0$)

$\mathbf{A} = \begin{pmatrix}-3 & 1 \\ 1 & -3\end{pmatrix}$. $p = -6$, $q = 8 > 0$, $D = 36 - 32 = 4 > 0$ → improper node.

$\lambda^2 + 6\lambda + 8 = (\lambda+2)(\lambda+4) = 0$. $\lambda_1 = -2$, $\lambda_2 = -4$.

$\mathbf{v}^{(1)} = \begin{pmatrix}1\\1\end{pmatrix}$, $\mathbf{v}^{(2)} = \begin{pmatrix}1\\-1\end{pmatrix}$.

$$\mathbf{y}(t) = c_1\begin{pmatrix}1\\1\end{pmatrix}e^{-2t} + c_2\begin{pmatrix}1\\-1\end{pmatrix}e^{-4t}.$$

All trajectories approach the origin tangent to $\mathbf{v}^{(1)}$ (slower mode $e^{-2t}$ dominates as $t\to\infty$).

---

**Example B — Saddle Point** ($\lambda_1 < 0 < \lambda_2$)

$\mathbf{A} = \begin{pmatrix}1 & 1 \\ 4 & 1\end{pmatrix}$. $p = 2$, $q = -3 < 0$ → saddle point.

$\lambda^2 - 2\lambda - 3 = (\lambda-3)(\lambda+1) = 0$. $\lambda_1 = 3$, $\lambda_2 = -1$.

$\mathbf{v}^{(1)} = \begin{pmatrix}1\\2\end{pmatrix}$, $\mathbf{v}^{(2)} = \begin{pmatrix}1\\-2\end{pmatrix}$.

$$\mathbf{y}(t) = c_1\begin{pmatrix}1\\2\end{pmatrix}e^{3t} + c_2\begin{pmatrix}1\\-2\end{pmatrix}e^{-t}.$$

With $\mathbf{y}(0) = \begin{pmatrix}3\\-2\end{pmatrix}$: $c_1 = 1$, $c_2 = 2$.
$$\mathbf{y}(t) = \begin{pmatrix}e^{3t}+2e^{-t}\\2e^{3t}-4e^{-t}\end{pmatrix}.$$
As $t\to\infty$: grows along $\mathbf{v}^{(1)}$ since $c_1 \neq 0$.

---

**Example C — Center** ($\lambda = \pm i\beta$)

$\mathbf{A} = \begin{pmatrix}0 & 1 \\ -4 & 0\end{pmatrix}$. $p = 0$, $q = 4 > 0$, $D = -16 < 0$ → center.

$\lambda^2 + 4 = 0$. $\lambda = \pm 2i$. Eigenvector for $\lambda = 2i$: $\mathbf{v} = \begin{pmatrix}1\\2i\end{pmatrix}$, so $\mathbf{a} = \begin{pmatrix}1\\0\end{pmatrix}$, $\mathbf{b} = \begin{pmatrix}0\\2\end{pmatrix}$.

$$\mathbf{y}(t) = c_1\begin{pmatrix}\cos 2t \\ -2\sin 2t\end{pmatrix} + c_2\begin{pmatrix}\sin 2t \\ 2\cos 2t\end{pmatrix}.$$

Trajectories are closed ellipses; the system oscillates at frequency $\beta = 2$ rad/s. Corresponds to the undamped oscillator $\ddot{y} + 4y = 0$ (Week 9).

---

**Example D — Stable Spiral Point** ($\lambda = \alpha \pm i\beta$, $\alpha < 0$)

$\mathbf{A} = \begin{pmatrix}-1 & -2 \\ 2 & -1\end{pmatrix}$. $p = -2$, $q = 5 > 0$, $D = 4 - 20 = -16 < 0$, $p < 0$ → stable spiral.

$\lambda^2 + 2\lambda + 5 = 0$. $\lambda = -1 \pm 2i$.

Eigenvector for $\lambda = -1+2i$: $\mathbf{v} = \begin{pmatrix}1\\-i\end{pmatrix}$, so $\mathbf{a} = \begin{pmatrix}1\\0\end{pmatrix}$, $\mathbf{b} = \begin{pmatrix}0\\-1\end{pmatrix}$.

$$\mathbf{y}(t) = e^{-t}\!\left[c_1\begin{pmatrix}\cos 2t\\\sin 2t\end{pmatrix} + c_2\begin{pmatrix}\sin 2t\\-\cos 2t\end{pmatrix}\right].$$

Trajectories spiral inward; corresponds to the damped oscillator $\ddot{y}+2\dot{y}+5y=0$ (underdamped, Week 9).

---

**Example E — Unstable Spiral Point** ($\lambda = \alpha \pm i\beta$, $\alpha > 0$)

$\mathbf{A} = \begin{pmatrix}1 & -2 \\ 2 & 1\end{pmatrix}$. $p = 2 > 0$, $q = 5 > 0$, $D = 4-20 < 0$ → unstable spiral.

$\lambda = 1 \pm 2i$. General solution has the same eigenvector structure as Example D but with $e^{t}$ instead of $e^{-t}$:
$$\mathbf{y}(t) = e^{t}\!\left[c_1\begin{pmatrix}\cos 2t\\\sin 2t\end{pmatrix} + c_2\begin{pmatrix}-\sin 2t\\\cos 2t\end{pmatrix}\right].$$

Trajectories spiral outward.

---

**Example F — Proper Node (Star Node)** (repeated eigenvalue, $\mathbf{A} = \lambda\mathbf{I}$)

$\mathbf{A} = \begin{pmatrix}-3 & 0 \\ 0 & -3\end{pmatrix} = -3\mathbf{I}$. $\lambda_1 = \lambda_2 = -3$; every nonzero vector is an eigenvector.

$$\mathbf{y}(t) = e^{-3t}\begin{pmatrix}c_1\\c_2\end{pmatrix}.$$

Trajectories are straight rays through the origin, all contracting at the same rate. Stable proper node.

---

**Example G — Improper Node (Defective, Repeated Eigenvalue)**

$\mathbf{A} = \begin{pmatrix}-2 & 1 \\ 0 & -2\end{pmatrix}$. $p = -4$, $q = 4$, $D = 16-16 = 0$ → repeated eigenvalue $\lambda = -2$, defective.

One eigenvector: $(\mathbf{A}+2\mathbf{I})\mathbf{v} = \begin{pmatrix}0&1\\0&0\end{pmatrix}\mathbf{v} = \mathbf{0}$ → $\mathbf{v} = \begin{pmatrix}1\\0\end{pmatrix}$.

Generalised eigenvector $\mathbf{u}$: $(\mathbf{A}+2\mathbf{I})\mathbf{u} = \mathbf{v}$ → $\begin{pmatrix}0&1\\0&0\end{pmatrix}\mathbf{u} = \begin{pmatrix}1\\0\end{pmatrix}$ → $\mathbf{u} = \begin{pmatrix}0\\1\end{pmatrix}$.

$$\mathbf{y}(t) = c_1\begin{pmatrix}1\\0\end{pmatrix}e^{-2t} + c_2\left(\begin{pmatrix}1\\0\end{pmatrix}t + \begin{pmatrix}0\\1\end{pmatrix}\right)e^{-2t}.$$

Stable improper node; all trajectories become tangent to the eigenvector $\mathbf{v} = \begin{pmatrix}1\\0\end{pmatrix}$ as $t\to\infty$ (since $te^{-2t}\to 0$).

---

#### 8. Connection to Week 9 — Oscillation Systems

For the undamped mass-spring ODE $\ddot{y} + \omega_0^2 y = 0$, the companion system has:
$$\mathbf{A} = \begin{pmatrix}0 & 1 \\ -\omega_0^2 & 0\end{pmatrix}, \qquad \text{tr}\,\mathbf{A} = 0, \quad \det\mathbf{A} = \omega_0^2 > 0.$$

Eigenvalues: $\lambda = \pm i\omega_0$ → **center** in the phase plane. The closed elliptic trajectories correspond to the perpetual oscillation $y = R\cos(\omega_0 t - \delta)$ of Week 9.

For the damped case ($c > 0$): $\text{tr}\,\mathbf{A} = -c/m < 0$, $\det\mathbf{A} = k/m > 0$ → **stable spiral** (underdamped) or **stable node** (overdamped/critical). This gives a unified geometric picture of everything in Week 9 Lecture 1.

---

#### 9. Summary — Lecture 3

**Eigenvalue method:**
$$\det(\mathbf{A} - \lambda\mathbf{I}) = 0 \;\to\; \lambda_k \;\to\; \mathbf{v}^{(k)} \;\to\; \mathbf{y}^{(k)} = \mathbf{v}^{(k)}e^{\lambda_k t} \;\to\; \mathbf{y} = \sum_k c_k\mathbf{y}^{(k)}.$$

**Phase portrait summary:**

| $q = \det\mathbf{A}$ | $p = \text{tr}\,\mathbf{A}$ | $D = p^2 - 4q$ | Type | Stable? |
|---------------------|-----------------------------|----------------|------|---------|
| $< 0$ | any | $> 0$ | Saddle | No |
| $> 0$ | $< 0$ | $> 0$ | Stable node | Yes |
| $> 0$ | $> 0$ | $> 0$ | Unstable node | No |
| $> 0$ | $< 0$ | $< 0$ | Stable spiral | Yes |
| $> 0$ | $> 0$ | $< 0$ | Unstable spiral | No |
| $> 0$ | $= 0$ | $< 0$ | Center | Neutral |

---

## Practice Session

**Theme:** Converting ODEs to systems; eigenvalue method; phase plane classification; IVP solutions.

---

### Practice Problems

**Set A — Converting Higher-Order ODEs**

1. Convert each ODE to a first-order system $\mathbf{y}' = \mathbf{A}\mathbf{y} + \mathbf{g}$ and write $\mathbf{A}$ explicitly:
   (a) $y'' - 3y' + 2y = e^t$
   (b) $y'' + \omega_0^2 y = 0$ (undamped oscillator)
   (c) $y'' + 2\zeta\omega_0 y' + \omega_0^2 y = 0$ (damped oscillator; express $\mathbf{A}$ in terms of $\zeta$, $\omega_0$)
   (d) $y''' - y'' - y' + y = 0$ (3×3 system)

2. For the companion matrix of $y'' + py' + qy = 0$, verify that its eigenvalues are the same as the roots of the characteristic equation $\lambda^2 + p\lambda + q = 0$.

**Set B — Eigenvalue Method and General Solutions**

3. Find the general solution using the eigenvalue method:
   (a) $\mathbf{y}' = \begin{pmatrix}2 & 1 \\ 0 & 3\end{pmatrix}\mathbf{y}$
   (b) $\mathbf{y}' = \begin{pmatrix}-1 & 2 \\ -2 & -1\end{pmatrix}\mathbf{y}$
   (c) $\mathbf{y}' = \begin{pmatrix}3 & -2 \\ 2 & -2\end{pmatrix}\mathbf{y}$
   (d) $\mathbf{y}' = \begin{pmatrix}2 & 1 \\ -1 & 4\end{pmatrix}\mathbf{y}$ (repeated eigenvalue)

4. Solve the IVP:
   $$\mathbf{y}' = \begin{pmatrix}4 & -2 \\ 1 & 1\end{pmatrix}\mathbf{y}, \qquad \mathbf{y}(0) = \begin{pmatrix}3 \\ 0\end{pmatrix}.$$

5. Find the general solution of $\mathbf{y}' = \begin{pmatrix}0 & 1 \\ -4 & 0\end{pmatrix}\mathbf{y}$ and identify the phase portrait type. What is the period of oscillation?

**Set C — Phase Plane Classification**

6. Classify the critical point at the origin without finding the explicit solution:
   (a) $\mathbf{A} = \begin{pmatrix}2 & 3 \\ 0 & -1\end{pmatrix}$
   (b) $\mathbf{A} = \begin{pmatrix}-2 & -5 \\ 1 & -2\end{pmatrix}$
   (c) $\mathbf{A} = \begin{pmatrix}1 & 4 \\ -1 & -3\end{pmatrix}$
   (d) $\mathbf{A} = \begin{pmatrix}0 & 3 \\ -3 & 0\end{pmatrix}$

7. A 2×2 system has $\text{tr}\,\mathbf{A} = -4$ and $\det\mathbf{A} = 5$. Classify the critical point and state its stability.

8. Determine the values of the parameter $k$ for which the system $\mathbf{y}' = \begin{pmatrix}k & 1 \\ -1 & k\end{pmatrix}\mathbf{y}$ is asymptotically stable at the origin.

**Set D — Engineering Applications**

9. Two coupled masses with $m_1 = m_2 = 1$, $k_1 = k_3 = 2$, $k_2 = 3$ N/m:
   (a) Write the equations of motion in matrix form.
   (b) Find the two normal mode frequencies.
   (c) Describe the physical motion in each mode.

10. Two tanks: Tank 1 has volume 100 L, Tank 2 has volume 50 L. Brine flows from Tank 1 to Tank 2 at 3 L/min and from Tank 2 to Tank 1 at 1 L/min (and out at 2 L/min). Initially: Tank 1 has 10 kg salt, Tank 2 has 0 kg.
    (a) Write the 2×2 system for salt amounts $y_1(t)$, $y_2(t)$.
    (b) Find the eigenvalues and classify the long-term behaviour.
    (c) Solve the IVP and find the salt amounts as $t \to \infty$.

**Set E — Wronskian and Theory**

11. For the system in Problem 3(a):
    (a) Compute $W(t)$ directly from the two solution vectors.
    (b) Verify Abel's formula: $W(t) = W(0)e^{(\text{tr}\,\mathbf{A})t}$.

12. Prove: if $\lambda_1 \neq \lambda_2$ are eigenvalues of $\mathbf{A}$ with eigenvectors $\mathbf{v}^{(1)}$, $\mathbf{v}^{(2)}$, then $\mathbf{v}^{(1)}$ and $\mathbf{v}^{(2)}$ are linearly independent.
    (Hint: suppose $c_1\mathbf{v}^{(1)} + c_2\mathbf{v}^{(2)} = \mathbf{0}$ and apply $(\mathbf{A} - \lambda_2\mathbf{I})$ to both sides.)
