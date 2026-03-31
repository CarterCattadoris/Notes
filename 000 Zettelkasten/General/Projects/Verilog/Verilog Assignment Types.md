202602121455
Status: #idea
Tags:[[Verilog]]

Continuous assignments (assign x = y;) can only be used when **not** in a procedure ("always" block)

Procedural blocking assignments (x = y;) can only be used in a procedure

Procedural non-blocking assigments (x <= y;) only in a procedure

in **combinational** always block (\*), use **blocking** assignments
in **clocked** always block (posedge clk) use **non-blocking** assignments