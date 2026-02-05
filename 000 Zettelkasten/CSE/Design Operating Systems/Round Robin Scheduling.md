202602051516
Status: #idea
Tags: [[Design Operating Systems]]

## Round Robin Scheduling
Round Robin (RR) is a preemptive scheduling algorithm designed specifically for time-sharing systems. It is similar to FIFO but includes preemption to switch between processes.

### Time Quantum
A small unit of time, called a **time quantum** (or time slice), is defined. The ready queue is treated as a circular queue. The CPU scheduler goes around the ready queue, allocating the CPU to each process for a time interval of up to 1 time quantum.

### Performance Considerations
- **Quantum too large**: RR degenerates into FIFO.
- **Quantum too small**: RR leads to excessive [[Context Switching]] overhead, reducing overall system throughput.
- **Standard**: Most systems aim for a time quantum where 80% of CPU bursts are shorter than the quantum.
