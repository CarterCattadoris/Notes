202602121252
Status: #idea
Tags:[[Verilog]]

Assigning multiple wires assuming all are correct width

```verilog
module top_module( 
    input a,b,c,
    output w,x,y,z );
    
    assign {w,x,y,z} = {a,b,b,c}
    // w = a, x,y = b, z = c
endmodule
```