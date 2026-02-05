202602051500
Status: #idea
Tags: [[Design Operating Systems]]

## Context Switching
Context switching is the process of storing the state of a process or thread so that it can be restored and resume execution at a later point. This allows multiple processes to share a single CPU and is a core feature of multitasking operating systems.

### Key Components
- **Process Control Block (PCB)**: Stores the state (registers, stack pointer, program counter) of the process.
- **State Save**: The current state of the running process is saved into its PCB.
- **State Restore**: The state of the next process to run is loaded from its PCB.

### Overhead
Context switching involves computational overhead because the CPU is not doing "useful" work for the user during the switch. Minimizing this overhead is critical for system performance.
