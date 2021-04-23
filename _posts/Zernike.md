---
layout:     post
title:      Zernike (教程翻译)
subtitle:   
date:       2020-08-04
author:     BY DW
header-img: img/post/post-bg-2.jpg
catalog: true
tags:
    - Zernike
---
[参考资料](https://en.wikipedia.org/wiki/Zernike_polynomials)
[参考资料](https://github.com/jacopoantonello/zernike)

#### class Zern(ABC):
  Shared code for `RZern` and `CZern`.
  ```
  def __init__(self, n, normalise=NORM_NOLL):
      nk = (n + 1) * (n + 2) // 2
      self.n = n
      self.nk = nk % 相当于是基底的最大阶数
      
      self.rhotab = rhotab  % coefficients of R_n^m(\rho)
      self.rhoitab = rhoitab % 积分
      self.ntab = ntab % n的取值
      self.mtab = mtab % m的取值
      self.coefnorm = coefnorm % 拟合的各个阶数
  ```
  
  ```
  @abstractmethod
  def ck(self, n, m):
        Normalisation coefficient for the `k`-th Zernike polynomial.
        
  def Rnm(self, k, rho):
        Compute the `k`-th radial polynomial :math:`R_n^m(\rho)`.
        
  def angular(self, k, theta):
        Compute the angular function for the `k`-th Zernike polynomial.
        
  def radial(self, k, rho):
        Compute the radial function for the `k`-th Zernike polynomial.
        
  def Zk(self, k, rho, theta):
        Compute the `k`-th Zernike polynomial.
        
  def eval_a(self, a, rho, theta):
        Compute the sum of `self.nk` Zernike polynomials at a point.
  
  def noll2nm(self, k):
        Convert Noll's index `k` to the indices `(n, m)`.
        
  def vect(self, Phi):
        "Reshape `Phi` into a vector"
        
  def matrix(self, Phi):
        "Reshape `Phi` into a matrix"
        
  def make_cart_grid(self, xx, yy, unit_circle=True):
        Make a cartesian grid to evaluate the Zernike polynomials.
        Parameters
        ----------
        - `xx`: `numpy` array generated with `numpy.meshgrid()`.
        - `yy`: `numpy` array generated with `numpy.meshgrid()`.
        - `unit_circle`: set `np.nan` for points where :math:`\rho > 1`.
        
  def eval_grid(self, a, matrix=False):
        Evaluate the Zernike polynomials using the coefficients in `a`.
        
  def fit_cart_grid(self, Phi, rcond=None):
        Fit a cartesian grid using least-squares.
  
  def make_pol_grid(self, rho_j, theta_i):
        Make a polar grid to evaluate the Zernike polynomials.
  ```
  #### class RZern(Zern):
  Real-valued Zernike polynomials.
  ```
  def __init__(self, n, normalise=Zern.NORM_NOLL):
        super().__init__(n, normalise)
        self.numpy_dtype = 'float'

  def ck(self, n, m):
        if self.normalise == self.NORM_NOLL:
            if m == 0:
                return np.sqrt(n + 1.0)
            else:
                return np.sqrt(2.0 * (n + 1.0))
        else:
            return 1.0

  def angular(self, j, theta):
        m = self.mtab[j]
        if m >= 0:
            return np.cos(m * theta)
        else:
            return np.sin(-m * theta)
  ```
  
  #### class FitZern:
  Compute the approximate inner products using Riemann sums in polar
  
  ```
  def __init__(self, z, L, K):
        Initialise a grid with `L` points for theta and `K` for rho.
        Parameters
        ----------
        - `z`: `RZern` or `CZern` object
        - `L`: number of points for sampling :math:`\theta`
        - `K`: number of points for sampling :math:`\rho`
        
  def fit_ak(self, k, Phi):
        Compute the inner product for the `k`-th coefficient.
        See Eq. (B2) and Eq. (B4) in Appendix B of [A2015]_.
        Parameters
        ----------
        -   `k`: `k`-th Zernike coefficient.
        -   `Phi`: `L` x `K` matrix stored in column major order into
            a list object.            
        Returns
        ----------
        - `ak`: `k`-th Zernike coefficient
        
  def _fit_slow(self, Phi):
        Compute all the inner products. `Phi` is a phase grid in polar
        coordinates.
        Parameters
        ----------
        -   `Phi`: `L` x `K` matrix stored in column major order into
            a list object.
        Returns
        ----------
        `a`: list of Zernike coefficients
        
   def fit(self, Phi):
        Compute all the inner products. `Phi` is a phase grid in polar
        coordinates.
        Parameters
        ----------
        -   `Phi`: `L` x `K` matrix stored in column major order into
            a `numpy` array.
        Returns
        ----------
        `a`: `numpy` vector of Zernike coefficients
  ```
  
