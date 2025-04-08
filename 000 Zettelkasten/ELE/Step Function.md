202501280941
Status: #idea
Tags:[[Linear Systems (ELE251)]]

Step function u(t) represents a signal that turns on and stays on, starting at t=0 unless specified
$$u(t) = \begin{cases}
0, & \text{if } t < 0,\\
1,  & \text{if } t \geq 0.
\end{cases}$$
$$u(t - 2) = \begin{cases}
0, & \text{if } t < 2,\\
1,  & \text{if } t \geq 2.
\end{cases}$$

The derivative of u(t) is the [[Dirac Delta function]]: 
$\frac{d}{dt} u(t)=\delta (t)$

scaled by number of volts applied

---
### References