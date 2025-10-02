
dynamic
dynamic
dynamic

6
1 bit: T T N N T T T N N T T
miss: 6
2 bit: 00 01 00 00 01 10 11 10 01 10 11
2 bit: N   N  N   N   N  T  T   T  N  T  T
miss: 7

LW R4, 0(R2)     f  d  e  m  wb
ADD R6, R4, R5     x   x   f   d    e  m  wb
SUB R7, R6, R8                     x   x    f   d    e   m   wb
SW R7, 4(R9)                                        x     x   f    d    e  m   wb

forwarding:
LW R4, 0(R2)     f  d  e  m  wb
ADD R6, R4, R5     x   f   d    e  m  wb
SUB R7, R6, R8                f   d    e   m   wb
SW R7, 4(R9)                        f    d    e   m   wb (maybe has NOP)



scheduling:
no changes?