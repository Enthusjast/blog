---
title: test-math
date: 2026-02-23 22:58:14
updated: 2026-02-23 22:58:14
tags: 
  - test
  - maths
categories: test
---

# Math Formulas Test Document (Markdown + LaTeX)

This document demonstrates various mathematical formulas and symbols using LaTeX syntax in Markdown.

---

## 1. Inline Math

Simple inline equations: $E = mc^2$, $a^2 + b^2 = c^2$, and $\alpha + \beta = \gamma$.

The quadratic formula: $x = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a}$ solves $ax^2 + bx + c = 0$.

---

## 2. Display Math

$$
\int_{-\infty}^{\infty} e^{-x^2} \, dx = \sqrt{\pi}
$$

$$
\lim_{n \to \infty} \left(1 + \frac{1}{n}\right)^n = e
$$

$$
\sum_{k=1}^{n} k = \frac{n(n+1)}{2}
$$

---

## 3. Fractions & Roots

Inline: $\frac{1}{2}$, $\dfrac{a+b}{c+d}$

Nested: $\frac{1}{1 + \frac{1}{x}}$

Square root: $\sqrt{x}$, Cube root: $\sqrt[3]{x}$

General: $\sqrt[n]{x^n + y^n}$

---

## 4. Superscripts & Subscripts

- Simple: $x^2$, $x_i$, $x_i^2$
- Multi-character: $e^{i\pi}$, $a_{ij}^{kl}$
- Nested: $x^{y^z}$, $a_{b_{c}}$

---

## 5. Greek Letters & Symbols

### Lowercase
$\alpha$ $\beta$ $\gamma$ $\delta$ $\epsilon$ $\zeta$ $\eta$ $\theta$ $\iota$ $\kappa$ $\lambda$ $\mu$ $\nu$ $\xi$ $\pi$ $\rho$ $\sigma$ $\tau$ $\upsilon$ $\phi$ $\chi$ $\psi$ $\omega$

### Uppercase
$\Gamma$ $\Delta$ $\Theta$ $\Lambda$ $\Xi$ $\Pi$ $\Sigma$ $\Upsilon$ $\Phi$ $\Psi$ $\Omega$

### Common Symbols
$\infty$ $\nabla$ $\partial$ $\forall$ $\exists$ $\neg$ $\land$ $\lor$ $\oplus$ $\otimes$

---

## 6. Relations & Operators

### Binary Operators
$+$ $-$ $\times$ $\div$ $\pm$ $\mp$ $\cdot$ $\ast$ $\star$ $\circ$ $\bullet$

### Relations
$=$ $\neq$ $\approx$ $\equiv$ $\leq$ $\geq$ $\ll$ $\gg$ $\sim$ $\propto$

### Set Theory
$\in$ $\notin$ $\subset$ $\subseteq$ $\supset$ $\cup$ $\cap$ $\emptyset$ $\mathbb{R}$ $\mathbb{Z}$ $\mathbb{Q}$ $\mathbb{C}$

### Arrows
$\rightarrow$ $\leftarrow$ $\leftrightarrow$ $\Rightarrow$ $\Leftarrow$ $\Leftrightarrow$ $\mapsto$

---

## 7. Calculus

### Derivatives
Inline: $\frac{dy}{dx}$, $\frac{d^2y}{dx^2}$, $f'(x)$, $\partial_t u$

Display:
$$
\frac{d}{dx}\left[\int_0^x f(t)\,dt\right] = f(x)
$$

### Integrals
Single: $\int f(x)\,dx$

Definite: $\int_a^b f(x)\,dx$

Double/Triple: $\iint_R f\,dA$, $\iiint_V f\,dV$

Contour: $\oint_C \mathbf{F} \cdot d\mathbf{r}$

---

## 8. Matrices & Arrays

### Basic Matrix
$$
A = \begin{pmatrix}
a & b \\\\
c & d
\end{pmatrix}
$$

### Bracket Variants
$$
\begin{bmatrix} 1 & 2 \\\\ 3 & 4 \end{bmatrix}
\quad
\begin{Bmatrix} 1 & 2 \\\\ 3 & 4 \end{Bmatrix}
\quad
\begin{vmatrix} a & b \\\\ c & d \end{vmatrix}
$$

### Large Matrix
$$
\begin{pmatrix}
a_{11} & a_{12} & \cdots & a_{1n} \\\\
a_{21} & a_{22} & \cdots & a_{2n} \\\\
\vdots & \vdots & \ddots & \vdots \\\\
a_{m1} & a_{m2} & \cdots & a_{mn}
\end{pmatrix}
$$

### Augmented Matrix
$$
\left[\begin{array}{cc|c}
1 & 2 & 5 \\\\
3 & 4 & 6
\end{array}\right]
$$

---

## 9. Piecewise Functions

$$
f(x) = 
\begin{cases} 
x^2 & \text{if } x < 0 \\\\
0   & \text{if } x = 0 \\\\
\sqrt{x} & \text{if } x > 0
\end{cases}
$$

---

## 10. Aligning Equations

$$
\begin{align}
(a+b)^2 &= (a+b)(a+b) \\\\
        &= a^2 + ab + ba + b^2 \\\\
        &= a^2 + 2ab + b^2
\end{align}
$$

---

## 11. Special Functions

- Trigonometric: $\sin(x)$, $\cos(x)$, $\tan(x)$, $\sec(x)$
- Inverse: $\arcsin(x)$, $\arctan(x)$
- Hyperbolic: $\sinh(x)$, $\cosh(x)$, $\tanh(x)$
- Logarithmic: $\log(x)$, $\ln(x)$, $\log_b(x)$
- Special: $\Gamma(z)$, $\zeta(s)$, $\text{erf}(x)$

---

## 12. Accents & Diacritics

$\hat{x}$ $\check{x}$ $\tilde{x}$ $\bar{x}$ $\vec{x}$ $\dot{x}$ $\ddot{x}$ $\breve{x}$

---

## 13. Spacing & Formatting

Tight: $ab$  
Small space: $a\,b$  
Medium: $a\;b$  
Large: $a\quad b$  
Extra large: $a\qquad b$

---

## 14. Complex Example: Maxwell's Equations

$$
\begin{align}
\nabla \cdot \mathbf{E} &= \frac{\rho}{\varepsilon_0} \\\\
\nabla \cdot \mathbf{B} &= 0 \\\\
\nabla \times \mathbf{E} &= -\frac{\partial \mathbf{B}}{\partial t} \\\\
\nabla \times \mathbf{B} &= \mu_0\mathbf{J} + \mu_0\varepsilon_0\frac{\partial \mathbf{E}}{\partial t}
\end{align}
$$

---

## 15. Common Pitfalls & Tips

✅ Use `\,` before differentials: $\int f(x)\,dx$  
✅ Use `\left`/`\right` for auto-sizing: $\left(\frac{a}{b}\right)$  
✅ Use `\text{}` for words in math: $x_{\text{max}}$  
❌ Avoid: `$sin(x)$` → ✅ Use: `$\sin(x)$`

---

*End of Math Formulas Test Document*