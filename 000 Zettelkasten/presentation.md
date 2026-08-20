
1. Was probing around buck circuit when i heard a pop and read 1.6V at the output
 2. immediately shut off power supply
 3. measured resistances from rails to ground, all seemed normal
 4. checked datasheet for overcurrent or shutdown modes, found one but after probing it was clear that it wasn't going into that
 5. removed inductor and injected 3.3 into the output, and the 3.0V regulator as well as everything downstream
 6. replaced the inductor and measured feedback pin which was stuck at 0.5V indicating the physical module failed
 7. replaced buck IC and it was back to fully functioning

SD card latency: 
worst stall: 496.5ms
stalls every roughly 17 seconds
to compensate, keep a 512kb buffer of data to write to the card which is larger than necessary but consumes ~6% of PSRAM
write speed of 2659 kb/s which is roughly 50x more than necessary


