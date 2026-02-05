# OS Roadmap

## 1. Introduction to Operating Systems
- [[Design of OS (CSE486)]]
- What is an operating system?
- OS structure and components
- System calls and APIs
- Kernel modes (user mode vs kernel mode)

## 2. Process Management
- Process concept
    - Process states (new, ready, running, waiting, terminated)
    - Process control block (PCB)
    - Process creation and termination
- [[Context Switching]]
    - Context switch overhead
    - Hardware support for context switching
- Threads
    - User-level vs kernel-level threads
    - Multithreading models
    - Thread libraries

## 3. CPU Scheduling
- Scheduling criteria
    - CPU utilization
    - Throughput
    - Turnaround time
    - Waiting time
    - Response time
- [[FIFO Scheduling]]
    - First-Come-First-Served (FCFS)
    - Advantages and disadvantages
    - Convoy effect
- [[Round Robin Scheduling]]
    - Time quantum selection
    - Performance characteristics
- Shortest Job First (SJF)
    - Preemptive and non-preemptive
    - Optimal average waiting time
- Priority scheduling
    - Static vs dynamic priorities
    - Priority inversion
    - Aging
- Multilevel queue scheduling
- Multilevel feedback queue scheduling
- Real-time scheduling
    - Rate monotonic scheduling
    - Earliest deadline first

## 4. Process Synchronization
- Critical section problem
    - Mutual exclusion
    - Progress
    - Bounded waiting
- Synchronization primitives
    - Locks and mutexes
    - Semaphores (binary and counting)
    - Monitors
    - Condition variables
- Classic synchronization problems
    - Producer-consumer problem
    - Readers-writers problem
    - Dining philosophers problem
- Deadlocks
    - Necessary conditions
    - Prevention and avoidance
    - Detection and recovery

## 5. Memory Management
- Memory hierarchy
- Address binding
- Logical vs physical address space
- Memory allocation
    - Contiguous allocation
    - Paging
    - Segmentation
    - Segmentation with paging
- Virtual memory
    - Demand paging
    - Page replacement algorithms (FIFO, LRU, optimal)
    - Thrashing
    - Working set model
- Memory-mapped files
- Kernel memory allocation

## 6. File Systems
- File concept
    - File attributes and operations
    - File types
    - Access methods
- Directory structure
    - Single-level, two-level, tree-structured
    - Acyclic graph directories
- File system implementation
    - Allocation methods (contiguous, linked, indexed)
    - Free-space management
    - Directory implementation
- File system performance
    - Caching
    - Read-ahead
    - Write buffering

## 7. I/O Systems
- I/O hardware
    - Devices and controllers
    - Memory-mapped I/O vs port-mapped I/O
- I/O methods
    - Programmed I/O
    - Interrupt-driven I/O
    - Direct memory access (DMA)
- Device drivers
- Disk structure and scheduling
    - FCFS, SSTF, SCAN, C-SCAN, LOOK
- RAID levels

## 8. Protection and Security
- Goals of protection
- Access control
    - Access matrix
    - Access control lists (ACL)
    - Capabilities
- Security threats
    - Malware (viruses, worms, trojans)
    - Attack vectors
- Authentication mechanisms
- Encryption and cryptography basics
