# Week 1 — Differentiation & Applications

**Course:** Engineering Mathematics 1
**Part:** I — Calculus Foundations (Review)
**Supplementary Material:** `01-1 eng_math_differentiation.pdf`, `01-2 eng_math_diff_appl.pdf`

---

## Lecture 1: The Derivative — Definition and Basic Rules

### Introduction

Calculus is built on two fundamental questions: *How fast is something changing?* and *How much has something accumulated?* Differentiation answers the first. Every time an engineer asks "how does the output change when I adjust this parameter?" — they are asking a calculus question.

This lecture establishes the derivative rigorously from limits, then develops the mechanical rules that make computation practical. By the end, students should be able to differentiate any combination of power, trigonometric, exponential, and logarithmic functions without returning to the limit definition each time.

**Why it matters in engineering:**
- Velocity is the derivative of position; acceleration is the derivative of velocity.
- The sensitivity of a circuit's output to a component value is a derivative.
- Structural stress analysis, fluid flow rates, heat transfer rates — all expressed as derivatives.

---

### Knowledge Points

---

#### 1. The Two Fundamental Problems of Calculus

**What:** Calculus emerged from two geometric problems that turned out to be inverses of each other:
1. **The tangent problem** — find the slope of the line tangent to a curve at a point.
2. **The area problem** — find the area enclosed by a curve.

**Intuition:** Before calculus, only the slope of a *straight* line was well-defined (rise over run). Curves presented a challenge: the slope changes continuously. The breakthrough was to define the tangent slope as a *limit* of slopes of secant lines.

**Example:** Consider y = x². At x = 1, what is the instantaneous slope? Draw secant lines from (1, 1) to (2, 4), then to (1.5, 2.25), then to (1.1, 1.21), then to (1.01, 1.0201). The slopes are 3, 2.5, 2.1, 2.01 — converging to **2**.

---

#### 2. Secant Lines and the Difference Quotient

**What:** A **secant line** passes through two points on a curve: $(x, f(x))$ and $(x+h, f(x+h))$.

**Definition (Difference Quotient):**
$$\frac{f(x+h) - f(x)}{h}$$

This is the average rate of change of $f$ over the interval $[x, x+h]$.

**Intuition:** As $h \to 0$, the second point slides toward the first, and the secant line approaches the tangent line.

**Example:** For $f(x) = x^2$:
$$\frac{(x+h)^2 - x^2}{h} = \frac{x^2 + 2xh + h^2 - x^2}{h} = \frac{2xh + h^2}{h} = 2x + h$$
As $h \to 0$, this gives $2x$ — the derivative of $x^2$.

---

#### 3. The Formal Definition of the Derivative

**Definition:** The **derivative** of $f$ at $x$ is:
$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$
provided the limit exists.

**Notation equivalences** (all mean the same thing):
$$f'(x) = \frac{dy}{dx} = \frac{d}{dx}f(x) = Df(x) = \dot{y} \text{ (physics, for time)}$$

**Intuition:** $f'(x)$ captures the instantaneous rate of change — the slope of the tangent line at a single point, obtained by shrinking the secant interval to zero.

**Example:** Prove $\frac{d}{dx}[c] = 0$ for constant $c$:
$$\lim_{h \to 0} \frac{c - c}{h} = \lim_{h \to 0} 0 = 0$$

---

#### 4. Geometric and Physical Interpretations

**Geometric:** $f'(a)$ is the slope of the tangent line to $y = f(x)$ at $x = a$.

**Equation of the tangent line at** $(a, f(a))$:
$$y - f(a) = f'(a)(x - a)$$

**Physical:** If $s(t)$ is position at time $t$, then:
- $v(t) = s'(t)$ is instantaneous **velocity**
- $a(t) = v'(t) = s''(t)$ is instantaneous **acceleration**

**Example:** A ball is thrown upward: $s(t) = 20t - 5t^2$ (m). Find velocity at $t = 1$ s.
$$v(t) = s'(t) = 20 - 10t \implies v(1) = 10 \text{ m/s}$$

---

#### 5. Differentiability and Continuity

**Theorem:** If $f$ is differentiable at $x = a$, then $f$ is continuous at $x = a$.

**Contrapositive:** If $f$ is *not* continuous at $a$, it cannot be differentiable there.

**Important:** Continuity does **not** imply differentiability.

**Where differentiability fails:**
- **Corner:** $f(x) = |x|$ at $x = 0$ — left and right slopes differ ($-1$ vs $+1$).
- **Cusp:** $f(x) = x^{2/3}$ at $x = 0$ — slope becomes $\pm\infty$.
- **Vertical tangent:** $f(x) = x^{1/3}$ at $x = 0$.
- **Discontinuity:** Jump, infinite, or removable discontinuity.

**Example:** $f(x) = |x|$ is continuous everywhere but not differentiable at $x = 0$:
$$f'(0^-) = -1 \neq +1 = f'(0^+)$$

---

#### 6. The Power Rule

**Rule:**
$$\frac{d}{dx}\left[x^n\right] = nx^{n-1}, \quad n \in \mathbb{R}$$

**Derivation (integer case, via binomial theorem):**
$$\lim_{h\to 0}\frac{(x+h)^n - x^n}{h} = \lim_{h\to 0}\frac{nx^{n-1}h + \binom{n}{2}x^{n-2}h^2 + \cdots}{h} = nx^{n-1}$$

**Examples:**
| Function | Derivative |
|----------|------------|
| $x^5$ | $5x^4$ |
| $x^{1/2} = \sqrt{x}$ | $\frac{1}{2}x^{-1/2} = \frac{1}{2\sqrt{x}}$ |
| $x^{-3}$ | $-3x^{-4}$ |
| $x^{\pi}$ | $\pi x^{\pi - 1}$ |

---

#### 7. Linearity of Differentiation

**Constant Multiple Rule:**
$$\frac{d}{dx}[c \cdot f(x)] = c \cdot f'(x)$$

**Sum/Difference Rule:**
$$\frac{d}{dx}[f(x) \pm g(x)] = f'(x) \pm g'(x)$$

**Intuition:** Differentiation is a *linear operator* — it distributes over addition and scales with constants. This mirrors linearity in linear algebra.

**Example:** Differentiate $p(x) = 5x^4 - 3x^2 + 7x - 2$:
$$p'(x) = 20x^3 - 6x + 7$$

**Example:** Differentiate $f(x) = \frac{4}{\sqrt{x}} - 3x^{1/3} = 4x^{-1/2} - 3x^{1/3}$:
$$f'(x) = -2x^{-3/2} - x^{-2/3}$$

---

#### 8. Derivatives of Trigonometric Functions

**Key limit (proved using squeeze theorem):**
$$\lim_{h \to 0} \frac{\sin h}{h} = 1, \qquad \lim_{h \to 0} \frac{\cos h - 1}{h} = 0$$

**Derivative of sin x (from definition):**
$$\frac{d}{dx}[\sin x] = \lim_{h\to 0}\frac{\sin(x+h)-\sin x}{h} = \cos x$$

**Derivative of cos x (similarly):**
$$\frac{d}{dx}[\cos x] = -\sin x$$

**Derived trigonometric derivatives:**

| Function | Derivative |
|----------|-----------|
| $\sin x$ | $\cos x$ |
| $\cos x$ | $-\sin x$ |
| $\tan x = \sin x/\cos x$ | $\sec^2 x$ |
| $\cot x$ | $-\csc^2 x$ |
| $\sec x$ | $\sec x \tan x$ |
| $\csc x$ | $-\csc x \cot x$ |

**Example:** Differentiate $f(x) = 3\sin x - 2\cos x + \tan x$:
$$f'(x) = 3\cos x + 2\sin x + \sec^2 x$$

---

#### 9. Derivatives of Exponential Functions

**The number e** is defined so that $\frac{d}{dx}[e^x] = e^x$ — the exponential function is its own derivative. This unique property makes $e^x$ fundamental throughout engineering mathematics.

$$\frac{d}{dx}[e^x] = e^x$$

**General base:**
$$\frac{d}{dx}[a^x] = a^x \ln a$$

**Intuition:** Each exponential function grows proportionally to itself. The constant of proportionality is $\ln a$; for $a = e$, $\ln e = 1$, giving the clean result.

**Example:** Differentiate $f(x) = 5e^x - 2^x$:
$$f'(x) = 5e^x - 2^x \ln 2$$

---

#### 10. Derivatives of Logarithmic Functions

$$\frac{d}{dx}[\ln x] = \frac{1}{x}, \quad x > 0$$

$$\frac{d}{dx}[\log_a x] = \frac{1}{x \ln a}$$

**Derivation of $\ln x$:** Use the inverse relationship with $e^x$. If $y = \ln x$ then $x = e^y$, so $\frac{dx}{dy} = e^y = x$, and $\frac{dy}{dx} = \frac{1}{x}$.

**Useful extension:**
$$\frac{d}{dx}[\ln|x|] = \frac{1}{x}, \quad x \neq 0$$

**Example:** Differentiate $f(x) = x^2 \ln x$ (uses product rule next lecture):
$$f'(x) = 2x \ln x + x^2 \cdot \frac{1}{x} = 2x\ln x + x = x(2\ln x + 1)$$

---

#### 11. The Product Rule

**Rule:**
$$\frac{d}{dx}[f(x)\,g(x)] = f'(x)\,g(x) + f(x)\,g'(x)$$

**Memory aid:** "derivative of first times second, plus first times derivative of second."

**Intuition:** If both $f$ and $g$ change simultaneously, the total rate of change accounts for both increments. The cross terms $f'g$ and $fg'$ come from the area interpretation.

**Example 1:** $h(x) = x^3 \sin x$:
$$h'(x) = 3x^2 \sin x + x^3 \cos x$$

**Example 2:** $h(x) = e^x \ln x$:
$$h'(x) = e^x \ln x + e^x \cdot \frac{1}{x} = e^x\!\left(\ln x + \frac{1}{x}\right)$$

---

#### 12. The Quotient Rule

**Rule:**
$$\frac{d}{dx}\!\left[\frac{f(x)}{g(x)}\right] = \frac{f'(x)\,g(x) - f(x)\,g'(x)}{[g(x)]^2}$$

**Memory aid:** "low d-high minus high d-low, over low squared."

**Derivation:** Write $f/g = f \cdot g^{-1}$ and apply the product rule combined with the chain rule $\frac{d}{dx}[g^{-1}] = -g^{-2}g'$.

**Example 1:** Derive $\frac{d}{dx}[\tan x] = \sec^2 x$:
$$\frac{d}{dx}\!\left[\frac{\sin x}{\cos x}\right] = \frac{\cos x \cdot \cos x - \sin x \cdot (-\sin x)}{\cos^2 x} = \frac{\cos^2 x + \sin^2 x}{\cos^2 x} = \frac{1}{\cos^2 x} = \sec^2 x$$

**Example 2:** $h(x) = \frac{x^2 + 1}{e^x}$:
$$h'(x) = \frac{2x \cdot e^x - (x^2+1)\cdot e^x}{e^{2x}} = \frac{e^x(2x - x^2 - 1)}{e^{2x}} = \frac{-(x^2 - 2x + 1)}{e^x} = \frac{-(x-1)^2}{e^x}$$

---

#### 13. Summary: Quick Reference — Lecture 1

| Function | Derivative |
|----------|-----------|
| $c$ | $0$ |
| $x^n$ | $nx^{n-1}$ |
| $cf(x)$ | $cf'(x)$ |
| $f \pm g$ | $f' \pm g'$ |
| $fg$ | $f'g + fg'$ |
| $f/g$ | $(f'g - fg')/g^2$ |
| $\sin x$ | $\cos x$ |
| $\cos x$ | $-\sin x$ |
| $\tan x$ | $\sec^2 x$ |
| $e^x$ | $e^x$ |
| $a^x$ | $a^x \ln a$ |
| $\ln x$ | $1/x$ |

---

## Lecture 2: Hyperbolic Functions, Chain Rule, and Implicit Differentiation

### Introduction

Lecture 1 handled "flat" compositions — sums and products of elementary functions. Real engineering problems involve **compositions**: the temperature depends on position, which depends on time. The **Chain Rule** is the engine for differentiating such nested functions. This lecture also introduces **hyperbolic functions**, which arise naturally in the shape of hanging cables, heat distribution, and wave propagation, and covers **implicit differentiation**, which handles curves that cannot be expressed as explicit functions $y = f(x)$.

**Why it matters:**
- Catenary cables (suspension bridges, power lines) have shape $y = a\cosh(x/a)$.
- The chain rule is the most-used differentiation technique in all of engineering.
- Implicit curves describe constraints in mechanical systems, thermodynamics, and circuit analysis.

---

### Knowledge Points

---

#### 1. Hyperbolic Functions — Definitions

**Motivation:** The ordinary trig functions parameterize the unit circle $x^2 + y^2 = 1$ via $(\cos\theta, \sin\theta)$. Hyperbolic functions parameterize the unit hyperbola $x^2 - y^2 = 1$ via $(\cosh t, \sinh t)$.

**Definitions:**
$$\sinh x = \frac{e^x - e^{-x}}{2} \qquad \cosh x = \frac{e^x + e^{-x}}{2}$$

$$\tanh x = \frac{\sinh x}{\cosh x} = \frac{e^x - e^{-x}}{e^x + e^{-x}}$$

$$\coth x = \frac{\cosh x}{\sinh x}, \qquad \text{sech}\, x = \frac{1}{\cosh x}, \qquad \text{csch}\, x = \frac{1}{\sinh x}$$

**Key values:**
- $\sinh 0 = 0$, $\cosh 0 = 1$, $\tanh 0 = 0$
- $\cosh x \geq 1$ for all $x$; $\sinh x$ is odd; $\cosh x$ is even

---

#### 2. Hyperbolic Identity: cosh²x − sinh²x = 1

**Proof:**
$$\cosh^2 x - \sinh^2 x = \left(\frac{e^x+e^{-x}}{2}\right)^2 - \left(\frac{e^x-e^{-x}}{2}\right)^2$$
$$= \frac{(e^x+e^{-x})^2 - (e^x-e^{-x})^2}{4} = \frac{4e^x e^{-x}}{4} = 1$$

**Analogy with trigonometry:**

| Trigonometric | Hyperbolic |
|--------------|-----------|
| $\cos^2 x + \sin^2 x = 1$ | $\cosh^2 x - \sinh^2 x = 1$ |
| $1 + \tan^2 x = \sec^2 x$ | $1 - \tanh^2 x = \text{sech}^2 x$ |
| $\sin(x+y) = \ldots$ | $\sinh(x+y) = \sinh x\cosh y + \cosh x\sinh y$ |

---

#### 3. Graphs and Behaviour of Hyperbolic Functions

**sinh x:**
- Domain: $\mathbb{R}$, Range: $\mathbb{R}$
- Odd function: $\sinh(-x) = -\sinh x$
- Strictly increasing; $\sinh x \approx x$ for small $x$
- $\sinh x \approx \frac{1}{2}e^x$ as $x \to +\infty$

**cosh x:**
- Domain: $\mathbb{R}$, Range: $[1, \infty)$
- Even function: $\cosh(-x) = \cosh x$
- Minimum value 1 at $x = 0$ (the catenary shape)

**tanh x:**
- Domain: $\mathbb{R}$, Range: $(-1, 1)$
- Odd; has horizontal asymptotes at $\pm 1$
- S-shaped, resembling the logistic curve

**Engineering application — the catenary:**
A flexible cable hanging under its own weight takes the shape $y = a\cosh(x/a)$, not a parabola. This exact shape governs power lines and suspension bridge cables.

---

#### 4. Derivatives of Hyperbolic Functions

$$\frac{d}{dx}[\sinh x] = \cosh x \qquad \frac{d}{dx}[\cosh x] = \sinh x$$

**Derivation of the first:**
$$\frac{d}{dx}\!\left[\frac{e^x - e^{-x}}{2}\right] = \frac{e^x + e^{-x}}{2} = \cosh x$$

**Note:** Unlike $\frac{d}{dx}[\cos x] = -\sin x$ (negative sign), $\frac{d}{dx}[\cosh x] = +\sinh x$ (positive sign).

$$\frac{d}{dx}[\tanh x] = \text{sech}^2 x \qquad \frac{d}{dx}[\text{sech}\,x] = -\text{sech}\,x\tanh x$$

| Hyperbolic | Derivative |
|-----------|-----------|
| $\sinh x$ | $\cosh x$ |
| $\cosh x$ | $\sinh x$ |
| $\tanh x$ | $\text{sech}^2 x$ |
| $\coth x$ | $-\text{csch}^2 x$ |
| $\text{sech}\,x$ | $-\text{sech}\,x\tanh x$ |
| $\text{csch}\,x$ | $-\text{csch}\,x\coth x$ |

---

#### 5. Chain Rule — Motivation

**Problem:** How do we differentiate $f(x) = \sin(x^2)$? The rules from Lecture 1 don't apply directly — this is a function *inside* another function.

**Setup:** Let $u = g(x) = x^2$ (inner function) and $y = f(u) = \sin u$ (outer function). Then $y = f(g(x))$.

**Intuition via Leibniz notation:**
$$\frac{dy}{dx} = \frac{dy}{du} \cdot \frac{du}{dx}$$
"The rate of change of $y$ with respect to $x$ equals the rate of change of $y$ with respect to $u$, times the rate of change of $u$ with respect to $x$."

---

#### 6. Chain Rule — Formal Statement

**Theorem (Chain Rule):** If $g$ is differentiable at $x$ and $f$ is differentiable at $g(x)$, then:
$$(f \circ g)'(x) = f'(g(x)) \cdot g'(x)$$

**In words:** Derivative of outer function (evaluated at inner) times derivative of inner function.

**Procedure:**
1. Identify the outer function $f$ and inner function $g$.
2. Differentiate $f$ but leave $g(x)$ intact inside.
3. Multiply by the derivative of $g(x)$.

---

#### 7. Chain Rule — Examples

**Example 1:** $h(x) = \sin(x^2)$

- Outer: $\sin(\cdot)$, derivative $\cos(\cdot)$; Inner: $x^2$, derivative $2x$
$$h'(x) = \cos(x^2) \cdot 2x = 2x\cos(x^2)$$

**Example 2:** $h(x) = e^{3x+1}$

$$h'(x) = e^{3x+1} \cdot 3 = 3e^{3x+1}$$

**Example 3:** $h(x) = (x^3 + 5)^{10}$

$$h'(x) = 10(x^3+5)^9 \cdot 3x^2 = 30x^2(x^3+5)^9$$

**Example 4:** $h(x) = \ln(\cos x)$

$$h'(x) = \frac{1}{\cos x} \cdot (-\sin x) = -\tan x$$

**Example 5 (triple composition):** $h(x) = e^{\sin(x^2)}$

$$h'(x) = e^{\sin(x^2)} \cdot \cos(x^2) \cdot 2x$$

---

#### 8. Inverse Function Theorem

**Motivation:** We now want to differentiate $f^{-1}$ — the inverse of a given function. Rather than finding a formula for $f^{-1}$ and differentiating it directly (often impossible), the Inverse Function Theorem gives the derivative of $f^{-1}$ directly in terms of the derivative of $f$.

**Theorem (Inverse Function Theorem):** Let $f$ be differentiable on an open interval containing $x_0$, and suppose $f'(x_0) \neq 0$. Then $f^{-1}$ exists and is differentiable near $y_0 = f(x_0)$, with:
$$(f^{-1})'(y_0) = \frac{1}{f'(x_0)} = \frac{1}{f'\!\left(f^{-1}(y_0)\right)}$$

**In Leibniz notation:** if $y = f(x)$, then
$$\frac{dx}{dy} = \frac{1}{\,dy/dx\,}$$

**Geometric intuition:** Reflecting a graph across $y = x$ exchanges the roles of the axes — a slope of $m$ in $f$ becomes a slope of $1/m$ in $f^{-1}$. If $f$ is steep, $f^{-1}$ is shallow, and vice versa. (This fails only where $f'(x_0) = 0$ — a horizontal tangent in $f$ becomes a vertical tangent in $f^{-1}$, where differentiability breaks down.)

**Proof:** Since $f(f^{-1}(y)) = y$ for all $y$ in the range of $f$, differentiate both sides with respect to $y$ using the Chain Rule:
$$f'\!\left(f^{-1}(y)\right)\cdot (f^{-1})'(y) = 1$$
$$\implies (f^{-1})'(y) = \frac{1}{f'\!\left(f^{-1}(y)\right)}$$

**Condition $f'(x_0) \neq 0$:** If $f'(x_0) = 0$, the formula gives division by zero — reflecting the fact that $f^{-1}$ has a vertical tangent at $y_0$ and is not differentiable there.

**Example 1 — power function:** $f(x) = x^3$, so $f^{-1}(y) = y^{1/3}$ and $f'(x) = 3x^2$.

Using the theorem at $y = y_0$, with $x_0 = y_0^{1/3}$:
$$(f^{-1})'(y_0) = \frac{1}{3x_0^2} = \frac{1}{3(y_0^{1/3})^2} = \frac{1}{3}y_0^{-2/3}$$
This matches $\frac{d}{dy}[y^{1/3}] = \frac{1}{3}y^{-2/3}$ from the Power Rule. ✓

**Example 2 — exponential/logarithm:** $f(x) = e^x$, $f^{-1}(y) = \ln y$, $f'(x) = e^x$.
$$(f^{-1})'(y) = \frac{1}{e^{f^{-1}(y)}} = \frac{1}{e^{\ln y}} = \frac{1}{y}$$
This recovers $\frac{d}{dy}[\ln y] = 1/y$. ✓

**Why this matters:** The derivatives of all inverse trigonometric and inverse hyperbolic functions in the next two sections are derived using exactly this theorem — or equivalently, via implicit differentiation of the defining relation $f(f^{-1}(x)) = x$.

---

#### 9. Derivatives of Inverse Trigonometric Functions

**Setup:** To differentiate $y = \arcsin x$, write $\sin y = x$ and differentiate implicitly.

$$\cos y \cdot \frac{dy}{dx} = 1 \implies \frac{dy}{dx} = \frac{1}{\cos y} = \frac{1}{\sqrt{1-\sin^2 y}} = \frac{1}{\sqrt{1-x^2}}$$

**Complete table of inverse trigonometric derivatives:**

| Function | Derivative | Domain |
|----------|-----------|--------|
| $\arcsin x$ | $\dfrac{1}{\sqrt{1-x^2}}$ | $|x| < 1$ |
| $\arccos x$ | $-\dfrac{1}{\sqrt{1-x^2}}$ | $|x| < 1$ |
| $\arctan x$ | $\dfrac{1}{1+x^2}$ | $\mathbb{R}$ |
| $\text{arccot}\,x$ | $-\dfrac{1}{1+x^2}$ | $\mathbb{R}$ |
| $\text{arcsec}\,x$ | $\dfrac{1}{|x|\sqrt{x^2-1}}$ | $|x| > 1$ |

**Example with Chain Rule:** $h(x) = \arctan(e^x)$:
$$h'(x) = \frac{1}{1 + e^{2x}} \cdot e^x = \frac{e^x}{1+e^{2x}}$$

---

#### 10. Derivatives of Inverse Hyperbolic Functions

**Key results:**

| Function | Derivative | Note |
|----------|-----------|------|
| $\sinh^{-1} x = \ln(x + \sqrt{x^2+1})$ | $\dfrac{1}{\sqrt{x^2+1}}$ | Domain: $\mathbb{R}$ |
| $\cosh^{-1} x = \ln(x + \sqrt{x^2-1})$ | $\dfrac{1}{\sqrt{x^2-1}}$ | $x > 1$ |
| $\tanh^{-1} x = \frac{1}{2}\ln\!\frac{1+x}{1-x}$ | $\dfrac{1}{1-x^2}$ | $|x| < 1$ |

**Example:** $h(x) = \tanh^{-1}(\sin x)$:
$$h'(x) = \frac{1}{1 - \sin^2 x} \cdot \cos x = \frac{\cos x}{\cos^2 x} = \sec x$$

---

#### 11. Implicit Differentiation — Motivation and Technique

**Motivation:** The equation $x^2 + y^2 = 25$ defines a circle. Solving for $y$ gives $y = \pm\sqrt{25 - x^2}$ — two branches, neither globally a function. Implicit differentiation finds $dy/dx$ directly from the equation without solving for $y$.

**Technique:**
1. Differentiate both sides with respect to $x$.
2. Treat $y$ as a function of $x$ — every time you differentiate a term in $y$, multiply by $\frac{dy}{dx}$.
3. Collect all $\frac{dy}{dx}$ terms and solve algebraically.

---

#### 12. Implicit Differentiation — Examples

**Example 1:** $x^2 + y^2 = 25$
$$2x + 2y\frac{dy}{dx} = 0 \implies \frac{dy}{dx} = -\frac{x}{y}$$

At $(3, 4)$: slope $= -3/4$. Tangent line: $y - 4 = -\frac{3}{4}(x - 3)$.

**Example 2:** $x^3 + y^3 = 6xy$ (Folium of Descartes)
$$3x^2 + 3y^2\frac{dy}{dx} = 6y + 6x\frac{dy}{dx}$$
$$\frac{dy}{dx}(3y^2 - 6x) = 6y - 3x^2 \implies \frac{dy}{dx} = \frac{6y - 3x^2}{3y^2 - 6x} = \frac{2y - x^2}{y^2 - 2x}$$

**Example 3:** $e^{xy} = x + y$
$$e^{xy}\!\left(y + x\frac{dy}{dx}\right) = 1 + \frac{dy}{dx} \implies \frac{dy}{dx} = \frac{1 - ye^{xy}}{xe^{xy} - 1}$$

---

#### 13. Logarithmic Differentiation

**Purpose:** Efficiently differentiates products of many terms, or functions of the form $[f(x)]^{g(x)}$.

**Technique:**
1. Take $\ln$ of both sides.
2. Differentiate implicitly.
3. Multiply through by $y$.

**Example:** $y = x^{\sin x}$ (variable base AND variable exponent):
$$\ln y = \sin x \cdot \ln x$$
$$\frac{1}{y}\frac{dy}{dx} = \cos x \ln x + \frac{\sin x}{x}$$
$$\frac{dy}{dx} = x^{\sin x}\!\left(\cos x \ln x + \frac{\sin x}{x}\right)$$

**Example:** $y = \frac{(x^2+1)^3 \sqrt{x-1}}{e^x \cos x}$

Take ln, differentiate, multiply by $y$ — far more efficient than product/quotient rule directly.

---

#### 14. Summary — Lecture 2

| Technique | When to use |
|-----------|-------------|
| Chain Rule | Composition $f(g(x))$ |
| Implicit differentiation | Curve not solved for $y$ |
| Logarithmic differentiation | $[f(x)]^{g(x)}$; large products/quotients |
| Inverse trig derivatives | $\arcsin$, $\arctan$, etc. |
| Inverse hyperbolic derivatives | $\sinh^{-1}$, $\tanh^{-1}$, etc. |

**Key identities to remember:**
$$\cosh^2 x - \sinh^2 x = 1, \qquad \frac{d}{dx}[\sinh x] = \cosh x, \qquad \frac{d}{dx}[\cosh x] = \sinh x$$

---

## Lecture 3: Mean Value Theorem, L'Hôpital's Rule, and Local Extrema

### Introduction

So far, differentiation has been a computational skill — finding $f'(x)$. This lecture shifts to **using** the derivative as an analytical tool. The **Mean Value Theorem** is the rigorous foundation that connects a function's average and instantaneous rates of change. **L'Hôpital's Rule** resolves the mysterious "0/0" and "∞/∞" forms that appear throughout engineering calculations. The theory of **local extrema** turns the derivative into an optimization machine — one of the most important applications in all of applied mathematics.

**Why it matters:**
- Optimization is ubiquitous: maximize power output, minimize material cost, find the fastest path.
- Indeterminate limits appear in signal processing, control theory, and numerical analysis.
- The MVT underpins error estimates, numerical methods, and stability analysis.

---

### Knowledge Points

---

#### 1. Rolle's Theorem

**Theorem (Rolle, 1691):** Let $f$ be continuous on $[a, b]$, differentiable on $(a, b)$, and $f(a) = f(b)$. Then there exists at least one $c \in (a, b)$ such that $f'(c) = 0$.

**Geometric interpretation:** If a smooth curve starts and ends at the same height, it must have at least one horizontal tangent somewhere in between.

**Intuition:** The function must turn around — which requires a critical point.

**Example:** $f(x) = x^3 - x$ on $[-1, 1]$: $f(-1) = 0 = f(1)$.
$$f'(x) = 3x^2 - 1 = 0 \implies x = \pm\frac{1}{\sqrt{3}} \in (-1,1) \checkmark$$

**Proof sketch:** $f$ attains its maximum and minimum on $[a,b]$ (Extreme Value Theorem). If both occur at the endpoints, then $f$ is constant and $f' \equiv 0$. Otherwise, an interior extremum exists — and at an interior extremum of a differentiable function, $f' = 0$.

---

#### 2. Mean Value Theorem (MVT)

**Theorem:** Let $f$ be continuous on $[a, b]$ and differentiable on $(a, b)$. Then there exists at least one $c \in (a, b)$ such that:
$$f'(c) = \frac{f(b) - f(a)}{b - a}$$

**Geometric interpretation:** There is a point where the tangent line is parallel to the secant line connecting $(a, f(a))$ to $(b, f(b))$.

**Physical interpretation:** If you travel 200 km in 2 hours, at some instant your speedometer read exactly 100 km/h.

**Proof:** Apply Rolle's Theorem to:
$$g(x) = f(x) - \left[f(a) + \frac{f(b)-f(a)}{b-a}(x-a)\right]$$
which satisfies $g(a) = g(b) = 0$.

---

#### 3. Consequences of the MVT

**Corollary 1 — Monotonicity test:**
- If $f'(x) > 0$ on $(a,b)$, then $f$ is **strictly increasing** on $[a,b]$.
- If $f'(x) < 0$ on $(a,b)$, then $f$ is **strictly decreasing** on $[a,b]$.
- If $f'(x) = 0$ on $(a,b)$, then $f$ is **constant** on $[a,b]$.

**Corollary 2 — Uniqueness of antiderivatives:** If $f'(x) = g'(x)$ for all $x \in (a,b)$, then $f(x) = g(x) + C$ for some constant $C$.

**Example:** Show $f(x) = x^3 - 3x^2 + 4$ is decreasing on $(0, 2)$.
$$f'(x) = 3x^2 - 6x = 3x(x-2) < 0 \text{ for } x \in (0,2) \checkmark$$

---

#### 4. Indeterminate Forms

**The problem:** Direct substitution in $\lim_{x\to 0}\frac{\sin x}{x}$ gives $\frac{0}{0}$ — a meaningless form. Standard limit rules do not apply.

**The seven indeterminate forms:**

| Form | Example |
|------|---------|
| $0/0$ | $\lim_{x\to 0}\frac{\sin x}{x}$ |
| $\infty/\infty$ | $\lim_{x\to\infty}\frac{x^2}{e^x}$ |
| $0 \cdot \infty$ | $\lim_{x\to 0^+} x\ln x$ |
| $\infty - \infty$ | $\lim_{x\to\infty}(\sqrt{x^2+x} - x)$ |
| $0^0$ | $\lim_{x\to 0^+} x^x$ |
| $1^\infty$ | $\lim_{x\to\infty}\left(1+\frac{1}{x}\right)^x$ |
| $\infty^0$ | $\lim_{x\to\infty} x^{1/x}$ |

**Key insight:** These forms are not defined because the limit could, in principle, take any value or diverge. We need additional analysis — which is where L'Hôpital's Rule comes in.

---

#### 5. L'Hôpital's Rule

**Theorem (L'Hôpital, 1696):** Suppose $\lim_{x\to a} f(x) = 0$ and $\lim_{x\to a} g(x) = 0$ (or both $\to \pm\infty$), and $g'(x) \neq 0$ near $a$. Then:
$$\lim_{x \to a} \frac{f(x)}{g(x)} = \lim_{x \to a} \frac{f'(x)}{g'(x)}$$
provided the right-hand limit exists (or is $\pm\infty$).

**Crucial warnings:**
- Apply **only** to $0/0$ or $\infty/\infty$ forms — not to ordinary limits.
- Check that you are differentiating $f$ and $g$ **separately**, not using the quotient rule.
- May be applied **repeatedly** if the result is still indeterminate.

---

#### 6. L'Hôpital's Rule — Examples (0/0 form)

**Example 1:** $\displaystyle\lim_{x\to 0}\frac{\sin x}{x}$
$$\to \frac{\cos x}{1}\bigg|_{x=0} = 1$$

**Example 2:** $\displaystyle\lim_{x\to 0}\frac{e^x - 1 - x}{x^2}$
$$\to \frac{e^x - 1}{2x} \to \frac{e^x}{2}\bigg|_{x=0} = \frac{1}{2}$$

**Example 3:** $\displaystyle\lim_{x\to 0}\frac{1 - \cos x}{x^2}$
$$\to \frac{\sin x}{2x} \to \frac{\cos x}{2}\bigg|_{x=0} = \frac{1}{2}$$

---

#### 7. L'Hôpital's Rule — Examples (∞/∞ and Other Forms)

**Example (∞/∞):** $\displaystyle\lim_{x\to\infty}\frac{\ln x}{x}$
$$\to \frac{1/x}{1} = \frac{1}{x} \to 0$$
**Conclusion:** Logarithm grows slower than any positive power of $x$.

**Example (0·∞ → convert):** $\displaystyle\lim_{x\to 0^+} x\ln x = \lim_{x\to 0^+}\frac{\ln x}{1/x}$
$$\to \frac{1/x}{-1/x^2} = -x \to 0$$

**Example (1^∞):** $\displaystyle\lim_{x\to\infty}\left(1 + \frac{1}{x}\right)^x$

Let $L = \lim_{x\to\infty} x\ln\!\left(1 + \frac{1}{x}\right) = \lim_{x\to\infty}\frac{\ln(1+1/x)}{1/x} \to \frac{-1/x^2 \cdot 1/(1+1/x)}{-1/x^2} = 1$

So the original limit is $e^L = e^1 = e$.

---

#### 8. Local Extrema — Definitions

**Definition:** A function $f$ has a **local maximum** at $c$ if $f(c) \geq f(x)$ for all $x$ near $c$.
A function $f$ has a **local minimum** at $c$ if $f(c) \leq f(x)$ for all $x$ near $c$.

**Definition:** $c$ is a **critical point** of $f$ if either $f'(c) = 0$ or $f'(c)$ does not exist.

**Theorem (Fermat):** If $f$ has a local extremum at $c$ and $f'(c)$ exists, then $f'(c) = 0$.

**Warning:** The converse is **false** — $f'(c) = 0$ does not guarantee an extremum. Example: $f(x) = x^3$ has $f'(0) = 0$ but no local extremum at $x = 0$.

---

#### 9. First Derivative Test

**Theorem:** Suppose $c$ is a critical point of $f$ and $f$ is continuous near $c$.

- If $f'$ changes from **positive to negative** at $c$ → **local maximum**.
- If $f'$ changes from **negative to positive** at $c$ → **local minimum**.
- If $f'$ does **not change sign** at $c$ → **neither** (inflection point).

**Procedure:**
1. Find critical points: solve $f'(x) = 0$ and find where $f'$ is undefined.
2. Build a sign chart for $f'$.
3. Read off the nature of each critical point.

**Example:** $f(x) = x^3 - 3x + 2$
$$f'(x) = 3x^2 - 3 = 3(x-1)(x+1) = 0 \implies x = \pm 1$$

| Interval | Sign of $f'$ | Behaviour |
|----------|-------------|-----------|
| $x < -1$ | $+$ | Increasing |
| $-1 < x < 1$ | $-$ | Decreasing |
| $x > 1$ | $+$ | Increasing |

Local maximum at $x = -1$: $f(-1) = 4$. Local minimum at $x = 1$: $f(1) = 0$.

---

#### 10. Second Derivative Test

**Theorem:** Let $f'(c) = 0$.
- If $f''(c) > 0$ → $f$ is concave up at $c$ → **local minimum**.
- If $f''(c) < 0$ → $f$ is concave down at $c$ → **local maximum**.
- If $f''(c) = 0$ → **inconclusive** (use First Derivative Test).

**Geometric intuition:** $f''(c) > 0$ means the slope is increasing through $c$ — the function is "bowl-shaped" upward, so $c$ is a minimum.

**Example:** $f(x) = x^4 - 4x^2$
$$f'(x) = 4x^3 - 8x = 4x(x^2-2) = 0 \implies x = 0,\ \pm\sqrt{2}$$
$$f''(x) = 12x^2 - 8$$
- $f''(0) = -8 < 0$ → local **maximum** at $x = 0$, $f(0) = 0$
- $f''(\pm\sqrt{2}) = 24 - 8 = 16 > 0$ → local **minimum** at $x = \pm\sqrt{2}$, $f(\pm\sqrt{2}) = -4$

---

#### 11. Concavity and Inflection Points

**Definition:** $f$ is **concave up** on $(a,b)$ if $f'$ is *increasing* on $(a,b)$ — the slope gets steeper as $x$ increases.
$f$ is **concave down** on $(a,b)$ if $f'$ is *decreasing* on $(a,b)$ — the slope gets less steep as $x$ increases.

**Intuition:** Concave up means the curve "holds water" (bowl shape); concave down means it "spills water" (dome shape). No assumption on the existence of $f''$ is needed — the definition is entirely about the behaviour of $f'$.

**Computational corollary (when $f''$ exists):** Since $f''$ is the derivative of $f'$:
- $f''(x) > 0$ on $(a,b)$ $\implies$ $f'$ is increasing $\implies$ $f$ is **concave up**.
- $f''(x) < 0$ on $(a,b)$ $\implies$ $f'$ is decreasing $\implies$ $f$ is **concave down**.

This corollary gives a convenient test whenever $f''$ exists, but the definition stands independently.

**Definition:** $c$ is an **inflection point** if $f$ changes concavity at $c$ (and $f$ is continuous at $c$).

**Necessary condition (when $f''$ exists):** $f''(c) = 0$ or $f''(c)$ does not exist at an inflection point.

**Example:** $f(x) = x^3$: $f'(x) = 3x^2$, which is decreasing on $(-\infty, 0)$ and increasing on $(0, \infty)$.
- $f'$ decreasing for $x < 0$: concave down.
- $f'$ increasing for $x > 0$: concave up.
- Inflection point at $x = 0$ (confirmed: $f''(x) = 6x$ changes sign there).

**Engineering relevance:** Inflection points mark where the rate of change begins decreasing — for example, the point of diminishing returns in a production model.

---

#### 12. Absolute Extrema and the Extreme Value Theorem

**Theorem (Extreme Value Theorem):** If $f$ is continuous on a **closed** interval $[a, b]$, then $f$ attains both an absolute maximum and an absolute minimum on $[a, b]$.

**Method for closed intervals — the Closed Interval Method:**
1. Find all critical points in $(a,b)$.
2. Evaluate $f$ at each critical point AND at the endpoints $a$ and $b$.
3. The largest value is the absolute maximum; the smallest is the absolute minimum.

**Example:** Find the absolute extrema of $f(x) = x^3 - 3x^2 + 1$ on $[-1/2, 4]$.
$$f'(x) = 3x^2 - 6x = 3x(x-2) = 0 \implies x = 0,\ x = 2$$

| Point | Value |
|-------|-------|
| $x = -1/2$ | $f(-1/2) = 5/8$ |
| $x = 0$ | $f(0) = 1$ |
| $x = 2$ | $f(2) = -3$ |
| $x = 4$ | $f(4) = 17$ |

Absolute maximum: $f(4) = 17$. Absolute minimum: $f(2) = -3$.

---

#### 13. A Complete Curve Sketching Procedure

**Step-by-step guide for sketching $y = f(x)$:**

1. **Domain:** Identify where $f$ is defined.
2. **Intercepts:** Find $f(0)$ (y-intercept) and solve $f(x) = 0$ (x-intercepts).
3. **Symmetry:** Check if $f$ is even ($f(-x) = f(x)$), odd ($f(-x) = -f(x)$), or periodic.
4. **Asymptotes:**
   - Horizontal: $\lim_{x\to\pm\infty} f(x)$
   - Vertical: where $f \to \pm\infty$
5. **Monotonicity:** Sign of $f'$ → intervals of increase and decrease.
6. **Local extrema:** Apply First or Second Derivative Test.
7. **Concavity:** Sign of $f''$ → concave up/down intervals.
8. **Inflection points:** Where $f''$ changes sign.
9. **Sketch:** Plot key points and join with the correct shape.

---

#### 14. Curve Sketching — Worked Example

**Sketch $f(x) = \dfrac{x^2}{x^2 - 1}$.**

1. **Domain:** $x \neq \pm 1$
2. **Intercepts:** $f(0) = 0$ (only intercept)
3. **Symmetry:** Even function ($f(-x) = f(x)$)
4. **Asymptotes:** Vertical at $x = \pm 1$; Horizontal: $\lim_{x\to\pm\infty} f(x) = 1$
5. **Monotonicity:** $f'(x) = \dfrac{-2x}{(x^2-1)^2}$
   - $f' > 0$ for $x < 0$ (excluding $x=-1$): increasing
   - $f' < 0$ for $x > 0$ (excluding $x=1$): decreasing
6. **Local extremum:** $f'(0) = 0$, $f''(0) > 0$ → local minimum at $(0,0)$
7. **Concavity:** $f''(x) = \dfrac{6x^2+2}{(x^2-1)^3}$ — analyze sign by region
8. **No inflection points** (sign of $f''$ doesn't change in each region)

---

#### 15. Summary — Lecture 3

**Mean Value Theorem toolkit:**

| Tool | Statement | Use |
|------|-----------|-----|
| Rolle's Theorem | $f(a)=f(b)$ → $\exists c$: $f'(c)=0$ | Existence of critical points |
| MVT | $\exists c$: $f'(c) = \frac{f(b)-f(a)}{b-a}$ | Monotonicity, error bounds |

**Optimization toolkit:**

| Test | Condition | Conclusion |
|------|-----------|------------|
| First Derivative | $f'$ changes $+$ to $-$ | Local max |
| First Derivative | $f'$ changes $-$ to $+$ | Local min |
| Second Derivative | $f'(c)=0$, $f''(c)<0$ | Local max |
| Second Derivative | $f'(c)=0$, $f''(c)>0$ | Local min |
| Closed Interval Method | Evaluate $f$ at critical pts + endpoints | Absolute extrema |

**L'Hôpital's Rule:** Valid for $0/0$ and $\infty/\infty$ forms only.
Other forms ($0\cdot\infty$, $\infty-\infty$, $0^0$, $1^\infty$, $\infty^0$) must first be algebraically converted.

---

## Practice Session

**Theme:** Finding derivatives; curve sketching using the first and second derivative tests.

### Practice Problems

**Set A — Differentiation drill (Lectures 1 & 2)**

1. Differentiate $f(x) = 3x^4 - \sqrt{x} + \frac{2}{x^3}$.
2. Differentiate $g(x) = e^{x^2}\sin(3x)$.
3. Differentiate $h(x) = \arctan\!\left(\frac{x}{a}\right)$ (a > 0 constant).
4. Find $dy/dx$ for $x^2y + y^3 = x + 1$.
5. Differentiate $y = (\sinh x)^{\cos x}$ using logarithmic differentiation.
6. Verify that $y = A\cosh(kx) + B\sinh(kx)$ satisfies $y'' = k^2 y$.

**Set B — L'Hôpital's Rule**

7. $\displaystyle\lim_{x\to 0}\frac{\tan x - x}{x^3}$
8. $\displaystyle\lim_{x\to\infty} x^2 e^{-x}$
9. $\displaystyle\lim_{x\to 0^+} x^x$
10. $\displaystyle\lim_{x\to 1}\frac{x^n - 1}{x - 1}$ (generalizes to derivative definition)

**Set C — Extrema and curve sketching**

11. Find all local extrema of $f(x) = x^4 - 8x^2 + 3$.
12. Find the inflection points of $g(x) = xe^{-x}$.
13. A rectangular box (no lid) with square base and volume $32\ \text{m}^3$: find dimensions minimizing surface area.
14. Sketch the full curve $f(x) = \dfrac{x}{x^2+1}$, identifying all features.
