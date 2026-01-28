202601271456
Status: #idea
Tags:[[Deep Learning (ELE400)]]

insert neuron image here

using exponential input output in form ($x_{1}, x_{2}, d$)
error: e = neuron output vs actual (desired) output = $x_{1}w_{1} + x_{2}w_{2} - d$
error squared: $e^2$ 
1) gets rid of +/- cancellation
2) punishes larger errors more
3) $()^2$ is easy to differentiate

learning rule: change $w_{1}$ in direction to reduce error by amount proportional to partial derivative of $e^2$ with respect to (wrt) $w_{i}$

$\Delta w_{i} = -\eta \frac{ \partial(e^2)}{\partial(w_{i})}$
