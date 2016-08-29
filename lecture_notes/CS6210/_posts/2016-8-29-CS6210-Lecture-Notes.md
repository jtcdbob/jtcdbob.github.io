---
title:  "CS6210: Matrix Computations - Topics overview"
excerpt: "Lecture Notes for CS 6210"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---
## 08/29/2016

### Announcements

* Shift HW to biweekly (see web)
* Piazza to be set up today
* Email Prof. if not enrolled & want HW access (CMS).

### Matrix

* Concrete vector space $$\mathbb{R}^n$$ or $$\mathbb{C}^n$$ (or $$\mathbb{R}^{m\times n}$$ or $$\mathbb{C}^{m\times n}$$)
* Abstract vector space $$\mathscr{V},~\mathscr{W}$, etc.
    * $$\mathscr{P}_d = \{p(z) = \sum_{j=0}^d a_j z^j\}$$, polynomials of degree basis (power basis) for $$\mathbb{P}_d$$ in matrix form.
    * $$V = [1, x, x^2, dots, x^d]$$ "Chebyshev(Tschebycheff)".
        * $$T_m(x) = \cos(ma\cos x),~x\in[-1, 1]$$.
        * $$T_0(x) = 1$$.
        * $$T_1(x) = x$$.
        * $$T_m(x) = 2xT_k(x) - T_{k-1}(x)$$.
    * Legendre polynomials - more later
        * $$V^{-1}$$ is the matrix inverse or mapping of vector onto expansion coefficients.
* Duality
    * $$R^{n}$$ is column vectors of length
    * $$x\in \mathbb{R}^n$$ column
    * $$x^*$$ row vector (or $$x^T$$, $$x^H$$)
    * $$x^*\in\mathscr{V}^*$$ means linear function on $$\mathscr{V}$$ i.e. $$x^*: \mathscr{V} \to \mathbb{R} (\mathbb{C})$$ linear map.
* Norms $$\|\cdot\|: \mathscr{V} \to \mathbb{R}$$.
    1. Homogenous: $$\|\alpha {\bf v}\| = \|\alpha\|~\|\bf v\|$$
    2. Positive definite: $$\|{\bf v}\| \ge 0$$, $$\|\bf v\| = 0 \Rightarrow {\bf v} = {\bf 0}$$
    3. Triangle inequality: $$ \bf \|v + w\| \le \| v\| + \|w\|$$
* Usual suspects
    * $$\|x\|_2^2 = x^* x$$.
    * $$\|x\|_1 = \sum_i \|x_i\|$$.
    * $$\|x\|_\inf = \max\|x_i\|$$.
* Dual norm:
    * $$\|x^*\| = \max_{\|{\bf y}\| = 1} \|\bf x^*y\|$$
* Equivalentce of norms on a finite dimensional space.
    * For any two norms on the same finite dimensional space, we can bound one norm using the other (though sometimes the bound can be quite loos).
* Innter Product $$<\cdot, \cdot>: \mathscr{V}\times\mathscr{V} \to \mathbb{C}$$
    1. Linear in first slot $$<\alpha u + v, w> = \alpha<u, w> + <v, w>$$
    2. Conjugate linear in second slot $$<u, \alpha v + w> = \overline{\alpha}<u, v> + <u, w>$$ & $$<u, v> = \overline{<v, u>}$$
    3.
    3. Positive definite $$<v, v> \ge 0$$, equal iff zero. ($$<v,v> = \|v,v\|_2^2$$)
    4. Angle between $$u, v$$.
        $$
        \cos\theta = \frac{<u, v>}{\|u\|_2 \|v\|_2}
        $$
    5. $$\mathscr{P}_d$$ space polynomial of degree $$\le d$$.
        $$
        <p, q> = \int_{-1}^1 p(x)\overline{q}(x)dx
        $$
* Matrices representations
    1. Linear map: $$y = Ax$$
    2. Bilinear form/sesquilinear form: $$(x,y) = y^HAx$$
    3. Quadratic form: $x \to x^HAx$
* Matrix norms
    * Treat matrices (or $$\mathscr{L}(\mathscr{V}, \mathscr{W})$$) as a vector space, use a vector norm.
    * Consistency (submultiplicative) $$\|y\| \le \|A\|\|x\|$$ if $$y = Ax$$
    * Operator norms $$\|A\| = \sup_{\|x\| = 1} \|Ax\|$$
    * Non-operator norms
        * Frobenius norm:
            * $$\|A\|_F^2 = \sum_{i, j} \|a_{i,j}\|^2$$.
            * $$<A, B>_F = tr(B^*A) = \sum_{i,j}a_{i,j} b^*{i,j}$$.
    * Operator norms
        * 2-norm
        * 1-norm $$max_j\sum_i\|a_{i,j}\|$$ (max absolute column sum)
        * $$\inf$$-norm $$\max_i \sum_j\|a_{i,j}\|$$ (max absolute row sum)
* Aside:
    * Orthogonal matrix $$Q^TA = I$$.
    * Unitary matrix $$U^*U = I$$
    * Invariance properties:
        * $$\|Qx\|_2 = \|x\|_2$$ (orthogonal invariance of 2-norm in $$\mathbb{R}^n$$ space)
        * $$\|QA\|_F = \|A\|_F$$.
        * $$\|AQ\|_F = \|A\|_F$$.
        * $$\|AQ\|_2 = \|A\|_2,~\|QA\|_2 = \|A\|_2$$
* Decompositions
    * LU factorization: $$PA = LU$$.
    * Cholesky $$A = LL^*$$
    * QR $$A = QR$$
    * SVD $$A = U\SigmaV^*$$
    * Eigen decomposition $$A = U\Lambda U^*$$
    * Schur $$A = UTU^*$$
