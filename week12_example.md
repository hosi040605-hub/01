# Hermite 미분방정식의 급수해

Hermite 미분방정식 $y'' - 2xy' + 2\lambda y = 0$, $\lambda=3$의 Power Series Solution을 두 가지 초기 조건($a_0=1, a_1=0$ 및 $a_0=0, a_1=1$)에 대해 해를 구한다.

---

## 1. 점화식(Recurrence Relation) 유도

### 1.1 급수해 가정과 미분

방정식 $y'' - 2xy' + 6y = 0$ ($\lambda = 3$인 경우)에 대해, $x = 0$이 정상점(ordinary point)이므로 다음과 같은 멱급수 해를 가정한다.

$$y(x) = \sum_{n=0}^{\infty} a_n x^n = a_0 + a_1 x + a_2 x^2 + a_3 x^3 + \cdots$$

이를 항별로 미분하면:

$$y'(x) = \sum_{n=1}^{\infty} n\, a_n x^{n-1} = \sum_{n=0}^{\infty} (n+1)\, a_{n+1} x^n$$

$$y''(x) = \sum_{n=2}^{\infty} n(n-1)\, a_n x^{n-2} = \sum_{n=0}^{\infty} (n+2)(n+1)\, a_{n+2}\, x^n$$

### 1.2 각 항을 미분방정식에 대입

**(i) $y''$ 항:**

$$y'' = \sum_{n=0}^{\infty} (n+2)(n+1)\, a_{n+2}\, x^n$$

**(ii) $-2xy'$ 항:** $y'$에 $x$를 곱하면 지수가 1 증가하므로

$$-2x y' = -2x \sum_{n=1}^{\infty} n\, a_n x^{n-1} = -2 \sum_{n=1}^{\infty} n\, a_n x^n = \sum_{n=0}^{\infty} (-2n)\, a_n x^n$$

(주의: $n=0$일 때 $-2n\,a_n = 0$이므로 합의 시작 지수를 $n=0$으로 통일 가능)

**(iii) $6y$ 항:**

$$6y = \sum_{n=0}^{\infty} 6\, a_n x^n$$

### 1.3 같은 지수 $x^n$끼리 묶기

세 항을 모두 더하면, 모든 합이 동일한 지수 $x^n$($n=0,1,2,\dots$)에 대해 정렬되어 있으므로

$$\sum_{n=0}^{\infty} \Big[ (n+2)(n+1)\, a_{n+2} \; - \; 2n\, a_n \; + \; 6\, a_n \Big] x^n = 0$$

### 1.4 항등식 조건: 모든 계수 = 0

멱급수가 모든 $x$에 대해 $0$이 되려면 **각 $x^n$의 계수가 모두 0**이어야 한다.

$$(n+2)(n+1)\, a_{n+2} + (6 - 2n)\, a_n = 0 \qquad (n \ge 0)$$

### 1.5 $a_{n+2}$에 대해 정리

$$a_{n+2} = -\frac{6 - 2n}{(n+2)(n+1)}\, a_n = \frac{2n - 6}{(n+2)(n+1)}\, a_n$$

$$\boxed{\; a_{n+2} = \frac{2(n - 3)}{(n+2)(n+1)}\, a_n \quad (n \ge 0) \;}$$

### 1.6 점화식의 구조적 특징

- **분리 구조**: 짝수 인덱스 $a_{2k}$는 $a_0$로부터, 홀수 인덱스 $a_{2k+1}$는 $a_1$로부터 결정된다. 즉 두 계열은 서로 독립적으로 진행되며, 이는 $a_0$, $a_1$ 두 개의 자유 상수를 갖는 2계 선형 ODE의 일반해 구조와 정확히 일치한다.
- **유한 종료 조건**: 점화식 분자에 $(n - 3)$이 있으므로 $n = 3$일 때 $a_5 = 0$이 되고, 그 이후 모든 $a_{2k+1}$ ($k \ge 2$)도 $0$이 된다. 따라서 $a_1 \ne 0$인 경우 홀수 계열은 **3차 다항식**으로 종료된다.
- **일반 원리**: Hermite 방정식 $y'' - 2xy' + 2\lambda y = 0$에서 $\lambda$가 비음의 정수 $n$이면, 그에 해당하는 패리티(parity)의 계열이 $n$차 다항식으로 끝나며, 이것이 곧 **Hermite 다항식** $H_n(x)$의 기원이다.

---

## 2. 조건별 급수해 유도

### Case 1: $a_0 = 1$, $a_1 = 0$ (짝수 함수 해)

초기 조건에 의해 모든 홀수 항 계수는 $0$이 된다 ($a_1 = a_3 = a_5 = \cdots = 0$). 짝수 항 계수는 점화식

$$a_{n+2} = \frac{2(n-3)}{(n+2)(n+1)}\, a_n$$

으로부터 다음과 같이 계산된다.

- $n=0 \;\Rightarrow\; a_2 = \dfrac{2(-3)}{2\cdot 1}\, a_0 = -3$
- $n=2 \;\Rightarrow\; a_4 = \dfrac{2(-1)}{4\cdot 3}\, a_2 = \dfrac{-2}{12}\cdot(-3) = \dfrac{1}{2}$
- $n=4 \;\Rightarrow\; a_6 = \dfrac{2(1)}{6\cdot 5}\, a_4 = \dfrac{2}{30}\cdot\dfrac{1}{2} = \dfrac{1}{30}$
- $n=6 \;\Rightarrow\; a_8 = \dfrac{2(3)}{8\cdot 7}\, a_6 = \dfrac{6}{56}\cdot\dfrac{1}{30} = \dfrac{1}{280}$
- $n=8 \;\Rightarrow\; a_{10} = \dfrac{2(5)}{10\cdot 9}\, a_8 = \dfrac{10}{90}\cdot\dfrac{1}{280} = \dfrac{1}{2520}$

$$\boxed{\; y_1(x) = 1 - 3x^2 + \tfrac{1}{2}x^4 + \tfrac{1}{30}x^6 + \tfrac{1}{280}x^8 + \tfrac{1}{2520}x^{10} + \cdots \;}$$

이 해는 무한급수이며, 모든 $x \in \mathbb{R}$에서 수렴한다 (수렴 반경 $R = \infty$).

---

### Case 2: $a_0 = 0$, $a_1 = 1$ (홀수 함수 해)

초기 조건에 의해 모든 짝수 항 계수는 $0$이 된다 ($a_0 = a_2 = a_4 = \cdots = 0$). 홀수 항 계수는 다음과 같다.

- $n=1 \;\Rightarrow\; a_3 = \dfrac{2(1-3)}{(1+2)(1+1)}\, a_1 = \dfrac{-4}{6} = -\dfrac{2}{3}$
- $n=3 \;\Rightarrow\; a_5 = \dfrac{2(3-3)}{(3+2)(3+1)}\, a_3 = 0$

$a_5 = 0$이 되는 순간 점화식의 연쇄 효과로 인해 $a_7 = a_9 = \cdots = 0$이 된다. 따라서 이 해는 무한급수가 아닌 **3차 다항식**으로 종료된다.

$$\boxed{\; y_2(x) = x - \tfrac{2}{3}x^3 \;}$$

> **참고:** $y_2(x)$는 표준화된 Hermite 다항식 $H_3(x) = 8x^3 - 12x$와 상수배 관계에 있다 ($H_3(x) = -12\, y_2(x)$).

---

## 3. 최종 일반해 종합

Hermite 미분방정식 $y'' - 2xy' + 6y = 0$의 최종 일반해는 선형독립인 두 기저 해 $y_1(x)$와 $y_2(x)$의 선형결합으로 다음과 같이 표현된다.

$$y(x) = a_0 \left( 1 - 3x^2 + \tfrac{1}{2}x^4 + \tfrac{1}{30}x^6 + \tfrac{1}{280}x^8 + \cdots \right) + a_1 \left( x - \tfrac{2}{3}x^3 \right)$$

여기서 $a_0$와 $a_1$은 임의의 상수이며, 초기조건 $y(0) = a_0$, $y'(0) = a_1$에 의해 결정된다.

---

## 참고문헌

1. Boyce, W. E., DiPrima, R. C., & Meade, D. B. (2017). *Elementary Differential Equations and Boundary Value Problems* (11th ed.), Chapter 5 (Series Solutions of Second Order Linear Equations), Wiley.
2. Arfken, G. B., Weber, H. J., & Harris, F. E. (2013). *Mathematical Methods for Physicists* (7th ed.), Chapter 18 (Hermite functions), Academic Press.
3. Abramowitz, M., & Stegun, I. A. (1972). *Handbook of Mathematical Functions*, Chapter 22 (Orthogonal Polynomials), Dover.
