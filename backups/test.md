#### Why choose Spherical Harmonics:  

Assumption: $\lambda_i \propto E\cdot G_i \cdot f[\theta(x_i)]$

+ $\lambda_i$ -  Expectation of $i$-th PMT
+ $E$ - kinetic energy of single event
+ $G_i$ - PMT occupancy
+ $f(\theta)$ - Photon propagation of complex model
+ $\theta$ - zenith angle in Legendre polynomial
+ $x_i$ - PMT position

Our propose is to decomposite $f(\theta)$ into Legendre polynomials:

#### Poisson Regression
Suppose we have components $X$ and observed $Y$, $Y$ satisfied Poisson distribution. Using Poisson regress model, we have:  

Observed $Y$ $\rightarrow$ expected $\Theta' X$    
$\ln E(Y|X) = \Theta' X $  
$\Rightarrow \lambda = \exp (\Theta' X) $  
$\Rightarrow  \ln \lambda = \Theta' X$

We regard $Y=\theta X+b$ as $\theta'X'$, $\theta'$ is $\theta$.append($b$) and $X'$ is $X$.append($1$).  

+ $\Theta$ - Legendre coefficients
+ $X$  - Legendre Polynomial of PMT position

Consider the expectation estimation in ML
$\ln \lambda = \xi_i + \sum_{l=0}^{L_\mathrm{cut}} \sum_{m=-l}^l \lambda_{lm}Y_{lm}(\theta_i(x_i), \phi_{i})$

+ $\theta$ - zenith angle
+ $\phi$ - azimuth angle
+ $\lambda$ - Legendre ${l,m}$ coefficient 
+ $x_i$  - PMT position
+ $\xi_i$ - $\ln G_i$ + $\ln E$

In spherical detector, $m=0$ and $\phi $ can be ignored. We simplified to   
$\ln \lambda = \mu + \ln E + \sum_{l=0}^{L_\mathrm{cut}} \lambda_{l0}Y_{l0}[\theta_i(x_i)]$
+ $\mu$ - PMT occupancy (vector)

Notice $Y_{00}$ = 1, we change the formula into
$\ln \lambda = \mu + \sum_{l=0}^{L_\mathrm{cut}} \lambda^*_{l0}Y_{l0}[\theta_i(x_i)]$
and $\lambda^*_{00} = \lambda_{00} + \ln E$  

#### Maximum likelihood based estimation  
$p(y\lvert x;\theta) = \frac{\lambda^y}{y!}\exp(-\lambda)$  
$\Rightarrow \frac{\exp[y(-\mu+\theta'x)]\cdot \exp[-\exp(\mu +\theta'x)]}{y!}$

$p(y_1,\cdots,y_m\lvert x_1,\cdots,x_m; \theta) = \prod_i^m \frac{\exp[y_i(-\mu_i+\theta'x_i)]\cdot \exp[-\exp(\mu_i +\theta'x_i)]}{y_i!}$

$\log L(\theta|X,Y) = \sum_{i=1}^m \{y_i(\mu_i+\theta'x_i)-\exp(\mu_i + \theta'x_i) - \ln(y_i!)\}$

since we want to get a optimized $\theta'$, the last part is nonsense:  
$\log L(\theta|X,Y) = \sum_{i=1}^m \{y_i(\mu_i+\theta'x_i)-\exp(\mu_i + \theta'x_i) \}$
