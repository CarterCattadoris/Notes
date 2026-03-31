202602121416
Status: #idea
Tags:[[Verilog]]

```verilog
always @ (*) begin
        case(sel)
            2'b00 : out = d;
            2'b01 : out = q1d2;
            2'b10 : out = q2d3;
            2'b11 : out = q;
        endcase
    end
```