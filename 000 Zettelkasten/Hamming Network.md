202601271508
Status: #idea
Tags:[[ELE 400 - Deep Learning]]

Distance computation and comparison are essential to unsupervised
learning networks. In most of the previous examples we’ve seen the
Euclidean distance used. One of the most efficient versions utilizes the
Hamming distance

$H(i_{1, i_{2}}) =$ # of bits where $i_{1,j} \& i_{2,j}$ have different binary values

ex: $i_{1}$ = 1 0 1 0
$i_{2}$ = 1 1 0 1

$i_{p} = \begin{pmatrix}i_{p,1} \\ \dots \\ i_{p,n}\end{pmatrix}$

where:
p=1,...,P is the input pattern index
j=1, ..., n is the index of the elements of the input pattern (either one of the P stored patterns or a new pattern presented to the network)
![[Pasted image 20260127151115.png]]

The weight matrix and threshold vector $\theta$ are given by

$W = \frac{1}{2} \begin{pmatrix} i^T_{1} \\ \dots \\ i^T_{P}\end{pmatrix}$   $\theta = -\frac{1}{2} \begin{pmatrix} n \\ \dots \\ N\end{pmatrix}$

$i_{k,n} \in \{ -1, +1 \}$ 

$i_{1}$: 1 1 -1 -1
$i_{2}$: 1 -1 1 -1
   1 -1 -1 1

Consider that a new input pattern vector i is applied to the input. Then the output vector o can be found as