202503301352
Status: #idea
Tags:[[Comparators]]

A carry-ripple comparator compares two N-bit numbers from left to right, with the result of each digit's comparison "rippling" to the next digit. For each digit, a 1-bit comparator compares two bits a and b only if the eq input is 1 from the higher digit, or else just passes along a gt 1 or an lt 1. The rightmost digit's output becomes the N-bit comparator's output.

![[Pasted image 20250330135313.png]]