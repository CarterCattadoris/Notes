202602121314
Status: #idea
Tags:[[Verilog]]

vectors group related signals together

```verilog
`default_nettype none // use to help combat implicit net errors

wire[99:0] my_vector; // declare a 100 element vector
assign out = my_vector[10]; // part select a bit


wire [7:0] w;         // 8-bit wire
reg  [4:1] x;         // 4-bit reg
output reg [0:0] y;   // 1-bit reg that is also an output port (this is still a vector)
input wire [3:-2] z;  // 6-bit wire input (negative ranges are allowed)
output [3:0] a;       // 4-bit output wire. Type is 'wire' unless specified otherwise.
wire [0:7] b;         // 8-bit wire where b[0] is the most-significant bit.

reg [7:0] mem [255:0];   // 256 unpacked elements, each of which is a 8-bit packed vector of reg.
```

