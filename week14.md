# Week 14 — Laplace Transforms I: Fundamentals

**Course:** Engineering Mathematics 1
**Part:** V — Laplace Transforms
**Kreyszig Sections:** §6.1, 6.2

> **Opening Part V:** Every ODE method so far has required guessing a solution form (characteristic equation, trial functions, power series). The **Laplace transform** takes a radically different approach: it converts an ODE in $t$ into an **algebraic equation** in $s$, which is solved by ordinary algebra, then converted back. Initial conditions are incorporated automatically — no separate step required. The price is learning a new integral transform and its inverse. The tools for the inverse — **partial fractions** and **completing the square** — were developed precisely in Week 2 for this purpose.

---

## Lecture 1: The Laplace Transform — Definition, Properties, and Table

### Introduction

The Laplace transform is an **integral transform**: it maps a function $f(t)$ defined on $[0,\infty)$ to a function $F(s)$ of a new variable $s$, by integrating $f(t)$ against the kernel $e^{-st}$. The transform is linear (it respects addition and scalar multiplication) and, crucially, it converts differentiation in $t$ into multiplication by $s$ in the $s$-domain — the key property that makes ODEs algebraic.

**Why it matters in engineering:**
- Control systems: the Laplace transform defines the **transfer function** $H(s)$, the ratio of output to input in the $s$-domain. System design (stability, frequency response) is done entirely in the $s$-domain.
- Circuit analysis: impedance $Z(s)$ generalises resistance to the complex frequency domain.
- Signal processing: convolution in time becomes multiplication in the $s$-domain.
- The Laplace transform handles discontinuous and impulsive forcing functions (Week 15) that the ODE methods of Parts II–III cannot address directly.

---

### Knowledge Points

---

#### 1. Piecewise Continuous Functions and Existence

**Definition:** $f$ is **piecewise continuous** on $[a, b]$ if there exist finitely many points $a = t_0 < t_1 < \cdots < t_n = b$ such that $f$ is continuous on each open subinterval $(t_{k-1}, t_k)$ and has *finite* one-sided limits at every $t_k$. Jump discontinuities are allowed; infinite jumps are not.

**Piecewise continuous on $[0,\infty)$:** $f$ is piecewise continuous on every finite interval $[0, T]$.

**Examples:**
- $f(t) = \begin{cases}t & 0 \leq t < 1 \\ t^2-1 & 1 \leq t \leq 2\end{cases}$ — piecewise continuous (finite jump at $t=1$).
- $g(t) = 1/t$ on $(0,1]$: NOT piecewise continuous ($g \to \infty$ as $t \to 0^+$, not a finite limit).
- $h(t) = \sin(1/t)$ on $(0,1]$: NOT piecewise continuous (oscillates infinitely often near $t=0$).

**Existence Theorem:** If $f$ is piecewise continuous on $[0,\infty)$ and of **exponential order** $c$ — meaning $|f(t)| \leq Me^{ct}$ for all $t \geq T$ (some constants $M>0$, $c \geq 0$) — then $\mathcal{L}\{f\}$ exists for all $s > c$ and $F(s) \to 0$ as $s \to \infty$.

**Examples of exponential order:** polynomials ($c=0$), $e^{at}$ ($c=a$), $\sin\omega t$ ($c=0$), $t^n e^{at}$ ($c=a$). **NOT of exponential order:** $e^{t^2}$ (grows faster than any $e^{ct}$).

---

#### 2. Definition of the Laplace Transform

**Definition:** The **Laplace transform** of $f(t)$ (defined for $t \geq 0$) is:
$$\mathcal{L}\{f(t)\} = F(s) = \int_0^\infty e^{-st}f(t)\,dt,$$
provided the improper integral converges (for some values of $s$).

**Notation:** $\mathcal{L}\{f\} = F$, or $f \longleftrightarrow F$. Lowercase $f$: time-domain; uppercase $F$: $s$-domain. Inverse: $\mathcal{L}^{-1}\{F(s)\} = f(t)$.

**Variable:** $s$ is in general complex, but for this course we treat $s$ as real ($s > s_0$ for some $s_0$).

**Key idea:** The Laplace transform converts *differential* equations in $t$ into *algebraic* equations in $s$. Solving algebraically and inverting gives the solution — with initial conditions built in automatically.

---

#### 3. Computing Transforms Directly — Derivations

**$\mathcal{L}\{1\}$:**
$$\mathcal{L}\{1\} = \int_0^\infty e^{-st}\,dt = \left[-\frac{e^{-st}}{s}\right]_0^\infty = \frac{1}{s}, \quad s > 0.$$

**$\mathcal{L}\{e^{at}\}$:**
$$\mathcal{L}\{e^{at}\} = \int_0^\infty e^{-(s-a)t}\,dt = \frac{1}{s-a}, \quad s > a.$$

**$\mathcal{L}\{t\}$ via IBP** ($u=t$, $dv=e^{-st}dt$):
$$\mathcal{L}\{t\} = \left[-\frac{t}{s}e^{-st}\right]_0^\infty + \frac{1}{s}\int_0^\infty e^{-st}\,dt = 0 + \frac{1}{s} \cdot \frac{1}{s} = \frac{1}{s^2}, \quad s > 0.$$
(Boundary term: $\lim_{t\to\infty}te^{-st} = 0$ for $s>0$ by L'Hôpital.)

**$\mathcal{L}\{t^n\}$ via substitution** $u = st$ ($t = u/s$, $dt = du/s$):
$$\mathcal{L}\{t^n\} = \int_0^\infty e^{-st}\,t^n\,dt = \int_0^\infty e^{-u}\!\left(\frac{u}{s}\right)^{\!n}\frac{du}{s} = \frac{1}{s^{n+1}}\int_0^\infty e^{-u}\,u^n\,du = \frac{\Gamma(n+1)}{s^{n+1}}.$$
For integer $n \geq 0$: $\Gamma(n+1) = n!$ (Week 13), so $\mathcal{L}\{t^n\} = \dfrac{n!}{s^{n+1}}$, $s > 0$.

**$\mathcal{L}\{\cos\omega t\}$ and $\mathcal{L}\{\sin\omega t\}$ via coupled IBP:**

Set $L_c = \mathcal{L}\{\cos\omega t\}$ and $L_s = \mathcal{L}\{\sin\omega t\}$.

IBP for $L_c$ ($u = \cos\omega t$, $dv = e^{-st}dt$):
$$L_c = \left[-\frac{e^{-st}}{s}\cos\omega t\right]_0^\infty - \int_0^\infty\!\left(-\frac{e^{-st}}{s}\right)(-\omega\sin\omega t)\,dt = \frac{1}{s} - \frac{\omega}{s}L_s. \tag{i}$$

IBP for $L_s$ ($u = \sin\omega t$, $dv = e^{-st}dt$):
$$L_s = \frac{\omega}{s}L_c. \tag{ii}$$

Substitute (ii) into (i): $L_c = \tfrac{1}{s} - \tfrac{\omega^2}{s^2}L_c$, giving $L_c(1 + \omega^2/s^2) = 1/s$:
$$\mathcal{L}\{\cos\omega t\} = \frac{s}{s^2+\omega^2}, \qquad \mathcal{L}\{\sin\omega t\} = \frac{\omega}{s^2+\omega^2}, \qquad s > 0.$$

**$\mathcal{L}\{\sinh at\}$ and $\mathcal{L}\{\cosh at\}$** from linearity and $\mathcal{L}\{e^{at}\} = 1/(s-a)$:
$$\mathcal{L}\{\sinh at\} = \frac{1}{2}\cdot\frac{1}{s-a} - \frac{1}{2}\cdot\frac{1}{s+a} = \frac{a}{s^2-a^2}, \quad s > |a|.$$
$$\mathcal{L}\{\cosh at\} = \frac{1}{2}\cdot\frac{1}{s-a} + \frac{1}{2}\cdot\frac{1}{s+a} = \frac{s}{s^2-a^2}, \quad s > |a|.$$

Compare with trig: replace $\omega^2 \to -a^2$ (equivalently $s^2+\omega^2 \to s^2-a^2$).

---

#### 4. The Standard Laplace Transform Table

| $f(t)$ | $F(s) = \mathcal{L}\{f\}$ | Condition |
|--------|--------------------------|-----------|
| $1$ | $\dfrac{1}{s}$ | $s > 0$ |
| $t^n$ ($n = 0,1,2,\ldots$) | $\dfrac{n!}{s^{n+1}}$ | $s > 0$ |
| $t^\alpha$ ($\alpha > -1$) | $\dfrac{\Gamma(\alpha+1)}{s^{\alpha+1}}$ | $s > 0$ |
| $e^{at}$ | $\dfrac{1}{s-a}$ | $s > a$ |
| $\sin\omega t$ | $\dfrac{\omega}{s^2+\omega^2}$ | $s > 0$ |
| $\cos\omega t$ | $\dfrac{s}{s^2+\omega^2}$ | $s > 0$ |
| $\sinh at$ | $\dfrac{a}{s^2-a^2}$ | $s > |a|$ |
| $\cosh at$ | $\dfrac{s}{s^2-a^2}$ | $s > |a|$ |
| $t e^{at}$ | $\dfrac{1}{(s-a)^2}$ | $s > a$ |
| $t^n e^{at}$ | $\dfrac{n!}{(s-a)^{n+1}}$ | $s > a$ |
| $e^{at}\sin\omega t$ | $\dfrac{\omega}{(s-a)^2+\omega^2}$ | $s > a$ |
| $e^{at}\cos\omega t$ | $\dfrac{s-a}{(s-a)^2+\omega^2}$ | $s > a$ |
| $t\sin\omega t$ | $\dfrac{2\omega s}{(s^2+\omega^2)^2}$ | $s > 0$ |
| $t\cos\omega t$ | $\dfrac{s^2-\omega^2}{(s^2+\omega^2)^2}$ | $s > 0$ |

---

#### 5. Linearity and Worked Forward Examples

**Linearity:** $\mathcal{L}\{af(t) + bg(t)\} = a\,\mathcal{L}\{f(t)\} + b\,\mathcal{L}\{g(t)\}$ (integral is linear).

**Example 1:** $\mathcal{L}\{4t^3 - 2t + 5e^{-3t}\} = \dfrac{24}{s^4} - \dfrac{2}{s^2} + \dfrac{5}{s+3}$.

**Example 2:** $\mathcal{L}\{e^{2t}\cos 3t\} = \dfrac{s-2}{(s-2)^2+9}$ (table with $a=2$, $\omega=3$).

**Example 3:** $\mathcal{L}\{(t+1)^2\} = \mathcal{L}\{t^2+2t+1\} = \dfrac{2}{s^3} + \dfrac{2}{s^2} + \dfrac{1}{s}$.

**Example 4** ($s$-derivative rule): $\mathcal{L}\{t^2 e^{-t}\} = (-1)^2\dfrac{d^2}{ds^2}\dfrac{1}{s+1} = \dfrac{2}{(s+1)^3}$. (Matches table entry $n!/(s-a)^{n+1}$ with $n=2$, $a=-1$ ✓)

**Example 5:** $\mathcal{L}\{3\sinh 2t - 4\cosh 2t\} = 3\cdot\dfrac{2}{s^2-4} - 4\cdot\dfrac{s}{s^2-4} = \dfrac{6-4s}{s^2-4}$.

---

#### 6. The $s$-Derivative Rule

**Theorem:**
$$\mathcal{L}\{t^n f(t)\} = (-1)^n\frac{d^n}{ds^n}F(s).$$

**Proof for $n=1$:** Differentiate $F(s) = \int_0^\infty e^{-st}f(t)\,dt$ under the integral sign:
$$F'(s) = \int_0^\infty (-t)\,e^{-st}f(t)\,dt = -\mathcal{L}\{tf(t)\}. \checkmark$$

**Applications:**
$$\mathcal{L}\{t\sin\omega t\} = -\frac{d}{ds}\frac{\omega}{s^2+\omega^2} = \frac{2\omega s}{(s^2+\omega^2)^2}.$$
$$\mathcal{L}\{t\cos\omega t\} = -\frac{d}{ds}\frac{s}{s^2+\omega^2} = \frac{s^2-\omega^2}{(s^2+\omega^2)^2}.$$

These arise in resonance problems (Week 10) where $r(t) = t\sin\omega_0 t$.

---

#### 7. Uniqueness — Lerch's Theorem

**Lerch's Theorem:** If $\mathcal{L}\{f\} = \mathcal{L}\{g\}$ for all sufficiently large $s$, then $f(t) = g(t)$ at every point of continuity.

**Consequence:** The inverse Laplace transform $\mathcal{L}^{-1}\{F\}$ is unique at continuity points. This justifies the table-based inversion strategy: once $F(s)$ is manipulated to match table entries, the result is the unique inverse.

---

#### 8. Summary — Lecture 1

| Property | Formula |
|----------|---------|
| Definition | $F(s) = \int_0^\infty e^{-st}f(t)\,dt$ |
| Linearity | $\mathcal{L}\{af+bg\} = aF + bG$ |
| $\mathcal{L}\{t\}$ via IBP | $1/s^2$ |
| $\mathcal{L}\{t^n\}$ via $u=st$ | $n!/s^{n+1} = \Gamma(n+1)/s^{n+1}$ |
| $\mathcal{L}\{\sin\omega t\}$, $\mathcal{L}\{\cos\omega t\}$ | Coupled IBP system |
| $\mathcal{L}\{\sinh at\}$, $\mathcal{L}\{\cosh at\}$ | From $\mathcal{L}\{e^{\pm at}\}$ by linearity |
| $s$-derivative | $\mathcal{L}\{tf(t)\} = -F'(s)$ |
| Existence | Piecewise continuous + exponential order |
| Uniqueness | $\mathcal{L}^{-1}\{F\}$ is unique (Lerch) |

---

## Lecture 2: Inverse Transforms — The First Shifting Theorem, Partial Fractions, and Completing the Square

### Introduction

Given $F(s)$, the **inverse Laplace transform** $f(t) = \mathcal{L}^{-1}\{F(s)\}$ recovers the time-domain function. The inversion formula involves a contour integral in the complex plane (Bromwich integral) — but in practice we never use it. Instead, we manipulate $F(s)$ algebraically until it matches entries in the transform table, then read off $f(t)$.

The two essential algebraic tools are:
- **Partial fraction decomposition** (Week 2): splits a rational $F(s)$ into simpler fractions matching table entries.
- **Completing the square** (Week 2): converts irreducible quadratic denominators into the form $(s-a)^2 + \omega^2$, matching the shifted sine/cosine table entries.

The **First Shifting Theorem** links these: it explains why $(s-a)^2 + \omega^2$ in the denominator corresponds to $e^{at}\sin\omega t$ or $e^{at}\cos\omega t$.

---

### Knowledge Points

---

#### 1. Linearity of the Inverse Transform

**Property:** $\mathcal{L}^{-1}\{aF + bG\} = a\mathcal{L}^{-1}\{F\} + b\mathcal{L}^{-1}\{G\}$.

**Application:** $\mathcal{L}^{-1}\!\left\{\dfrac{3}{s-2} - \dfrac{5}{s^2+4}\right\} = 3e^{2t} - \dfrac{5}{2}\sin 2t$.

---

#### 2. The First Shifting Theorem ($s$-Shifting)

**Theorem:**
$$\mathcal{L}\{e^{at}f(t)\} = F(s-a), \qquad \text{i.e., } \quad \mathcal{L}^{-1}\{F(s-a)\} = e^{at}f(t).$$

**Proof:**
$$\mathcal{L}\{e^{at}f(t)\} = \int_0^\infty e^{-st}e^{at}f(t)\,dt = \int_0^\infty e^{-(s-a)t}f(t)\,dt = F(s-a). \checkmark$$

**How to use it (forward):** Replace $s$ by $s-a$ in the known transform of $f(t)$.

**How to use it (inverse):** If $F(s)$ contains $(s-a)$ wherever $s$ would appear in a standard table entry, factor out the $e^{at}$:
$$\mathcal{L}^{-1}\{F(s-a)\} = e^{at}\,\mathcal{L}^{-1}\{F(s)\} = e^{at}f(t).$$

**Examples:**
$$\mathcal{L}^{-1}\!\left\{\frac{1}{(s-3)^2}\right\} = e^{3t}\mathcal{L}^{-1}\!\left\{\frac{1}{s^2}\right\} = e^{3t}\cdot t = te^{3t}.$$

$$\mathcal{L}^{-1}\!\left\{\frac{s+1}{(s+1)^2+4}\right\} = e^{-t}\mathcal{L}^{-1}\!\left\{\frac{s}{s^2+4}\right\} = e^{-t}\cos 2t.$$

$$\mathcal{L}^{-1}\!\left\{\frac{3}{(s-2)^2+9}\right\} = e^{2t}\mathcal{L}^{-1}\!\left\{\frac{3}{s^2+9}\right\} = e^{2t}\sin 3t.$$

---

#### 3. Completing the Square — Connecting to Shifting

When the denominator is an irreducible quadratic $as^2 + bs + c$ (with $b^2 - 4ac < 0$), complete the square:
$$as^2 + bs + c = a\left[(s-\alpha)^2 + \omega^2\right], \quad \alpha = -\frac{b}{2a}, \quad \omega = \frac{\sqrt{4ac-b^2}}{2a}.$$

**Recipe:** Set $\alpha = -b/(2a)$, $\omega^2 = c/a - b^2/(4a^2)$.

**Example 1:** Find $\mathcal{L}^{-1}\!\left\{\dfrac{1}{s^2+4s+13}\right\}$.

$s^2+4s+13 = (s+2)^2 + 9$. $\Rightarrow \dfrac{e^{-2t}}{3}\sin 3t$.

**Example 2:** Find $\mathcal{L}^{-1}\!\left\{\dfrac{s+5}{s^2+2s+5}\right\}$.

$s^2+2s+5 = (s+1)^2+4$. Split numerator: $s+5 = (s+1) + 4$.
$$\mathcal{L}^{-1}\!\left\{\frac{s+1}{(s+1)^2+4} + 2\cdot\frac{2}{(s+1)^2+4}\right\} = e^{-t}\cos 2t + 2e^{-t}\sin 2t.$$

**Example 3:** Find $\mathcal{L}^{-1}\!\left\{\dfrac{2s-1}{s^2-6s+25}\right\}$.

$s^2-6s+25 = (s-3)^2+16$. Rewrite numerator: $2s-1 = 2(s-3)+5$.
$$= 2e^{3t}\cos 4t + \frac{5}{4}e^{3t}\sin 4t.$$

---

#### 4. Partial Fraction Decomposition — Setup Rules

**Setup:** $F(s) = P(s)/Q(s)$ proper (deg $P$ < deg $Q$). If improper: long-divide first.

**Type 1 — Distinct real poles:** $A_k = (s-a_k)F(s)\big|_{s=a_k}$ (cover-up rule).

**Type 2 — Repeated pole $(s-a)^k$:** write $A_1/(s-a) + \cdots + A_k/(s-a)^k$; use $w = s-a$ substitution to read off coefficients.

**Type 3 — Irreducible quadratic $(s-\alpha)^2+\omega^2$:** write $(As+B)/(\cdots)$; complete the square; rewrite numerator to match $\cos$ and $\sin$ forms.

---

#### 5. Worked Examples — Distinct Real Poles

**Example 1:** $\mathcal{L}^{-1}\!\left\{\dfrac{2s+3}{(s-2)(s+1)}\right\}$: $A = 7/3$, $B = -1/3$. $f = \tfrac{7}{3}e^{2t} - \tfrac{1}{3}e^{-t}$.

**Example 2:** $\mathcal{L}^{-1}\!\left\{\dfrac{s}{(s+1)(s+3)}\right\}$: $A = -1/2$, $B = 3/2$. $f = -\tfrac{1}{2}e^{-t} + \tfrac{3}{2}e^{-3t}$.

**Example 3 (three poles):** $\mathcal{L}^{-1}\!\left\{\dfrac{1}{s(s-1)(s+2)}\right\}$:
$$A = -\frac{1}{2}, \quad B = \frac{1}{3}, \quad C = \frac{1}{6}. \qquad f(t) = -\frac{1}{2} + \frac{1}{3}e^{t} + \frac{1}{6}e^{-2t}.$$

---

#### 6. Worked Examples — Repeated Poles

**Example 1:** $\mathcal{L}^{-1}\!\left\{\dfrac{s}{(s-1)^2(s+2)}\right\}$:
$B = 1/3$ (cover-up), $C = -2/9$ (cover-up), $A = 2/9$ (from $A+C=0$).
$$f(t) = \frac{2}{9}e^t + \frac{1}{3}te^t - \frac{2}{9}e^{-2t}.$$

**Example 2** (substitution $w = s+1$): $\mathcal{L}^{-1}\!\left\{\dfrac{s^2+1}{(s+1)^3}\right\}$.

Let $w = s+1$: $s^2+1 = (w-1)^2+1 = w^2 - 2w + 2$, so:
$$\frac{s^2+1}{(s+1)^3} = \frac{w^2-2w+2}{w^3} = \frac{1}{w} - \frac{2}{w^2} + \frac{2}{w^3} = \frac{1}{s+1} - \frac{2}{(s+1)^2} + \frac{2}{(s+1)^3}.$$
$$f(t) = e^{-t} - 2te^{-t} + t^2 e^{-t} = (t-1)^2 e^{-t}.$$

---

#### 7. Worked Example — Irreducible Quadratic Factor

$\mathcal{L}^{-1}\!\left\{\dfrac{3s^2+7s+5}{(s+1)(s^2+2s+5)}\right\}$.

PFD: $A/(s+1) + (Bs+C)/(s^2+2s+5)$. Cover-up: $A = 1/4$. Numerator match: $B = 11/4$, $C = 15/4$.

$(s^2+2s+5) = (s+1)^2+4$; $\tfrac{11}{4}s + \tfrac{15}{4} = \tfrac{11}{4}(s+1) + 1$.
$$f(t) = \frac{1}{4}e^{-t} + \frac{11}{4}e^{-t}\cos 2t + \frac{1}{2}e^{-t}\sin 2t.$$

---

#### 8. Combined Example — All Tools Together

$\mathcal{L}^{-1}\!\left\{\dfrac{s^2+3s+1}{(s+2)^2(s^2+2s+5)}\right\}$.

PFD: $A/(s+2) + B/(s+2)^2 + (Cs+D)/(s^2+2s+5)$.

Cover-up for $B$: $B = (4-6+1)/(4-4+5) = -1/5$.

Numerator match: $A = -7/25$, $C = 7/25$, $D = 6/5$.

$(s^2+2s+5) = (s+1)^2+4$; numerator $\tfrac{7}{25}s + \tfrac{6}{5} = \tfrac{7}{25}(s+1) + \tfrac{23}{25}$.
$$f(t) = -\frac{7}{25}e^{-2t} - \frac{1}{5}te^{-2t} + \frac{7}{25}e^{-t}\cos 2t + \frac{23}{50}e^{-t}\sin 2t.$$

---

#### 9. Summary — Lecture 2

| Situation | Tool | Result |
|-----------|------|--------|
| Direct table match | Lookup | Read off $f(t)$ |
| $(s-a)$ replaces $s$ everywhere | 1st Shifting Thm | $e^{at}f(t)$ |
| Irreducible quadratic denom. | Complete the square | $(s-\alpha)^2+\omega^2$ form |
| Rational, distinct real poles | PFD + cover-up | Sum of exponentials |
| Repeated pole $(s-a)^k$ | $k$ terms + $w=s-a$ substitution | Exponential $\times$ polynomial |
| Complex poles | PFD + complete square | Exponential $\times$ sinusoid |
| Improper ($\deg P \geq \deg Q$) | Long division first | Polynomial + proper part |

---

## Lecture 3: Transforms of Derivatives — Solving IVPs

### Introduction

The power of the Laplace transform for ODEs lies in a single key property: **differentiation in $t$ becomes multiplication by $s$** in the $s$-domain. Applied to an ODE, this converts it into an algebraic equation for $Y(s) = \mathcal{L}\{y(t)\}$, which is solved by algebra and inverted. Crucially, the initial conditions $y(0)$ and $y'(0)$ appear automatically in the algebraic equation — there is no need to apply them separately after finding the general solution.

This is the complete **Laplace Transform Pipeline**:
$$\text{IVP for }y(t) \xrightarrow{\mathcal{L}} \text{Algebraic equation for }Y(s) \xrightarrow{\text{algebra}} Y(s) \xrightarrow{\mathcal{L}^{-1}} y(t).$$

---

### Knowledge Points

---

#### 1. Laplace Transform of the Derivative

**Theorem:**
$$\mathcal{L}\{y'(t)\} = s\,Y(s) - y(0),$$
where $Y(s) = \mathcal{L}\{y(t)\}$.

**Proof:** Integration by parts:
$$\mathcal{L}\{y'\} = \int_0^\infty e^{-st}y'(t)\,dt = \left[e^{-st}y(t)\right]_0^\infty + s\int_0^\infty e^{-st}y(t)\,dt = -y(0) + sY(s).$$
(The boundary term $\left[e^{-st}y(t)\right]_0^\infty = 0 - y(0) = -y(0)$, assuming $y(t)$ is of exponential order.) ✓

---

#### 2. Laplace Transform of Higher Derivatives

**Second derivative:**
$$\mathcal{L}\{y''(t)\} = s^2 Y(s) - s\,y(0) - y'(0).$$

**Proof:** Apply the derivative formula twice:
$\mathcal{L}\{y''\} = s\mathcal{L}\{y'\} - y'(0) = s[sY(s) - y(0)] - y'(0) = s^2 Y - sy(0) - y'(0)$. ✓

**$n$-th derivative:**
$$\mathcal{L}\{y^{(n)}(t)\} = s^n Y(s) - s^{n-1}y(0) - s^{n-2}y'(0) - \cdots - y^{(n-1)}(0).$$

**Pattern:** Each derivative adds one power of $s$ and picks up one initial condition term. Initial conditions appear automatically as part of the algebraic equation.

---

#### 3. Transform of an Integral

**Theorem (§6.5):**
$$\mathcal{L}\!\left\{\int_0^t f(\tau)\,d\tau\right\} = \frac{F(s)}{s}.$$

**Proof:** Let $g(t) = \int_0^t f(\tau)\,d\tau$. Then $g'(t) = f(t)$ and $g(0) = 0$. Apply the derivative formula:
$$\mathcal{L}\{g'\} = sG(s) - g(0) = sG(s) = F(s) \;\Longrightarrow\; G(s) = \frac{F(s)}{s}. \checkmark$$

**Applications:**
$$\mathcal{L}\!\left\{\int_0^t \sin\omega\tau\,d\tau\right\} = \frac{\omega}{s(s^2+\omega^2)}, \qquad \mathcal{L}\!\left\{\int_0^t e^{a\tau}\,d\tau\right\} = \frac{1}{s(s-a)}.$$

**Use case — Integro-differential equations:** An equation involving both $y'$ and $\int_0^t y\,d\tau$ can be transformed term by term, yielding a purely algebraic equation for $Y(s)$.

---

#### 4. The Laplace Pipeline and Zero-State/Zero-Input Split

**Pipeline:**
$$\text{IVP for }y(t) \xrightarrow{\mathcal{L}} \text{Algebraic eq. for }Y(s) \xrightarrow{\text{algebra}} Y(s) \xrightarrow{\mathcal{L}^{-1}} y(t).$$

**For the IVP** $ay'' + by' + cy = r(t)$, $y(0) = k_0$, $y'(0) = k_1$:

After transforming: $(as^2 + bs + c)Y(s) = R(s) + (as+b)k_0 + ak_1$.

$$Y(s) = \underbrace{\frac{R(s)}{as^2+bs+c}}_{\text{zero-state }Y_{zs}} + \underbrace{\frac{(as+b)k_0 + ak_1}{as^2+bs+c}}_{\text{zero-input }Y_{zi}}.$$

- **Zero-state $Y_{zs}$:** driven by input $r(t)$ with $k_0 = k_1 = 0$. Corresponds to the particular solution $y_p$.
- **Zero-input $Y_{zi}$:** driven by ICs with $r(t) = 0$. Corresponds to homogeneous solution $y_h$ with constants set by $k_0$, $k_1$.
- **Transfer function:** $H(s) = 1/(as^2+bs+c)$. Poles of $H$ = characteristic roots (same as Week 7).

**Connection to Week 10:** For the mass-spring system $m\ddot{y} + c\dot{y} + ky = F_0\cos\omega t$: $H(s) = 1/(ms^2+cs+k)$, and $|H(i\omega)|$ is the magnification factor from Week 10.

**Step 4 — Invert:** Apply PFD / completing the square / First Shifting Theorem.

---

#### 5. Worked Example 1 — Simple First-Order IVP

**Solve:** $y' + 2y = 4$, $y(0) = 1$.

**Transform:** $[sY - 1] + 2Y = 4/s$.
$(s+2)Y = \frac{4}{s} + 1 = \frac{4+s}{s}$.
$Y = \dfrac{s+4}{s(s+2)}$.

**PFD:** $\dfrac{A}{s} + \dfrac{B}{s+2}$. $A = (s+4)/( s+2)\big|_{s=0} = 2$. $B = (s+4)/s\big|_{s=-2} = -1$.

$$Y = \frac{2}{s} - \frac{1}{s+2}.$$

**Invert:** $y(t) = 2 - e^{-2t}$.

*(Check: $y(0) = 2 - 1 = 1$ ✓; $y' + 2y = 2e^{-2t} + 4 - 2e^{-2t} = 4$ ✓.)*

---

#### 6. Worked Example 2 — Second-Order IVP (Distinct Real Roots)

**Solve:** $y'' - 3y' + 2y = 0$, $y(0) = 1$, $y'(0) = 0$.

**Transform:** $[s^2 Y - s - 0] - 3[sY - 1] + 2Y = 0$.
$(s^2 - 3s + 2)Y = s - 3$.
$Y = \dfrac{s-3}{(s-1)(s-2)}$.

**PFD:** $\dfrac{A}{s-1} + \dfrac{B}{s-2}$.
$A = (s-3)/(s-2)\big|_{s=1} = -2/(-1) = 2$. $B = (s-3)/(s-1)\big|_{s=2} = -1$.

$$y(t) = 2e^t - e^{2t}.$$

*(Matches Week 7 homogeneous solution with ICs applied directly.)*

---

#### 7. Worked Example 3 — Second-Order IVP (Complex Roots)

**Solve:** $y'' + 2y' + 5y = 0$, $y(0) = 2$, $y'(0) = -1$.

**Transform:** $[s^2 Y - 2s + 1] + 2[sY - 2] + 5Y = 0$.
$(s^2+2s+5)Y = 2s + 3$.
$Y = \dfrac{2s+3}{(s+1)^2+4}$.

**Rewrite numerator:** $2s+3 = 2(s+1) + 1$.

$$Y = \frac{2(s+1)}{(s+1)^2+4} + \frac{1}{(s+1)^2+4} = \frac{2(s+1)}{(s+1)^2+4} + \frac{1}{2}\cdot\frac{2}{(s+1)^2+4}.$$

$$y(t) = 2e^{-t}\cos 2t + \frac{1}{2}e^{-t}\sin 2t.$$

---

#### 8. Worked Example 4 — Nonhomogeneous IVP

**Solve:** $y'' + y = \sin 2t$, $y(0) = 1$, $y'(0) = 0$.

**Transform:** $(s^2+1)Y - s = \dfrac{2}{s^2+4}$.

$Y = \dfrac{s}{s^2+1} + \dfrac{2}{(s^2+1)(s^2+4)}$.

**PFD for $\dfrac{2}{(s^2+1)(s^2+4)}$:** $\dfrac{A}{s^2+1} + \dfrac{B}{s^2+4}$.

$2 = A(s^2+4) + B(s^2+1)$. Set $s^2 = -1$: $2 = 3A \Rightarrow A = 2/3$.
Set $s^2 = -4$: $2 = -3B \Rightarrow B = -2/3$.

$$Y = \frac{s}{s^2+1} + \frac{2/3}{s^2+1} - \frac{2/3}{s^2+4}.$$

$$y(t) = \cos t + \frac{2}{3}\sin t - \frac{1}{3}\sin 2t.$$

**Note:** No resonance here ($\omega = 2 \neq \omega_0 = 1$). Compare with the UC result from Week 9 — same answer.

---

#### 9. Worked Example — Integro-Differential Equation

**Solve:** $y'(t) + 2y(t) + 4\displaystyle\int_0^t y(\tau)\,d\tau = 1$, $y(0) = 0$.

**Transform each term:**
$$[sY - 0] + 2Y + 4\cdot\frac{Y}{s} = \frac{1}{s}.$$

**Factor $Y$:**
$$Y\!\left(s + 2 + \frac{4}{s}\right) = \frac{1}{s} \;\Longrightarrow\; Y\cdot\frac{s^2+2s+4}{s} = \frac{1}{s} \;\Longrightarrow\; Y = \frac{1}{s^2+2s+4}.$$

**Complete the square:** $s^2+2s+4 = (s+1)^2+3$.
$$Y = \frac{1}{\sqrt{3}}\cdot\frac{\sqrt{3}}{(s+1)^2+3}.$$

$$\boxed{y(t) = \frac{1}{\sqrt{3}}\,e^{-t}\sin\sqrt{3}\,t.}$$

Verify: $y(0) = 0$ ✓.

---

#### 10. Systems of ODEs via Laplace Transform (§6.7)

**Setup:** First-order linear system with ICs:
$$y_1' = a_{11}y_1 + a_{12}y_2 + r_1(t), \quad y_1(0) = k_1,$$
$$y_2' = a_{21}y_1 + a_{22}y_2 + r_2(t), \quad y_2(0) = k_2.$$

**Method:** Transform each equation using $\mathcal{L}\{y_j'\} = sY_j - y_j(0)$:
$$(s-a_{11})Y_1 - a_{12}Y_2 = k_1 + R_1(s),$$
$$-a_{21}Y_1 + (s-a_{22})Y_2 = k_2 + R_2(s).$$

This is a **linear algebraic system** in $Y_1$, $Y_2$. Solve by Cramer's rule or elimination; then invert each $Y_j$.

**Advantages:** ICs incorporated automatically; step/impulse forcing handled without modification; scales to $n \times n$ systems.

**Worked example:** Solve $y_1' = y_1 + y_2$, $y_2' = 4y_1 + y_2$, $y_1(0) = 3$, $y_2(0) = -1$.

**Transform:**
$(s-1)Y_1 - Y_2 = 3$; $\quad -4Y_1 + (s-1)Y_2 = -1$.

**Eliminate $Y_2$:** From eq.1: $Y_2 = (s-1)Y_1 - 3$. Substitute into eq.2:
$$-4Y_1 + (s-1)[(s-1)Y_1 - 3] = -1 \;\Longrightarrow\; [(s-1)^2-4]Y_1 = 3(s-1) - 1 = 3s-4.$$

$(s-1)^2-4 = (s-3)(s+1)$, so $Y_1 = \dfrac{3s-4}{(s-3)(s+1)}$.

PFD: $A = 5/4$, $B = 7/4$. $\;\Rightarrow\; y_1 = \tfrac{5}{4}e^{3t} + \tfrac{7}{4}e^{-t}$. Check: $y_1(0) = 3$ ✓.

**Find $Y_2$:** $Y_2 = (s-1)Y_1 - 3 = \dfrac{-s+13}{(s-3)(s+1)}$. PFD: $A = 5/2$, $B = -7/2$.
$$y_2 = \frac{5}{2}e^{3t} - \frac{7}{2}e^{-t}. \quad y_2(0) = -1 \checkmark.$$

**Verify eq.1:** $y_1' = \tfrac{15}{4}e^{3t} - \tfrac{7}{4}e^{-t} = y_1 + y_2$ ✓.

---

#### 11. Laplace Transform vs. Classical Methods

| Feature | Classical (Weeks 7, 9) | Laplace Transform |
|---------|----------------------|-------------------|
| ICs applied | After finding general solution | Automatically during $\mathcal{L}$ step |
| Homogeneous + particular | Two separate steps | One algebraic step for $Y$ |
| Handles $r(t)$ = step/impulse | Not directly | Yes (Week 15) |
| Reveals transfer function | No | Yes — $H(s) = 1/(as^2+bs+c)$ |
| Integro-differential equations | Difficult | Transform each term directly |
| Systems of ODEs | Elimination (tedious) | Algebraic system in $Y_j$ |

---

#### 12. Summary — Lecture 3

| Formula | Expression |
|---------|-----------|
| $\mathcal{L}\{y'\}$ | $sY - y(0)$ |
| $\mathcal{L}\{y''\}$ | $s^2Y - sy(0) - y'(0)$ |
| $\mathcal{L}\{\int_0^t f\,d\tau\}$ | $F(s)/s$ |
| Zero-state response | $Y_{zs} = R(s)/Q(s)$ |
| Zero-input response | $Y_{zi} = [\text{IC terms}]/Q(s)$ |
| Transfer function | $H(s) = 1/Q(s)$; poles = characteristic roots |
| Integro-differential eq. | Transform integral term as $Y/s$ |
| System of ODEs (§6.7) | Transform each eq. → algebraic system in $Y_j$ |

---

## Practice Session

**Theme:** Computing Laplace transforms; inverse transforms (PFD, completing the square, shifting); solving IVPs end-to-end via the Laplace pipeline.

---

### Practice Problems

**Set A — Forward Transforms**

1. Compute $\mathcal{L}\{f(t)\}$ for each of the following (state the domain of $s$):
   (a) $f(t) = 5t^3 - 2e^{-t} + 7\sin 3t$
   (b) $f(t) = (t+2)^2$
   (c) $f(t) = e^{3t}\cos 2t$
   (d) $f(t) = t^2 e^{-t}$
   (e) $f(t) = \sinh 2t + \cosh 2t$
   (f) $f(t) = e^{-t}\sin^2 t$ *(use $\sin^2 t = (1-\cos 2t)/2$)*

2. Use the $s$-derivative rule $\mathcal{L}\{tf(t)\} = -F'(s)$ to find:
   (a) $\mathcal{L}\{t\cos 3t\}$
   (b) $\mathcal{L}\{te^{2t}\sin t\}$
   (c) $\mathcal{L}\{t^2\sin t\}$

3. Verify the formula $\mathcal{L}\{\sinh at\} = a/(s^2-a^2)$ directly from the definition, using $\sinh at = (e^{at}-e^{-at})/2$.

**Set B — Inverse Transforms**

4. Find $f(t) = \mathcal{L}^{-1}\{F(s)\}$ for each:
   (a) $F(s) = \dfrac{4}{s^3} - \dfrac{3}{s-2} + \dfrac{1}{s+5}$
   (b) $F(s) = \dfrac{1}{(s-1)^4}$
   (c) $F(s) = \dfrac{2s-1}{s^2+4s+8}$
   (d) $F(s) = \dfrac{s+2}{s^2+6s+13}$
   (e) $F(s) = \dfrac{1}{s^2-4s+5}$

5. Use partial fractions to find $\mathcal{L}^{-1}\{F(s)\}$:
   (a) $F(s) = \dfrac{3}{(s+1)(s-2)}$
   (b) $F(s) = \dfrac{s+4}{s(s^2+4)}$
   (c) $F(s) = \dfrac{2s^2+3s-1}{(s-1)(s+1)(s+2)}$
   (d) $F(s) = \dfrac{s}{(s+2)^2(s-1)}$

6. Find $\mathcal{L}^{-1}\{F(s)\}$ where $F(s) = \dfrac{2s+5}{s^2+4s+13}$:
   (a) Complete the square in the denominator.
   (b) Rewrite the numerator to match cosine and sine forms.
   (c) Apply the First Shifting Theorem and state $f(t)$.

7. *(Challenge)* Find $\mathcal{L}^{-1}\!\left\{\dfrac{s^3+2s^2+4s+3}{(s^2+1)(s^2+4)}\right\}$.
   *(Hint: use PFD with quadratic factors $\dfrac{As+B}{s^2+1} + \dfrac{Cs+D}{s^2+4}$.)*

**Set C — Solving IVPs via Laplace Transform**

8. Solve each IVP using the Laplace transform:
   (a) $y' - y = e^{2t}$, $y(0) = 0$
   (b) $y'' - y = 0$, $y(0) = 2$, $y'(0) = 0$
   (c) $y'' + 4y = 0$, $y(0) = 0$, $y'(0) = 3$
   (d) $y'' + 2y' + y = 0$, $y(0) = 1$, $y'(0) = -1$

9. Solve each nonhomogeneous IVP using the Laplace transform:
   (a) $y'' + 3y' + 2y = e^{-t}$, $y(0) = 0$, $y'(0) = 0$
   (b) $y'' + y = 2\cos t$ (resonant forcing), $y(0) = 0$, $y'(0) = 0$
   *(Hint: $\mathcal{L}\{\cos t\} = s/(s^2+1)$; after transforming, the denominator $(s^2+1)^2$ appears — use PFD with quadratic factors.)*
   (c) $y'' - 4y' + 4y = t\,e^{2t}$, $y(0) = 0$, $y'(0) = 0$

10. For the system $y'' + 4y' + 5y = 10$, $y(0) = 0$, $y'(0) = 0$:
    (a) Compute $Y(s)$ and identify the transfer function $H(s)$.
    (b) Find the poles of $H(s)$ and identify the damping regime.
    (c) Invert $Y(s)$ to find $y(t)$.
    (d) Verify that $y(t) \to 2$ as $t \to \infty$ (the steady-state response).

11. Solve the IVP $y'' - 5y' + 6y = 2e^t$, $y(0) = 1$, $y'(0) = 2$ using the Laplace transform.
    Compare with the classical method (Week 9) and verify both give the same answer.

12. A mass-spring-damper system has $m = 1$, $c = 2$, $k = 5$, and is driven by $F(t) = 10$ (constant force), starting from rest: $y(0) = 0$, $\dot{y}(0) = 0$.
    (a) Write the ODE and take the Laplace transform.
    (b) Identify $H(s)$ and its poles. Is the system underdamped, critically damped, or overdamped?
    (c) Find $Y(s)$ and invert to find $y(t)$.
    (d) Find the steady-state displacement $y_{\infty} = \lim_{t\to\infty}y(t)$.
    *(Hint: Final Value Theorem: $\lim_{t\to\infty}y(t) = \lim_{s\to 0}sY(s)$, provided the limit exists.)*
