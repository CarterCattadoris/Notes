202510281041
Status: #idea
Tags:[[CSE 381]]

**Given**

- Physical address: **32 bits**
    
- Total cache size: **64 KiB**
    
- Block size: **32 B**
    
- Mapping: **Direct-mapped (1-way)**

offset = $\log_{2}{(32B)} = 5B$

\# blocks = $\frac{64KiB}{32B} = \frac{65536}{32} = 2048$

index bits = $\log_2{(2048)} = 11$

tag bits = 32 - index bits - offset = 32 - 11 - 5 = 16