# Week 9 — Applications of Second-Order ODEs and Matrix Foundations

**Course:** Engineering Mathematics 1
**Part:** III–IV — Second-Order Linear ODEs and Introduction to Systems
**Kreyszig Sections:** §2.4, 2.8, 2.9; §4.0

> **Building on Weeks 6 & 7:** The homogeneous equation $ay'' + by' + cy = 0$ (Week 6) and the nonhomogeneous equation with particular solutions (Week 7) now receive their most important engineering interpretation. The mass-spring system and RLC circuit translate every abstract concept — characteristic roots, resonance, modification rule — into directly observable physical phenomena. Lecture 3 then introduces the 2D matrix algebra that underpins the system of ODEs theory in Week 10.

---

## Lecture 1: Free Oscillations — Mass-Spring Systems (§2.4, §2.8)

### Introduction

A mass attached to a spring and released from rest will oscillate. The mathematics governing this motion is the second-order linear ODE $my'' + cy' + ky = 0$, whose solutions we can now write down immediately from Week 6 — and whose physical meaning we can now fully interpret.

This lecture translates the three characteristic root cases (real distinct, repeated, complex) into **overdamped**, **critically damped**, and **underdamped** motion. Each case has a distinct physical signature observed in engineering systems ranging from automotive suspensions to building earthquake isolators.

**Why it matters in engineering:**
- Structural dynamics: every building, bridge, and machine has natural frequencies that must be identified and controlled.
- Automotive engineering: suspension design requires choosing damping carefully — overdamped suspensions are stiff, underdamped ones bounce.
- Control engineering: understanding free oscillation is the prerequisite for understanding feedback control stability.

---

### Knowledge Points

---

#### 1. Newton's Second Law — Setting Up the ODE

**Physical setup:** A mass $m > 0$ is attached to a spring with spring constant $k > 0$ and a dashpot with damping coefficient $c \geq 0$. Three forces act on the mass:

- **Spring force** (Hooke's law): $F_\text{spring} = -ky$ — restoring force proportional to displacement $y$ from rest.
- **Damping force** (viscous dashpot): $F_\text{damp} = -c\dot{y}$ — resists motion, proportional to velocity.
- **External force**: $F_\text{ext} = r(t)$ — applied forcing (zero for *free* oscillations).

**Newton's Second Law** $\sum F = ma = m\ddot{y}$:
$$m\ddot{y} = -ky - c\dot{y} + r(t),$$
or in standard form:
$$m\ddot{y} + c\dot{y} + ky = r(t). \tag{$*$}$$

For **free oscillations** set $r(t) = 0$. The IVP $(*)$ with $y(0) = y_0$, $\dot{y}(0) = v_0$ has a unique solution on $[0, \infty)$ (Existence & Uniqueness Theorem).

**Parameters:**
- $m$ = mass [kg], $c$ = damping coefficient [N·s/m], $k$ = spring constant [N/m].

---

#### 2. Characteristic Equation and Natural Frequency

**Characteristic equation** of $(*)$ with $r = 0$: substitute $y = e^{\lambda t}$:
$$m\lambda^2 + c\lambda + k = 0 \implies \lambda = \frac{-c \pm \sqrt{c^2 - 4mk}}{2m}.$$

**Undamped natural frequency:**
$$\omega_0 = \sqrt{\frac{k}{m}} \quad \text{[rad/s]}.$$

**Discriminant:** $\Delta = c^2 - 4mk$.

| $\Delta$ | Root type | Damping regime |
|----------|-----------|---------------|
| $\Delta < 0$ | Complex conjugate | Underdamped |
| $\Delta = 0$ | Repeated real | Critically damped |
| $\Delta > 0$ | Real distinct | Overdamped |

---

#### 3. Case 1 — Undamped Free Oscillation ($c = 0$)

**Characteristic roots:** $\lambda = \pm i\omega_0$.

**General solution:**
$$y(t) = c_1\cos\omega_0 t + c_2\sin\omega_0 t = R\cos(\omega_0 t - \delta),$$
where $R = \sqrt{c_1^2+c_2^2}$ is the amplitude and $\tan\delta = c_2/c_1$ is the phase angle.

- **Period:** $T = 2\pi/\omega_0$; **Frequency:** $f = \omega_0/(2\pi)$ Hz.
- The oscillation continues forever with constant amplitude — no energy loss.

**Energy:** $E = \tfrac{1}{2}m\dot{y}^2 + \tfrac{1}{2}ky^2 = \tfrac{1}{2}kR^2 = \text{const}$. Kinetic and potential energies exchange, but total is constant.

**Example:** $m = 1$ kg, $k = 4$ N/m, $y(0) = 1$, $\dot{y}(0) = 0$:
$\omega_0 = 2$ rad/s, $c_1 = 1$, $c_2 = 0$ $\Rightarrow$ $y(t) = \cos 2t$. Period $T = \pi$ s.

---

#### 4. Case 2 — Underdamped ($\Delta < 0$)

**Define:** $\alpha = c/(2m) > 0$ (decay rate), $\omega_d = \sqrt{\omega_0^2 - \alpha^2} > 0$ (damped natural frequency).

**General solution:**
$$y(t) = e^{-\alpha t}(c_1\cos\omega_d t + c_2\sin\omega_d t) = Re^{-\alpha t}\cos(\omega_d t - \delta).$$

- $e^{-\alpha t}$ is the **decaying envelope**; $\omega_d < \omega_0$ is the **damped natural frequency**.
- Half-life of amplitude: $t_{1/2} = \ln 2/\alpha$.

**Example:** $m = 1$, $c = 2$, $k = 5$ $\Rightarrow$ $\alpha = 1$, $\omega_d = 2$. $y(t) = e^{-t}(c_1\cos 2t + c_2\sin 2t)$. Oscillates but amplitude $\to 0$.

**Engineering context:** Automotive suspensions, seismic dampers; most practical systems are designed underdamped ($\zeta < 1$) — oscillatory but settling.

---

#### 5. Case 3 — Critically Damped ($\Delta = 0$)

**Characteristic root:** $\lambda = -\alpha$ (double root), $\alpha = c/(2m) = \omega_0$.

**General solution:**
$$y(t) = (c_1 + c_2 t)\,e^{-\alpha t}.$$

- Returns to equilibrium **as fast as possible without oscillating**.
- Crosses zero at most once.

**Why fastest?** In the overdamped case the dominant term decays as $e^{(-\alpha+\beta)t}$. Since $0 < \beta < \alpha$, its decay rate $\alpha - \beta < \alpha$, so the overdamped response returns more slowly than $e^{-\alpha t}$.

**Engineering context:** Optimal door closers, precision instrument mounts, control systems where overshoot is not tolerable.

**Worked Example:** Solve $4\ddot{y} + 4\dot{y} + y = 0$, $y(0) = 2$, $\dot{y}(0) = 0$.

$4\lambda^2 + 4\lambda + 1 = (2\lambda+1)^2 = 0 \Rightarrow \lambda = -1/2$ (double). $y(t) = (c_1 + c_2 t)e^{-t/2}$. $y(0) = c_1 = 2$, $\dot{y}(0) = c_2 - c_1/2 = 0 \Rightarrow c_2 = 1$.

**Solution:** $y(t) = (2+t)e^{-t/2}$. Decays to zero without oscillation.

---

#### 6. Case 4 — Overdamped ($\Delta > 0$)

**Characteristic roots:** $\lambda_{1,2} = -\alpha \pm \beta$, $\beta = \sqrt{\alpha^2 - \omega_0^2} > 0$. Both roots are **real and negative**: $\lambda_1 = -\alpha + \beta < 0$, $\lambda_2 = -\alpha - \beta < 0$.

**General solution:**
$$y(t) = c_1 e^{\lambda_1 t} + c_2 e^{\lambda_2 t}.$$

- Returns to equilibrium without oscillating, but **more slowly** than critical damping.
- **Dominant term:** $e^{\lambda_1 t}$ (less negative exponent decays slower).

**Engineering context:** Heavy shock absorbers. Avoided when a fast response is needed ("sluggish" system).

| Regime | Response | Character |
|--------|----------|-----------|
| Underdamped | Oscillatory, decaying envelope | Most common design |
| Critically damped | Non-oscillatory, fastest return | Optimal threshold |
| Overdamped | Non-oscillatory, slow return | Too much damping |

---

#### 7. Damping Ratio and Engineering Classification

**Damping ratio:**
$$\zeta = \frac{c}{2\sqrt{mk}} = \frac{c}{c_{\text{crit}}}, \qquad c_{\text{crit}} = 2\sqrt{mk}.$$

$\zeta$ is dimensionless; $\zeta = 1$ is the boundary between oscillatory and monotone response.

| $\zeta$ | Regime | $y(t)$ form |
|---------|--------|-------------|
| $\zeta = 0$ | Undamped | $R\cos(\omega_0 t - \delta)$ |
| $0 < \zeta < 1$ | Underdamped | $Re^{-\alpha t}\cos(\omega_d t - \delta)$ |
| $\zeta = 1$ | Critically damped | $(c_1+c_2 t)e^{-\alpha t}$ |
| $\zeta > 1$ | Overdamped | $c_1 e^{\lambda_1 t} + c_2 e^{\lambda_2 t}$ |

**Key relations:** $\alpha = \zeta\omega_0$, $\omega_d = \omega_0\sqrt{1-\zeta^2}$.

**Practical target:** $\zeta \approx 0.6$–$0.7$ often gives a good balance between speed of response and overshoot in vibration control.

---

#### 8. Energy Dissipation

$$E = \tfrac{1}{2}m\dot{y}^2 + \tfrac{1}{2}ky^2.$$

With $c = 0$: $E = \tfrac{1}{2}kR^2 = \text{const}$ (no energy loss).

With $c > 0$: $\dfrac{d}{dt}E = -c\dot{y}^2 \leq 0$ — energy is continuously dissipated by the dashpot. The system must eventually return to rest.

---

#### 9. Summary — Lecture 1

| Concept | Formula | Notes |
|---------|---------|-------|
| ODE | $m\ddot{y}+c\dot{y}+ky=0$ | Newton's 2nd Law |
| Natural freq. | $\omega_0 = \sqrt{k/m}$ | $c=0$ oscillation rate |
| Decay rate | $\alpha = c/(2m)$ | Underdamped/critical |
| Damped freq. | $\omega_d = \sqrt{\omega_0^2-\alpha^2}$ | Underdamped only |
| Damping ratio | $\zeta = c/(2\sqrt{mk})$ | Dimensionless design param |
| Critical damp. | $c_{\text{crit}} = 2\sqrt{mk}$ | Threshold $\zeta=1$ |
| Energy | $E = \tfrac{1}{2}m\dot{y}^2+\tfrac{1}{2}ky^2$ | Const. if $c=0$; decays if $c>0$ |

---

## Lecture 2: Forced Oscillations, Resonance, and the RLC Circuit (§2.8, §2.9)

### Introduction

A mass-spring system driven by $r(t) = F_0\cos\omega t$ is the canonical nonhomogeneous second-order ODE with sinusoidal forcing. Its general solution $y = y_h + y_p$ gives direct physical meaning: $y_h$ is the **transient** (decays) and $y_p$ is the **steady-state response** (persists). The most important phenomenon is **resonance** — when the driving frequency $\omega$ matches the natural frequency $\omega_0$, the amplitude grows dramatically or without bound.

The series RLC circuit is governed by the **same ODE** as the mass-spring system. The mechanical–electrical analogy shows that every result derived for the spring carries over instantly to the circuit, and vice versa.

---

### Knowledge Points

---

#### 1. The Forced Mass-Spring ODE

$$m\ddot{y} + c\dot{y} + ky = F_0\cos\omega t. \tag{$**$}$$

**General solution:** $y = y_h + y_p$, where $y_h$ is the homogeneous solution (Lecture 1, transient) and $y_p$ is found by the UC method (Week 7, steady-state).

**Physical timeline:**
- Early: both $y_h$ and $y_p$ present; response depends on ICs.
- After $t \gg 1/\alpha$ (where $\alpha = c/(2m)$): $y_h$ has decayed; only $y_p$ remains (steady state).
- ICs are applied to the **full** solution $y = y_h + y_p$.

**Key parameters:** $\omega_0 = \sqrt{k/m}$ (natural freq.), $\omega$ (driving freq.), $r = \omega/\omega_0$ (frequency ratio).

---

#### 2. Finding $y_p$ by Undetermined Coefficients (Undamped, $\omega \neq \omega_0$)

**ODE:** $m\ddot{y} + ky = F_0\cos\omega t$ ($c = 0$, $\omega \neq \omega_0$).

**Step 1 — Trial solution.** The homogeneous solution is $y_h = c_1\cos\omega_0 t + c_2\sin\omega_0 t$. Since $\omega \neq \omega_0$, the driving frequency does not appear in $y_h$, so try:
$$y_p = A\cos\omega t.$$
(With $c = 0$, a $\sin\omega t$ term is not needed — its coefficient comes out zero.)

**Step 2 — Substitute** $\ddot{y}_p = -A\omega^2\cos\omega t$:
$$m(-A\omega^2)\cos\omega t + k(A\cos\omega t) = F_0\cos\omega t \implies A(k - m\omega^2) = F_0.$$

**Step 3 — Solve for $A$:**
$$A = \frac{F_0}{k - m\omega^2} = \frac{F_0/m}{\omega_0^2 - \omega^2}.$$

$$y_p = \frac{F_0/m}{\omega_0^2 - \omega^2}\cos\omega t, \qquad |A| \to \infty \text{ as } \omega \to \omega_0.$$

---

#### 3. Undamped Forced Oscillation ($c = 0$, $\omega \neq \omega_0$) — Beats

**Full solution** with ICs $y(0) = \dot{y}(0) = 0$:
$$y = c_1\cos\omega_0 t + c_2\sin\omega_0 t + \frac{F_0/m}{\omega_0^2-\omega^2}\cos\omega t.$$
Apply ICs: $c_1 = -\dfrac{F_0/m}{\omega_0^2-\omega^2}$, $c_2 = 0$. Using the identity $\cos\alpha - \cos\beta = 2\sin\tfrac{\alpha+\beta}{2}\sin\tfrac{\beta-\alpha}{2}$:

$$y(t) = \frac{2F_0/m}{\omega_0^2-\omega^2}
  \sin\!\left(\frac{\omega_0-\omega}{2}\,t\right)
  \sin\!\left(\frac{\omega_0+\omega}{2}\,t\right).$$

- **Fast oscillation** at $(\omega_0+\omega)/2 \approx \omega_0$ (inner carrier).
- **Slow modulation** (envelope) at $(\omega_0-\omega)/2$ — small when $\omega \approx \omega_0$.
- **Beat frequency:** $f_\text{beat} = |f_0 - f|$; **Beat period:** $T_\text{beat} = \dfrac{2\pi}{|\omega_0-\omega|}$.

**Example:** $\omega_0 = 5$, $\omega = 4$, $F_0/m = 1$: $y(t) = \tfrac{2}{9}\sin(0.5t)\sin(4.5t)$. Beat period $T_\text{beat} = 2\pi$. The amplitude oscillates between $0$ and $\tfrac{2}{9}$ — bounded.

**Physical example:** Two slightly detuned tuning forks produce a pulsating volume.

---

#### 4. Pure Resonance ($c = 0$, $\omega = \omega_0$)

When $\omega = \omega_0$, the trial $y_p = A\cos\omega_0 t$ **duplicates** $y_h$ — the UC method fails. **Modification rule** (Week 7): multiply the trial by $t$:
$$y_p = t(A\cos\omega_0 t + B\sin\omega_0 t).$$

Substituting into $m\ddot{y} + ky = F_0\cos\omega_0 t$ and collecting terms gives $2m\omega_0 B = F_0$ and $A = 0$:

$$y_p = \frac{F_0}{2m\omega_0}\,t\sin\omega_0 t.$$

The factor $t$ causes the amplitude to grow **linearly without bound** — structural failure in practice.

**Engineering disasters:**
- **Tacoma Narrows (1940):** Wind oscillation near torsional natural frequency — collapse. Soldiers now break step on bridges (Broughton, 1831).
- **Millennium Bridge (2000):** Synchronized pedestrian steps caused lateral resonance; tuned mass dampers installed.

---

#### 5. Damped Forced Oscillation ($c > 0$) — Deriving the Steady-State Amplitude

**ODE:** $m\ddot{y} + c\dot{y} + ky = F_0\cos\omega t$. **Trial:** $y_p = A\cos\omega t + B\sin\omega t$.

**Substitute and collect** $\cos\omega t$ and $\sin\omega t$ terms:
$$\cos\omega t: \quad (k-m\omega^2)\,A + c\omega\,B = F_0,$$
$$\sin\omega t: \quad -c\omega\,A + (k-m\omega^2)\,B = 0.$$

**Solve the $2\times2$ system.** Let $p = k - m\omega^2$ and $q = c\omega$:
$$A = \frac{pF_0}{p^2+q^2}, \qquad B = \frac{qF_0}{p^2+q^2}, \qquad p^2+q^2 = (k-m\omega^2)^2 + c^2\omega^2.$$

**Write in amplitude-phase form** $y_p = C(\omega)\cos(\omega t - \phi)$, where $C = \sqrt{A^2+B^2}$ and $\tan\phi = B/A$:

$$C(\omega) = \frac{F_0}{\sqrt{(k-m\omega^2)^2+c^2\omega^2}}, \qquad \tan\phi = \frac{c\omega}{k-m\omega^2}.$$

---

#### 6. Steady-State Amplitude, Magnification Factor, and Q-Factor

$$y_p = C(\omega)\cos(\omega t - \phi), \qquad C(\omega) = \frac{F_0}{\sqrt{(k-m\omega^2)^2+c^2\omega^2}}, \qquad \tan\phi = \frac{c\omega}{k-m\omega^2}.$$

**Magnification factor** ($r = \omega/\omega_0$, $\zeta = c/(2\sqrt{mk})$):
$$M(\omega) = \frac{C(\omega)}{F_0/k} = \frac{1}{\sqrt{(1-r^2)^2+(2\zeta r)^2}},$$
where $F_0/k$ is the **static deflection**. Note $M(0) = 1$ for all $\zeta$ (static case).

**Resonance peak** (exists only for $\zeta < 1/\sqrt{2} \approx 0.707$):
$$\omega_\text{res} = \omega_0\sqrt{1-2\zeta^2}, \qquad M_{\max} = \frac{1}{2\zeta\sqrt{1-\zeta^2}}.$$
For small $\zeta$: $M_{\max} \approx 1/(2\zeta) = Q$. When $\zeta \geq 1/\sqrt{2}$, $M$ decreases monotonically — no resonance peak.

**Q-factor:** $Q = \dfrac{1}{2\zeta} = \dfrac{\sqrt{mk}}{c}$. High $Q$ ($\zeta$ small) gives a sharp resonance peak. Half-power bandwidth: $\Delta\omega \approx \omega_0/Q$.

---

#### 7. Finding the Resonance Peak — Derivation

Maximising $M(r)$ is equivalent to **minimising** $D(r) = (1-r^2)^2 + 4\zeta^2 r^2$.

**Substitute $u = r^2 \geq 0$:**
$$D(u) = (1-u)^2 + 4\zeta^2 u = 1 - 2u + u^2 + 4\zeta^2 u.$$

**Differentiate and set to zero:**
$$\frac{dD}{du} = -2 + 2u + 4\zeta^2 = 0 \implies u_* = 1 - 2\zeta^2.$$

A minimum exists only when $u_* > 0$, i.e. $\zeta < 1/\sqrt{2}$.

**Resonance frequency:** $r_\text{res} = \sqrt{1-2\zeta^2}$, so $\omega_\text{res} = \omega_0\sqrt{1-2\zeta^2}$.

**Peak value:** Substitute $u_* = 1-2\zeta^2$ back into $D$:
$$D(u_*) = 4\zeta^4 + 4\zeta^2 - 8\zeta^4 = 4\zeta^2(1-\zeta^2),$$
$$\boxed{M_{\max} = \frac{1}{2\zeta\sqrt{1-\zeta^2}}.}$$

---

#### 8. Engineering Consequences of Resonance

**Design strategies:** Detune natural frequencies from excitation; add damping; use vibration isolators; install tuned mass dampers.

| Scenario | $y_p$ | Key feature |
|----------|-------|-------------|
| Undamped, $\omega \neq \omega_0$ | $\frac{F_0/m}{\omega_0^2-\omega^2}\cos\omega t$ | Amplitude $\to\infty$ as $\omega\to\omega_0$ |
| Resonance ($c=0$, $\omega=\omega_0$) | $\frac{F_0}{2m\omega_0}t\sin\omega_0 t$ | Linearly growing amplitude |
| Damped, any $\omega$ | $C(\omega)\cos(\omega t-\phi)$ | Finite steady-state |

---

#### 9. The Series RLC Circuit — KVL Derivation

**Component voltage drops** in a series RLC circuit ($q(t)$ = charge, $I = \dot{q}$ = current):
- **Inductor** $L$ [H]: $V_L = L\dot{I} = L\ddot{q}$ (Faraday: voltage $\propto$ rate of current change)
- **Resistor** $R$ [$\Omega$]: $V_R = RI = R\dot{q}$ (Ohm's law)
- **Capacitor** $C$ [F]: $V_C = q/C$ (charge-voltage: $q = CV$)

**Kirchhoff's Voltage Law (KVL):** Around any closed loop, the sum of voltage drops equals the applied EMF:
$$\underbrace{L\ddot{q}}_{V_L} + \underbrace{R\dot{q}}_{V_R} + \underbrace{\frac{q}{C}}_{V_C} = E(t).$$

$$L\ddot{q} + R\dot{q} + \frac{1}{C}\,q = E(t). \tag{RLC}$$

This is **structurally identical** to $(**)$ with the correspondence $m \to L$, $c \to R$, $k \to 1/C$.

**Key circuit formulas (direct substitution from mechanical results):**
$$\omega_0 = \frac{1}{\sqrt{LC}}, \quad \zeta = \frac{R}{2}\sqrt{\frac{C}{L}}, \quad R_{\text{crit}} = 2\sqrt{\frac{L}{C}}, \quad Q = \frac{1}{R}\sqrt{\frac{L}{C}}.$$

---

#### 10. Reactance, Impedance, and the Mechanical–Electrical Analogy

**Reactance and Impedance** for the forced circuit $E(t) = E_0\cos\omega t$:
- **Inductive reactance:** $X_L = L\omega$ [$\Omega$] — inductor resists high-frequency current.
- **Capacitive reactance:** $X_C = \dfrac{1}{C\omega}$ [$\Omega$] — capacitor resists low-frequency current.
- **Impedance** (apparent resistance): $Z = \sqrt{R^2 + (X_L - X_C)^2} = \sqrt{R^2+\left(L\omega-\frac{1}{C\omega}\right)^2}$ [$\Omega$].

**Steady-state current amplitude:** $I_0 = E_0/Z$ (generalised Ohm's law).

**At electrical resonance** ($\omega = \omega_0 = 1/\sqrt{LC}$): $X_L = X_C$ $\Rightarrow$ $Z = R$, $I_0 = E_0/R$ is **maximum**. The inductive and capacitive reactances cancel each other; the circuit "sees" only $R$.

| Mechanical | Symbol | Electrical | Symbol |
|-----------|--------|-----------|--------|
| Mass — resists acceleration | $m$ | Inductance — resists change in $I$ | $L$ |
| Damping — dissipates energy | $c$ | Resistance — Joule heat | $R$ |
| Spring — stores/returns energy | $k$ | $1/$Capacitance — stores charge | $1/C$ |
| Displacement | $y$ | Charge | $q$ |
| Velocity | $\dot{y}$ | Current | $I = \dot{q}$ |
| External force | $F(t)$ | Applied EMF | $E(t)$ |

**Universality:** The same ODE $\ddot{x} + 2\alpha\dot{x} + \omega_0^2 x = f(t)$ governs mass-spring systems, RLC circuits, torsional pendulums, acoustic waves, and more. **Solving it once solves all of them simultaneously.**

---

#### 11. Worked Example — Forced RLC Circuit (Kreyszig §2.9 Ex. 1)

**Circuit:** $L = 1$ H, $R = 2\ \Omega$, $C = 1/5$ F, $E(t) = 5\cos t$ V; $q(0) = I(0) = 0$.

KVL gives $\ddot{q} + 2\dot{q} + 5q = 5\cos t$ — identical to the mass-spring ODE with $m=1$, $c=2$, $k=5$, $F_0=5$, $\omega=1$.

**Step 1 — Homogeneous.** $\lambda^2 + 2\lambda + 5 = 0 \Rightarrow \lambda = -1 \pm 2i$ (underdamped: $\alpha = 1$, $\omega_d = 2$).
$$q_h = e^{-t}(c_1\cos 2t + c_2\sin 2t).$$

**Step 2 — Particular.** $p = k - m\omega^2 = 5 - 1 = 4$, $q_\text{coeff} = c\omega = 2$.
$$A = \frac{pF_0}{p^2+q^2} = \frac{20}{20} = 1, \qquad B = \frac{qF_0}{p^2+q^2} = \frac{10}{20} = \tfrac{1}{2}.$$
$$q_p = \cos t + \tfrac{1}{2}\sin t. \qquad C_p = \sqrt{1^2+(1/2)^2} = \tfrac{\sqrt{5}}{2}, \quad \phi = \arctan\tfrac{1}{2} \approx 27°.$$

**Step 3 — Apply ICs** ($q(0) = 0$, $\dot{q}(0) = 0$): $c_1 = -1$, $c_2 = -3/4$.

$$q(t) = \underbrace{e^{-t}\!\left(-\cos 2t - \tfrac{3}{4}\sin 2t\right)}_{\text{transient} \to 0} + \underbrace{\cos t + \tfrac{1}{2}\sin t}_{\text{steady-state}}.$$

By $t = 4\pi$: $e^{-4\pi} \approx 3\times10^{-6}$; the transient is negligible.

---

#### 12. Summary — Lecture 2

| Scenario | Result |
|----------|--------|
| Undamped, $\omega\neq\omega_0$ | $y_p=\dfrac{F_0/m}{\omega_0^2-\omega^2}\cos\omega t$ |
| Resonance ($c=0$, $\omega=\omega_0$) | $y_p=\dfrac{F_0}{2m\omega_0}t\sin\omega_0 t$ (grows linearly) |
| Damped, any $\omega$ | $y_p=C(\omega)\cos(\omega t-\phi)$, $C=\dfrac{F_0}{\sqrt{(k-m\omega^2)^2+c^2\omega^2}}$ |
| Magnification | $M=\bigl[(1-r^2)^2+(2\zeta r)^2\bigr]^{-1/2}$ |
| Q-factor | $Q=1/(2\zeta)=\sqrt{mk}/c$ |
| RLC analogy | $m\!\to\!L$, $c\!\to\!R$, $k\!\to\!1/C$, $\omega_0=1/\sqrt{LC}$ |

---

## Lecture 3: Basics of Matrices and Vectors in 2D (§4.0)

### Introduction

From Week 10 onward, systems of ODEs replace single equations as the primary object of study. The solution method — the **eigenvalue method** — is built entirely on 2×2 matrix algebra. This lecture first shows how a single second-order ODE naturally leads to the eigenvalue problem, then develops the essential tools: matrix operations, the determinant, the inverse, and most importantly the **eigenvalue problem** itself.

**Motivation — from scalar ODE to matrix eigenvalue problem:**

The free oscillation ODE $m\ddot{y} + c\dot{y} + ky = 0$ can be written as a first-order system with $y_1 = y$, $y_2 = \dot{y}$:
$$\mathbf{y}' = \underbrace{\begin{pmatrix}0 & 1 \\ -k/m & -c/m\end{pmatrix}}_{\mathbf{A}}\mathbf{y}.$$

Substituting the ansatz $\mathbf{y} = \mathbf{v}e^{\lambda t}$ gives $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$ — the **eigenvalue problem**. The roots of $m\lambda^2 + c\lambda + k = 0$ are precisely the eigenvalues of $\mathbf{A}$.

**Conclusion:** To solve ODEs and systems of ODEs (Week 10), we need to find eigenvalues and eigenvectors of matrices. This lecture develops that machinery.

---

### Knowledge Points

---

#### 1. Vectors in $\mathbb{R}^2$

A **column vector** $\mathbf{v} = \begin{pmatrix}v_1 \\ v_2\end{pmatrix} \in \mathbb{R}^2$.

**Operations:**
$$\mathbf{u} + \mathbf{v} = \begin{pmatrix}u_1+v_1 \\ u_2+v_2\end{pmatrix}, \qquad c\mathbf{v} = \begin{pmatrix}cv_1 \\ cv_2\end{pmatrix}.$$

**Linear independence:** $\mathbf{v}^{(1)}$ and $\mathbf{v}^{(2)}$ are **linearly independent** if $c_1\mathbf{v}^{(1)} + c_2\mathbf{v}^{(2)} = \mathbf{0}$ implies $c_1 = c_2 = 0$ — neither is a scalar multiple of the other.

**Geometric meaning:** Two non-parallel vectors in $\mathbb{R}^2$ are linearly independent and span the whole plane.

---

#### 2. 2×2 Matrices — Operations

A **2×2 matrix** $\mathbf{A} = \begin{pmatrix}a & b \\ c & d\end{pmatrix}$.

**Matrix-vector product:**
$$\mathbf{A}\mathbf{v} = \begin{pmatrix}a & b \\ c & d\end{pmatrix}\begin{pmatrix}v_1 \\ v_2\end{pmatrix} = \begin{pmatrix}av_1 + bv_2 \\ cv_1 + dv_2\end{pmatrix}.$$

**Matrix-matrix product:** $(\mathbf{AB})_{ij} = \sum_k A_{ik}B_{kj}$.

Matrix multiplication is **not commutative** in general: $\mathbf{AB} \neq \mathbf{BA}$.

**Transpose:** $\mathbf{A}^T = \begin{pmatrix}a & c \\ b & d\end{pmatrix}$.

**Identity matrix:** $\mathbf{I} = \begin{pmatrix}1 & 0 \\ 0 & 1\end{pmatrix}$, satisfying $\mathbf{AI} = \mathbf{IA} = \mathbf{A}$.

---

#### 3. Determinant and Trace

**Determinant:**
$$\det\mathbf{A} = \det\begin{pmatrix}a & b \\ c & d\end{pmatrix} = ad - bc.$$

**Trace:**
$$\text{tr}\,\mathbf{A} = a + d \quad \text{(sum of diagonal entries)}.$$

**Geometric meaning:** $|\det\mathbf{A}|$ is the area of the parallelogram spanned by the columns of $\mathbf{A}$. If $\det\mathbf{A} = 0$, the columns are linearly dependent.

**Key properties:**
- $\det(\mathbf{AB}) = \det\mathbf{A}\cdot\det\mathbf{B}$.
- $\det(\mathbf{A}^T) = \det\mathbf{A}$.
- $\det\mathbf{A} \neq 0$ iff $\mathbf{A}$ is invertible.

---

#### 4. Inverse of a 2×2 Matrix

If $\det\mathbf{A} = ad - bc \neq 0$:
$$\mathbf{A}^{-1} = \frac{1}{ad-bc}\begin{pmatrix}d & -b \\ -c & a\end{pmatrix}.$$

**Use in systems:** $\mathbf{A}\mathbf{x} = \mathbf{b}$ has unique solution $\mathbf{x} = \mathbf{A}^{-1}\mathbf{b}$ iff $\det\mathbf{A} \neq 0$.

**Example:** $\mathbf{A} = \begin{pmatrix}2 & 1 \\ 5 & 3\end{pmatrix}$, $\det\mathbf{A} = 6-5 = 1$.
$$\mathbf{A}^{-1} = \begin{pmatrix}3 & -1 \\ -5 & 2\end{pmatrix}.$$

---

#### 5. Homogeneous Linear Systems $\mathbf{A}\mathbf{v} = \mathbf{0}$

The system $\mathbf{A}\mathbf{v} = \mathbf{0}$ always has the trivial solution $\mathbf{v} = \mathbf{0}$.

**Non-trivial solutions exist iff $\det\mathbf{A} = 0$.**

If $\det\mathbf{A} = 0$ and $\mathbf{A} \neq \mathbf{0}$, the solution set is a **line through the origin** — a one-dimensional subspace of $\mathbb{R}^2$.

**Example:** $\begin{pmatrix}2 & -4 \\ -1 & 2\end{pmatrix}\mathbf{v} = \mathbf{0}$.

$\det\mathbf{A} = 4 - 4 = 0$ → non-trivial solutions exist. From the first row: $2v_1 = 4v_2$ → $\mathbf{v} = s\begin{pmatrix}2 \\ 1\end{pmatrix}$, $s \in \mathbb{R}$.

---

#### 6. The Eigenvalue Problem

**Definition:** A scalar $\lambda$ is an **eigenvalue** of $\mathbf{A}$ and $\mathbf{v} \neq \mathbf{0}$ is a corresponding **eigenvector** if:
$$\mathbf{A}\mathbf{v} = \lambda\mathbf{v}.$$

**Geometric meaning:** $\mathbf{A}$ maps $\mathbf{v}$ to a scalar multiple of itself — the direction $\mathbf{v}$ is preserved (or reversed) under the transformation.

**Finding eigenvalues:** Rewrite as $(\mathbf{A} - \lambda\mathbf{I})\mathbf{v} = \mathbf{0}$. Non-trivial $\mathbf{v}$ exists iff:
$$\det(\mathbf{A} - \lambda\mathbf{I}) = 0. \qquad \text{(characteristic equation)}$$

For $\mathbf{A} = \begin{pmatrix}a & b \\ c & d\end{pmatrix}$:
$$\det(\mathbf{A} - \lambda\mathbf{I}) = \lambda^2 - \underbrace{(a+d)}_{\text{tr}\,\mathbf{A}}\,\lambda + \underbrace{(ad-bc)}_{\det\mathbf{A}} = 0.$$

The two eigenvalues satisfy: $\lambda_1 + \lambda_2 = \text{tr}\,\mathbf{A}$ and $\lambda_1\lambda_2 = \det\mathbf{A}$.

**Algorithm:**
1. Solve $\det(\mathbf{A}-\lambda\mathbf{I})=0$ for eigenvalues $\lambda_1,\lambda_2$.
2. For each $\lambda_k$: form $\mathbf{A}-\lambda_k\mathbf{I}$ and solve $(\mathbf{A}-\lambda_k\mathbf{I})\mathbf{v}=\mathbf{0}$.
3. Read off a non-trivial $\mathbf{v}^{(k)}$ from one row equation.

---

#### 7. Eigenvector Row Equation Method

**Key observation:** Since $\det(\mathbf{A}-\lambda_k\mathbf{I})=0$, the two rows of $\mathbf{B}=\mathbf{A}-\lambda_k\mathbf{I}$ are **proportional**. One row equation is enough to find $\mathbf{v}$.

**Recipe:**
1. Pick any nonzero row of $\mathbf{B}=\mathbf{A}-\lambda_k\mathbf{I}$ and write the equation, e.g. $(a-\lambda_k)v_1 + b\,v_2 = 0$.
2. Set one component free (e.g. $v_1 = 1$) and solve for the other.
3. Any nonzero scalar multiple of $\mathbf{v}^{(k)}$ is equally valid.

**Worked Example:** $\mathbf{A}=\begin{pmatrix}4&1\\2&3\end{pmatrix}$. Characteristic equation: $\lambda^2-7\lambda+10=(\lambda-2)(\lambda-5)=0$. $\lambda_1=2$, $\lambda_2=5$.

$\lambda_1=2$: $\mathbf{B}=\begin{pmatrix}2&1\\2&1\end{pmatrix}$. Row 1: $2v_1+v_2=0$. Set $v_1=1 \Rightarrow v_2=-2$. $\mathbf{v}^{(1)}=\begin{pmatrix}1\\-2\end{pmatrix}$.

$\lambda_2=5$: $\mathbf{B}=\begin{pmatrix}-1&1\\2&-2\end{pmatrix}$. Row 1: $-v_1+v_2=0$. Set $v_1=1 \Rightarrow v_2=1$. $\mathbf{v}^{(2)}=\begin{pmatrix}1\\1\end{pmatrix}$.

**Check:** $\mathbf{A}\mathbf{v}^{(1)}=\begin{pmatrix}2\\-4\end{pmatrix}=2\mathbf{v}^{(1)}$ ✓ $\quad$ $\mathbf{A}\mathbf{v}^{(2)}=\begin{pmatrix}5\\5\end{pmatrix}=5\mathbf{v}^{(2)}$ ✓

---

#### 8. Three Cases for Eigenvalues of a Real 2×2 Matrix

The discriminant of the characteristic equation $\lambda^2 - (\text{tr}\,\mathbf{A})\lambda + \det\mathbf{A} = 0$ is:
$$D = (\text{tr}\,\mathbf{A})^2 - 4\det\mathbf{A}.$$

| $D$ | Eigenvalues | Phase-plane type (Week 10) |
|-----|-------------|---------------------------|
| $D > 0$ | Two distinct real $\lambda_1 \neq \lambda_2$ | Node or saddle point |
| $D = 0$ | Repeated real $\lambda_1 = \lambda_2$ | Improper or proper node |
| $D < 0$ | Complex conjugate $\alpha \pm i\beta$ | Spiral point or center |

**Connection to Week 6:** This is exactly the same three-case structure as the characteristic equation of a second-order scalar ODE. The matrix eigenvalue problem is the generalisation.

---

#### 9. Worked Examples

**Example 1 — Distinct real eigenvalues:**

$\mathbf{A} = \begin{pmatrix}3 & 1 \\ 1 & 3\end{pmatrix}$.

Characteristic equation: $\lambda^2 - 6\lambda + 8 = (\lambda-2)(\lambda-4) = 0$. Eigenvalues: $\lambda_1 = 2$, $\lambda_2 = 4$.

$\lambda_1 = 2$: $(\mathbf{A} - 2\mathbf{I})\mathbf{v} = \begin{pmatrix}1 & 1 \\ 1 & 1\end{pmatrix}\mathbf{v} = \mathbf{0}$ → $\mathbf{v}^{(1)} = \begin{pmatrix}1 \\ -1\end{pmatrix}$.

$\lambda_2 = 4$: $(\mathbf{A} - 4\mathbf{I})\mathbf{v} = \begin{pmatrix}-1 & 1 \\ 1 & -1\end{pmatrix}\mathbf{v} = \mathbf{0}$ → $\mathbf{v}^{(2)} = \begin{pmatrix}1 \\ 1\end{pmatrix}$.

**Example 2 — Complex eigenvalues:**

$\mathbf{A} = \begin{pmatrix}1 & -2 \\ 1 & 3\end{pmatrix}$.

Characteristic equation: $\lambda^2 - 4\lambda + 5 = 0$. Eigenvalues: $\lambda = 2 \pm i$.

For $\lambda = 2+i$: second row gives $v_1 + (1-i)v_2 = 0$. Take $v_2 = 1$: $\mathbf{v} = \begin{pmatrix}-(1-i) \\ 1\end{pmatrix} = \begin{pmatrix}-1 \\ 1\end{pmatrix} + i\begin{pmatrix}1 \\ 0\end{pmatrix}$.

The real and imaginary parts of the eigenvector generate two real solution vectors in Week 10.

---

#### 10. Quick Reference — Eigenvalue Diagnostics

Given $\mathbf{A}$ with $p = \text{tr}\,\mathbf{A}$ and $q = \det\mathbf{A}$:

| Condition | Eigenvalue type | Phase-plane (Week 10) |
|-----------|----------------|-----------------------|
| $q < 0$ | Real, opposite signs | Saddle point |
| $q > 0$, $p = 0$ | Purely imaginary | Center |
| $q > 0$, $p \neq 0$, $D < 0$ | Complex with real part | Spiral point |
| $q > 0$, $p^2 > 4q$ | Real, same sign | Node |
| $q > 0$, $p^2 = 4q$ | Repeated real | Improper/proper node |

---

#### 11. Summary — Lecture 3

**Core formulas:**

$$\det\begin{pmatrix}a & b \\ c & d\end{pmatrix} = ad - bc, \qquad \mathbf{A}^{-1} = \frac{1}{ad-bc}\begin{pmatrix}d & -b \\ -c & a\end{pmatrix}.$$

$$\text{Characteristic equation: } \lambda^2 - (\text{tr}\,\mathbf{A})\lambda + \det\mathbf{A} = 0.$$

$$\lambda_1 + \lambda_2 = \text{tr}\,\mathbf{A}, \qquad \lambda_1\lambda_2 = \det\mathbf{A}.$$

**Eigenvector method:** For each $\lambda_k$, solve $(\mathbf{A} - \lambda_k\mathbf{I})\mathbf{v} = \mathbf{0}$ — possible only because $\det(\mathbf{A} - \lambda_k\mathbf{I}) = 0$. Use the row equation method: pick any nonzero row and solve for the ratio $v_1 : v_2$.

**Preview of Week 10:** The ansatz $\mathbf{y}(t) = \mathbf{v}e^{\lambda t}$ in $\mathbf{y}' = \mathbf{A}\mathbf{y}$ reduces the ODE problem directly to $\mathbf{A}\mathbf{v} = \lambda\mathbf{v}$. The eigenvalue computations practised today are the computational core of the entire system-of-ODEs theory.

---

## Practice Session

**Theme:** Damped and forced oscillations; RLC circuits; 2×2 matrix algebra and eigenvalues.

---

### Practice Problems

**Set A — Free and Forced Oscillations**

1. Classify each system and find the general solution:
   (a) $\ddot{y} + 6\dot{y} + 9y = 0$
   (b) $\ddot{y} + 2\dot{y} + 10y = 0$
   (c) $4\ddot{y} + 12\dot{y} + 9y = 0$
   (d) $\ddot{y} + 5\dot{y} + 4y = 0$

2. Solve the IVP $\ddot{y} + 4\dot{y} + 4y = 0$, $y(0) = 1$, $\dot{y}(0) = -1$. Find the time at which $y = 0$ (if any).

3. Solve $\ddot{y} + 9y = 4\cos 3t$ (pure resonance):
   (a) Explain why the standard UC trial fails.
   (b) Apply the modification rule and find $y_p$.
   (c) Write the general solution with $y(0) = 1$, $\dot{y}(0) = 0$.

4. For the damped system $\ddot{y} + 2\dot{y} + 26y = 100\cos\omega t$:
   (a) Find $\omega_0$ and $\zeta$.
   (b) Find the resonance frequency $\omega_\text{res}$ and the Q-factor.
   (c) Find the steady-state particular solution at $\omega = 1$.

5. Show using the beat formula that as $\omega \to \omega_0$, the beat period $T_\text{beat} \to \infty$ while the amplitude approaches $t F_0/(2m\omega_0)$ — recovering the resonance solution. (Hint: use Taylor expansion $\sin\epsilon \approx \epsilon$ for small $\epsilon$.)

**Set B — RLC Circuits**

6. An RLC series circuit has $L = 0.5$ H, $R = 10\ \Omega$, $C = 0.02$ F. Initial conditions: $q(0) = 5$ C, $I(0) = 0$ A.
   (a) Determine the damping regime.
   (b) Find $q(t)$ and $I(t)$.

7. A series RLC circuit has $L = 1$ H, $R = 2\ \Omega$, $C = 1/5$ F, $E(t) = 5\cos t$ V, $q(0) = I(0) = 0$.
   (a) Find the impedance $Z$ at the driving frequency $\omega = 1$.
   (b) Verify that $C_p = \sqrt{5}/2$ using the impedance formula $C_p = E_0/Z$.
   (c) Find the resonant frequency $\omega_0$ and the Q-factor.

8. A damped spring-mass system has $m = 0.1$ kg, $c = 0.2$ N·s/m, $k = 10$ N/m. Design an RLC circuit with $L = 1$ H having the same natural frequency and damping ratio. Find $R$ and $C$.

**Set C — 2×2 Matrix Algebra and Eigenvalues**

9. For each matrix, compute $\det\mathbf{A}$, $\text{tr}\,\mathbf{A}$, and $\mathbf{A}^{-1}$ (if it exists):

   (a) $\begin{pmatrix}3 & -1 \\ 2 & 4\end{pmatrix}$ \quad (b) $\begin{pmatrix}2 & 6 \\ 1 & 3\end{pmatrix}$ \quad (c) $\begin{pmatrix}0 & -1 \\ 1 & 0\end{pmatrix}$

10. Find all eigenvalues and eigenvectors using the row equation method:

    (a) $\begin{pmatrix}4 & 1 \\ 2 & 3\end{pmatrix}$ \quad (b) $\begin{pmatrix}-1 & 2 \\ -2 & -1\end{pmatrix}$ \quad (c) $\begin{pmatrix}5 & -4 \\ 1 & 0\end{pmatrix}$

11. Without computing eigenvalues explicitly, determine the type (real distinct / repeated / complex) and phase-plane classification (node, saddle, spiral, center) using $\text{tr}\,\mathbf{A}$ and $\det\mathbf{A}$:

    (a) $\begin{pmatrix}2 & 3 \\ -3 & 2\end{pmatrix}$ \quad (b) $\begin{pmatrix}1 & 4 \\ 1 & 1\end{pmatrix}$ \quad (c) $\begin{pmatrix}3 & -1 \\ 1 & 1\end{pmatrix}$

12. Show that if $\lambda_1 \neq \lambda_2$ are eigenvalues of a 2×2 matrix $\mathbf{A}$ with corresponding eigenvectors $\mathbf{v}^{(1)}$ and $\mathbf{v}^{(2)}$, then $\mathbf{v}^{(1)}$ and $\mathbf{v}^{(2)}$ are linearly independent. (Hint: suppose $c_1\mathbf{v}^{(1)} + c_2\mathbf{v}^{(2)} = \mathbf{0}$ and multiply both sides by $\mathbf{A} - \lambda_2\mathbf{I}$.)
