# Week 15 — Laplace Transforms II: Advanced Techniques and Course Review

**Course:** Engineering Mathematics 1
**Part:** V — Laplace Transforms (concluded); Comprehensive Review
**Kreyszig Sections:** §6.3 (step/shifting), §6.4 (delta), §6.5 (convolution)

> **Completing Part V and the Course:** This week extends the Laplace transform to handle the forcing functions that classical ODE methods cannot: **piecewise continuous** inputs (suddenly switched forces, pulse loads) via the Heaviside step function and Second Shifting Theorem, and **impulsive** inputs (hammer blows, lightning strikes) via the Dirac delta. The Convolution Theorem then unifies everything — it shows that the system's response to any input is completely encoded in the **impulse response** $h(t) = \mathcal{L}^{-1}\{H(s)\}$. Lecture 3 is a comprehensive course review, synthesising all methods across Parts I–V with a method-selection flowchart.

---

## Lecture 1: The Unit Step Function and the Second Shifting Theorem

### Introduction

Real engineering inputs are often not smooth, continuous functions of time. A switch is thrown at $t = a$, applying a constant voltage to a circuit. A force is applied from $t = a$ to $t = b$, then removed. A rectangular pulse is delivered. These are **piecewise defined** functions — and they are awkward to handle with the classical ODE methods of Parts II–III (which would require matching solutions across each piece). The Laplace transform handles them effortlessly, once we introduce the **Heaviside unit step function**.

**Why it matters in engineering:**
- Control systems: step inputs (sudden set-point changes), ramp inputs, gate functions.
- Power electronics: square wave driving of circuits.
- Structural dynamics: suddenly applied loads, on/off forcing.

---

### Knowledge Points

---

#### 1. The Heaviside Unit Step Function

**Definition:**
$$u(t-a) = \begin{cases} 0 & t < a \\ 1 & t \geq a \end{cases}, \quad a \geq 0.$$

Also written $H(t-a)$ or $\theta(t-a)$.

**Special case:** $u(t) = u(t-0)$ — the standard unit step at $t = 0$.

**Building piecewise functions:** Any piecewise function can be written using step functions.

**Rectangle (pulse) from $a$ to $b$:**
$$\text{rect}_{[a,b]}(t) = u(t-a) - u(t-b).$$

**Switched function:** $f(t)$ switched on at $t = a$:
$$u(t-a)\,f(t-a) = \begin{cases}0 & t < a \\ f(t-a) & t \geq a\end{cases}.$$

**Examples of piecewise representation:**
$$g(t) = \begin{cases}t & 0 \leq t < 2 \\ 4 & t \geq 2\end{cases} = t + (4-t)u(t-2).$$

Or equivalently: $g(t) = t\,[1 - u(t-2)] + 4\,u(t-2) = t + (4-t)u(t-2)$.

---

#### 2. Systematic Piecewise-to-Step Conversion

For a function defined on multiple intervals, the systematic formula is:

$$g(t) = f_0(t) + [f_1(t)-f_0(t)]\,u(t-a_1) + [f_2(t)-f_1(t)]\,u(t-a_2) + \cdots$$

where $f_0$ is the formula on $[0, a_1)$, $f_1$ is the formula on $[a_1, a_2)$, and so on. Each step function "switches" from the previous branch to the new one.

**Three-piece example:** Convert to step-function form and find $\mathcal{L}\{g\}$:
$$g(t) = \begin{cases}0 & 0 \leq t < 1 \\ t-1 & 1 \leq t < 3 \\ 1 & t \geq 3\end{cases}.$$

**Applying the formula** with $f_0=0$, $f_1=t-1$, $f_2=1$, $a_1=1$, $a_2=3$:
$$g(t) = 0 + [(t-1)-0]\,u(t-1) + [1-(t-1)]\,u(t-3) = (t-1)\,u(t-1) + (2-t+1)\,u(t-3).$$

Since $2-t+1 = -(t-3)+0 = -(t-3)$ when rewritten as a function of $(t-3)$: note $2-t+1 = -(t-3)$ at $t \geq 3$? Check: at $t=3$: $2-3+1=0$; $-(3-3)=0$. At $t=4$: $2-4+1=-1$; $-(4-3)=-1$. Yes.

So $g(t) = (t-1)\,u(t-1) - (t-3)\,u(t-3)$.

**Transform:**
$$\mathcal{L}\{g\} = \frac{e^{-s}}{s^2} - \frac{e^{-3s}}{s^2}.$$

*(Using $\mathcal{L}\{(t-a)\,u(t-a)\} = e^{-as}/s^2$.)*

---

#### 3. Laplace Transform of the Unit Step Function (§6.3)

$$\mathcal{L}\{u(t-a)\} = \int_a^\infty e^{-st}\,dt = \left[-\frac{e^{-st}}{s}\right]_a^\infty = \frac{e^{-as}}{s}, \quad s > 0.$$

**Result:** $\mathcal{L}\{u(t-a)\} = \dfrac{e^{-as}}{s}$.

The factor $e^{-as}$ encodes the **delay** $a$ — a key signature in the $s$-domain.

---

#### 4. The Second Shifting Theorem ($t$-Shifting)

**Theorem:**
$$\mathcal{L}\{u(t-a)\,f(t-a)\} = e^{-as}\,F(s),$$
where $F(s) = \mathcal{L}\{f(t)\}$.

**Equivalently (inverse form):**
$$\mathcal{L}^{-1}\{e^{-as}F(s)\} = u(t-a)\,f(t-a).$$

**Proof:**
$$\mathcal{L}\{u(t-a)f(t-a)\} = \int_a^\infty e^{-st}f(t-a)\,dt \stackrel{\tau=t-a}{=} \int_0^\infty e^{-s(\tau+a)}f(\tau)\,d\tau = e^{-as}F(s). \checkmark$$

**Comparison with First Shifting Theorem (Lecture 2, Week 14):**

| Theorem | Time domain | $s$-domain | Effect |
|---------|-------------|-----------|--------|
| 1st Shifting ($s$-shift) | $e^{at}f(t)$ | $F(s-a)$ | Multiply by $e^{at}$ ↔ shift $s$ |
| 2nd Shifting ($t$-shift) | $u(t-a)f(t-a)$ | $e^{-as}F(s)$ | Delay by $a$ ↔ multiply by $e^{-as}$ |

---

#### 5. Using the Second Shifting Theorem — Forward Direction

**Key:** To apply the theorem, write the function as $u(t-a)\cdot f(t-a)$ — the same function $f$, but delayed by $a$.

**Example 1:** $\mathcal{L}\{u(t-2)\} = e^{-2s}/s$ (using $f(t) = 1$, $F(s) = 1/s$).

**Example 2:** $\mathcal{L}\{u(t-3)\sin 2(t-3)\}$.
$f(t) = \sin 2t$, $F(s) = 2/(s^2+4)$.
$$= e^{-3s}\cdot\frac{2}{s^2+4}.$$

**Example 3:** $\mathcal{L}\{u(t-1)(t-1)^2\}$.
$f(t) = t^2$, $F(s) = 2/s^3$.
$$= e^{-s}\cdot\frac{2}{s^3}.$$

**When the function is NOT already in the shifted form $f(t-a)$:**
Rewrite! If given $u(t-a)\,g(t)$, write $g(t) = g(a + (t-a)) = f(t-a)$ where $f(\tau) = g(a+\tau)$.

**Example 4:** $\mathcal{L}\{u(t-2)\cdot t\}$.
$g(t) = t$; $g(t) = (t-2) + 2$, so $f(\tau) = \tau + 2$, $F(s) = 1/s^2 + 2/s$.
$$\mathcal{L}\{u(t-2)\,t\} = e^{-2s}\left(\frac{1}{s^2}+\frac{2}{s}\right).$$

---

#### 6. Using the Second Shifting Theorem — Inverse Direction

**Key:** If $F(s)$ contains a factor $e^{-as}$, factor it out: $\mathcal{L}^{-1}\{e^{-as}G(s)\} = u(t-a)\,g(t-a)$ where $g = \mathcal{L}^{-1}\{G\}$.

**Example 1:** $\mathcal{L}^{-1}\!\left\{\dfrac{e^{-2s}}{s-3}\right\}$.
$G(s) = 1/(s-3)$, $g(t) = e^{3t}$.
$$= u(t-2)\,e^{3(t-2)}.$$

**Example 2:** $\mathcal{L}^{-1}\!\left\{\dfrac{e^{-\pi s}}{s^2+4}\right\}$.
$G(s) = 1/(s^2+4)$, $g(t) = \frac{1}{2}\sin 2t$.
$$= u(t-\pi)\cdot\frac{1}{2}\sin 2(t-\pi) = u(t-\pi)\cdot\frac{1}{2}\sin(2t-2\pi) = \frac{1}{2}u(t-\pi)\sin 2t.$$

*(Using $\sin(2t - 2\pi) = \sin 2t$.)*

---

#### 7. Solving IVPs with Piecewise Forcing

**Procedure:** The same Laplace pipeline as Week 14, but now $R(s)$ involves $e^{-as}$ factors from the step functions.

**Example:** Solve $y'' + y = u(t-\pi)$, $y(0) = 0$, $y'(0) = 0$.

**Transform:** $(s^2+1)Y = \mathcal{L}\{u(t-\pi)\} = e^{-\pi s}/s$.

$Y = \dfrac{e^{-\pi s}}{s(s^2+1)}$.

**Invert $G(s) = 1/[s(s^2+1)]$ first** (no exponential factor):
PFD: $\dfrac{1}{s(s^2+1)} = \dfrac{1}{s} - \dfrac{s}{s^2+1}$.
$g(t) = 1 - \cos t$.

**Apply 2nd Shifting Theorem:**
$$y(t) = u(t-\pi)\,g(t-\pi) = u(t-\pi)\,[1 - \cos(t-\pi)] = u(t-\pi)(1+\cos t).$$

**Interpretation:** Before $t = \pi$, $y = 0$ (no forcing). After $t = \pi$, the step turns on and the system responds with $1 + \cos t$.

---

#### 8. Rectangular Pulse Forcing

**Example:** Solve $y'' + y = u(t-1) - u(t-2)$ (unit pulse from $t=1$ to $t=2$), $y(0) = 0$, $y'(0) = 0$.

**Transform:** $(s^2+1)Y = \dfrac{e^{-s} - e^{-2s}}{s}$.

$Y = (e^{-s} - e^{-2s})\cdot\dfrac{1}{s(s^2+1)}$.

Using $g(t) = 1 - \cos t$ as before:
$$y(t) = u(t-1)(1-\cos(t-1)) - u(t-2)(1-\cos(t-2)).$$

**Three phases:**
- $0 \leq t < 1$: $y = 0$.
- $1 \leq t < 2$: $y = 1 - \cos(t-1)$ (pulse is on).
- $t \geq 2$: $y = (1-\cos(t-1)) - (1-\cos(t-2)) = \cos(t-2) - \cos(t-1)$ (oscillates freely).

---

#### 9. Application: RC Circuit with Step Input

**Setup:** An RC circuit with resistance $R$ and capacitance $C$ has a voltage source $V_0$ switched on at $t = a$. The charge $q$ satisfies:
$$\frac{q}{C} + R\dot{q} = V_0\,u(t-a).$$

**Solution via Laplace:** Taking the transform and inverting:
$$q(t) = V_0 C\,u(t-a)\left(1 - e^{-(t-a)/RC}\right).$$

**Physical interpretation:**
- For $t < a$: no charge ($q = 0$).
- For $t \geq a$: the capacitor charges from 0 toward the steady state $V_0 C$ with time constant $\tau = RC$.
- The factor $u(t-a)$ times the delayed exponential is exactly the 2nd Shifting Theorem applied.

---

#### 10. Laplace Transform of Periodic Functions

**Definition:** $f$ is periodic with period $T$ if $f(t+T) = f(t)$ for all $t \geq 0$.

**Theorem:**
$$\mathcal{L}\{f\} = \frac{1}{1-e^{-Ts}}\int_0^T e^{-st}f(t)\,dt, \quad s > 0.$$

**Proof:** Split the integral over each period and use the substitution $\tau = t - nT$ on the $n$-th piece:
$$\mathcal{L}\{f\} = \sum_{n=0}^\infty \int_{nT}^{(n+1)T}e^{-st}f(t)\,dt = \sum_{n=0}^\infty e^{-nTs}\int_0^T e^{-s\tau}f(\tau)\,d\tau = \frac{1}{1-e^{-Ts}}\int_0^T e^{-st}f(t)\,dt.$$

*(The geometric series $\sum_{n=0}^\infty e^{-nTs} = 1/(1-e^{-Ts})$ converges for $s > 0$.)*

**Square wave** (period $T=2$; $f = 1$ on $[0,1)$, $f = -1$ on $[1,2)$):
$$\int_0^2 e^{-st}f\,dt = \frac{1-e^{-s}}{s} - \frac{e^{-s}-e^{-2s}}{s} = \frac{(1-e^{-s})^2}{s}.$$
$$\mathcal{L}\{f\} = \frac{1-e^{-s}}{s(1+e^{-s})} = \frac{1}{s}\tanh\frac{s}{2}.$$

---

#### 11. Summary — Lecture 1

| Concept | Formula |
|---------|---------|
| Unit step | $u(t-a) = 0$ ($t<a$), $1$ ($t\geq a$) |
| Piecewise-to-step | $g = f_0 + [f_1-f_0]u(t-a_1) + [f_2-f_1]u(t-a_2) + \cdots$ |
| $\mathcal{L}\{u(t-a)\}$ | $e^{-as}/s$ |
| 2nd Shifting Theorem | $\mathcal{L}\{u(t-a)f(t-a)\} = e^{-as}F(s)$ |
| Inverse | $\mathcal{L}^{-1}\{e^{-as}G(s)\} = u(t-a)\,g(t-a)$ |
| Pulse | $u(t-a) - u(t-b)$ = rectangular pulse on $[a,b]$ |
| RC circuit | $q(t) = V_0 C\,u(t-a)(1-e^{-(t-a)/RC})$ |
| Periodic functions | $\mathcal{L}\{f\} = \dfrac{1}{1-e^{-Ts}}\int_0^T e^{-st}f\,dt$ |

---

## Lecture 2: The Dirac Delta and Convolution Theorem

### Introduction

Two more powerful tools complete the Laplace transform toolkit:

**The Dirac delta** $\delta(t-a)$ models a unit impulse — an infinitely concentrated force or voltage spike of infinitely short duration. Engineers encounter it as a hammer blow, an electrical surge, or a shockwave. The Dirac delta is not a function in the classical sense (it is a **distribution**), but the Laplace transform handles it cleanly.

**The Convolution Theorem** reveals the deepest structure of the transform: the product of two transforms $F(s)\cdot G(s)$ corresponds in the time domain to the **convolution** $(f * g)(t)$ — the "running integral" of $f$ against a time-reversed $g$. For systems, this means: the output for any input $r(t)$ is the convolution of $r(t)$ with the system's **impulse response** $h(t) = \mathcal{L}^{-1}\{H(s)\}$.

---

### Knowledge Points

---

#### 1. The Dirac Delta Function (§6.4)

**Physical motivation:** A hammer blow, lightning strike, or explosion delivers an enormous force $F_\varepsilon$ over an infinitesimally short interval $[a, a+\varepsilon]$, but with a finite **impulse** $F_\varepsilon \cdot \varepsilon = 1$ (kept constant). As $\varepsilon \to 0$: taller, narrower, same area 1.

**Definition via Heaviside differences:** The rectangular pulse of unit area on $[a, a+\varepsilon]$ can be written exactly as:
$$d_\varepsilon(t-a) = \frac{1}{\varepsilon}\bigl[u(t-a) - u(t-a-\varepsilon)\bigr].$$

The **Dirac delta** is the limit:
$$\delta(t-a) = \lim_{\varepsilon\to 0}\frac{u(t-a)-u(t-a-\varepsilon)}{\varepsilon}.$$

**Formal properties:**
$$\delta(t-a) = 0 \text{ for } t \neq a, \qquad \int_{-\infty}^\infty \delta(t-a)\,dt = 1.$$

**Sifting property:** For any continuous $f$:
$$\int_{-\infty}^\infty f(t)\,\delta(t-a)\,dt = f(a).$$

This is the operationally useful form — $\delta$ "sifts out" the value of $f$ at $t = a$.

**Connection to step function:** $\dfrac{d}{dt}u(t-a) = \delta(t-a)$ — the delta is the derivative of the step; the step is the running integral of the delta.

**Note:** $\delta$ is not a classical function but a *distribution*. Its Laplace transform is nonetheless perfectly well-defined and gives correct physical answers.

---

#### 2. Proof: $\mathcal{L}\{\delta(t-a)\} = e^{-as}$

**Strategy:** Use the definition $\delta(t-a) = \lim_{\varepsilon\to 0} d_\varepsilon(t-a)$ and compute the transform of $d_\varepsilon$ first, then take the limit.

**Step 1 — Transform of the rectangular pulse $d_\varepsilon$:**
$$\mathcal{L}\{d_\varepsilon(t-a)\} = \frac{1}{\varepsilon}\bigl[\mathcal{L}\{u(t-a)\} - \mathcal{L}\{u(t-a-\varepsilon)\}\bigr] = \frac{1}{\varepsilon}\cdot\frac{e^{-as} - e^{-(a+\varepsilon)s}}{s} = \frac{e^{-as}(1-e^{-\varepsilon s})}{\varepsilon s}.$$

**Step 2 — Take the limit $\varepsilon \to 0$** (Taylor: $e^{-\varepsilon s} \approx 1 - \varepsilon s$ as $\varepsilon \to 0$):
$$\mathcal{L}\{\delta(t-a)\} = \lim_{\varepsilon\to 0}\frac{e^{-as}(1-e^{-\varepsilon s})}{\varepsilon s} = e^{-as}\cdot\lim_{\varepsilon\to 0}\frac{1-e^{-\varepsilon s}}{\varepsilon s} = e^{-as}\cdot 1 = e^{-as}. \checkmark$$

**Result:**
$$\mathcal{L}\{\delta(t-a)\} = e^{-as}\;(a\geq 0), \qquad \mathcal{L}\{\delta(t)\} = 1.$$

**Confirmation via sifting:** $\displaystyle\int_0^\infty e^{-st}\delta(t-a)\,dt = e^{-sa}$ (sifting property with $f(t) = e^{-st}$). $\checkmark$

---

#### 3. Solving IVPs with Impulsive Forcing

**Example:** Solve $y'' + 4y = 3\delta(t-\pi)$, $y(0) = 1$, $y'(0) = 0$.

**Transform:** $(s^2+4)Y - s = 3e^{-\pi s}$.
$(s^2+4)Y = s + 3e^{-\pi s}$.
$Y = \dfrac{s}{s^2+4} + \dfrac{3e^{-\pi s}}{s^2+4}$.

**Invert:** $G(s) = 1/(s^2+4)$, $g(t) = \frac{1}{2}\sin 2t$.

$$y(t) = \cos 2t + \frac{3}{2}u(t-\pi)\sin 2(t-\pi) = \cos 2t + \frac{3}{2}u(t-\pi)\sin 2t.$$

*(Using $\sin 2(t-\pi) = \sin(2t - 2\pi) = \sin 2t$.)*

**Interpretation:**
- For $0 \leq t < \pi$: $y = \cos 2t$ (free oscillation from ICs).
- At $t = \pi$: the impulse instantaneously changes the velocity. $y(\pi^-) = \cos 2\pi = 1$, but the velocity jumps by $+3$ (the impulse magnitude divided by the coefficient of $y''$, which is $1$).
- For $t > \pi$: $y = \cos 2t + \frac{3}{2}\sin 2t$ (superposition).

---

#### 4. Impulse Response — The Green's Function Connection

**Definition:** The **impulse response** $h(t)$ of the system $ay'' + by' + cy = f(t)$ is the solution to:
$$ah'' + bh' + ch = \delta(t), \quad h(0) = 0,\ h'(0) = 0.$$

**Laplace transform:** $(as^2+bs+c)H(s) = 1$, so:
$$H(s) = \frac{1}{as^2+bs+c} \quad \text{(the transfer function)}.$$

**Therefore:** $h(t) = \mathcal{L}^{-1}\{H(s)\}$ — the impulse response is the inverse transform of the transfer function.

**Example:** For $y'' + 2y' + 5y = \delta(t)$, $H(s) = 1/(s^2+2s+5) = 1/((s+1)^2+4)$.
$h(t) = \frac{1}{2}e^{-t}\sin 2t$.

**Connection to Week 9:** The Green's function from Variation of Parameters (Week 9, §9) is exactly $h(t)$ — the impulse response. The Laplace approach makes this algebraic.

---

#### 5. The Convolution Theorem

**Definition:** The **convolution** of $f$ and $g$ is:
$$(f * g)(t) = \int_0^t f(\tau)\,g(t-\tau)\,d\tau.$$

**Properties:**
- Commutativity: $f * g = g * f$.
- Associativity: $(f*g)*h = f*(g*h)$.
- Distributivity: $f*(g+h) = f*g + f*h$.

**Theorem (Convolution Theorem):**
$$\mathcal{L}\{(f*g)(t)\} = F(s)\cdot G(s).$$

**Equivalently:**
$$\mathcal{L}^{-1}\{F(s)\cdot G(s)\} = (f*g)(t) = \int_0^t f(\tau)\,g(t-\tau)\,d\tau.$$

**Proof:** Substitute, exchange order of integration (Fubini), and re-index. ✓

---

#### 6. Using Convolution — System Response

**Key application:** For a system with transfer function $H(s)$ driven by input $R(s)$:
$$Y(s) = H(s)\cdot R(s) \implies y(t) = (h * r)(t) = \int_0^t h(t-\tau)\,r(\tau)\,d\tau.$$

**Interpretation:** The output $y(t)$ is the convolution of the impulse response $h(t)$ with the input $r(t)$. Each impulse $r(\tau)\,d\tau$ at time $\tau$ produces a scaled, delayed copy of $h$; the total output is the superposition of all these responses.

This is exactly the **Green's function integral** from Week 9 (§9) — now derived algebraically via Laplace transforms.

---

#### 7. Worked Examples — Convolution Theorem

**Example 1 — Inversion via convolution:** Find $\mathcal{L}^{-1}\!\left\{\dfrac{\omega}{s(s^2+\omega^2)}\right\}$.

$F(s) = 1/s \to f(t) = 1$; $G(s) = \omega/(s^2+\omega^2) \to g(t) = \sin\omega t$. Then $F\cdot G = \omega/[s(s^2+\omega^2)]$:
$$(f * g)(t) = \int_0^t\sin\omega\tau\,d\tau = \frac{1-\cos\omega t}{\omega}. \checkmark$$

**Example 2 — IVP via convolution with verification:** $y'' + y = r(t)$, $y(0) = 0$, $y'(0) = 0$.

$H(s) = 1/(s^2+1)$, $h(t) = \sin t$. General solution: $y(t) = \displaystyle\int_0^t \sin(t-\tau)\,r(\tau)\,d\tau$.

*Case $r(t) = 1$:*
$$y(t) = \int_0^t\sin(t-\tau)\,d\tau = \bigl[\cos(t-\tau)\bigr]_0^t = \cos 0 - \cos t = 1 - \cos t.$$
Check: $y'' + y = \cos t + 1 - \cos t = 1$. $\checkmark$

*Case $r(t) = e^t$:*
$$y(t) = \int_0^t\sin(t-\tau)\,e^\tau\,d\tau.$$
Using $\sin(t-\tau) = \sin t\cos\tau - \cos t\sin\tau$ and the IBP results $\int_0^t e^\tau\cos\tau\,d\tau = \frac{e^t(\cos t+\sin t)-1}{2}$, $\int_0^t e^\tau\sin\tau\,d\tau = \frac{e^t(\sin t-\cos t)+1}{2}$:
$$y = \frac{1}{2}\bigl[e^t(\sin t\cos t + \sin^2 t) - e^t(\cos t\sin t - \cos^2 t) - \sin t - \cos t\bigr] = \frac{e^t - \sin t - \cos t}{2}.$$
Check: $y'' + y = \frac{e^t+\sin t+\cos t}{2} + \frac{e^t-\sin t-\cos t}{2} = e^t$. $\checkmark$ Also $y(0) = (1-0-1)/2 = 0$. $\checkmark$

**Example 3 — Convolution of exponentials:** $e^{at}*e^{bt}$ ($a\neq b$):
$$\int_0^t e^{a\tau}e^{b(t-\tau)}\,d\tau = e^{bt}\cdot\frac{e^{(a-b)t}-1}{a-b} = \frac{e^{at}-e^{bt}}{a-b}.$$

---

#### 8. Integral Equations via Laplace Transform (Volterra)

**Volterra integral equation of the 2nd kind:**
$$y(t) = f(t) + \int_0^t k(t-\tau)\,y(\tau)\,d\tau = f(t) + (k*y)(t).$$

**Solution by Laplace:** $Y = F + K\cdot Y \;\Rightarrow\; Y = \dfrac{F(s)}{1-K(s)}$ (purely algebraic).

**Example 1:** $y(t) = 1 + \displaystyle\int_0^t y(\tau)\,d\tau$.

$K(s) = 1/s$, $F(s) = 1/s$.
$$Y = \frac{1/s}{1-1/s} = \frac{1}{s-1} \;\Rightarrow\; y = e^t. \checkmark$$

**Example 2:** $y(t) = t + \displaystyle\int_0^t (t-\tau)\,y(\tau)\,d\tau$.

$K(s) = 1/s^2$, $F(s) = 1/s^2$.
$$Y = \frac{1/s^2}{1-1/s^2} = \frac{1}{s^2-1} = \frac{1}{2}\left(\frac{1}{s-1}-\frac{1}{s+1}\right) \;\Rightarrow\; y = \tfrac{1}{2}(e^t-e^{-t}) = \sinh t.$$

Verify: $\displaystyle\int_0^t(t-\tau)\sinh\tau\,d\tau = t(\cosh t-1) - [t\sinh t - \cosh t + 1] = \sinh t - t$. So $f + k*y = t + \sinh t - t = \sinh t = y$. $\checkmark$

---

#### 9. Step vs Impulse Response Comparison

**System:** $y'' + 2y' + y = r(t)$, zero ICs. (Double characteristic root $\lambda = -1$; overdamped.)

Transfer function: $H(s) = 1/(s+1)^2$, impulse response: $h(t) = te^{-t}$.

| | Step forcing $r = u(t)$ | Impulse forcing $r = \delta(t)$ |
|--|--|--|
| $Y(s)$ | $H(s)/s = 1/[s(s+1)^2]$ | $H(s) = 1/(s+1)^2$ |
| PFD / result | $1/s - 1/(s+1) - 1/(s+1)^2$ | direct |
| $y(t)$ | $1 - (1+t)e^{-t}$ | $te^{-t}$ |
| $t\to\infty$ | $1$ (steady state = $1/c$) | $0$ (transient) |
| Physical meaning | Sustained forcing | Instantaneous kick |

**Fundamental relation:**
$$y_\text{step}(t) = \int_0^t h(\tau)\,d\tau, \qquad h(t) = \frac{d}{dt}y_\text{step}(t).$$

Check: $\dfrac{d}{dt}[1-(1+t)e^{-t}] = -e^{-t} + (1+t)e^{-t} = te^{-t} = h(t)$. $\checkmark$

---

#### 10. Summary — Lecture 2

| Concept | Formula |
|---------|---------|
| Dirac delta (definition) | $\delta(t-a) = \lim_{\varepsilon\to 0}[u(t-a)-u(t-a-\varepsilon)]/\varepsilon$ |
| Formal properties | $\delta = 0$ for $t\neq a$; $\int\delta\,dt = 1$; sifting: $\int f\delta(t-a)\,dt = f(a)$ |
| $\mathcal{L}\{\delta(t-a)\}$ | $e^{-as}$ (proof via L'Hôpital/Taylor on rectangular pulse) |
| Impulse response | $h(t) = \mathcal{L}^{-1}\{H(s)\}$, $H = 1/(as^2+bs+c)$ |
| Convolution | $(f*g)(t) = \int_0^t f(\tau)g(t-\tau)\,d\tau$ |
| Convolution Theorem | $\mathcal{L}\{f*g\} = F(s)G(s)$ |
| System response | $y(t) = (h*r)(t) = \int_0^t h(t-\tau)r(\tau)\,d\tau$ |
| Step vs impulse | $y_\text{step}(t) = \int_0^t h(\tau)\,d\tau$; $h = d/dt\,y_\text{step}$ |
| Volterra equation | $Y = F/(1-K)$; transforms integral equation to algebra |

---

## Lecture 3: Comprehensive Course Review

### Introduction

This final lecture synthesises the entire course — Parts I through V — into a coherent whole. The central organising tool is a **method-selection flowchart**: given a problem, which technique should be applied? The connections between Parts are emphasised: the integration tools of Part I underpin everything; the ODE structure of Parts II–III is re-expressed algebraically in Part V; and the special functions of Part IV arise as solutions to the ODEs of Part III.

---

### Knowledge Points

---

#### 1. Course Architecture — The Big Picture

```
PART I   Calculus Foundations (Weeks 1–3)
│  Differentiation rules · integration techniques · partial fractions
│  completing the square · improper integrals · parametric/polar
│
│  ↓ Tools reused in every subsequent Part
│
PART II  First-Order ODEs (Weeks 4–5)
│  Separable · linear (IF) · exact · Bernoulli · autonomous
│  Modelling: mixing, circuits (RL), cooling, population
│
│  ↓ Same structure extended to 2nd order
│
PART III Second-Order ODEs (Weeks 6–9)
│  Homogeneous: char. equation → 3 root cases → Wronskian
│  Nonhomogeneous: UC + VoP → y = yₕ + yₚ
│  Applications: mass-spring (free/forced), resonance, RLC
│  Higher-order: char. polynomial degree n
│
│  ↓ Solutions when elementary methods fail
│
PART IV  Series Methods (Weeks 11–13)
│  Convergence theory → power series → Taylor/Maclaurin
│  Power series method → Legendre polynomials → Bessel functions
│
│  ↓ Algebraic alternative to all ODE solving
│
PART V   Laplace Transforms (Weeks 14–15)
   Definition · table · shifting theorems · inverse (PFD + completing square)
   Pipeline: ODE → algebraic Y(s) → invert → y(t)
   Step functions · delta functions · convolution · impulse response
```

---

#### 2. Method-Selection Flowchart — ODEs

```
Given ODE: order? constant or variable coefficients? homogeneous?
│
├─ FIRST ORDER
│   ├─ Separable?          → Separate and integrate (Wk 4)
│   ├─ Linear y'+p(x)y=r? → IF = e^∫p dx (Wk 5)
│   ├─ Exact Mdy=Ndx?      → Find potential F (Wk 4)
│   ├─ Bernoulli?          → Substitute v = y^(1-n) (Wk 5)
│   └─ Autonomous y'=f(y)? → Phase line analysis (Wk 6)
│
├─ SECOND ORDER, CONSTANT COEFFICIENTS
│   ├─ Homogeneous ay''+by'+cy=0
│   │   → Characteristic equation → 3 root cases (Wk 7)
│   └─ Nonhomogeneous ay''+by'+cy=r(x)
│       ├─ r(x) in UC family?
│       │   → Undetermined Coefficients + modification rule (Wk 9)
│       └─ r(x) not UC, or variable coefficients?
│           → Variation of Parameters (Wk 9)
│
├─ EULER–CAUCHY x²y''+axy'+by=r
│   → Auxiliary equation m²+(a-1)m+b=0 (Wk 7)
│
├─ HIGHER ORDER, CONSTANT COEFFICIENTS
│   → Characteristic polynomial degree n (Wk 9)
│   → UC or VoP for particular solution
│
├─ VARIABLE COEFFICIENTS, ORDINARY POINT
│   → Power series method: y=Σcₙxⁿ → recurrence (Wk 12–13)
│
└─ ANY SECOND-ORDER, CONSTANT COEFFICIENTS + IVP
    → Laplace transform pipeline (Wk 14–15)
    → Especially: discontinuous or impulsive r(t)
```

---

#### 3. Method-Selection Flowchart — Inverse Laplace

```
Given F(s): find f(t) = ℒ⁻¹{F}
│
├─ Direct table match?              → Read off immediately
│
├─ Contains e^{-as} factor?
│   → Factor out; identify G(s); find g(t) = ℒ⁻¹{G}
│   → f(t) = u(t-a)·g(t-a)         [2nd Shifting Theorem]
│
├─ Rational function P(s)/Q(s)?
│   ├─ Improper (deg P ≥ deg Q)?    → Long division first
│   └─ Proper:
│       ├─ Q has distinct real roots  → PFD, cover-up rule
│       ├─ Q has repeated real roots  → PFD with (s-a)^k terms
│       └─ Q has irreducible quadratic
│           → Complete the square → (s-α)²+ω²
│           → Rewrite numerator     → e^{αt}(cos/sin)
│           → Apply 1st Shifting Theorem
│
└─ Product F(s)·G(s) (neither simple)?
    → Convolution: f*g = ∫₀ᵗ f(τ)g(t-τ)dτ
```

---

#### 4. The Unifying Thread: $y = y_h + y_p$

This structure runs through the entire course:

| Part | Equation | Homogeneous solution | Particular solution |
|------|----------|---------------------|---------------------|
| II | $y' + py = r$ | $y_h = Ce^{-\int p\,dx}$ | $y_p$ via IF or VoP |
| III | $ay''+by'+cy = r$ | $y_h = c_1y_1 + c_2y_2$ (char. roots) | $y_p$ via UC or VoP |
| V | Laplace | $Y_h$: from IC terms + char. poly | $Y_p$: from $R(s)/Q(s)$ |

In the Laplace domain: $Y(s) = \underbrace{\dfrac{\text{IC terms}}{Q(s)}}_{\text{transient}} + \underbrace{\dfrac{R(s)}{Q(s)}}_{\text{forced response}}$.

---

#### 5. Integrated Worked Example 1

**Problem:** Solve $y'' + 2y' + 5y = e^{-t}u(t-1)$, $y(0) = 0$, $y'(0) = 0$.

**Tools needed:** Laplace (Week 14–15); 2nd Shifting Theorem; 1st Shifting Theorem; completing the square.

**Step 1 — Transform forcing:** $e^{-t}u(t-1) = e^{-a}e^{-(t-1)}u(t-1)$ with $a=1$.
$\mathcal{L}\{e^{-t}u(t-1)\} = e^{-1}\cdot\mathcal{L}\{e^{-(t-1)}u(t-1)\} = e^{-1}\cdot\dfrac{e^{-s}}{s+1} = \dfrac{e^{-(s+1)}}{s+1}$.

**Step 2 — Transform ODE:**
$(s^2+2s+5)Y = \dfrac{e^{-(s+1)}}{s+1}$.
$Y = \dfrac{e^{-(s+1)}}{(s+1)(s^2+2s+5)} = e^{-1}\cdot\dfrac{e^{-s}}{(s+1)((s+1)^2+4)}$.

**Step 3 — Invert $G(s) = \dfrac{1}{(s+1)\bigl((s+1)^2+4\bigr)}$:**

Let $w = s+1$: $\dfrac{1}{w(w^2+4)} = \dfrac{1}{4w} - \dfrac{w}{4(w^2+4)}$.

Back-substituting $w = s+1$ and applying the 1st Shifting Theorem:
$$G(s) = \frac{1}{4}\cdot\frac{1}{s+1} - \frac{1}{4}\cdot\frac{s+1}{(s+1)^2+4}.$$
$$g(t) = \frac{e^{-t}}{4}(1 - \cos 2t).$$

**Step 4 — Apply 2nd Shifting Theorem:**

From Step 2: $Y(s) = e^{-1}\cdot e^{-s}\cdot G(s)$, so
$$y(t) = e^{-1}\cdot u(t-1)\cdot g(t-1) = e^{-1}\cdot u(t-1)\cdot\frac{e^{-(t-1)}}{4}(1-\cos 2(t-1)).$$
$$= u(t-1)\cdot\frac{e^{-t}}{4}(1-\cos 2(t-1)).$$

---

#### 6. Integrated Worked Example 2

**Problem:** Solve $y'' + 4y = 3\delta(t-\pi) + u(t-2\pi)$, zero ICs. (Delta impulse at $t=\pi$ plus step forcing switched on at $t = 2\pi$.)

**Transform:**
$$(s^2+4)Y = 3e^{-\pi s} + \frac{e^{-2\pi s}}{s}.$$
$$Y = \frac{3e^{-\pi s}}{s^2+4} + \frac{e^{-2\pi s}}{s(s^2+4)}.$$

**Invert piece 1:** $g_1(t) = \mathcal{L}^{-1}\{3/(s^2+4)\} = \frac{3}{2}\sin 2t$.
$$\Rightarrow \frac{3}{2}u(t-\pi)\sin 2(t-\pi) = \frac{3}{2}u(t-\pi)\sin 2t.$$

**Invert piece 2:** $G_2(s) = \dfrac{1}{s(s^2+4)} = \dfrac{1}{4s} - \dfrac{s}{4(s^2+4)}$.
$g_2(t) = \frac{1}{4}(1-\cos 2t)$.
$$\Rightarrow \frac{1}{4}u(t-2\pi)(1-\cos 2(t-2\pi)) = \frac{1}{4}u(t-2\pi)(1-\cos 2t).$$

**Full solution:**
$$\boxed{y(t) = \frac{3}{2}\,u(t-\pi)\sin 2t + \frac{1}{4}\,u(t-2\pi)(1-\cos 2t).}$$

**Phases:**
- $0 \leq t < \pi$: $y = 0$.
- $\pi \leq t < 2\pi$: $y = \frac{3}{2}\sin 2t$ (post-impulse oscillation).
- $t \geq 2\pi$: $y = \frac{3}{2}\sin 2t + \frac{1}{4}(1-\cos 2t)$ (impulse + step responses superposed).

---

#### 7. Key Formulas Across All Parts — Quick Reference

**Part I (Calculus tools):**
- IBP: $\int u\,dv = uv - \int v\,du$; LIATE order.
- PFD: distinct linear / repeated / irreducible quadratic factors.
- Completing the square: $s^2+bs+c = (s+b/2)^2 + (c-b^2/4)$.
- Improper integral: $\int_1^\infty x^{-p}\,dx$ converges iff $p > 1$.

**Part II (First-order ODEs):**
- IF for $y'+py=r$: $\mu = e^{\int p\,dx}$; $y = \frac{1}{\mu}\int\mu r\,dx$.
- Bernoulli: $v = y^{1-n}$, $v' + (1-n)pv = (1-n)r$.

**Part III (Second-order ODEs):**
- Char. roots: $\lambda = \frac{-b\pm\sqrt{b^2-4ac}}{2a}$.
- Underdamped: $e^{\alpha t}(c_1\cos\omega_d t + c_2\sin\omega_d t)$.
- Resonance: trial $\to$ $x^s \times$ trial when trial $\in y_h$.
- VoP: $y_p = -y_1\int\frac{y_2 r}{W}\,dx + y_2\int\frac{y_1 r}{W}\,dx$.
- RLC analogy: $m\leftrightarrow L$, $c\leftrightarrow R$, $k\leftrightarrow 1/C$.

**Part IV (Series):**
- Ratio Test: $R = \lim|c_n/c_{n+1}|$.
- Taylor: $c_n = f^{(n)}(x_0)/n!$; $|R_N| \leq M|x-x_0|^{N+1}/(N+1)!$.
- Recurrence from power series ODE: $(n+2)(n+1)c_{n+2} + \cdots = 0$.
- Legendre: $P_n(1)=1$; $\int_{-1}^1 P_mP_n = \frac{2}{2n+1}\delta_{mn}$.

**Part V (Laplace):**
- $\mathcal{L}\{y''\} = s^2Y - sy(0) - y'(0)$.
- 1st Shift: $\mathcal{L}\{e^{at}f\} = F(s-a)$.
- 2nd Shift: $\mathcal{L}\{u(t-a)f(t-a)\} = e^{-as}F(s)$.
- $\mathcal{L}\{\delta(t-a)\} = e^{-as}$.
- Convolution: $\mathcal{L}^{-1}\{F\cdot G\} = f*g = \int_0^t f(\tau)g(t-\tau)\,d\tau$.

---

#### 8. Exam Strategy

**Exam priorities (high to low):**
1. **Laplace pipeline** — IVPs, PFD, 1st/2nd shift, delta (Weeks 14–15).
2. **Nonhomogeneous 2nd-order ODEs** — UC method and modification rule (Week 9).
3. **Mass-spring oscillations and resonance** (Week 10).
4. **Power series recurrence relations and Frobenius method** (Weeks 12–13).
5. **Variation of Parameters; series convergence tests** (Weeks 9, 11).

**Common pitfalls to avoid:**
- **2nd Shift:** Ensure the time-domain function is written as $f(t-a)$, not $f(t)$.
- **UC modification rule:** Always check for overlap with $y_h$ before writing trial $y_p$.
- **PFD for repeated poles:** Write $k$ separate terms for $(s-a)^k$.
- **ICs in Laplace:** Apply at the transform step, not after inverting.
- **Frobenius $r$ values:** Check both roots; use second solution when roots differ by integer.

**Time management during the exam:**
- Read all problems first; solve easiest ones first to secure those marks.
- For Laplace problems: always write $Y(s)$ explicitly before inverting.
- For UC problems: always check the modification rule before writing the trial.
- For series problems: write out the first 4 terms before trying to identify a pattern.

---

## Practice Session

**Theme:** Discontinuous and impulsive forcing; convolution; comprehensive multi-method problems; exam preparation.

---

### Practice Problems

**Set A — Unit Step Function and Second Shifting Theorem**

1. Express each function using Heaviside step functions and find its Laplace transform:
   (a) $f(t) = \begin{cases}0 & 0\leq t < 2 \\ t-2 & t \geq 2\end{cases}$
   (b) $f(t) = \begin{cases}\sin t & 0\leq t < \pi \\ 0 & t \geq \pi\end{cases}$
   (c) $f(t) = \begin{cases}1 & 0\leq t < 1 \\ t & 1\leq t < 2 \\ 0 & t \geq 2\end{cases}$

2. Find $\mathcal{L}^{-1}\{F(s)\}$:
   (a) $F(s) = \dfrac{e^{-3s}}{s+2}$
   (b) $F(s) = \dfrac{e^{-s}(s+1)}{s^2+2s+5}$
   (c) $F(s) = \dfrac{1-e^{-2s}}{s^2}$
   (d) $F(s) = \dfrac{e^{-\pi s/2}}{s^2+1}$

3. Solve each IVP:
   (a) $y' + 2y = u(t-3)$, $y(0) = 0$
   (b) $y'' + 9y = u(t-\pi) - u(t-2\pi)$, $y(0) = 0$, $y'(0) = 0$

**Set B — Dirac Delta and Convolution**

4. Solve each IVP with impulsive forcing:
   (a) $y' + y = 2\delta(t-1)$, $y(0) = 0$
   (b) $y'' + 4y = \delta(t-\pi)$, $y(0) = 0$, $y'(0) = 1$
   (c) $y'' + 2y' + y = \delta(t-2)$, $y(0) = 1$, $y'(0) = 0$

5. Use the Convolution Theorem to find $\mathcal{L}^{-1}\{F(s)\}$:
   (a) $F(s) = \dfrac{1}{s^2(s+1)}$
   (b) $F(s) = \dfrac{1}{(s^2+1)(s^2+4)}$
   (c) $F(s) = \dfrac{s}{(s^2+\omega^2)^2}$ *(result: $\frac{t}{2\omega}\sin\omega t$)*

6. A system with impulse response $h(t) = e^{-t}\sin t$ receives input $r(t) = e^{-t}$.
   (a) Find the transfer function $H(s)$.
   (b) Compute $Y(s) = H(s)\cdot R(s)$.
   (c) Find $y(t)$ using the Convolution Theorem (set up the integral) and also via $\mathcal{L}^{-1}$.

**Set C — Comprehensive Review Problems**

7. Solve the IVP $y'' + 4y' + 4y = e^{-2t}$, $y(0) = 0$, $y'(0) = 1$:
   (a) Using the classical method (Week 9: UC with modification rule).
   (b) Using the Laplace transform.
   (c) Verify both answers agree.

8. Solve $y'' - 2y' + y = e^t/t^2$ ($t > 0$) using Variation of Parameters (Week 9).
   *(Hint: $y_1 = e^t$, $y_2 = te^t$, $W = e^{2t}$.)*

9. For the ODE $y'' + xy' - 2y = 0$:
   (a) Find the recurrence relation (Power Series Method, $x_0 = 0$).
   (b) Show that the even series terminates at degree 2. Write the polynomial.
   (c) Find the first three terms of the non-terminating odd series.

10. For the resonant system $y'' + \omega_0^2 y = F_0\sin\omega_0 t$, $y(0) = 0$, $y'(0) = 0$:
    (a) Solve using Undetermined Coefficients (Week 9) — identify the modification rule.
    (b) Solve using the Laplace transform — identify how resonance appears algebraically ($s^2+\omega_0^2$ in denominator squared).
    (c) Identify the physical consequence of resonance.

11. (Legendre review) For $(1-x^2)y'' - 2xy' + 12y = 0$:
    (a) Identify this as Legendre's equation and find $n$.
    (b) State the polynomial solution $P_n(x)$ without derivation.
    (c) What is the second solution, and where does it converge?

12. (Full pipeline) Solve $y'' + 2y' + 5y = 10\,u(t-2)$, $y(0) = 1$, $y'(0) = 0$:
    (a) Transform the ODE — write $Y(s)$ explicitly.
    (b) Decompose $Y(s)$ into parts not involving $e^{-2s}$ and parts involving $e^{-2s}$.
    (c) Invert each part using the First and Second Shifting Theorems.
    (d) Write the full solution $y(t)$, clearly indicating the three time regions.
