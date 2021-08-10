EM (Expectation Maximization)

Observed data are N samples independently generated from the mixture probalilistic model:
$P(X|\Theta) = \sum_{k=1}^K \pi_k p_i(X|\theta_i)$
Here $\Theta = \{{\pi_1,…,\pi_M,\theta_1,…,\theta_M}\}$.

Suppose $z$ is a hidden variable that describe which class $x_{i}$ comes from, including

## GMM

latent data: type $z_k$: K-dimensional binary random variable $z$ having a 1-of-K encoding.  
$z_k\in\{0,1\}$, $\sum_k z_k = 1$  
$p(x|\omega_j,\theta_j)\sim \mathcal{N}(\mu_i,
\Sigma_i)$ notice that $\omega_i$ indicates the type.

Joint distribution:
$p(x,z) = p(x|z)p(z)$
$p(z_k = 1) = \pi_k$ and $\sum_{k=1}^K\pi_k = 1$. 

Notice that $p(z) = \prod_{k=1}^{K} \pi_k^{z_k}$


Conditional distribution of x given a particular value z is a Gaussian

$p(x|z) = \prod_{k=1}^{K} \mathcal{N} (x|\mu_k, \Sigma_k)^{z_k}$

$p(x) = \sum_{k=1}^K \pi_k \mathcal{N}(x|\mu_k, \Sigma_k)$
Every data point has its own latent variable $z^{(n)}$

Using Bayesian rule, the conditional probability of $z$ given $x$

$\gamma(z_k) := p(z_k = 1|x) = \frac{p(z_k=1)p(x|z_k=1)}{p(x)} $

$= \frac{p(z_k=1)p(x|z_k=1)}{\sum_{j=1}^{K}p(z_j=1)p(x|z_j=1)} = \frac{\pi_k \mathcal{N}(x|\mu_k, \Sigma_k)}{\sum_{j=1}^{K} \pi_j \mathcal{N}(x|\mu_j, \Sigma_j)}$
$p(X|\theta) = \prod_{i=1}^{N}\sum_{j=1}^{c} \mathcal{N}(x_i|\mu_j, \theta_j) P(\omega_j)$

$\ln p(X|\theta) = \sum_{i=1}^{N}\ln\sum_{j=1}^{c} \mathcal{N}(x_i|\mu_j, \theta_j) P(\omega_j)$

#### E step:
We are not sure which Gaussian generate each datapoint, so it is probability over all datapoints:
$\gamma(z_k^{(n)}) = p(z_k=1|x)$
#### M step:
Each Gaussian generate a certain amount of posterior probability for each datapoint, the optimum satisfies:

$\frac{\partial \ln p(X|\theta)}{\partial \Theta} = 0$

$\sum_{i=1}^{N}\frac{\mathcal{N}(x_i|\mu_k, \theta_k) P(\omega_k)}{\sum_{j=1}^{c} \mathcal{N}(x_i|\mu_j, \theta_j)P(\omega_j)} \Sigma_k^{-1}(x_i-\mu_k)= 0$

$P(\omega_k| x_i, \mu_k, \Sigma_k) = \frac{\mathcal{N}(x_i|\mu_k, \theta_k)P(\omega_k)}{\sum_{j=1}^{c} \mathcal{N}(x_i|\mu_j, \theta_j)P(\omega_j)}$

$\mu_k = \frac{\sum_{i=1}^{N} P(\omega_k| x_i, \mu_k, \Sigma_k) x_i}{\sum_{i=1}^{N} P(\omega_k| x_i, \mu_k, \Sigma_k)}$

$ P(\omega_k) = \frac{1}{N} \sum_{i=1}^{N} P(\omega_k| x_i, \mu_k, \Sigma_k) $

$ \Sigma_k = \frac{\sum_{i=1}^{N} P(\omega_k| x_i, \mu_k, \Sigma_k) (x_i-\mu_k)(x_i-\mu_k)^T}{\sum_{i=1}^{N} P(\omega_k| x_i, \mu_k, \Sigma_k)}$

## BAPPE
$ p(X|\theta) = \pi_k p_i(X|\theta_i) $
$ p(x_i|\theta) = \alpha L(t_i) Z(r,\theta) = \alpha L(t_i) R_m^n(r) \cos(m \phi)$


