---
layout:     post
title:      内点法基本推导
subtitle:   
date:       2019-09-20
author:     BY DW
header-img: img/post/post-bg-2.jpg
catalog: true
tags:
    - Interior point
    - Optimization
---

# Question:  
#### Nonlinear Constrained Optimization
>$ \min f(x) $
s.t.  
$c(x)=0$ & $ x \geq 0$  

#### Using slack variable  

>$\min_{x\in R^n} f(x)$
s.t.
$ g(x)\geq b $
$ h(x) = 0$ 

$\Rightarrow$

>$\min_{x\in R^n} f(x)$
s.t.
$ c(x) = 0 $
$ x \geq 0$ 

###### e.g.
> $\min_x x_1 x_4(x_1+x_2+x_3)$
s.t.
$x_1 x_2 x_3 x_4 \geq 25$
$x_1^2 + x_2^2 + x_3^2 + x_4^2 = 40$

$\Rightarrow$

> $f(x) = x_1 x_4(x_1+x_2+x_3)$
$c_1(x) : x_1 x_2 x_3 x_4 - 25 - s = 0$
$x_2(x) : x_1^2 + x_2^2 + x_3^2 + x_4^2 - 40 = 0$
$s \geq 0$

#### Barrier function
>$\min_{x\in R^n} f(x)$
s.t.
$ c(x) = 0 $
$ x \geq 0$ 

$\Rightarrow$

>$\min_{x\in R^n} f(x) - \mu\sum_{i=1}^n \ln(x_i)$
s.t.
$ c(x) = 0 $

The logarithm include $x\geq 0$

###### e.g.
>$\min_{x\in R} (x-3)^2$
s.t.
$ x \geq 0$

$\Rightarrow$

>$\min_{x\in R} (x-3)^2 - \mu\ln(x)$

#### How to solve a barrier function  
+ KKT conditions  

> $\min_{x\in R^n} f(x)-\mu\ln\sum_{i=1}^n\ln(x_i)$
s.t.
$c(x)=0$

$\Rightarrow$

> $\nabla f(x)-\nabla c(x)\lambda - \mu\ln\sum_{i=1}^n \frac{1}{x_i}$
s.t.
$c(x)=0$  
  
***  

##### KKT condition:  
$\min_{x\in R} f(x)$ s.t. $h_i(x)=0$ and $g_j(x)\leq 0$  
Lagrangian:  
$L(x,\mu,\lambda) = f(x)+\mu^th(x) + \lambda^t g(x)$  

$x^\*$ is a local minimum $\Leftrightarrow$ There is a unique $\lambda^*$ s.t.   
1. $\nabla_x \mathcal{L}(x^\*,\lambda^\*) = 0$
2. $\lambda^\*>0 $
3. $\lambda^\*g(x^\*)=0$
4. $ g(x) \leq 0 $
5. $ h(x^\*) = 0 $
6. Positive definite constraints: $\nabla_{xx}\mathcal{L}(x^\*,\lambda^\*)$  

---

#### Solve 
##### step1
Define $z_i=\frac{\mu}{x_i}$, the function will be
>$ \nabla f(x) + \nabla c(x) \lambda - z = 0 $
$c(x) = 0$
$XZe-\mu e = 0$

Here $e$ is a column of ones.

##### step2
using Newton-Raphson method
$
\left(              
  \begin{array}{ccc}
    W_k & \nabla c(x_k) & -I\\\\  
    \nabla c(x_k)^T & 0 & 0\\\\  
    Z_k & 0 & X_k\\\\  
  \end{array}
\right)
\left(
    \begin{array}{c}
    d_k^x\\\\  
    d_k^\lambda\\\\  
    d_k^z\\\\  
    \end{array}
\right)
 =-
\left(
    \begin{array}{c}
    \nabla f(x) + \nabla c(x) \lambda - z\\\\  
    c(x) \\\\  
    XZe-\mu e\\\\  
    \end{array}
\right)
$  

where:
$W_k = \nabla_{xx}^2 (f(x_k)+x(x_k)^T -z_k)$  
$z_k = 
\left[
    \begin{array}{ccc}
    z_1 & 0 & 0\\\\  
    0 & \cdots & 0 \\\\  
    0 & 0 & z_n\\\\  
    \end{array}
\right]
$  
$X_k = 
\left[
    \begin{array}{ccc}
    x_1 & 0 & 0\\\\  
    0 & \cdots & 0 \\\\  
    0 & 0 & x_n\\\\  
    \end{array}
\right]
$
  
#### Rearrange
$
\left[                 
  \begin{array}{cc}
    W_k+\Sigma_k & \nabla c(x_k)\\\\    
    \nabla c(x_k)^T & 0\\\\    
  \end{array}
\right]
\left(
    \begin{array}{c}
    d_k^x\\\\  
    d_k^\lambda\\\\  
    \end{array}
\right)
=-
\left(
    \begin{array}{c}
    \nabla f(x_k) + \nabla c(x_k) \lambda_k - z\\\\  
    c(x_k) \\\\  
    \end{array}
\right)
$  
Where $\Sigma_k = X_k^{-1}Z_k$  
and $d_k^z = \mu_kX_k^{-1}e-z_k-\Sigma_kd_k^x$  

#### Stepsize $\alpha$
+ 2 objectives in evaluating progress
  * minimize objective
  * minimize constraint violations

+ 2 popular approaches
  * discrete in merit function, $merit =f(x)+\nu \sum|c(x)|$  

