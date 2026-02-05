202602051515
Status: #idea
Tags: [[Design Operating Systems]]

## FIFO Scheduling
First-In, First-Out (FIFO), also known as First-Come, First-Served (FCFS), is the simplest CPU scheduling algorithm. Processes are dispatched to the CPU in the order they arrive in the ready queue.

### Characteristics
- **Non-preemptive**: Once a process starts, it runs until it completes or blocks for I/O.
- **Implementation**: Managed with a FIFO queue.

### The Convoy Effect
A significant disadvantage of FIFO is the **convoy effect**, where short processes must wait for one long process to finish. This leads to poor CPU and device utilization if a CPU-bound process holds the processor while I/O-bound processes wait in the ready queue.
