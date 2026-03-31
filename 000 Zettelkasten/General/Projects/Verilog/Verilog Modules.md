202602121346
Status: #MOC
Tags:[[Verilog]]

connecting wires by position to modules follows standard syntax:
```verilog
mod_a instance1 ( wa, wb, wc );
```

Connecting wires by name:
```Verilog
mod_a instance2 (.out(wc), .in1(wa), .in2(wb));
```

