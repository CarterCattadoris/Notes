202501231534
Status: #idea
Tags:[[Binary]]

Leftmost bit serves as a sign bit
- 0 for positive numbers
- 1 for negative numbers

Suppose we're working with 8 bit quantities (for simplicity's sake) and suppose we want to find how -28 would be expressed in two's complement notation. First we write out 28 in binary form:

00011100

Then we invert the digits. 0 becomes 1, 1 becomes 0.

11100011

Then we add 1.

11100100

That is how one would write -28 in 8 bit binary.

100 in 2's complement:

4(in normal binary) - 2^3 = -4

101(5) - 2^3 = -3


---
### References