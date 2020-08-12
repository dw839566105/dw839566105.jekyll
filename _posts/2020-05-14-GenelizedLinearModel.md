---
layout:     post
title:      广义线性模型
subtitle:   
date:       2020-05-14
author:     BY DW
header-img: img/post/post-bg-2.jpg
catalog: true
tags:
    - Generalized linear model
    - Linear model
---
[参考资料](https://en.wikipedia.org/wiki/Generalized_linear_model)
[参考资料](https://en.wikipedia.org/wiki/Exponential_family)

# Generalized linear model
## Linear model
Given an $n$ statistical unit data set $$\{y_i, x_{i1},\cdots,x_{ip}\}$$ 
+ $y_i$ is observed values 
+ $\vec{x}_i$ is a $p$-vector regressor  

Satisfy:
$$ y_i = \beta_0 + \beta_1 x_{i1} + \cdots + \beta_p x_{ip} + \epsilon_i = \vec{x_i}^T \vec{\beta} + \epsilon_i \qquad i=1,\cdots,n$$  
Written into a matrix multiplier:  
$$ \vec{y} = X\vec{\beta}+\vec{\epsilon} $$

+ predicted variables $\vec{y} = [y_1, y_2,\cdots, y_n]^T$ 
+ predictor variables, regressors $X =
	\left[
    		\begin{array}{c}
        	\vec{x}_1^T \\\\
        	\vec{x}_2^T \\\\
        	\cdots \\\\
        	\vec{x}_n^T \\\\
    		\end{array}
	\right] = 
	\left[
    		\begin{array}{cccc}
        	1 & x_{11} & \cdots & x_{1p} \\\\
        	1 & x_{21} & \cdots & x_{2p} \\\\
        	\cdots & \cdots & \cdots & \cdots\\\\
        	1 & x_{ni} & \cdots & x_{np} \\\\
    		\end{array}
	\right]$
+ regression coefficients $\vec{\beta} = [\beta_0, \beta_1,\cdots, \beta_p]^T$  
+ error term $\vec{\epsilon} = [\epsilon_1, \epsilon_2,\cdots, \epsilon_n]^T$ 

Note: Predicted variables $\vec{y}$ is different from predicted values are donated as $\hat{\vec{y}}$

#### Examples:
Consider a situation where a small ball is being tossed up in the air
Height $h_i$ and time $t_i$ (ignoring drag) satisfying:

$$ h_i = \beta_1 t_i + \beta_2 t_i^2 + \epsilon_i$$
Model is non-linear with time but linear with $\vec{\beta}$
Here $\vec{x_i} = [t_i, t_i^2]$  

## Generalized linear model:
In statistics, the generalized linear model (GLM) is a flexible generalization of ordinary linear regression that allows for response variables that have **error distribution models other than a normal distribution**. The GLM generalizes linear regression by allowing the linear model to be related to the response variable via a **link function** and by allowing the magnitude of the variance of each measurement to be a function of its predicted value.  

In a generalized linear model (GLM), each outcome $y_i$ of the dependent variables is assumed to be generated from a particular distribution in an exponential family, a large class of probability distributions that includes the   

+ Normal
+ Binomial
+ Poisson
+ Gamma distributions, among others.  

## Exponetial family:  
Most of the commonly used distributions form an exponential family or subset of an exponential family, include:  
+ normal
+ exponential
+ gamma
+ chi-squared
+ beta
+ Dirichlet
+ Bernoulli
+ categorical
+ Poisson
+ Wishart
+ inverse Wishart
+ geometric  

A number of common distributions are exponential families, but only when certain parameters are fixed and known. For example:

+ binomial (with fixed number of trials)
+ multinomial (with fixed number of trials)
+ negative binomial (with fixed number of failures)  

Examples of common distributions that are not exponential families are  

+ Student's t
+ Most mixture distributions
+ The family of uniform distributions when the bounds are not fixed

pdf:
$$ p(x|\theta) = h(x)\exp[\eta(\theta)\cdot T(x)-A(\theta)]$$ 
Here $\theta$ is the parameter of the distribution.
###### eg
[eg](https://people.eecs.berkeley.edu/~jordan/courses/260-spring10/other-readings/chapter8.pdf)
1. The Bernoulli distribution
$$p(x|\pi) = \pi^x (1-\pi)^{1-x} = \exp\{\log(\frac{\pi}{1-\pi})x + \log(1-\pi)\}$$
we have
$$ \eta = \frac{\pi}{1-\pi} $$
$$ T(x) = x $$
$$ A = - \log(1-\pi) $$
$$ h(x) = 1 $$
Note $ \pi = \frac{1}{1+\exp{(\eta)}} $ which is logistic regression.

2. The Poisson distribution
$$p(x|\lambda) = \frac{1}{\lambda} = \frac{\lambda^x \exp{(-\lambda)}}{x!} = \frac{1}{x!}\exp\{x\log \lambda - \lambda\}$$

we have
$$ \eta = \log\lambda $$
$$ T(x) = x $$
$$ A = - \lambda $$
$$ h(x) = \frac{1}{x!} $$

We can obviously invert the relationship between $\eta$ and $\lambda$:
$$\lambda = \exp\{\lambda\}$$

3. The Gaussion distribution
$$p(x|\mu,\sigma^2) = \frac{1}{\sqrt{2\pi}\sigma} \exp\{-\frac{1}{2\sigma^2}(x-\mu)^2\}$$
$$ = \frac{1}{\sqrt{2\pi}\sigma} \exp\{\frac{\mu}{\sigma^2}x - \frac{1}{2\sigma^2}x - \frac{1}{2\sigma^2}\mu^2 - \log\sigma\}$$

we have:  

$\eta = \left[
    		\begin{array}{c}
        	\mu/\sigma^2 \\\\
        	-1/\sigma^2 \\\\
    		\end{array}
	\right]$

$T(x) = \left[
		\begin{array}{c}
		x \\\\
		x^2 \\\\
		\end{array}
\right]$

$A(\eta) = \frac{\mu^2}{2\sigma^2} + \log \sigma = -\frac{\eta_1^2}{4\eta_2} - \frac{1}{2}\log(-2\eta_2)$

$h(x) = 1/\sqrt{2\pi}$
