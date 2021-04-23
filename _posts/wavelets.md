
Euler's formula:
$\exp(2\pi i \theta) = \cos(2\pi i \theta) + i\sin(2\pi i \theta)$
## Fourier Transform:
There are several common conventions for defining the Fourier transform of an integrable function $f: \mathcal{R}\rightarrow \mathcal{C} $  
One of them: 
$\hat f(\xi) = \int_\infty^\infty f(x) \exp(-2\pi i x \xi) dx$

Inverse transform:
$f(x) = \int_\infty^\infty \hat f(\xi) \exp(-2\pi i x \xi) d\xi$


exponent part is a signal with zero initial phase and frequency $\xi _{0}$, and the angular frequency is $\omega_0=2\pi\xi_0 $

This form is a correlation of $f(x)$ and the different sine and cosine component.