# Week 3 — Parametric Equations & Polar Coordinates

**Course:** Engineering Mathematics 1
**Part:** I — Calculus Foundations (Review)
**Supplementary Material:** `03 parametric equations and polar coordinates.pdf`

> **Backward links from Week 2:**
> - Parametric arc length $\int\sqrt{\dot x^2+\dot y^2}\,dt$ and surface area often require **trig substitution** (Week 2 Lecture 3, §16–17).
> - Polar area $\frac{1}{2}\int r^2\,d\theta$ and arc length $\int\sqrt{r^2+(r')^2}\,d\theta$ use **trig identities and reduction formulas** (Week 2 Lecture 3, §11–15).
> - The conic section eccentricity derivation uses **completing the square** (Week 2 Lecture 3, §1–2).
>
> **Forward link:** The polar representation $re^{i\theta}$ is introduced here as a preview and will be formalized with Euler's Formula in Week 7.

---

## Lecture 1: Parametric Curves — Calculus and Geometry

### Introduction

When we write $y = f(x)$ we implicitly assume a single value of $x$ determines the point on the curve. Many engineering curves violate this: the path of a projectile loops and retraces, the shape of a cycloid gear tooth cannot be expressed as a function, and robot arm trajectories require specifying position as a function of time rather than one coordinate in terms of the other. **Parametric equations** escape this restriction by expressing both $x$ and $y$ as functions of an independent parameter $t$, tracing the curve dynamically.

This lecture develops the complete calculus of parametric curves: slopes, concavity, curvature, arc length, area, and surface area — all without eliminating the parameter.

**Why it matters in engineering:**
- Kinematics uses $x(t),y(t)$ directly; $\dot x$ and $\dot y$ are velocity components.
- CNC machines and robotic arms are programmed in parametric form.
- The cycloid is the brachistochrone — the curve of fastest descent — and governs gear tooth design.
- Arc length integrals give travel distance, cable length, and wavefront propagation.

---

### Knowledge Points

---

#### 1. What Are Parametric Equations?

**Definition:** A **parametric curve** is defined by continuous functions
$$x = x(t), \qquad y = y(t), \qquad t \in [\alpha, \beta].$$
Each value of $t$ yields a point $(x(t), y(t))$ in the plane; as $t$ sweeps its domain the point traces the curve.

**Why not just use $y = f(x)$?** A function requires a unique $y$ for each $x$. Parametric form has no such restriction — the curve may self-intersect, loop, or double back.

**Intuition:** Think of $t$ as time and $(x(t), y(t))$ as the position of a moving particle. The parametric equations encode both the **path** and the **speed of traversal** along it.

**Example 1 — Unit circle:** $x = \cos t$, $y = \sin t$, $t \in [0, 2\pi]$. As $t$ increases the point moves counterclockwise. No single-valued $y = f(x)$ describes the full circle.

**Example 2 — Line:** $x = 1 + 3t$, $y = 2 + 4t$. Eliminating $t$: $4x - 3y = -2$.

**Example 3 — Cycloid:** $x = r(t - \sin t)$, $y = r(1 - \cos t)$ — the path traced by a point on the rim of a wheel of radius $r$ rolling along the $x$-axis. No closed-form Cartesian equation exists.

---

#### 2. Eliminating the Parameter

**Method:** Solve $x = x(t)$ for $t$ and substitute into $y = y(t)$ to get a Cartesian relation.

**Example — Power curve:** $x = t^2$, $y = t^3$, $t \geq 0$. Then $t = \sqrt{x}$, so $y = x^{3/2}$.

**Example — Ellipse:** $x = 3\cos t$, $y = 2\sin t$. Then
$$\frac{x^2}{9} + \frac{y^2}{4} = \cos^2 t + \sin^2 t = 1.$$

**When elimination is impossible or inconvenient:**
- The cycloid: $t - \sin t = x/r$ cannot be inverted for $t$ in closed form.
- Even when elimination succeeds, the parametric form is better for arc length and area calculations.

**Key warning:** Eliminating the parameter may lose the orientation (direction of traversal) or may capture only part of the original curve. Example: $x = t^2$, $y = t$ gives $x = y^2$, but only the branch $x \geq 0$ is represented, and the direction $t$ increasing = $y$ increasing is encoded only in the parametric form.

---

#### 3. First Derivative — Slope of a Parametric Curve

**Goal:** Find $dy/dx$ for $x = x(t)$, $y = y(t)$.

Applying the chain rule to $y = y(x(t))$:
$$\frac{dy}{dx} = \frac{dy/dt}{dx/dt}, \qquad \text{provided } \frac{dx}{dt} \neq 0.$$

**Intuition:** $dy/dt$ is the vertical rate of change; $dx/dt$ is the horizontal rate. Slope is their ratio.

**Example 1 — Cycloid** $x = t - \sin t$, $y = 1 - \cos t$:
$$\frac{dy}{dx} = \frac{\sin t}{1 - \cos t}.$$
At $t = \pi/2$: slope $= 1/(1-0) = 1$.

**Example 2 — Ellipse** $x = 3\cos t$, $y = 2\sin t$:
$$\frac{dy}{dx} = \frac{2\cos t}{-3\sin t} = -\frac{2\cos t}{3\sin t}.$$
At $t = \pi/4$: slope $= -2/3$.

---

#### 4. Horizontal and Vertical Tangents

- **Horizontal tangent** ($dy/dx = 0$): $\dot y = 0$ **and** $\dot x \neq 0$.
- **Vertical tangent** ($|dy/dx| \to \infty$): $\dot x = 0$ **and** $\dot y \neq 0$.
- **Cusp or indeterminate:** both $\dot x = 0$ and $\dot y = 0$ — analyse via $\lim_{t \to t_0} \dot y / \dot x$.

**Example — Cycloid** $x = t - \sin t$, $y = 1 - \cos t$:
- $\dot y = \sin t = 0$ at $t = 0, \pi, 2\pi, \ldots$
- $\dot x = 1 - \cos t = 0$ only at $t = 0, 2\pi, 4\pi, \ldots$
- At $t = \pi$: $\dot y = 0$, $\dot x = 2 \neq 0$ → **horizontal tangent** at $(\pi, 2)$.
- At $t = 0$: $\dot x = \dot y = 0$ → **cusp**. Check: $\dot y/\dot x = \sin t/(1-\cos t) \to 0/0$; L'Hôpital gives $\cos t/\sin t \to \pm\infty$ → vertical tangent direction at cusp.

---

#### 5. Second Derivative and Concavity

**Definition (concavity for parametric curves):** The curve is **concave up** on an interval if the slope $dy/dx$ is *increasing* as $x$ increases; **concave down** if $dy/dx$ is *decreasing*. This requires no assumption on the existence of $d^2y/dx^2$.

**Computing $d^2y/dx^2$:** Let $\varphi(t) = dy/dx = \dot y/\dot x$. Then:
$$\frac{d^2 y}{dx^2} = \frac{d\varphi/dt}{dx/dt} = \frac{\dot\varphi}{\dot x}.$$

**Warning:** $d^2y/dx^2 \neq \ddot y/\ddot x$.

**Corollary:** When $d^2y/dx^2 > 0$ the slope $dy/dx$ is increasing (concave up); when $< 0$ it is decreasing (concave down).

**Example:** $x = t^2$, $y = t^3$.
$$\frac{dy}{dx} = \frac{3t^2}{2t} = \frac{3t}{2}, \qquad \frac{d^2y}{dx^2} = \frac{3/2}{2t} = \frac{3}{4t}.$$
- $t > 0$: $d^2y/dx^2 > 0$ → $dy/dx = 3t/2$ increasing → concave up.
- $t < 0$: $d^2y/dx^2 < 0$ → concave down.
- Inflection at $t = 0$ (the origin), confirmed by sign change.

---

#### 6. Speed, Velocity Vector, and the Unit Tangent

**Physical interpretation:** If $t$ is time, then the **velocity vector** is:
$$\mathbf{v}(t) = (\dot x(t),\, \dot y(t)).$$
Its magnitude is the **speed**:
$$v(t) = |\mathbf{v}(t)| = \sqrt{[\dot x(t)]^2 + [\dot y(t)]^2}.$$

**Unit tangent vector:** $\mathbf{T}(t) = \mathbf{v}/v$ — a unit vector pointing in the direction of motion.

**Acceleration vector:** $\mathbf{a}(t) = (\ddot x(t), \ddot y(t))$.

**Example — Projectile:** $x = v_0\cos\alpha\cdot t$, $y = v_0\sin\alpha\cdot t - \frac{1}{2}gt^2$.
$$\dot x = v_0\cos\alpha, \quad \dot y = v_0\sin\alpha - gt, \quad v(t) = \sqrt{v_0^2 - 2v_0 gt\sin\alpha + g^2t^2}.$$
Maximum height when $\dot y = 0$: $t^* = v_0\sin\alpha/g$. At this point the speed equals $v_0\cos\alpha$ (horizontal only).

**Example — Cycloid** $x = t - \sin t$, $y = 1 - \cos t$:
$$v(t) = \sqrt{(1-\cos t)^2 + \sin^2 t} = \sqrt{2-2\cos t} = 2\left|\sin\frac{t}{2}\right|.$$
Speed is zero at $t = 0, 2\pi, \ldots$ (cusps — wheel momentarily stationary) and maximum $= 2$ at $t = \pi$ (top of arch).

---

#### 7. Arc Length of a Parametric Curve

**Derivation via general partition:** Let $P = \{t_0, t_1, \ldots, t_n\}$ be a partition of $[\alpha,\beta]$ with mesh $\|P\| = \max_i \Delta t_i$. The chord length on $[t_{i-1}, t_i]$ is
$$\sqrt{(\Delta x_i)^2 + (\Delta y_i)^2} \approx \sqrt{[\dot x(t_i^*)]^2 + [\dot y(t_i^*)]^2}\,\Delta t_i$$
by the MVT. Summing and taking $\|P\| \to 0$:
$$\boxed{L = \int_\alpha^\beta \sqrt{[\dot x(t)]^2 + [\dot y(t)]^2}\,dt}$$

Note: arc length $= \int v(t)\,dt$ — the total distance travelled at speed $v(t)$.

**Example 1 — Circumference** $x = r\cos t$, $y = r\sin t$, $t \in [0, 2\pi]$:
$$L = \int_0^{2\pi} r\,dt = 2\pi r.\checkmark$$

**Example 2 — One arch of the cycloid** $x = t - \sin t$, $y = 1 - \cos t$, $t \in [0, 2\pi]$:
$$\dot x^2 + \dot y^2 = 4\sin^2(t/2), \qquad L = \int_0^{2\pi} 2\sin\frac{t}{2}\,dt = 8.$$
One arch (unit wheel radius) has length $8$ — four times the wheel's diameter.

---

#### 8. Area Under and Enclosed by a Parametric Curve

**Area under the curve** (traced left-to-right, $\dot x > 0$, above $x$-axis):
$$A = \int_a^b y\,dx = \int_\alpha^\beta y(t)\,\dot x(t)\,dt.$$

**Enclosed area** (closed curve, counterclockwise) via the shoelace integral:
$$A = \frac{1}{2}\left|\int_\alpha^\beta \bigl(x(t)\dot y(t) - y(t)\dot x(t)\bigr)dt\right|.$$

**Example — Area under one arch of the cycloid:**
$$A = \int_0^{2\pi}(1-\cos t)^2\,dt = \int_0^{2\pi}(1 - 2\cos t + \cos^2 t)\,dt = 3\pi.$$
Three times the area of the rolling circle — a famous result.

**Example — Ellipse** $x = 3\cos t$, $y = 2\sin t$:
$$A = \frac{1}{2}\left|\int_0^{2\pi}(6\cos^2 t + 6\sin^2 t)\,dt\right| = 6\pi = \pi ab.\checkmark$$

---

#### 9. Surface Area of Revolution

Rotating $x = x(t)$, $y = y(t) \geq 0$, $t\in[\alpha,\beta]$ about the $x$-axis:
$$S = 2\pi\int_\alpha^\beta y(t)\sqrt{[\dot x(t)]^2 + [\dot y(t)]^2}\,dt.$$

Each arc element $ds = v(t)\,dt$ generates a band of circumference $2\pi y$.

**Example — Sphere:** Rotate upper semicircle $x = r\cos t$, $y = r\sin t$, $t\in[0,\pi]$:
$$S = 2\pi\int_0^\pi r\sin t\cdot r\,dt = 2\pi r^2\cdot 2 = 4\pi r^2.\checkmark$$

---

#### 10. Lissajous Figures

**Definition:** A **Lissajous figure** is the curve traced by:
$$x = A\sin(\omega_1 t + \phi), \qquad y = B\sin(\omega_2 t)$$
where $\omega_1, \omega_2$ are angular frequencies and $\phi$ is a phase shift.

**Structure:**
- If $\omega_1/\omega_2$ is rational, the curve is closed and periodic.
- The shape depends on the frequency ratio and phase.

| $\omega_1:\omega_2$ | $\phi$ | Shape |
|---------------------|--------|-------|
| $1:1$ | $0$ | Line |
| $1:1$ | $\pi/2$ | Ellipse (circle if $A=B$) |
| $2:1$ | $0$ | Figure-eight |
| $2:1$ | $\pi/2$ | Parabolic arc |
| $3:2$ | $\pi/4$ | Complex closed curve |

**Engineering applications:**
- **Oscilloscope:** Lissajous figures are displayed when two sinusoidal signals drive the $x$ and $y$ channels. Used to measure frequency ratios and phase differences.
- **Vibration analysis:** When two perpendicular vibration modes are present, the resulting trajectory is a Lissajous figure. The frequency ratio is immediately readable from the figure.
- **Control systems:** Lissajous testing verifies the linearity of a system by checking whether the input-output Lissajous figure is an ellipse.

---

#### 11. Worked Example — Full Analysis of an Ellipse

**Curve:** $x = 3\cos t$, $y = 2\sin t$, $t \in [0, 2\pi]$.

1. **Cartesian form:** $x^2/9 + y^2/4 = 1$ — ellipse, semi-axes $a=3$, $b=2$.
2. **Slope:** $dy/dx = -2\cos t/(3\sin t)$.
3. **Horizontal tangents** ($\dot y = 0$): $t = \pi/2, 3\pi/2$ → $(0, 2)$, $(0, -2)$.
4. **Vertical tangents** ($\dot x = 0$): $t = 0, \pi$ → $(3, 0)$, $(-3, 0)$.
5. **Concavity:** $d^2y/dx^2 = -2/(9\sin^3 t)$. Upper half ($\sin t > 0$): $d^2y/dx^2 < 0$ → slope decreasing → concave down. Lower half: concave up.
6. **Speed:** $v = \sqrt{9\sin^2 t + 4\cos^2 t}$. Maximum at $t = \pi/2$: $v = 3$.
7. **Arc length:** $L = \int_0^{2\pi}\sqrt{9\sin^2 t+4\cos^2 t}\,dt$ — elliptic integral.
8. **Area:** $A = 6\pi = \pi ab$.

---

#### 12. Summary — Lecture 1

| Quantity | Formula |
|----------|---------|
| Slope | $dy/dx = \dot y/\dot x$ |
| Concavity | $dy/dx$ increasing (up) or decreasing (down); corollary $d^2y/dx^2 = \dot\varphi/\dot x$ |
| Speed | $v = \sqrt{\dot x^2 + \dot y^2}$ |
| Arc length | $\int_\alpha^\beta v\,dt$ |
| Area under curve | $\int_\alpha^\beta y\dot x\,dt$ |
| Enclosed area | $\tfrac{1}{2}\left|\int_\alpha^\beta \bigl(x(t)\dot y(t) - y(t)\dot x(t)\bigr)dt\right|$ |
| Surface of revolution | $2\pi\int y\,v\,dt$ |

---

## Lecture 2: Polar Coordinate System

### Introduction

Cartesian coordinates describe location by horizontal and vertical displacement. But many physical phenomena — gravitational fields, antenna radiation patterns, planetary orbits, stress fields around circular holes — have **radial symmetry**: what matters is the distance from a center and the direction. **Polar coordinates** express points by radius $r$ and angle $\theta$, making such problems far more natural.

This lecture develops polar coordinates from scratch, introduces the main families of polar curves with detailed analysis, and presents the preview $re^{i\theta}$, which connects polar geometry to complex analysis and Euler's Formula (Week 7).

**Why it matters in engineering:**
- Antenna radiation patterns, Nyquist diagrams, and Smith charts use polar/complex representations.
- Stress around circular holes (Lamé problem) and magnetic fields of wires are polar by nature.
- Every planetary orbit is a conic section with the focus at the origin.

---

### Knowledge Points

---

#### 1. Polar Coordinates — Definition and Conversion

A point $P$ is located by:
- $r$: radial distance from the origin (the **pole**)
- $\theta$: angle counterclockwise from the positive $x$-axis

**Conversion formulas:**
$$x = r\cos\theta, \quad y = r\sin\theta, \quad r = \sqrt{x^2+y^2}, \quad \tan\theta = y/x \text{ (with quadrant check).}$$

**Example 1 — Polar to Cartesian:** $(2, \pi/3)$:
$x = 2\cdot\frac{1}{2} = 1$, $y = 2\cdot\frac{\sqrt{3}}{2} = \sqrt{3}$.

**Example 2 — Cartesian to polar:** $(-1, -\sqrt{3})$:
$r = 2$; point in Quadrant III: $\theta = \pi + \pi/3 = 4\pi/3$.

**Negative $r$:** $(r,\theta)$ and $(-r,\theta+\pi)$ represent the same point. Allowing $r < 0$ extends the usefulness of some curve equations.

---

#### 2. Non-Uniqueness of Polar Representation

$(r,\theta) \equiv (r, \theta+2\pi k)$ for any integer $k$, and $(r,\theta) \equiv (-r,\theta+\pi)$.

**Consequence for intersections:** Two curves may intersect even if their equations never give the same $(r,\theta)$ pair simultaneously. Always check:
1. **Algebraic:** $r_1(\theta) = r_2(\theta)$.
2. **Pole:** both may have $r = 0$ at different angles.
3. **Shifted form:** $(r,\theta)$ equals $(-r,\theta+\pi)$ on the other curve.

---

#### 3. Converting Polar Equations to Cartesian

Use $r^2 = x^2+y^2$, $r\cos\theta = x$, $r\sin\theta = y$ to convert.

**Strategy:** Multiply both sides by $r$ if needed to introduce $r^2 = x^2+y^2$.

**Example 1:** $r = 2a\cos\theta$. Multiply by $r$: $r^2 = 2ar\cos\theta \Rightarrow x^2+y^2 = 2ax \Rightarrow (x-a)^2+y^2 = a^2$.
A circle of radius $|a|$ centred at $(a, 0)$. Passes through origin.

**Example 2:** $r = \sec\theta$. Then $r\cos\theta = 1 \Rightarrow x = 1$. A vertical line.

**Example 3:** $r = 2/(1 - \cos\theta)$. Multiply: $r - r\cos\theta = 2 \Rightarrow r = 2 + x$.
Square: $x^2+y^2 = (2+x)^2 = 4+4x+x^2 \Rightarrow y^2 = 4+4x = 4(1+x)$. A parabola with vertex at $(-1,0)$, focus at origin.

**Example 4:** $\theta = \pi/4$. Then $y/x = \tan(\pi/4) = 1 \Rightarrow y = x$ (for $x > 0$).

---

#### 4. Common Polar Curves

| Curve | Equation | Shape |
|-------|----------|-------|
| Circle (origin) | $r = a$ | Radius $|a|$, centred at origin |
| Circle (on axis) | $r = 2a\cos\theta$ | Radius $|a|$, passes through origin |
| Cardioid | $r = a(1\pm\cos\theta)$ | Heart-shaped, passes through pole |
| Limaçon | $r = a + b\cos\theta$ | Shape depends on $a/b$ ratio |
| Rose ($n$ odd) | $r = a\cos(n\theta)$ | $n$ petals |
| Rose ($n$ even) | $r = a\cos(n\theta)$ | $2n$ petals |
| Lemniscate | $r^2 = a^2\cos(2\theta)$ | Figure-eight |
| Archimedean spiral | $r = a\theta$ | Uniformly-spaced coils |

**Sketching strategy:** Table of $(θ, r)$ at $0, \pi/6, \pi/4, \pi/3, \pi/2, \ldots$; locate zeros and maxima; apply symmetry.

---

#### 5. Limaçons — Detailed Analysis

The **limaçon** $r = a + b\cos\theta$ (with $a, b > 0$) has three distinct shapes depending on the ratio $a/b$:

| Condition | Shape | Description |
|-----------|-------|-------------|
| $a \geq 2b$ | Convex | No dimple or inner loop; widest case |
| $b < a < 2b$ | Dimpled | Concave indentation, no inner loop |
| $a = b$ | Cardioid | Exactly passes through pole at $\theta = \pi$ |
| $a < b$ | Inner loop | The curve crosses itself; inner loop on the left |

**Why the inner loop?** When $a < b$, $r = a + b\cos\theta < 0$ for $\theta$ near $\pi$. The negative-$r$ portion plots as a loop in the direction $\theta + \pi$ — wrapping inside the outer curve.

**Finding the inner loop:** It is traced where $r \leq 0$, i.e., $\cos\theta \leq -a/b$, i.e., $\theta\in[\arccos(-a/b),\, 2\pi - \arccos(-a/b)]$.

**Example: $r = 1 + 2\cos\theta$ ($a=1$, $b=2$, inner loop since $a < b$) — full sketching procedure:**

**Step 1 (Symmetry):** $r(-\theta) = 1+2\cos\theta = r(\theta)$ → symmetric about polar axis. Build table for $\theta\in[0,\pi]$ only, then reflect.

**Step 2 (Zeros and maxima):** $r=0 \Rightarrow \cos\theta = -1/2 \Rightarrow \theta = 2\pi/3$. Maximum $r=3$ at $\theta=0$; $r(\pi) = -1$ (inner loop tip at distance 1).

**Step 3 (Table):**

| $\theta$ | $0$ | $\pi/3$ | $\pi/2$ | $2\pi/3$ | $\pi$ |
|----------|-----|---------|---------|---------|-------|
| $r = 1+2\cos\theta$ | $3$ | $2$ | $1$ | $0$ | $-1$ |

**Step 4 (Sketch):** For $\theta\in[0,2\pi/3]$, $r\geq 0$: traces the outer loop upper half. For $\theta\in(2\pi/3,\pi]$, $r<0$: points plot in opposite direction, tracing the inner loop. Reflect below polar axis to complete both loops.

- Outer loop: $r \geq 0$ for $\theta\in[-2\pi/3, 2\pi/3]$.
- Inner loop: $r \leq 0$ for $\theta\in[2\pi/3, 4\pi/3]$, traced as positive $r$ in the opposite direction.

---

#### 6. Symmetry Tests and Sketching the Cardioid

**Symmetry tests:**
- **About polar axis:** $r(-\theta) = r(\theta)$.
- **About $\theta = \pi/2$:** $r(\pi-\theta) = r(\theta)$.
- **About pole:** $r(\theta+\pi) = r(\theta)$ or $= -r(\theta)$.

**Cardioid $r = 1 + \cos\theta$ — full sketching procedure:**

**Step 1 (Symmetry):** $r(-\theta) = 1+\cos\theta = r(\theta)$ → symmetric about polar axis. Build table for $\theta\in[0,\pi]$ only, then reflect.

**Step 2 (Zeros and maxima):** $r=0 \Rightarrow \cos\theta=-1 \Rightarrow \theta=\pi$ (curve touches the pole). Maximum $r=2$ at $\theta=0$ (rightmost point).

**Step 3 (Table):**

| $\theta$ | $0$ | $\pi/3$ | $\pi/2$ | $2\pi/3$ | $\pi$ |
|----------|-----|---------|---------|---------|-------|
| $r=1+\cos\theta$ | $2$ | $3/2$ | $1$ | $1/2$ | $0$ |

**Step 4 (Sketch):** Plot the five points above the polar axis — $r$ decreases monotonically from 2 to 0, tracing the upper half. Reflect below the polar axis to complete the cardioid.

Maximum $r=2$ at $\theta=0$; pinches to pole at $\theta=\pi$.

**Engineering note:** The cardioid is the radiation pattern of a directional antenna and the pickup pattern of cardioid microphones.

---

#### 7. The Rose Curve $r = a\cos(n\theta)$

**For $n$ odd:** $n$ petals traced in $\theta \in [0, \pi]$.
**For $n$ even:** $2n$ petals traced in $\theta \in [0, 2\pi]$.

**Why the doubling for even $n$?** When $n$ is even, $r$ takes negative values during the second half-period, tracing petals in the opposite direction. These are new petals (not retraced), doubling the count.

**Example — 3-petal rose $r = \cos(3\theta)$:** Zeros at $\theta = \pi/6, \pi/2, 5\pi/6, \ldots$ — petals centred at $\theta = 0, 2\pi/3, 4\pi/3$.

**Example — 4-petal rose $r = \cos(2\theta)$ — full sketching procedure:**

**Step 1 (Symmetry):** $r(-\theta) = r(\theta)$ → symmetric about polar axis. Also $r(\pi-\theta) = \cos(2\pi-2\theta) = r(\theta)$ → symmetric about $\theta=\pi/2$. Table one petal ($\theta\in[0,\pi/2]$), use symmetry for all four.

**Step 2 (Zeros and maxima):** $r=0$: $2\theta = \pi/2 \Rightarrow \theta=\pi/4$ (petal boundary). Maximum $r=1$ at $\theta=0$.

**Step 3 (Table):**

| $\theta$ | $0$ | $\pi/6$ | $\pi/4$ | $\pi/3$ | $\pi/2$ |
|----------|-----|---------|---------|---------|---------|
| $r=\cos(2\theta)$ | $1$ | $1/2$ | $0$ | $-1/2$ | $-1$ |

**Step 4 (Sketch):** $r$ decreases from $1$ to $0$ at $\theta=\pi/4$ (first petal). For $\theta\in(\pi/4,\pi/2]$, $r<0$: second petal is traced in the opposite direction. Symmetry gives the remaining two petals; $n=2$ even → $2n=4$ petals total.

---

#### 8. Tangent Lines to Polar Curves

Parametrize $r = f(\theta)$ with $\theta$ as parameter: $x = f\cos\theta$, $y = f\sin\theta$.

$$\frac{dy}{dx} = \frac{f'\sin\theta + f\cos\theta}{f'\cos\theta - f\sin\theta}$$

**Horizontal tangents:** numerator $= 0$, denominator $\neq 0$.
**Vertical tangents:** denominator $= 0$, numerator $\neq 0$.

**Example — Cardioid $r = 1+\cos\theta$:**
$dy/d\theta = (1+\cos\theta)\cos\theta - \sin^2\theta = \cos\theta + \cos2\theta$.
Setting to zero: $(2\cos\theta-1)(\cos\theta+1) = 0$ → $\theta = \pi/3, 5\pi/3$ (horizontal tangents) and $\theta = \pi$ (pole — special case).

---

#### 9. Spirals and the Lemniscate

**Archimedean spiral $r = a\theta$:** Equally-spaced coils (spacing $2\pi a$ per revolution). Used in spiral springs, vinyl record grooves, and scroll pumps. Can be unwound into a straight line by a transformation.

**Logarithmic (equiangular) spiral $r = e^{a\theta}$:** The tangent makes a constant angle $\arctan(1/a)$ with the radial direction at every point. Appears in nautilus shells, spiral galaxies, and radar antenna design. Self-similar under rotation.

**Fermat's spiral $r^2 = a^2\theta$:** Spacing decreases as $\theta$ grows — gives optimal packing, explaining the sunflower seed spiral.

**Lemniscate $r^2 = a^2\cos(2\theta)$:** Figure-eight curve; exists only where $\cos(2\theta)\geq0$, i.e., $\theta\in[-\pi/4,\pi/4]\cup[3\pi/4,5\pi/4]$. Crosses itself at origin with tangent slopes $\pm1$.

---

#### 10. Complex Numbers and the Preview $z = re^{i\theta}$

A complex number $z = x + iy$ has polar form $z = r(\cos\theta + i\sin\theta)$ with $r = |z|$ and $\theta = \arg(z)$.

**Preview of Euler's Formula** (proved in Week 7):
$$e^{i\theta} = \cos\theta + i\sin\theta \implies \boxed{z = re^{i\theta}}.$$

**Key consequences:**
- Multiplication: $z_1z_2 = r_1r_2\,e^{i(\theta_1+\theta_2)}$ — multiply moduli, add arguments.
- Rotation: multiplying by $e^{i\alpha}$ rotates every point by $\alpha$.
- Unit circle: $r=1$ is the locus $|z|=1$, traced by $e^{i\theta}$.
- **De Moivre:** $(re^{i\theta})^n = r^n e^{in\theta}$, so $(\cos\theta+i\sin\theta)^n = \cos(n\theta)+i\sin(n\theta)$.

**Example:** $(1+i)^8 = (\sqrt{2}\,e^{i\pi/4})^8 = 16\,e^{i2\pi} = 16$.

**Connection to polar curves:** The polar curve $r = f(\theta)$ is the locus of complex numbers $z = f(\theta)e^{i\theta}$ — a set in $\mathbb{C}$.

---

#### 11. Summary — Lecture 2

| Concept | Formula / Rule |
|---------|----------------|
| Polar ↔ Cartesian | $x = r\cos\theta$, $y = r\sin\theta$; $r^2 = x^2+y^2$ |
| Non-uniqueness | $(r,\theta) = (r,\theta+2\pi k) = (-r,\theta+\pi)$ |
| Polar → Cartesian | Multiply by $r$; use $r^2=x^2+y^2$, $r\cos\theta=x$, $r\sin\theta=y$ |
| Slope | $dy/dx = (r'\sin\theta + r\cos\theta)/(r'\cos\theta - r\sin\theta)$ |
| Complex form | $z = re^{i\theta}$ *(Euler's Formula, Week 7)* |
| De Moivre | $(re^{i\theta})^n = r^n e^{in\theta}$ |

---

## Lecture 3: Area and Arc Length in Polar; Conic Sections

### Introduction

With polar curves understood geometrically, we now develop the integral calculus of polar regions. The **area formula** $A = \frac{1}{2}\int r^2\,d\theta$ and the **arc length formula** $L = \int\sqrt{r^2+(r')^2}\,d\theta$ are each derived from a general partition. The lecture closes with **conic sections in polar form** — a single equation producing ellipses, parabolas, and hyperbolas from one parameter (eccentricity), with the focus at the origin.

**Why it matters:**
- Polar area encodes Kepler's Second Law: equal areas in equal times.
- Arc length in polar gives spiral antenna lengths and gear tooth profiles.
- The polar conic equation describes all planetary and satellite trajectories.

---

### Knowledge Points

---

#### 1. Polar Area Formula — Derivation via General Partition

**Setup:** Area swept by $r = f(\theta) \geq 0$ for $\theta\in[\alpha,\beta]$.

**General partition:** $P = \{\theta_0,\ldots,\theta_n\}$ with mesh $\|P\| = \max_i\Delta\theta_i$.

**Approximation:** On $[\theta_{i-1},\theta_i]$, approximate by a circular sector of radius $r(\theta_i^*)$ and angle $\Delta\theta_i$ — area $= \frac{1}{2}[r(\theta_i^*)]^2\Delta\theta_i$.

**Riemann sum:**
$$S = \sum_{i=1}^n \tfrac{1}{2}[r(\theta_i^*)]^2\Delta\theta_i.$$

Taking $\|P\|\to 0$ (independent of partition and sample point choice):
$$\boxed{A = \frac{1}{2}\int_\alpha^\beta [r(\theta)]^2\,d\theta}$$

**Example:** Circle $r = a$: $A = \frac{1}{2}\int_0^{2\pi}a^2\,d\theta = \pi a^2$. ✓

---

#### 2. Area Between Two Polar Curves

If $0\leq r_1(\theta)\leq r_2(\theta)$ on $[\alpha,\beta]$:
$$A = \frac{1}{2}\int_\alpha^\beta\bigl([r_2]^2 - [r_1]^2\bigr)d\theta.$$

**Procedure:** Find $[\alpha,\beta]$ by solving $r_1 = r_2$; verify $r_2 \geq r_1 \geq 0$; check the pole separately.

**Example:** Area inside $r = 4\cos\theta$ and outside $r = 2$:
$4\cos\theta = 2 \Rightarrow \theta = \pm\pi/3$.
$$A = \frac{1}{2}\int_{-\pi/3}^{\pi/3}(16\cos^2\theta - 4)\,d\theta = \frac{1}{2}\left[4\theta+4\sin2\theta\right]_{-\pi/3}^{\pi/3} = \frac{4\pi}{3} + 2\sqrt{3}.$$

---

#### 3. Area of a Cardioid and a Rose Petal

**Cardioid $r = a(1+\cos\theta)$:** By $x$-axis symmetry:
$$A = a^2\int_0^\pi(1+\cos\theta)^2\,d\theta = a^2\left[\frac{3\theta}{2}+2\sin\theta+\frac{\sin2\theta}{4}\right]_0^\pi = \frac{3\pi a^2}{2}.$$

**One petal of $r = \sin(2\theta)$** (4-petal rose), $\theta\in[0,\pi/2]$:
$$A = \frac{1}{2}\int_0^{\pi/2}\sin^2(2\theta)\,d\theta = \frac{\pi}{8}.$$
Total area of all four petals: $\pi/2$.

---

#### 4. Intersection Points — Three Cases

Due to non-uniqueness, intersections require checking all three cases:

**Case 1 — Algebraic:** Solve $r_1(\theta) = r_2(\theta)$.

**Case 2 — Pole:** $r_1 = 0$ and $r_2 = 0$ at possibly different angles — same point.

**Case 3 — Shifted:** $(r,\theta)$ on curve 1 equals $(-r,\theta+\pi)$ on curve 2.

**Example:** $r_1 = \sin\theta$, $r_2 = \cos\theta$.
- Algebraic: $\theta = \pi/4$, $r = \sqrt{2}/2$.
- Pole: $r_1 = 0$ at $\theta = 0$; $r_2 = 0$ at $\theta = \pi/2$ — both pass through origin.
- Two intersections: $(\sqrt{2}/2, \pi/4)$ and the pole.

---

#### 5. Arc Length in Polar Coordinates

Write $r = f(\theta)$ parametrically with $\theta$ as parameter; compute $(dx/d\theta)^2+(dy/d\theta)^2$:
$$(f')^2\cos^2\theta - 2ff'\sin\theta\cos\theta + f^2\sin^2\theta + (f')^2\sin^2\theta + 2ff'\sin\theta\cos\theta + f^2\cos^2\theta = (f')^2 + f^2.$$

$$\boxed{L = \int_\alpha^\beta\sqrt{r^2 + \left(\frac{dr}{d\theta}\right)^2}\,d\theta}$$

**Example 1:** Circle $r = a$: $L = \int_0^{2\pi} a\,d\theta = 2\pi a$. ✓

**Example 2:** Cardioid $r = a(1+\cos\theta)$:
$$r^2 + (r')^2 = a^2(1+\cos\theta)^2 + a^2\sin^2\theta = 4a^2\cos^2\!\frac{\theta}{2}.$$
$$L = \int_0^{2\pi}2a\left|\cos\frac{\theta}{2}\right|d\theta = 4a\int_0^\pi\cos\frac{\theta}{2}\,d\theta = 8a.$$

---

#### 6. Surface Area of Revolution in Polar

Rotating $r = f(\theta)$, $y = r\sin\theta \geq 0$, $\theta\in[\alpha,\beta]$ about the polar axis ($x$-axis):
$$S = 2\pi\int_\alpha^\beta r\sin\theta\cdot\sqrt{r^2+(r')^2}\,d\theta.$$

**Example:** Rotate cardioid $r = a(1+\cos\theta)$ about polar axis:
$$S = 2\pi\int_0^\pi a(1+\cos\theta)\sin\theta\cdot 2a\cos\frac{\theta}{2}\,d\theta.$$
Using $\sin\theta = 2\sin(\theta/2)\cos(\theta/2)$ and $1+\cos\theta = 2\cos^2(\theta/2)$:
$$S = 2\pi\int_0^\pi 4a^2\cos^2\frac{\theta}{2}\cdot\sin\frac{\theta}{2}\cdot 2a\cos\frac{\theta}{2}\,d\theta = 16\pi a^2\int_0^\pi\cos^3\!\frac{\theta}{2}\sin\frac{\theta}{2}\,d\theta = \frac{32\pi a^2}{5}.$$

---

#### 7. Conic Sections — Focus, Directrix, and Eccentricity

**Focus:** A fixed point $F$ in the plane.

**Directrix:** A fixed line $\ell$ in the plane that does not pass through $F$.

**Eccentricity:** A non-negative constant $e$ that controls the shape of the conic.

**Unified definition (focus-directrix property):** A **conic section** is the locus of all points $P$ satisfying
$$\frac{|PF|}{d(P,\ell)} = e$$
where $|PF|$ is the distance from $P$ to the focus and $d(P,\ell)$ is the perpendicular distance from $P$ to the directrix.

| $e$ | Conic | Geometric meaning |
|-----|-------|-------------------|
| $0$ | Circle | All points equidistant from center (directrix at infinity) |
| $0 < e < 1$ | Ellipse | Points closer to focus than to directrix |
| $e = 1$ | Parabola | Points equidistant from focus and directrix |
| $e > 1$ | Hyperbola | Points farther from focus than from directrix |

**Each conic has two foci** (for the ellipse and hyperbola) or one focus (parabola). The polar form in §8 places one focus at the origin; the associated directrix is perpendicular to the polar axis.

**Standard Cartesian forms** (centre at origin, major axis along $x$-axis):
- Ellipse: $x^2/a^2 + y^2/b^2 = 1$, $c = ae$, $b^2 = a^2(1-e^2)$.
- Parabola: $y^2 = 4px$, focus at $(p,0)$.
- Hyperbola: $x^2/a^2 - y^2/b^2 = 1$, $c = ae$, $b^2 = a^2(e^2-1)$.

---

#### 8. Polar Form of Conic Sections

Place the **focus at the origin**, directrix perpendicular to polar axis, distance $d$ away. The focus-directrix condition gives:
$$\boxed{r = \frac{l}{1 + e\cos\theta}}, \qquad l = ed \text{ (semi-latus rectum).}$$

Orientations:

| Equation | Directrix position |
|----------|--------------------|
| $r = l/(1+e\cos\theta)$ | Directrix right; conic opens left |
| $r = l/(1-e\cos\theta)$ | Directrix left; conic opens right |
| $r = l/(1+e\sin\theta)$ | Directrix above; conic opens down |
| $r = l/(1-e\sin\theta)$ | Directrix below; conic opens up |

**Semi-latus rectum $l$:** The value of $r$ at $\theta = \pi/2$ — the half-chord through the focus perpendicular to the axis.

---

#### 9. Identifying and Sketching Polar Conics

**Example 1:** $r = 3/(1-\cos\theta)$: $e=1$ → parabola, directrix left, opens right.
Vertex (closest point to focus) at $\theta=\pi$: $r = 3/(1-(-1)) = 3/2$.
*(At $\theta=0$: denominator $= 1-1 = 0$, so $r\to\infty$ — this is the axial direction away from the vertex.)*

**Example 2:** $r = 6/(2+\sin\theta) = 3/(1+\frac{1}{2}\sin\theta)$: $e=1/2$ → **ellipse**, $l=3$.
Vertices: $\theta=\pi/2$ gives $r=2$; $\theta=3\pi/2$ gives $r=6$. Semi-major axis $a=4$, $c=2$, $e=1/2$. ✓

**Example 3:** $r = 4/(1-3\cos\theta)$: $e=3$ → **hyperbola**, $l=4$, directrix left.
Near vertex at $\theta=\pi$: $r = 4/(1+3) = 1$, Cartesian $(-1,0)$.
Far vertex: $r = 4/(1-3) = -2$ at $\theta=0$, i.e.\ distance 2 in direction $\theta=\pi$, Cartesian $(-2,0)$.
Center at $(-3/2,\,0)$; semi-major axis $a=1/2$. Hyperbola $\displaystyle\frac{(x+3/2)^2}{1/4}-\frac{y^2}{2}=1$.

---

#### 10. Kepler's Laws and Polar Conics

**Kepler's First Law:** Every planetary orbit is an ellipse with the Sun at one focus.
Polar form: $r = a(1-e^2)/(1+e\cos\theta)$.

**Kepler's Second Law:** A planet sweeps equal areas in equal times. Since $dA/dt = \frac{1}{2}r^2\dot\theta$, this is equivalent to $h = r^2\dot\theta = \text{const}$ — conservation of angular momentum.

**Perihelion and aphelion:**
$$r_{\min} = a(1-e), \qquad r_{\max} = a(1+e).$$

**Earth:** $e \approx 0.0167$, $a \approx 1.496\times10^8$ km. $r_{\min}\approx1.471\times10^8$ km, $r_{\max}\approx1.521\times10^8$ km.

**Halley's comet:** $e \approx 0.967$, period $\approx 75$ years.

**Orbit energy:** Total mechanical energy $E = -GMm/(2a)$ — depends only on semi-major axis $a$, not on eccentricity. An ellipse and a circle with the same $a$ have the same energy.

---

#### 11. Converting a Polar Conic to Standard Cartesian Form

From $r = l/(1+e\cos\theta)$: multiply by denominator, use $r\cos\theta = x$, $r^2 = x^2+y^2$:
$$r = l - ex \implies x^2+y^2 = (l-ex)^2.$$
$$(1-e^2)x^2 + 2lex + y^2 = l^2.$$
For ellipse ($e<1$): complete the square → standard form $\tilde x^2/a^2 + y^2/b^2 = 1$ in shifted coordinates, with $a = l/(1-e^2)$, $b = l/\sqrt{1-e^2}$.

---

#### 12. Summary — Lecture 3

| Quantity | Formula |
|----------|---------|
| Polar area | $\frac{1}{2}\int r^2\,d\theta$ |
| Area between curves | $\frac{1}{2}\int(r_2^2-r_1^2)\,d\theta$ |
| Arc length | $\int\sqrt{r^2+(r')^2}\,d\theta$ |
| Surface of revolution | $2\pi\int r\sin\theta\sqrt{r^2+(r')^2}\,d\theta$ |
| Polar conic | $r = l/(1+e\cos\theta)$; $e<1$ ellipse, $e=1$ parabola, $e>1$ hyperbola |
| Kepler's 2nd law | $r^2\dot\theta = h = \text{const}$ |

---

## Practice Session

**Theme:** Parametric calculus; polar areas, arc lengths, and curve identification.

---

### Practice Problems

**Set A — Parametric Curves**

1. For $x = t^2-1$, $y = t^3-3t$: (a) find all horizontal tangents; (b) show the curve crosses itself and find the crossing point; (c) find the concavity at $t=2$.

2. Find the arc length of $x = e^t\cos t$, $y = e^t\sin t$, $t\in[0,\pi]$.

3. Find the area enclosed by the loop of $x = t^2$, $y = t^3-3t$.

4. Verify that rotating the astroid $x = \cos^3 t$, $y = \sin^3 t$ about the $x$-axis gives surface area $12\pi/5$.

**Set B — Polar Areas and Arc Lengths**

5. Find the total area enclosed by $r = 3\cos\theta$.

6. Find the area inside $r = 3\sin\theta$ and outside $r = 1+\sin\theta$.

7. Find the area of one petal of $r = 4\cos(3\theta)$.

8. Find the arc length of $r = e^\theta$, $\theta\in[0,2\pi]$.

9. Find the surface area generated by rotating $r = \cos\theta$, $\theta\in[0,\pi/2]$ about the polar axis.

**Set C — Polar Curves and Conics**

10. Identify and find the vertices of $r = 5/(2-2\cos\theta)$.

11. Write the polar equation of the ellipse with focus at origin, $l=4$, $e=1/3$, directrix to the right.

12. Find all intersection points of $r = 1$ and $r = 2\cos\theta$, including at the pole.
