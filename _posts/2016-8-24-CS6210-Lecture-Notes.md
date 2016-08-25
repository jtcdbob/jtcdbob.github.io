---
title:  "CS6210: Matrix Computations"
excerpt: "Lecture Notes for CS 6210"
categories:
  - LectureNotes
tags:
  - Notes
  - Cornell
  - Lectures
use_math: true
---
## Introduction

#### Course information
Lecturer: Prof. David Bindel

Course [website](http://www.cs.cornell.edu/%7Ebindel/class/cs6210%2Df16/).

Office Hours: 1:30-2:30 W, 10-11R

TA: David Eriksson

#### Today (08/24/16)
* Logistics
* Matrix interpretation / matrix algebra vs. linear algebra
* Dense matrix layouts, matvec, matmul, and Basic LA Subroutines (BLAS)

Problems:
$$\bf Ax = b$$

$$\min ||\bf Ax - b||$$

$$\bf Ax = \lambda x$$

$$\bf A = U\Sigma V^T$$

##### Linear Algebra
Vector spaces, norms, positive definite, linear maps, bilinear forms, quadratic forms

##### Matrix Algebra
Representation of LA, graphs of matrices, shapes of matrices, representation of matrices as data structure.

##### Dense representation of matrices
* Vectors: one major representation
    * Each element in a consecutive cell.
* Matrices: col-major, row-major. memory.
* Matrix vector ($$\bf Ax $$)
    * Two loops:
        1. $$\bf y = Ax$$.
        2. Compute
           
            ```
            for i = 1:n
                for j = 1:n
                    y(i) = y(i) + A(i,j)*x(j);
            ```
        3. Total cost: $$2n^2$$ flops (floating point ops), $$o(n^2)$$ time
    * Row oriented.
        
        ```
        for i = 1:n
            y(i) = y(i) + A(i,:)*x(:);
        ```
    * Col oriented
        
        ```
        for j = 1:n
            y = y + A(:,j)*x(j);
        ```
* Matrix addition.
* Matrix multiplication.
    * Row-oriented
    * Col-oriented
* Blocking.

Notes on performance for the lazy.

1. Don't write your own BLAS
    * MATLAB uses a well-tuned BLAS
    * NumPy/SciPy - faster if you use (e.g.) Intel MKL
    * MKL - gratis
    * OpenBLAS
    * Learn to think in blocks
    * FLOP $$\not =$$ Performance
