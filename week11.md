# Week 11 — Sequences and Infinite Series

**Course:** Engineering Mathematics 1
**Part:** IV — Sequences, Series & Power Series Solutions
**Kreyszig Sections:** Supplementary Notes (§11)

> **Opening Part IV:** Weeks 1–10 dealt with functions of a real variable and ODEs whose solutions are expressible in closed form — exponentials, sines, polynomials. Part IV confronts the limits of this: many important ODEs have solutions that cannot be expressed in elementary functions. The answer is to represent functions as **infinite series** — sums of infinitely many terms. This week builds the convergence theory needed to work with such sums rigorously: when does an infinite series have a finite value, and when does it not? The Ratio Test emerges as the primary practical tool, and the week closes with **power series** — the central object of Weeks 12–13.

---

## Lecture 1: Sequences and Series — Foundations

### Introduction

An **infinite series** $\sum_{n=1}^\infty a_n$ is defined as the limit of its partial sums. Without understanding this limit, manipulating infinite sums is meaningless — or worse, leads to contradictions (famous: $1 - 1 + 1 - 1 + \cdots = 1/2$?). This lecture establishes the rigorous foundation: sequences, their limits, and the geometric and $p$-series as the fundamental benchmarks for all convergence tests.

**Why it matters in engineering:**
- Taylor series expansions (Week 12) are only valid within their radius of convergence — knowing where a series converges is essential before using it.
- Numerical methods truncate infinite series; the error bounds require knowing the series converges.
- Signal processing: Fourier series (not this course, but the same convergence principles apply).

---

### Knowledge Points

---

#### 1. Sequences — Definition and Limits

**Definition:** A **sequence** is an ordered list $\{a_n\}_{n=1}^\infty = a_1, a_2, a_3, \ldots$, where each $a_n$ is a real number.

**Limit:** $\lim_{n \to \infty} a_n = L$ (the sequence **converges** to $L$) means: for every $\varepsilon > 0$, there exists $N$ such that $|a_n - L| < \varepsilon$ for all $n > N$.

If no such $L$ exists, the sequence **diverges**.

**Standard limits (memorise):**

| Sequence | Limit | Condition |
|----------|-------|-----------|
| $r^n$ | $0$ | $|r| < 1$ |
| $r^n$ | diverges | $|r| > 1$ |
| $n^{1/n}$ | $1$ | — |
| $x^n/n!$ | $0$ | any $x$ |
| $(1 + x/n)^n$ | $e^x$ | any $x$ |
| $\ln n / n$ | $0$ | — |
| $n^k/e^n$ | $0$ | any $k$ |

**Squeeze Theorem for sequences:** If $a_n \leq b_n \leq c_n$ for all large $n$ and $a_n \to L$, $c_n \to L$, then $b_n \to L$.

**Example using Squeeze:** Show $\sin(1/\sqrt{n}) \cdot \sqrt{n} \to 1$.

Use the inequality $|\sin\theta| \leq |\theta|$ and the limit $\sin\theta/\theta \to 1$ as $\theta\to 0$. With $\theta = 1/\sqrt{n}\to 0$: $\sqrt{n}\sin(1/\sqrt{n}) = \dfrac{\sin(1/\sqrt{n})}{1/\sqrt{n}} \to 1$. ✓

**Connection to functions:** If $\lim_{x \to \infty} f(x) = L$ and $a_n = f(n)$, then $\lim_{n\to\infty} a_n = L$. (L'Hôpital's rule is available for $f$.)

---

#### 2. The Monotone Convergence Theorem (MCT)

**Definition:** A sequence $\{a_n\}$ is **monotone increasing** if $a_n \leq a_{n+1}$ for all $n$, and **monotone decreasing** if $a_n \geq a_{n+1}$.

**Theorem (MCT):** Every monotone bounded sequence converges.
- If $\{a_n\}$ is increasing and bounded above, then $\lim a_n$ exists (and equals $\sup\{a_n\}$).
- If $\{a_n\}$ is decreasing and bounded below, then $\lim a_n$ exists (and equals $\inf\{a_n\}$).

**Why it matters:** The MCT guarantees convergence *without* knowing the limit in advance. It is used in the proof of the Alternating Series Test (Lecture 2).

**Example:** The sequence $a_n = (1 + 1/n)^n$ is monotone increasing and bounded above (by $3$). MCT guarantees $\lim a_n$ exists. The limit is $e \approx 2.718$.

**Example:** The sequence of partial sums of a positive-term series, $S_N = \sum_{n=1}^N a_n$ (with $a_n > 0$), is monotone increasing. It converges iff it is bounded above. This is the key insight behind all positive-series convergence tests.

---

#### 3. Infinite Series — Definition via Partial Sums

**Definition:** Given a sequence $\{a_n\}$, define the $N$-th **partial sum** $S_N = \sum_{n=1}^N a_n$.

The **infinite series** $\displaystyle\sum_{n=1}^\infty a_n$ **converges** to $S$ if $\lim_{N\to\infty} S_N = S$; otherwise it **diverges**.

**Key insight:** An infinite series is a limit — specifically, the limit of a sequence of partial sums. All of sequence theory applies to $\{S_N\}$.

---

#### 4. The Geometric Series

**Series:** $\displaystyle\sum_{n=0}^\infty r^n = 1 + r + r^2 + \cdots$

**Partial sum:** $S_N = \dfrac{1 - r^{N+1}}{1-r}$ for $r \neq 1$.

**Convergence:**
$$\sum_{n=0}^\infty r^n = \frac{1}{1-r} \quad \text{if } |r| < 1; \qquad \text{diverges if } |r| \geq 1.$$

**Proof:** $\lim_{N\to\infty} r^{N+1} = 0$ iff $|r| < 1$. ✓

**Generalized form:** $\displaystyle\sum_{n=0}^\infty ar^n = \dfrac{a}{1-r}$ for $|r| < 1$.

**Why it's fundamental:** The geometric series is the benchmark. Every convergence test ultimately compares an unknown series to a known one (often geometric).

**Engineering application:** Geometric series appear in signal processing (infinite impulse response filters), probability (expected values of geometric distributions), and control theory (discrete-time systems).

---

#### 5. The Divergence Test (Necessary Condition)

**Theorem:** If $\sum a_n$ converges, then $\lim_{n\to\infty} a_n = 0$.

**Contrapositive (the test):** If $\lim_{n\to\infty} a_n \neq 0$ (or the limit does not exist), then $\sum a_n$ **diverges**.

**Warning:** The converse is FALSE. $\lim a_n = 0$ does NOT guarantee convergence. The harmonic series $\sum 1/n$ has $a_n \to 0$ but diverges (see §6).

**Quick application:** $\sum \dfrac{n}{n+1}$ diverges since $\lim a_n = 1 \neq 0$.

---

#### 6. The $p$-Series

**Series:** $\displaystyle\sum_{n=1}^\infty \frac{1}{n^p}$.

**Convergence:**
$$\sum_{n=1}^\infty \frac{1}{n^p} \begin{cases} \text{converges} & p > 1 \\ \text{diverges} & p \leq 1 \end{cases}.$$

**Special cases:**
- $p = 1$: $\sum 1/n$ (harmonic series) — diverges.
- $p = 2$: $\sum 1/n^2 = \pi^2/6$ (Basel problem) — converges.

**The harmonic series diverges** — proof via grouping:
$$1 + \frac{1}{2} + \underbrace{\frac{1}{3}+\frac{1}{4}}_{\geq 1/2} + \underbrace{\frac{1}{5}+\frac{1}{6}+\frac{1}{7}+\frac{1}{8}}_{\geq 1/2} + \cdots$$
Each group contributes at least $1/2$, so the partial sums grow without bound.

**Proof of $p > 1$ convergence:** Demonstrated rigorously by the Integral Test in Lecture 2 (§3).

---

#### 7. Algebraic Properties of Convergent Series

If $\sum a_n = A$ and $\sum b_n = B$ (both convergent), then:
- **Linearity:** $\sum (c\,a_n + d\,b_n) = cA + dB$.
- **Adding/removing finitely many terms** does not change convergence (but changes the sum).

**Caution:** Rearranging terms of a **conditionally convergent** series can change its sum (Riemann rearrangement theorem — discussed in Lecture 2).

---

#### 8. The Comparison Test

**Direct Comparison Test:** Let $0 \leq a_n \leq b_n$ for all large $n$.
- If $\sum b_n$ converges, then $\sum a_n$ converges.
- If $\sum a_n$ diverges, then $\sum b_n$ diverges.

**Intuition:** A smaller series cannot diverge if a larger one converges; a larger series cannot converge if a smaller one diverges.

**Limit Comparison Test:** Let $a_n, b_n > 0$ and $L = \lim_{n\to\infty} \dfrac{a_n}{b_n}$.
- If $0 < L < \infty$: $\sum a_n$ and $\sum b_n$ have the **same** convergence behaviour.
- If $L = 0$: $\sum b_n$ convergent $\Rightarrow$ $\sum a_n$ convergent.
- If $L = \infty$: $\sum b_n$ divergent $\Rightarrow$ $\sum a_n$ divergent.

**Procedure:** Choose $b_n$ based on the dominant terms of $a_n$ as $n \to \infty$.

**Trigonometric examples using Limit Comparison:**

**Example:** Does $\displaystyle\sum_{n=1}^\infty \tan\!\left(\frac{1}{n^2}\right)$ converge?

Compare with $b_n = 1/n^2$. Since $\tan\theta \approx \theta$ for small $\theta$: $\lim_{n\to\infty}\dfrac{\tan(1/n^2)}{1/n^2} = 1$. Same behaviour as $\sum 1/n^2$ → **converges**. ✓

**Example:** Does $\displaystyle\sum_{n=1}^\infty \sin\!\left(\frac{1}{\sqrt{n}}\right)$ converge?

Compare with $b_n = 1/\sqrt{n}$: $\lim_{n\to\infty}\dfrac{\sin(1/\sqrt{n})}{1/\sqrt{n}} = 1$. Same behaviour as $\sum 1/\sqrt{n}$ ($p=1/2$) → **diverges**. ✓

---

#### 9. Telescoping Series

**Form:** $\displaystyle\sum_{n=1}^\infty (b_n - b_{n+1}) = b_1 - \lim_{n\to\infty} b_{n+1}$ (if the limit exists).

**Example:** $\displaystyle\sum_{n=1}^\infty \frac{1}{n(n+1)}$. Using partial fractions: $\frac{1}{n(n+1)} = \frac{1}{n} - \frac{1}{n+1}$.

$S_N = \left(1 - \frac{1}{2}\right) + \left(\frac{1}{2} - \frac{1}{3}\right) + \cdots + \left(\frac{1}{N} - \frac{1}{N+1}\right) = 1 - \frac{1}{N+1} \to 1$.

$$\sum_{n=1}^\infty \frac{1}{n(n+1)} = 1.$$

Telescoping series are one of the few cases where the exact sum can be computed.

---

#### 10. Summary — Lecture 1

| Tool | Convergence criterion | Best used for |
|------|-----------------------|--------------|
| MCT | Monotone + bounded → converges | Existence proofs, partial sums of positive series |
| Geometric series | $|r| < 1$: converges to $a/(1-r)$ | Recognizing geometric terms |
| Divergence Test | $a_n \not\to 0$ → diverges | Quick divergence check |
| $p$-series | $p > 1$: converges | Comparison benchmark |
| Harmonic series | $p = 1$: diverges | Comparison benchmark |
| Comparison Test | $a_n \leq b_n$, etc. | Series with dominant terms |
| Limit Comparison | $\lim a_n/b_n = L \in (0,\infty)$ | Rational-like terms, trig approximations |
| Telescoping | Partial-fraction decomposition | Exact sum computation |

---

## Lecture 2: Convergence Tests — Ratio, Root, Integral, Alternating

### Introduction

The Comparison Test requires finding a suitable benchmark series, which can be non-obvious. The tests in this lecture are more systematic: the **Ratio Test** and **Root Test** work by comparing the series to a geometric series implicitly; the **Integral Test** connects series to improper integrals; the **Alternating Series Test** handles series with sign changes. The Ratio Test is the primary tool for the remainder of the course — it is exactly what determines the radius of convergence of a power series.

---

### Knowledge Points

---

#### 1. The Ratio Test

**Theorem:** Let $a_n > 0$ and $L = \lim_{n\to\infty} \dfrac{a_{n+1}}{a_n}$.
$$\sum a_n \begin{cases} \text{converges} & L < 1 \\ \text{diverges} & L > 1 \\ \text{inconclusive} & L = 1 \end{cases}.$$

**Proof (sketch):**
- **$L < 1$:** Choose $r$ with $L < r < 1$. For large $n$ (say $n \geq N$), $a_{n+1} < r\,a_n$. By induction, $a_{N+k} < r^k a_N$ for all $k \geq 0$. The tail $\sum_{k=0}^\infty a_{N+k} < a_N \sum_{k=0}^\infty r^k = a_N/(1-r) < \infty$ (geometric). ✓
- **$L > 1$:** Choose $r$ with $1 < r < L$. For large $n$, $a_{n+1} > r\,a_n > a_n$, so $a_n$ is eventually increasing → $a_n \not\to 0$ → diverges by Divergence Test. ✓

**Form for power series:** If $a_n = c_n(x-x_0)^n$, the Ratio Test gives directly:
$$L = \lim_{n\to\infty} \left|\frac{c_{n+1}}{c_n}\right| |x - x_0|.$$
Setting $L < 1$ yields the interval of convergence. This is precisely the formula used in Lecture 3.

**Inconclusive at $L = 1$:** The $p$-series $\sum 1/n^p$ all give $L = 1$ regardless of $p$ — the Ratio Test cannot distinguish them.

---

#### 2. Worked Examples — Ratio Test

**Example 1:** $\displaystyle\sum_{n=1}^\infty \frac{n!}{n^n}$.

$\dfrac{a_{n+1}}{a_n} = \dfrac{(n+1)!}{(n+1)^{n+1}} \cdot \dfrac{n^n}{n!} = \dfrac{n^n}{(n+1)^n} = \left(\dfrac{n}{n+1}\right)^n = \left(1 - \dfrac{1}{n+1}\right)^n \to e^{-1} < 1$.

**Converges.** ✓

**Example 2:** $\displaystyle\sum_{n=0}^\infty \frac{x^n}{n!}$ (for any fixed $x$).

$\dfrac{|a_{n+1}|}{|a_n|} = \dfrac{|x|^{n+1}}{(n+1)!} \cdot \dfrac{n!}{|x|^n} = \dfrac{|x|}{n+1} \to 0 < 1$.

**Converges for all $x \in \mathbb{R}$** — confirming that $e^x = \sum x^n/n!$ is valid everywhere.

**Example 3:** $\displaystyle\sum_{n=1}^\infty n!\,x^n$.

$\dfrac{a_{n+1}}{a_n} = (n+1)|x| \to \infty$ for $x \neq 0$.

**Diverges for all $x \neq 0$** — this series has radius of convergence $R = 0$.

---

#### 3. The Root Test

**Theorem:** Let $L = \lim_{n\to\infty} \sqrt[n]{|a_n|} = \lim_{n\to\infty} |a_n|^{1/n}$.
$$\sum a_n \begin{cases} \text{converges (absolutely)} & L < 1 \\ \text{diverges} & L > 1 \\ \text{inconclusive} & L = 1 \end{cases}.$$

**Proof (sketch):**
- **$L < 1$:** For large $n$, $|a_n|^{1/n} < r < 1$, so $|a_n| < r^n$. Comparison with geometric $\sum r^n$ gives convergence. ✓
- **$L > 1$:** For large $n$, $|a_n|^{1/n} > 1$, so $|a_n| > 1 \not\to 0$ → diverges. ✓

**Best for:** Series involving $n$-th powers, e.g., $a_n = (f(n))^n$.

**Cauchy–Hadamard Formula** (connects to Lecture 3): The radius of convergence of $\sum c_n(x-x_0)^n$ is:
$$R = \frac{1}{\limsup_{n\to\infty} |c_n|^{1/n}}.$$

**Example:** $\displaystyle\sum_{n=1}^\infty \left(\frac{2n+1}{3n+2}\right)^n$.

$\sqrt[n]{a_n} = \dfrac{2n+1}{3n+2} \to \dfrac{2}{3} < 1$. **Converges.** ✓

---

#### 4. The Integral Test

**Theorem:** Let $f$ be continuous, positive, and **decreasing** on $[1, \infty)$, with $f(n) = a_n$. Then:
$$\sum_{n=1}^\infty a_n \text{ converges} \iff \int_1^\infty f(x)\,dx \text{ converges.}$$

**Proof idea:** $a_{n+1} \leq \int_n^{n+1} f(x)\,dx \leq a_n$ (since $f$ is decreasing). Summing gives:
$$S_N - a_1 \leq \int_1^N f\,dx \leq S_N - a_{N+1} + a_1 - a_{N+1}.$$
So $S_N$ and $\int_1^N f\,dx$ are bounded together.

**Application — $p$-series proof:**
$\int_1^\infty x^{-p}\,dx$ converges iff $p > 1$ (from Week 2, improper integrals). Therefore $\sum 1/n^p$ converges iff $p > 1$. ✓

**Application — Logarithmic series:** $\displaystyle\sum_{n=2}^\infty \frac{1}{n\ln n}$.
$f(x) = 1/(x\ln x)$ is decreasing and positive on $[2,\infty)$.
$\int_2^\infty \frac{dx}{x\ln x} = \ln(\ln x)\Big|_2^\infty = \infty$. **Diverges.** ✓

**Error bound (remainder estimate):**
$$\int_{N+1}^\infty f(x)\,dx \leq R_N \leq \int_N^\infty f(x)\,dx,$$
where $R_N = S - S_N$ is the tail remainder. This is used to estimate how many terms are needed to achieve a desired accuracy.

---

#### 5. The Alternating Series Test (AST) and Proof

**Definition:** An **alternating series** has the form $\displaystyle\sum_{n=1}^\infty (-1)^{n-1} a_n = a_1 - a_2 + a_3 - \cdots$ with $a_n > 0$.

**Alternating Series Test (Leibniz):** If $a_n$ is **decreasing** ($a_{n+1} \leq a_n$ for all large $n$) and $a_n \to 0$, then the series **converges**.

**Proof via MCT:**
- The even partial sums $S_{2N} = (a_1-a_2)+(a_3-a_4)+\cdots+(a_{2N-1}-a_{2N})$ form an **increasing** sequence (each term $a_{2k-1}-a_{2k} \geq 0$).
- The odd partial sums $S_{2N+1} = S_{2N} + a_{2N+1}$ form a **decreasing** sequence (we add a positive but shrinking term).
- $S_1 \geq S_{2N+1} \geq S_{2N} \geq 0$, so both sequences are bounded.
- By MCT, both $S_{2N}$ and $S_{2N+1}$ converge. Their common limit is $S$ since $S_{2N+1} - S_{2N} = a_{2N+1} \to 0$. ✓

**Remainder estimate:** $|R_N| = |S - S_N| \leq a_{N+1}$ (the error is bounded by the first omitted term).

**Examples:**
- **Alternating harmonic series:** $\displaystyle\sum_{n=1}^\infty \frac{(-1)^{n-1}}{n} = 1 - \frac{1}{2} + \frac{1}{3} - \cdots = \ln 2$. Converges (even though $\sum 1/n$ diverges).
- **Error estimate for $\ln 2$:** $|\text{error}| \leq a_{N+1} = 1/(N+1)$. For accuracy $0.01$, need $1/(N+1) \leq 0.01$, i.e., $N \geq 99$ terms.
- $\displaystyle\sum_{n=1}^\infty \frac{(-1)^{n-1}}{\sqrt{n}}$: $a_n = 1/\sqrt{n} \to 0$ decreasingly. **Converges.**

---

#### 6. Absolute vs. Conditional Convergence

**Definition:** $\sum a_n$ **converges absolutely** if $\sum |a_n|$ converges.

**Definition:** $\sum a_n$ **converges conditionally** if $\sum a_n$ converges but $\sum |a_n|$ diverges.

**Theorem:** Absolute convergence implies convergence.

**Proof:** $0 \leq a_n + |a_n| \leq 2|a_n|$. Since $\sum |a_n|$ converges, $\sum(a_n + |a_n|)$ converges by comparison. Then $\sum a_n = \sum(a_n + |a_n|) - \sum|a_n|$ converges. ✓

**Examples:**
- $\sum (-1)^n/n^2$: $\sum 1/n^2$ converges → **absolutely convergent**.
- $\sum (-1)^{n-1}/n$: $\sum 1/n$ diverges but $\sum (-1)^{n-1}/n = \ln 2$ → **conditionally convergent**.

**Riemann Rearrangement Theorem:** A conditionally convergent series can be rearranged to converge to **any** desired value, or to $\pm\infty$. This is why arbitrary rearrangement of conditionally convergent series is forbidden.

**Absolutely convergent series** can be rearranged freely (the sum is unchanged).

---

#### 7. The Cauchy Condensation Test (Optional — not on exam)

**Theorem:** Let $a_n$ be a decreasing sequence of non-negative terms. Then:
$$\sum_{n=1}^\infty a_n \text{ converges} \iff \sum_{k=0}^\infty 2^k\,a_{2^k} \text{ converges.}$$

**Why it works:** The doubled-index sum $\sum 2^k a_{2^k}$ groups consecutive terms of $\sum a_n$ into blocks of size $2^k$ and estimates each block by its largest term (since $a_n$ decreases).

**Application:** Prove $\sum 1/(n(\ln n)^p)$ converges iff $p > 1$.
Condensed: $\sum 2^k \cdot \frac{1}{2^k(\ln 2^k)^p} = \sum \frac{1}{(k\ln 2)^p} \sim \frac{1}{(\ln 2)^p}\sum \frac{1}{k^p}$, which converges iff $p > 1$. ✓

This extends the $p$-series to a logarithmic refinement.

---

#### 8. Strategy for Convergence Testing

**Flowchart for determining convergence of $\sum a_n$:**

1. **Divergence Test first:** If $a_n \not\to 0$, stop — diverges.
2. **Is the series geometric or $p$-series?** Apply directly.
3. **Does $a_n$ involve $n!$, $n^n$, or exponentials?** Try the **Ratio Test**.
4. **Does $a_n$ involve $n$-th powers?** Try the **Root Test**.
5. **Does $a_n$ look like $f(n)$ for a nice integrable function?** Try the **Integral Test**.
6. **Does $a_n$ look like a rational function of $n$?** Try the **Limit Comparison Test** with a $p$-series.
7. **Alternating signs?** Try the **Alternating Series Test** (then check absolute convergence separately).

**Priority in this course:** Ratio Test first (it will be used most heavily in Weeks 12–13 for power series).

---

#### 9. Summary — Lecture 2

| Test | Best for | Criterion | Proof mechanism |
|------|---------|-----------|----------------|
| Ratio | Factorials, exponentials | $L = \lim|a_{n+1}/a_n|$; converges if $L<1$ | Compare tail to geometric series |
| Root | $n$-th powers | $L = \lim|a_n|^{1/n}$; converges if $L<1$ | Compare to geometric series |
| Integral | Decreasing, integrable $f(n)$ | $\sum a_n$ conv. $\iff \int f\,dx$ conv. | Bounding sums by integrals |
| AST (Leibniz) | Sign-alternating, $a_n \to 0$ decreasingly | Converges; error $\leq a_{N+1}$ | MCT on even/odd partial sums |
| Absolute convergence | $\sum|a_n|$ converges | Implies convergence; rearrangement safe | Comparison |
| Conditional convergence | $\sum a_n$ conv., $\sum|a_n|$ div. | Converges; do NOT rearrange | Riemann theorem |

---

## Lecture 3: Power Series

### Introduction

A **power series** $\sum_{n=0}^\infty c_n(x-x_0)^n$ is an infinite polynomial in $(x - x_0)$. Unlike a general series, it defines a **function** of $x$ — but only for those values of $x$ where the series converges. The set of such $x$ is always an interval (the **interval of convergence**), determined by the **radius of convergence** $R$ via the Ratio Test.

Inside the interval of convergence, power series behave like polynomials: they can be differentiated and integrated term by term, composed with other functions, multiplied together. This makes them extraordinarily powerful for representing and solving ODEs.

**Why it matters in engineering:**
- Every elementary function ($e^x$, $\sin x$, $\cos x$, $\ln(1+x)$, etc.) has a power series representation valid on its interval of convergence.
- Power series methods solve ODEs with variable coefficients (Weeks 12–13).
- The Laplace transform table entries often arise from power series expansions.

---

### Knowledge Points

---

#### 1. Definition and Convergence Structure

**Definition:** A **power series centred at $x_0$** is:
$$\sum_{n=0}^\infty c_n(x-x_0)^n = c_0 + c_1(x-x_0) + c_2(x-x_0)^2 + \cdots$$

**Radius of convergence $R$:**

By the Ratio Test (or Root Test), there exists $R \in [0, \infty]$ such that:
- The series **converges absolutely** for $|x - x_0| < R$.
- The series **diverges** for $|x - x_0| > R$.
- At $|x - x_0| = R$ (the endpoints): behaviour must be checked separately for each series.

**Ratio Test formula for $R$:**
$$R = \lim_{n\to\infty} \left|\frac{c_n}{c_{n+1}}\right| \quad \text{(when the limit exists)}.$$

**Cauchy–Hadamard formula:**
$$R = \frac{1}{\limsup_{n\to\infty} |c_n|^{1/n}}.$$

**Special cases:** $R = \infty$ (converges for all $x$), $R = 0$ (converges only at $x = x_0$).

---

#### 2. Finding the Radius and Interval of Convergence

**Procedure:**
1. Apply the Ratio Test to $a_n = c_n(x-x_0)^n$:
   $$L = \lim_{n\to\infty}\left|\frac{c_{n+1}(x-x_0)^{n+1}}{c_n(x-x_0)^n}\right| = \lim_{n\to\infty}\left|\frac{c_{n+1}}{c_n}\right| \cdot |x-x_0|.$$
2. Convergence requires $L < 1$: $|x-x_0| < R$ where $R = \lim|c_n/c_{n+1}|$.
3. Check endpoints $x = x_0 \pm R$ separately using the tests from Lectures 1–2.
4. Write the **interval of convergence** (IOC) with the correct bracket/parenthesis notation.

---

#### 3. Worked Examples — Finding the IOC

**Example 1:** $\displaystyle\sum_{n=1}^\infty \frac{x^n}{n}$.

$L = \lim_{n\to\infty}\dfrac{|x|^{n+1}}{n+1}\cdot\dfrac{n}{|x|^n} = |x|\lim_{n\to\infty}\dfrac{n}{n+1} = |x|$.

$R = 1$: converges for $|x| < 1$.

Endpoints:
- $x = 1$: $\sum 1/n$ (harmonic) — **diverges**.
- $x = -1$: $\sum (-1)^n/n$ (alternating harmonic) — **converges** (AST).

**IOC:** $[-1, 1)$.

**Example 2:** $\displaystyle\sum_{n=0}^\infty \frac{(-1)^n x^{2n}}{(2n)!}$.

$L = \lim_{n\to\infty}\dfrac{|x|^{2n+2}}{(2n+2)!}\cdot\dfrac{(2n)!}{|x|^{2n}} = |x|^2 \lim_{n\to\infty}\dfrac{1}{(2n+2)(2n+1)} = 0$ for any $x$.

$R = \infty$. **IOC:** $(-\infty, \infty)$.

*(This is the series for $\cos x$.)*

**Example 3:** $\displaystyle\sum_{n=0}^\infty n!\,(x-2)^n$.

$L = \lim_{n\to\infty}(n+1)!\,|x-2|^{n+1} \cdot \dfrac{1}{n!\,|x-2|^n} = (n+1)|x-2| \to \infty$ for $x \neq 2$.

$R = 0$. Converges only at $x = 2$. **IOC:** $\{2\}$.

---

#### 4. Term-by-Term Differentiation and Integration

**Theorem:** If $f(x) = \displaystyle\sum_{n=0}^\infty c_n(x-x_0)^n$ with radius of convergence $R > 0$, then:

**Differentiation:**
$$f'(x) = \sum_{n=1}^\infty n\,c_n(x-x_0)^{n-1} = \sum_{n=0}^\infty (n+1)\,c_{n+1}(x-x_0)^n, \quad |x-x_0| < R.$$

**Integration:**
$$\int f(x)\,dx = C + \sum_{n=0}^\infty \frac{c_n}{n+1}(x-x_0)^{n+1}, \quad |x-x_0| < R.$$

Both operations preserve the radius of convergence $R$ (endpoints may change).

**Key fact:** A power series is **infinitely differentiable** inside its radius of convergence — this is what makes it so powerful for ODE solutions.

---

#### 5. Uniqueness of Power Series Representation

**Theorem:** If $f(x) = \sum_{n=0}^\infty c_n(x-x_0)^n$ for $|x-x_0| < R$ ($R > 0$), then the coefficients are uniquely determined by $f$:
$$c_n = \frac{f^{(n)}(x_0)}{n!}.$$

**Consequence:** There is only ONE power series centred at $x_0$ that represents $f$ in a neighbourhood of $x_0$ — the Taylor series. Any method of finding the series (term-by-term, manipulation, substitution) gives the same answer.

---

#### 6. Operations on Power Series

**Substitution:** Replace $x$ by $g(x)$ in a known series.

Example: $\displaystyle e^{-x^2} = \sum_{n=0}^\infty \frac{(-1)^n x^{2n}}{n!}$, valid for all $x$.

**Multiplication (Cauchy product):** $(f \cdot g)(x) = \left(\sum a_n x^n\right)\left(\sum b_n x^n\right) = \sum_{n=0}^\infty\left(\sum_{k=0}^n a_k b_{n-k}\right)x^n$.

Valid for $|x| < \min(R_f, R_g)$.

**Verification via Cauchy product:** $e^x \cdot e^x = e^{2x}$.

LHS: $c_n = \sum_{k=0}^n \dfrac{1}{k!}\cdot\dfrac{1}{(n-k)!} = \dfrac{1}{n!}\sum_{k=0}^n\binom{n}{k} = \dfrac{2^n}{n!}$. RHS: $e^{2x} = \sum \dfrac{(2x)^n}{n!} = \sum\dfrac{2^n x^n}{n!}$. ✓

**Division of series (long division):**

To find $\tan x = \sin x / \cos x$ as a power series:

$$\sin x = x - \frac{x^3}{6} + \frac{x^5}{120} - \cdots, \qquad \cos x = 1 - \frac{x^2}{2} + \frac{x^4}{24} - \cdots$$

Perform long division $\sin x \div \cos x$ in ascending powers:
- $x \div 1 = x$. Remainder: $\sin x - x\cos x = \dfrac{x^3}{3} - \dfrac{x^5}{30} + \cdots$
- $\dfrac{x^3}{3} \div 1 = \dfrac{x^3}{3}$. Remainder: $\dfrac{2x^5}{15} + \cdots$
- $\dfrac{2x^5}{15} \div 1 = \dfrac{2x^5}{15}$.

$$\tan x = x + \frac{x^3}{3} + \frac{2x^5}{15} + \cdots, \qquad |x| < \frac{\pi}{2}.$$

*(Verify: $\tan'(0) = 1$, $(\tan x)''(0)/2! = 0$, $(\tan x)'''(0)/3! = 1/3$, etc. ✓)*

**Differentiation of $\ln(1+x)$:**
$\dfrac{1}{1+x} = \sum_{n=0}^\infty (-1)^n x^n$, $|x| < 1$.
Integrate: $\ln(1+x) = \displaystyle\sum_{n=1}^\infty \frac{(-1)^{n-1}}{n} x^n = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots$, $|x| \leq 1$, $x \neq -1$.

*(At $x = 1$: $\sum(-1)^{n-1}/n = \ln 2$ — AST; at $x = -1$: $-\sum 1/n$ — diverges.)*

---

#### 7. Standard Power Series to Know

These series will be used extensively in Weeks 12–13:

$$e^x = \sum_{n=0}^\infty \frac{x^n}{n!}, \quad R = \infty.$$
$$\sin x = \sum_{n=0}^\infty \frac{(-1)^n x^{2n+1}}{(2n+1)!}, \quad R = \infty.$$
$$\cos x = \sum_{n=0}^\infty \frac{(-1)^n x^{2n}}{(2n)!}, \quad R = \infty.$$
$$\frac{1}{1-x} = \sum_{n=0}^\infty x^n, \quad R = 1.$$
$$\ln(1+x) = \sum_{n=1}^\infty \frac{(-1)^{n-1}}{n} x^n, \quad R = 1.$$
$$(1+x)^\alpha = \sum_{n=0}^\infty \binom{\alpha}{n} x^n, \quad R = 1 \quad \text{(binomial series; } \binom{\alpha}{n} = \frac{\alpha(\alpha-1)\cdots(\alpha-n+1)}{n!}).$$

---

#### 8. Power Series and ODEs — Preview

A key application (developed in Weeks 12–13): if we assume $y = \sum_{n=0}^\infty c_n x^n$ satisfies an ODE, we can substitute the series (term by term) and match coefficients to find a **recurrence relation** for $c_n$.

**Example (preview):** For $y'' + y = 0$, assume $y = \sum c_n x^n$.
$y'' = \sum_{n=2}^\infty n(n-1)c_n x^{n-2} = \sum_{n=0}^\infty (n+2)(n+1)c_{n+2}x^n$.
Substituting: $\sum_{n=0}^\infty[(n+2)(n+1)c_{n+2} + c_n]x^n = 0$.
Matching: $(n+2)(n+1)c_{n+2} + c_n = 0$ for all $n$ → $c_{n+2} = -c_n/[(n+2)(n+1)]$.

With $c_0 = 1$, $c_1 = 0$: recovers $\cos x = \sum (-1)^n x^{2n}/(2n)!$. ✓
With $c_0 = 0$, $c_1 = 1$: recovers $\sin x = \sum (-1)^n x^{2n+1}/(2n+1)!$. ✓

The power series method will be fully developed in Weeks 12–13.

---

#### 9. Endpoint Behaviour and Abel's Theorem

The interval of convergence $(-R+x_0, R+x_0)$ is always open in the interior. At the two endpoints, each of the four combinations is possible:

| IOC form | Interpretation |
|----------|---------------|
| $(x_0-R,\; x_0+R)$ | Diverges at both endpoints |
| $[x_0-R,\; x_0+R)$ | Converges at left endpoint only |
| $(x_0-R,\; x_0+R]$ | Converges at right endpoint only |
| $[x_0-R,\; x_0+R]$ | Converges at both endpoints |

**Endpoint convergence is often conditional** (not absolute) — check using AST or Comparison.

**Abel's Theorem:** If $f(x) = \sum_{n=0}^\infty c_n(x-x_0)^n$ has radius of convergence $R$, and the series converges at the endpoint $x = x_0 + R$ (to some value $S$), then:
$$\lim_{x \to (x_0+R)^-} f(x) = S.$$
In other words, the power series function is **continuous up to and including the endpoint** from inside the interval.

**Example (Leibniz formula for $\pi$):** From $\arctan x = \sum_{n=0}^\infty \dfrac{(-1)^n}{2n+1}x^{2n+1}$, $R = 1$.

At $x = 1$: the series $\sum \dfrac{(-1)^n}{2n+1} = 1 - \dfrac{1}{3} + \dfrac{1}{5} - \cdots$ converges by the AST.

By Abel's Theorem: $\lim_{x\to 1^-}\arctan x = \pi/4 = \sum_{n=0}^\infty \dfrac{(-1)^n}{2n+1}$.

$$\boxed{\frac{\pi}{4} = 1 - \frac{1}{3} + \frac{1}{5} - \frac{1}{7} + \cdots}$$

*(This is the Gregory–Leibniz series. It converges very slowly — $\sim 10^6$ terms needed for 6 decimal places.)*

---

#### 10. Summary — Lecture 3

| Concept | Key Formula / Rule |
|---------|--------------------|
| Power series | $f(x) = \sum_{n=0}^\infty c_n(x-x_0)^n$ |
| Radius of convergence | $R = \lim|c_n/c_{n+1}|$ (Ratio Test) |
| Cauchy–Hadamard | $R = 1/\limsup|c_n|^{1/n}$ |
| IOC | $(x_0-R, x_0+R)$ open; check endpoints separately |
| Term-by-term diff. | $f'(x) = \sum_{n=1}^\infty nc_n(x-x_0)^{n-1}$, same $R$ |
| Term-by-term int. | $\int f\,dx = C + \sum \frac{c_n}{n+1}(x-x_0)^{n+1}$, same $R$ |
| Uniqueness | $c_n = f^{(n)}(x_0)/n!$ — Taylor coefficients |
| Cauchy product | $(\sum a_n)(\sum b_n) = \sum c_n$ where $c_n = \sum_{k=0}^n a_k b_{n-k}$ |
| Long division | $\sin x \div \cos x \to \tan x = x + x^3/3 + 2x^5/15 + \cdots$ |
| Abel's Theorem | Continuity of power series up to convergent endpoint |

---

## Practice Session

**Theme:** Convergence testing — method selection; radius and interval of convergence for power series; endpoint analysis; term-by-term operations.

---

### Practice Problems

**Set A — Series Convergence**

1. Determine whether each series converges or diverges. State which test you use and why.
   (a) $\displaystyle\sum_{n=1}^\infty \frac{3n+1}{n^2+4}$
   (b) $\displaystyle\sum_{n=1}^\infty \frac{n!}{(2n)!}$
   (c) $\displaystyle\sum_{n=1}^\infty \frac{2^n}{3^n + 1}$
   (d) $\displaystyle\sum_{n=2}^\infty \frac{1}{n(\ln n)^2}$
   (e) $\displaystyle\sum_{n=1}^\infty \left(\frac{n}{2n+1}\right)^n$
   (f) $\displaystyle\sum_{n=1}^\infty \sin\!\left(\dfrac{1}{n^2}\right)$

2. Determine absolute convergence, conditional convergence, or divergence:
   (a) $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n}{\sqrt{n}}$
   (b) $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n n}{n^2+1}$
   (c) $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n}{\ln(n+1)}$
   (d) $\displaystyle\sum_{n=1}^\infty (-1)^n\frac{3^n}{n\cdot 4^n}$

3. (a) Use the Integral Test to prove that $\displaystyle\sum_{n=2}^\infty \frac{1}{n\ln n}$ diverges.
   (b) Use the remainder estimate for the AST: how many terms of $\displaystyle\sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}$ are needed to estimate $\ln 2$ with error less than $0.01$?

4. Prove using the MCT that $\displaystyle\sum_{n=1}^\infty \frac{1}{n^2}$ converges. (Show the partial sums are increasing and bounded above by $2$, using the comparison $1/n^2 \leq 1/(n(n-1))$ for $n \geq 2$ and the telescoping result from Lecture 1.)

**Set B — Power Series: Radius and Interval of Convergence**

5. Find the radius of convergence and interval of convergence (including endpoint analysis):
   (a) $\displaystyle\sum_{n=0}^\infty \frac{x^n}{n+1}$
   (b) $\displaystyle\sum_{n=1}^\infty \frac{(-1)^n x^n}{n\cdot 3^n}$
   (c) $\displaystyle\sum_{n=0}^\infty n!\,(x-1)^n$
   (d) $\displaystyle\sum_{n=0}^\infty \frac{(x+2)^n}{4^n}$
   (e) $\displaystyle\sum_{n=1}^\infty \frac{x^n}{n^2}$

6. Find the radius of convergence of each series without determining endpoint behaviour:
   (a) $\displaystyle\sum_{n=0}^\infty \frac{n^2}{3^n}x^n$
   (b) $\displaystyle\sum_{n=0}^\infty \frac{(-1)^n(2n)!}{(n!)^2}x^n$
   (c) $\displaystyle\sum_{n=0}^\infty \frac{x^{2n}}{4^n}$
   *(Careful: not every power of $x$ appears.)*

7. Apply Abel's Theorem: the series $\displaystyle\sum_{n=1}^\infty \frac{(-1)^{n-1}}{n}x^n$ has IOC $(-1,1]$ and equals $\ln(1+x)$ inside $(−1,1)$. State what Abel's Theorem implies at $x=1$, and hence verify the Gregory series $\ln 2 = 1 - 1/2 + 1/3 - \cdots$.

**Set C — Operations on Power Series**

8. Starting from $\dfrac{1}{1-x} = \displaystyle\sum_{n=0}^\infty x^n$ ($|x| < 1$):
   (a) Differentiate to find a series for $\dfrac{1}{(1-x)^2}$ and state its IOC.
   (b) Integrate to find a series for $-\ln(1-x)$ and determine the IOC including endpoints.
   (c) Substitute $x \to -x^2$ to find a series for $\dfrac{1}{1+x^2}$ and integrate to obtain the series for $\arctan x$.

9. Find the power series centred at $x_0 = 0$ for each function, using known series:
   (a) $f(x) = e^{-3x}$
   (b) $f(x) = x^2\sin x$
   (c) $f(x) = \dfrac{1}{(1-x)^3}$ *(differentiate the geometric series twice)*
   (d) $f(x) = \cos(x^2)$

10. Use the Cauchy product to find the first five terms of the product series $e^x \cdot \sin x$. Verify the $x^1$, $x^2$, $x^3$ terms match the known expansion $e^x\sin x = x + x^2 + x^3/3 + \cdots$

11. Use long division of power series to find the first three non-zero terms of:
    (a) $\sec x = 1/\cos x$ *(divide $1$ by the series for $\cos x$)*
    (b) $\dfrac{e^x}{1-x}$ *(multiply by $(1-x)^{-1} = \sum x^n$)*

12. **(Challenge)** The series $\displaystyle\sum_{n=0}^\infty \frac{x^{2n+1}}{2n+1}$ converges on $(-1, 1]$.
    (a) Find its radius of convergence and check convergence at $x = -1$ and $x = 1$.
    (b) Differentiate to identify the sum; hence find the closed form.
    (c) Evaluate the sum at $x = 1$ and state the result.
