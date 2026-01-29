202501301003
Status: #idea
Tags:[[Laplace Transform]]


| Time Domain              | Laplace Domain                                                           | Notes                                      |
| ------------------------ | ------------------------------------------------------------------------ | ------------------------------------------ |
| $1,u(t)$                 | $\frac{1}{s}$                                                            | unit step                                  |
| $\delta(t)$              | $1$                                                                      | unit impulse                               |
| $t$                      | $\frac{1}{s^2}$                                                          | unit ramp                                  |
| $e^{at}$                 | $\frac{1}{s-a}$                                                          | exponential, a is a constant               |
| $af(t)$                  | $aF(s)$                                                                  | constant time is a time dependant variable |
| $f(t) +g(t)$             | $F(t)+G(t)$                                                              | add 2 time dependent variables             |
| $\frac{df(t)}{dt}$       | $sF(t)-f(0)$                                                             | for ELE251, f(0) = 0                       |
| $\int_0^t f(\tau) d\tau$ | $\frac{F(s)}{s}$                                                         | integral                                   |
| $\cos(\omega t)$         | $\frac{s}{s^2+w^2}=\frac{1/2}{s-j\omega} + \frac{1/2}{s+j\omega}$        |                                            |
| $\sin(\omega t)$         | $\frac{\omega}{s^2+w^2}=\frac{1/2j}{s-j\omega} - \frac{1/2j}{s+j\omega}$ |                                            |
| $A\sin(\omega t)$        | $A\frac{e^{j(\omega t)} - e^{-j(\omega t )}}{2j}$                        | notebook 2_3                               |
|                          |                                                                          |                                            |


---
### References