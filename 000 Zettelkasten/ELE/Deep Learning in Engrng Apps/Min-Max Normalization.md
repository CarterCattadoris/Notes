202602261022
Status: #idea
Tags: [[Deep Learning (ELE400)]]

**Min-Max Normalization** scales a value $x \in [x_{\min}, x_{\max}]$ to a target range $[n_{\min}, n_{\max}]$.

## Formula (to [0, 1])

$$n = \frac{x - x_{\min}}{x_{\max} - x_{\min}}$$

Steps:
1. Subtract $x_{\min}$ from $x$.
2. Divide by the range $(x_{\max} - x_{\min})$.

## General Formula (to [n_min, n_max])

$$n = (x - x_{\min}) \cdot \frac{n_{\max} - n_{\min}}{x_{\max} - x_{\min}} + n_{\min}$$

Steps:
1. Subtract $x_{\min}$ from $x$.
2. Multiply by $\frac{n_{\max} - n_{\min}}{x_{\max} - x_{\min}}$.
3. Add $n_{\min}$.

## Example

For $x_3 = 0$ with $x_{\min} = -20$, $x_{\max} = 30$, normalizing to $[0, 1]$:
$$n_3 = \frac{0 - (-20)}{30 - (-20)} = \frac{20}{50} = 0.4$$

## Usage

Used in [[Transformer]] attention blocks and generally in preprocessing neural network inputs to ensure values lie within consistent ranges.
