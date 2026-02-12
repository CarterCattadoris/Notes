202602121410
Status: #idea
Tags:[[Verilog]]

# Syntax:
```verilog
always @ (event)
	[statement]

always @ (event) begin
	[multiple statements]
end

// Execute always block whenever value of "a" or "b" change
always @ (a or b) begin
	[statements]
end

// Execute always block at positive edge of signal "clk"
always @ (posedge clk) begin
	[statements]
end
```

For combinational always blocks, always use sensitivity list of (\*). For sys verilog, use always_comb
