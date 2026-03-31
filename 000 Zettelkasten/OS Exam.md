# OS Quiz Study Sheet

## PART A: PROCESSES AND THREADS

---
### 1. What Is a Process?

A **process** is a program in execution. A program is just source code stored on disk; a process is that code loaded into memory with its own state, ready to be run by the CPU.

**How a process is created (what the OS does when you double-click an icon):**

1. OS creates a **PCB (Process Control Block)** — the data structure that represents the process.
2. OS creates the **address space** and loads the program into it.
3. OS inserts the PCB into the **ready queue**.
4. OS performs a **context switch** to let the new process run.

**Three ways a process can be created:**

- A user explicitly launches a program (double-click, command line).
- A running process creates a child prompted by an external event.
- A running process explicitly calls `fork()`.
- All three are fundamentally the same — they all reduce to a running process calling fork().

---

### 2. Address Space Segments

Every process has a virtual address space divided into four segments:

- **Text segment:** The compiled executable code. Fixed size.
- **Static data segment:** Global/static variables. Fixed size.
- **Dynamic data segment (heap):** Grows when `malloc()` / `new` is called.
- **Stack segment:** Grows when subroutine calls are made (pushes arguments + return address).

The heap grows upward, the stack grows downward — they can collide if unchecked.

---

### 3. PCB (Process Control Block) — Know This Table

|Process Management|Memory Management|File Management|
|---|---|---|
|Registers|Pointer to text segment|Root directory|
|Program counter (PC)|Pointer to data segment|Working directory|
|Program status word|Pointer to stack segment|File descriptors|
|Stack pointer||User ID|
|Process state||Group ID|
|Priority|||
|Scheduling parameters|||
|Process ID|||
|Parent process|||
|Process group|||
|Signals|||
|Time when process started|||
|CPU time used|||
|Children's CPU time|||
|Time of next alarm|||

---

### 4. Process States & Transitions

**States:** Created → Ready → Running → Blocked → (back to Ready)

|Transition|Cause|
|---|---|
|Created → Ready|Process just created, inserted in ready queue|
|Ready → Running|Scheduler picks this process from the ready queue|
|Running → Blocked|Process makes a blocking system call (e.g. I/O request via `read()`, `write()`)|
|Running → Ready|Timer interrupt fires (quantum expired in round-robin)|
|Blocked → Ready|The event the process was waiting for completes (e.g. I/O done → interrupt fires → ISR moves process back to ready queue)|

Key point: a process going from Blocked → Ready does **not** immediately run. It waits in the ready queue for the scheduler.

---

### 5. Multi-Programming & Why It Matters

**Multi-programming** = loading multiple programs in memory and switching among them so the CPU and I/O devices stay busy.

**Three types of tasks (know the examples from the textbook):**

- **I/O-bound:** Spends most time doing I/O (e.g. Hello World printing a million times). CPU mostly idle.
- **CPU-bound:** Spends most time computing (e.g. `while(1);` infinite loop). I/O devices idle.
- **Interactive:** Waits for user input, computes, outputs result (e.g. `getchar()` program). Response time matters most.

**Why mix them?** If you only run CPU-bound jobs, all I/O devices sit idle. If you only run I/O-bound jobs, the CPU sits idle. Mixing all three types keeps every part of the system utilized. This is the core motivation for multi-programming.

**Batch processing** = run one program to completion before starting the next. Inefficient — like a student refusing to start homework #2 while waiting on a library book for homework #1.

---

### 6. Context Switching — Detailed Steps

A context switch has overhead but happens fast enough that humans perceive simultaneous execution.

**Detailed steps (from textbook + slides):**

1. Currently running process P1 gives up the CPU (I/O call, timer interrupt, etc.). CPU transitions to OS code.
2. **Hardware** saves P1's PC value to a known location.
3. OS saves the rest of P1's CPU register contents into **P1's PCB**.
4. OS performs bookkeeping for P1:
    - If P1 made an I/O call → insert P1 into the **I/O wait queue** (blocked state).
    - If P1's quantum expired → insert P1 at the back of the **ready queue**.
5. OS calls the **scheduler**. Scheduler picks the next process P2 from the ready queue.
6. P2's register values (including PC) are loaded from **P2's PCB** into the physical CPU registers.
7. P2 starts running from exactly where it left off.

**From the slides — skeleton of what happens at the lowest level when an interrupt occurs:**

1. Hardware stacks program counter, etc.
2. Hardware loads new program counter from interrupt vector.
3. Assembly language procedure saves registers (→ to P1's PCB).
4. Assembly language procedure sets up new stack.
5. C interrupt service runs (typically reads and buffers input).
6. Scheduler decides which process to run next.
7. C procedure returns to the assembly code.
8. Assembly language procedure starts up new current process.

---

### 7. fork(), exec(), waitpid(), exit() — The Big Four

#### fork()

- Creates a **child process** that is an **exact copy** of the parent (same address space content, same register values, same PC).
- Returns the **child's PID** to the parent.
- Returns **0** to the child.
- The child starts executing from the **same line** as the parent (the line containing `fork()`), because the PC was copied.
- **Implementation in OS:** (1) create a child process identical to parent; (2) insert child in ready queue; (3) return child PID to parent via a CPU register; (4) when child eventually runs and calls fork(), return 0.

#### exec()

- **Replaces** the calling process's entire **core image** (address space + CPU context) with a new program.
- After `execvp("ls", argv)`, the process _becomes_ an instance of `ls`.
- The old program is gone — exec does not return (unless it fails).

#### waitpid(pid, &status, 0)

- **Blocks** the calling process in the **waitpid queue** until the process with the given PID terminates.
- If the child already finished before `waitpid()` is called, the parent passes through without blocking.

#### exit()

- Terminates the process. Releases all resources (memory, file pointers, etc.).
- Even if the programmer doesn't write `exit()`, the **compiler** inserts it at the appropriate places.

#### Classic pattern — trace this carefully:

```c
pid = fork();
if (pid == 0) {              // CHILD runs this
    static char *argv[] = {"ls", "-a", NULL};
    execvp("ls", argv);      // child becomes "ls"
}
else {                        // PARENT runs this
    waitpid(pid, &status, 0); // parent waits for child
    printf("I am the parent!\n");
}
// exit() is called implicitly at the end
```

**Execution flow:** Parent calls fork() → child is created and put in ready queue → parent continues to `waitpid()` and blocks → child runs, exec replaces it with `ls` → `ls` finishes → `exit()` is called → parent is unblocked from waitpid queue → parent prints message.

**Important subtlety:** Due to nondeterministic scheduling, the child may finish before the parent even reaches `waitpid()`. In that case, the parent just passes through without blocking.

#### The init process

- Root of the Unix process tree. Created at boot time.
- All other processes are descendants of init (created via fork).
- init uses fork/exec/waitpid to create daemon processes (e.g. SSH server, web server).
- Daemon processes run in the background serving system/user needs.
- Except for init, every process has exactly one parent.

---

### 8. Threads

**Thread** = a lightweight unit of execution within a process. A process traditionally had exactly one thread.

**What threads share (within the same process):** code, data, files, address space. **What each thread has its own:** registers, program counter, stack, stack pointer.

**Single-threaded process:** [code | data | files] + one set of [registers | stack] **Multi-threaded process:** [code | data | files] shared + each thread has its own [registers | stack]

#### Why threads? (Three benefits from the textbook)

**1. Parallelism within a process:** In round-robin scheduling, if a single-threaded process makes an I/O call halfway through its quantum, the whole process blocks — wasting the remaining quantum. With multiple threads, only the thread that made the I/O call blocks. Another thread within the same process can keep running, using the remaining quantum time productively.

**2. Cheaper context switches:** Switching between threads _within the same process_ is much faster than switching between two different processes, because you don't need to swap the entire address space — only the thread's registers and stack. More time spent running application code, less time in OS switching code.

**3. Natural problem decomposition:** Some problems naturally decompose into concurrent sub-tasks. A web server spawning a worker thread per request. A robot with separate threads for sensor I/O and flight control. Thinking in threads is conceptually simpler than managing multiple processes.

#### The Web Server Example (know both versions)

**Single-threaded web server:**

```
Webserver() {
  While (true) {
    request = listen_to_port();
    if (request_is_in_cache())
      return request.content;
    else {
      make_disk_read(request);  // BLOCKS here
      return request.content;
    }
  }
}
```

Problem: While blocked on disk read, the server can't accept new incoming requests. Performance bottlenecked by disk speed.

**Multi-threaded web server:**

```
Webserver() {
  While (true) {
    request = listen_to_port();
    Create_Thread(request);     // worker handles it
  }
}
```

The main (dispatcher) thread never blocks — it just listens and spawns workers. Each worker thread handles cache check / disk read independently. If one worker blocks on disk, other workers and the dispatcher keep running.

**From slides:** The architecture is: dispatcher thread → spawns worker threads → workers access web page cache (in user space) → kernel handles network connection.

#### Blocking vs. Non-Blocking System Calls

- **Blocking:** The calling process/thread _waits_ until the operation is complete. Example: `read()`, `write()`. The process gives up the CPU.
- **Non-blocking:** Returns immediately. The process continues running while the OS serves the call in the background. Example: the `select()` system call.

#### Kernel-Level vs. User-Level Threads

**Kernel-level threads:**

- OS (kernel) knows about and manages the threads.
- Scheduler can switch from a thread in Process A to a thread in Process B.
- Possible scheduling: A1, B1, A2, B2, A3, B3 — threads from different processes can interleave, leading to fewer full process switches.

**User-level threads:**

- Threads are completely hidden from the OS. Managed by a user-space library.
- Faster context switching between threads (no kernel code needed).
- Can work on OSes that don't natively support threads.
- Each process can have its own custom thread scheduling.
- **Drawbacks:** Blocking system calls block the _entire process_ (all threads), since the kernel only sees one process. No preemption among threads (no clock interrupt at thread level). Kernel can't schedule threads across processes.

**Hybrid implementation:** Multiple user-level threads multiplexed onto kernel-level threads. Combines advantages of both.

#### Thread Systems

- **POSIX threads (pthreads):** Standard thread library for Unix/Linux. Used with C.
- **Java threads:** Managed by the JVM. Created by extending `Thread` class or implementing `Runnable`. `synchronized` keyword for mutual exclusion. A JVM is a process from the host OS's perspective; Java programs within it are threads.
- **Linux threads:** Kernel-level, POSIX-compliant.

#### Key Exam Detail: Thread Data Structure

A thread minimally needs: **thread ID, program counter, registers, stack pointer, state**. Without a stack pointer, a thread system would lose the ability to manage separate subroutine call chains per thread.

---

### 9. Scheduling Algorithms

#### Round-Robin

- Each process gets a fixed **quantum** (e.g. 3ms).
- Process runs until: (a) quantum expires → timer interrupt → process goes to back of ready queue, or (b) process makes a blocking system call → goes to I/O wait queue before quantum is up.
- Fair — no process starves. Simple to implement.
- Context-switching overhead exists (e.g. ~1ms per switch).

**Trace example from textbook:** P1 runs 0–3ms (full quantum) → 1ms context switch → P2 runs 4–6ms (makes `read()` at 6ms, blocked early) → context switch → P3 runs, etc.

#### FIFO (First-In-First-Out)

- Run each process to completion before starting the next. Pure batch processing.
- No preemption. Simple, but inefficient for interactive or mixed workloads.

#### Priority-Based

- Scheduler always picks the highest-priority process from the ready queue.
- Risk: **starvation** — low-priority processes never get CPU time if higher-priority ones keep arriving.

#### Multi-Level Priority Queues

- Multiple ready queues at different priority levels.
- Addresses starvation by adjusting priorities over time (e.g. aging — increase priority of long-waiting processes).

#### Preemptive vs. Non-Preemptive

- **Preemptive** (e.g. round-robin): OS can forcibly stop a running process (via timer interrupt).
- **Non-preemptive** (e.g. pure FIFO): process runs until it voluntarily yields, blocks, or terminates.

#### Special Systems

- **Batch systems:** Throughput matters most. FIFO or similar.
- **Real-time (hard):** Processes have strict deadlines (e.g. autopilot landing gear). Missed deadline = catastrophic. Use redundant systems rather than clever scheduling.
- **Real-time (soft):** Deadlines matter but missing them isn't catastrophic (e.g. multimedia frame rendering). Many innovative scheduling algorithms exist for these.

---

---

## PART B: SYSTEM CALLS

---

### 10. What Are System Calls?

A **system call** is how a user program requests a service from the OS that requires privileged access. When a program calls `read()`, `write()`, `fork()`, etc., a system call is made that transitions the CPU from **user mode → kernel (privileged) mode**.

**User mode:** CPU running a user application. Restricted hardware access. **Privileged/Kernel mode:** CPU running OS code. Full access to hardware and system resources.

**Three ways to transition user mode → kernel mode:**

|Mechanism|Trigger|Intentional?|Example|
|---|---|---|---|
|**System call**|Program explicitly requests OS service|Yes (programmer intended it)|`read()`, `write()`, `fork()`, `exec()`, `waitpid()`, `exit()`|
|**Trap (exception)**|Error during program execution|No (accidental)|Division by zero, invalid memory access (segfault)|
|**Interrupt**|External hardware device signals the CPU|No (external event)|Disk controller done, keyboard stroke, timer tick|

**Traps:** CPU encounters an error → jumps to the OS exception handler → OS usually kills the offending process.

**Interrupts:** External device (hard disk, keyboard, timer) sends a signal to the CPU's interrupt pin → CPU stops current execution → looks up the interrupt type in the **interrupt vector table** → jumps to the corresponding **interrupt service routine (ISR)** in the OS → after ISR, the scheduler may pick the same or a different process to run.

**System calls:** The programmer _intentionally_ invokes them. For example, `printf()` eventually triggers a system call. OS runs the appropriate routine in kernel mode, then returns control to user mode.

#### Process Control System Calls (from this course)

- `fork()` — create a child process
- `exec()` — replace process core image with a new program
- `waitpid()` — block until a specific process terminates
- `exit()` — terminate and release resources
- `yield()` — voluntarily give up CPU, go to ready queue
- `sleep()` — block the process for a specified time

---

---

## PART C: I/O INTERRUPTS AND I/O METHODS

---

### 11. I/O Architecture Basics

Every I/O device has an **I/O controller** (hardware) with at least three registers:

- **Command register:** Stores the command (e.g. "read from disk address m").
- **Data register:** Holds data being transferred.
- **Status register:** Indicates whether the device is busy/done.

Each I/O device also comes with a **device driver** (software), written by the hardware manufacturer. The stack is: I/O device (HW) → controller (HW) → device driver (SW) → OS (SW) → application programs.

---

### 12. Three I/O Methods (in order of sophistication)

#### Programmed I/O

- CPU handles **every step** of the I/O.
- OS runs a subroutine that sends one character at a time to the device's data register, polls the status register, waits for completion — repeat.
- CPU is **completely tied up** during the entire I/O. No other process can run.
- Pseudocode:

```
programmed_io(char[] data_output) {
  for (i = 0; i < length(data_output); i++) {
    copy_char_to_data_register(data_output[i]);
    set_up_other_registers();
    wait_for_io_done();    // CPU busy-waits here!
  }
}
```

#### Interrupt-Driven I/O

- After the I/O request is made, OS **blocks** the requesting process (P1) and puts it in the **I/O wait queue**.
- The **scheduler** runs another process (P2) on the CPU while the I/O device works independently.
- When the I/O completes, the device's controller raises an **interrupt** to the CPU.
- CPU runs the **interrupt service routine (ISR)**, which moves P1 from the I/O wait queue back to the **ready queue**.
- P1 does NOT immediately run — it waits for the scheduler to pick it.
- **Limitation:** After a `read()`, data arrives in the OS memory area first. The CPU must still **copy the data** from the OS buffer to the user process's address space. This copy still uses CPU time.

#### DMA (Direct Memory Access) I/O

- Same as interrupt-driven, PLUS a **DMA controller** (dedicated hardware) handles the data transfer.
- CPU just **programs the DMA controller** (writes address, count, and control to the DMA's registers), then is completely free.
- DMA controller transfers data directly between the I/O device and memory **without CPU involvement**.
- DMA **still uses interrupts** — it interrupts the CPU when the transfer is complete.
- **Key difference from interrupt-driven:** The data copy to the user's address space is done by DMA hardware, NOT the CPU.

#### Summary Table

||Programmed I/O|Interrupt-Driven I/O|DMA I/O|
|---|---|---|---|
|CPU during I/O|Busy (polling)|Free (runs other processes)|Free (runs other processes)|
|Data transfer|CPU does it|CPU copies from OS buffer to user space|DMA hardware does it|
|Uses interrupts?|No|Yes|Yes|
|CPU freed most?|No|Partially|Yes|

---

### 13. The Full Disk I/O Sequence (Interrupt + DMA) — From Slides

**This is a key sequence — know it step by step:**

1. A user process **P1** requests a disk I/O via a **system call** (e.g. `read()`).
2. **OS runs:**
    - Inserts P1 into the **I/O wait queue** (P1 is now blocked).
    - Calls the **disk device driver** subroutine.
3. Device driver **programs** the disk controller (or DMA controller) — i.e., writes proper values to the controller's registers (address, count, control). This causes the disk hardware to start operating.
4. **Scheduler subroutine** in OS runs: picks a ready process **P2** from the ready queue, performs context switch to P2.
5. **P2 runs** on the CPU. (Note: P1's I/O may not be done yet.)
6. When **P1's I/O is done**, an interrupt is raised by the disk controller or DMA controller.
    - The **disk interrupt handler** (ISR) in OS runs:
        - If interrupt-driven (no DMA): copies data from disk buffer to P1's address space.
        - If DMA: data has **already been copied** by the DMA hardware.
        - Inserts P1 back into the **ready queue**.

**After step 6:** P2 resumes where it left off (it was interrupted). P1 is now in the ready queue waiting for its turn.

**Key slide note:** "For DMA I/O, the copying of data has already been done by the DMA hardware."

---

### 14. Timer & Timer Interrupts

A **timer** is a hardware device connected to the CPU's interrupt pin. It generates an interrupt signal at a designated time interval.

**Role in scheduling:** In round-robin, the timer fires after each quantum expires. The timer ISR calls the scheduler, which saves the current process's state, puts it back in the ready queue, and picks the next process.

**The timer interrupt pin is shared** with other interrupt-generating devices (disk controllers, keyboard controllers, etc.). When the CPU receives an interrupt, it must determine _which_ device caused it and run the appropriate ISR.

---

### 15. Interrupt Vector Table

When an interrupt fires, the CPU needs to know which ISR to jump to. The **interrupt vector table** maps device IDs to ISR addresses:

|Index|Device|ISR Address|
|---|---|---|
|0|Keyboard|→ Keyboard ISR in OS|
|1|Disk|→ Disk ISR in OS|
|2|Network|→ Network ISR in OS|
|...|...|...|

The hardware loads the new PC value from this table so the CPU starts executing the correct handler.

---

### 16. Tying It All Together — How Everything Connects

The three topics are deeply intertwined. Here's how they relate:

**A process makes an I/O system call** → triggers transition to kernel mode → OS runs → uses one of the three I/O methods → if interrupt-driven or DMA, the process is blocked → scheduler context-switches to another process → when I/O completes, an interrupt fires → ISR puts the original process back in the ready queue → scheduler eventually picks it up.

**A timer interrupt fires** → current process is preempted → context switch → scheduler picks next process from ready queue (this is round-robin scheduling).

**A trap occurs** → CPU transitions to kernel mode → OS exception handler runs → usually kills the process → scheduler picks the next process.

**Threads interact with I/O:** In a multi-threaded process, only the thread that made the blocking I/O call gets blocked. Other threads can continue running, making better use of the quantum. This is the core advantage of threads over single-threaded processes for I/O-heavy workloads like web servers.