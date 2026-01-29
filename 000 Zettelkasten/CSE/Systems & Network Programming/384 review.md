# Additional Practice Problems - Focused Review

Here are additional problems targeting the concepts you missed:

---

## Buffered vs Unbuffered I/O

### Problem 41 [5 points]
Which of the following are unbuffered I/O system calls? Choose all that apply.
- **A. `open()`**
- B. `fprintf()`
- **C. `read()`**
- D. `fwrite()`
- **E. `lseek()`**
- F. `fclose()`

### Problem 42 [5 points]
You need to write a program that reads exactly 512 bytes from a specific offset in a file for maximum performance. Which approach should you use?
- A. Standard I/O with fseek() and fread()
- B. Unbuffered I/O with lseek() and read()
- **C. Either approach works equally well**
- D. Standard I/O is always faster

### Problem 43 [10 points]
**Short Answer**: Explain why Standard I/O (buffered) is generally more efficient than unbuffered I/O for text file processing, but unbuffered I/O might be preferred for network programming.

**Answer:**
_______________________________________________________________________________
I don't know and that seems to be out of the scope of this class unless it is referenced specifically
_______________________________________________________________________________

_______________________________________________________________________________

### Problem 44 [5 points]
Which header files correspond to unbuffered vs buffered I/O?
- **A. Unbuffered: `<unistd.h>`, Buffered: `<stdio.h>`**
- B. Unbuffered: `<stdio.h>`, Buffered: `<unistd.h>`
- C. Both use `<stdio.h>`
- D. Both use `<unistd.h>`

---

## Fork Return Values and Process Counting

### Problem 45 [10 points]
**Code Analysis**: What will this code print and how many times?
```c
int x = 10;
pid_t pid = fork();

if (pid > 0) {
    x = 20;
    printf("A: x = %d\n", x);
} else if (pid == 0) {
    x = 30;
    printf("B: x = %d\n", x);
} else {
    printf("Fork failed\n");
}
```
- **A. "A: x = 20" once, "B: x = 30" once**
- B. "A: x = 20" twice
- C. "B: x = 30" twice
- D. "A: x = 20" once, "B: x = 20" once

### Problem 46 [10 points]
How many processes are created by this code (including the original)?
```c
if (fork() == 0) {
    fork();
}
fork();
```
- A. 4
- B. 5
- **C. 6**
- D. 8

### Problem 47 [15 points]
**Code Tracing**: Draw the process tree and determine how many times "Hello" is printed:
```c
fork();
if (fork() == 0) {
    printf("Hello\n");
}
```

**Answer:**
```
Process tree:
ignored on purpose

Total "Hello" prints: _____
```

### Problem 48 [10 points]
What is the purpose of checking the return value of fork()?
```c
pid_t pid = fork();
if (pid < 0) {
    // Why do we check this?
}
```
- **A. To detect if fork() failed**
- B. To identify the child process
- C. To identify the parent process
- D. To count how many processes were created

### Problem 49 [15 points]
**Short Answer**: In the following code, what value of `pid` does the parent see, and what value does the child see? If the child's actual PID is 5432, explain what gets printed by each process.
```c
pid_t pid = fork();
printf("pid = %d, my PID = %d\n", pid, getpid());
```

**Answer:**
_______________________________________________________________________________
skipped
_______________________________________________________________________________

_______________________________________________________________________________

---

## Signals (SIGINT, SIGKILL, SIGALRM)

### Problem 50 [5 points]
Which signal is sent by the command `kill -9 1234`?
- A. SIGINT
- B. SIGTERM
- **C. SIGKILL**
- D. SIGALRM

### Problem 51 [5 points]
A program has installed a handler for SIGINT. What happens when the user presses CTRL-C?
- A. The program terminates immediately
- B. The signal handler runs, then program continues
- C. The signal is ignored
- **D. The program terminates after the handler runs**

### Problem 52 [10 points]
**Code Analysis**: What happens when this program runs for 3 seconds?
```c
void handler(int sig) {
    printf("Alarm!\n");
}

int main() {
    signal(SIGALRM, handler);
    alarm(3);
    
    while (1) {
        printf("Working...\n");
        sleep(1);
    }
}
```
- A. Program terminates after 3 seconds
- **B. "Alarm!" prints after 3 seconds, program continues**
- C. "Alarm!" prints after 3 seconds, program terminates
- D. Program runs forever without "Alarm!" printing

### Problem 53 [10 points]
Why can't SIGKILL be caught by a signal handler?
- A. It's a kernel limitation
- **B. By design, to ensure processes can always be killed**
- C. It's too fast to catch
- D. It requires root privileges

### Problem 54 [15 points]
**Code Writing**: Write the signal handler and setup code for a program that counts how many times the user presses CTRL-C, and only exits after 3 presses.

**Answer:**
```c
// Your code here:

void handler(int sig) {
	im confused
}
```

### Problem 55 [10 points]
What's the difference between these two signals?
```c
kill(pid, SIGTERM);  // Signal A
kill(pid, SIGKILL);  // Signal B
```
- **A. SIGTERM can be caught, SIGKILL cannot**
- B. SIGKILL can be caught, SIGTERM cannot
- C. Both can be caught
- D. Neither can be caught

### Problem 56 [10 points]
**Short Answer**: Explain the difference between `alarm()` and `sleep()`. When would you use each?

**Answer:**
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

---

## Socket Programming (Blocking, Order, Client vs Server)

### Problem 57 [5 points]
Why doesn't the client call `bind()`?
- A. Clients don't need specific ports
- B. The OS automatically assigns a port to the client
- C. bind() is only for servers
- D. All of the above

### Problem 58 [10 points]
**Code Analysis**: What's wrong with this server code?
```c
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
listen(sockfd, 5);
bind(sockfd, (struct sockaddr*)&addr, sizeof(addr));
int conn = accept(sockfd, NULL, NULL);
```
- A. listen() should come after accept()
- B. bind() should come before listen()
- C. socket() parameters are wrong
- D. accept() parameters are wrong

### Problem 59 [5 points]
What happens when `accept()` is called and no clients are trying to connect?
- A. Returns immediately with -1
- B. Returns immediately with 0
- C. Blocks (waits) until a client connects
- D. Raises SIGINT

### Problem 60 [10 points]
**Short Answer**: You call `write()` on a socket to send 1MB of data. The function returns immediately. Does this mean the data has been received by the remote computer? Explain.

**Answer:**
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

### Problem 61 [15 points]
**Code Ordering**: Fix the order of operations in this server code:
```c
// Current (wrong) order:
int conn_fd = accept(listen_fd, NULL, NULL);
int listen_fd = socket(AF_INET, SOCK_STREAM, 0);
listen(listen_fd, 5);
bind(listen_fd, (struct sockaddr*)&addr, sizeof(addr));
```

**Correct order:**
```c
// Line 1:

// Line 2:

// Line 3:

// Line 4:
```

### Problem 62 [10 points]
Which of these operations typically takes the longest time to complete?
- A. `socket()`
- B. `bind()`
- C. `listen()`
- D. `accept()`

### Problem 63 [15 points]
**Scenario**: You're writing a chat server that must handle 100 simultaneous clients. Compare these two approaches:

**Approach A**: Single process server (one accept loop)
**Approach B**: Multiprocess server (fork for each client)

Which is better and why?

**Answer:**
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

### Problem 64 [10 points]
In a multiprocess server, why does the parent close `conn_fd` and the child close `listen_fd`?
```c
int conn_fd = accept(listen_fd, ...);
if (fork() == 0) {
    close(listen_fd);  // Why?
    // handle client
} else {
    close(conn_fd);    // Why?
}
```

**Answer:**
_______________________________________________________________________________

_______________________________________________________________________________

### Problem 65 [5 points]
What must you do to port numbers before using them in network code?
- A. Convert to network byte order with htons()
- B. Convert to host byte order with ntohs()
- C. Add 1000 to them
- D. Nothing, they work as-is

### Problem 66 [10 points]
**True or False with Explanation**: 

"In a multiprocess server, if the parent process terminates, all child processes automatically terminate too."

**Answer:** _______________

**Explanation:**
_______________________________________________________________________________

_______________________________________________________________________________

---

## Mixed Concepts

### Problem 67 [15 points]
**Comprehensive Scenario**: You're building a multiprocess web server. For each client connection, you fork a child process. The child needs to handle the request and potentially write to a log file. 

Answer these questions:
1. Should the log file use buffered or unbuffered I/O? Why?
2. What happens if a child process crashes? Does it affect other clients?
3. What signal should you catch to implement graceful shutdown?

**Answers:**

1. _______________________________________________________________________________

2. _______________________________________________________________________________

3. _______________________________________________________________________________

### Problem 68 [15 points]
**Code Analysis**: Find and explain ALL the bugs in this code:
```c
int main() {
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);
    
    struct sockaddr_in addr;
    addr.sin_family = AF_INET;
    addr.sin_port = 8080;  // Bug 1?
    addr.sin_addr.s_addr = INADDR_ANY;
    
    bind(sockfd, (struct sockaddr*)&addr, sizeof(addr));
    accept(sockfd, NULL, NULL);  // Bug 2?
    
    char buffer[100];
    read(sockfd, buffer, 100);  // Bug 3?
    printf("%s\n", buffer);
}
```

**Bugs found:**

1. _______________________________________________________________________________

2. _______________________________________________________________________________

3. _______________________________________________________________________________

### Problem 69 [10 points]
**Code Completion**: Fill in the blanks to create a proper signal handler for SIGALRM:
```c
void alarm_handler(int sig) {
    printf("Time's up!\n");
    _____________;  // What should go here to terminate?
}

int main() {
    _____________(SIGALRM, alarm_handler);  // Install handler
    _____________(5);  // Set 5 second alarm
    
    while(1) {
        // Do work
    }
}
```

### Problem 70 [20 points]
**Comprehensive Problem**: Write a complete multiprocess server that:
1. Listens on port 9000
2. For each client, forks a child
3. Child reads a number from client, doubles it, sends it back
4. Parent catches SIGINT (CTRL-C) to shutdown gracefully

**Skeleton provided - fill in the blanks:**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <signal.h>
#include <sys/socket.h>
#include <netinet/in.h>

volatile int keep_running = 1;

void sigint_handler(int sig) {
    keep_running = 0;
}

int main() {
    // 1. Create socket
    int listen_fd = ______________________________________________;
    
    // 2. Setup address
    struct sockaddr_in addr;
    memset(&addr, 0, sizeof(addr));
    addr.sin_family = AF_INET;
    addr.sin_port = ______________;  // Port 9000
    addr.sin_addr.s_addr = INADDR_ANY;
    
    // 3. Bind
    ______________________________________________;
    
    // 4. Listen
    ______________________________________________;
    
    // 5. Install signal handler
    signal(_____________, sigint_handler);
    
    printf("Server listening on port 9000...\n");
    
    while (keep_running) {
        // 6. Accept client
        int conn_fd = ______________________________________________;
        if (conn_fd < 0) continue;
        
        // 7. Fork child
        pid_t pid = fork();
        if (pid == 0) {
            // CHILD
            close(_____________);  // Don't need this
            
            int num;
            read(conn_fd, &num, sizeof(num));
            num = num * 2;
            write(conn_fd, &num, sizeof(num));
            
            close(conn_fd);
            exit(0);
        } else {
            // PARENT
            close(_____________);  // Don't need this
        }
    }
    
    printf("Server shutting down...\n");
    close(listen_fd);
    return 0;
}
```

---

## Answer Key for Additional Problems

### Buffered vs Unbuffered I/O
- **41:** A, C, E
- **42:** B
- **43:** Standard I/O buffers multiple small operations into fewer system calls, reducing overhead for text processing. Unbuffered I/O gives precise control over when data is sent/received, which is crucial for network protocols and real-time communication.
- **44:** A

### Fork Return Values
- **45:** A (parent prints x=20, child prints x=30)
- **46:** C (6 processes total)
- **47:** 2 "Hello" prints
- **48:** A
- **49:** Parent sees 5432 (child's PID), child sees 0. Parent prints "pid = 5432, my PID = [parent's PID]", child prints "pid = 0, my PID = 5432"

### Signals
- **50:** C
- **51:** B
- **52:** B
- **53:** B
- **54:** See detailed solution below
- **55:** A
- **56:** alarm() schedules a future signal without blocking; sleep() blocks execution. Use alarm() for timeouts while doing work, sleep() to deliberately pause.

### Socket Programming
- **57:** D
- **58:** B
- **59:** C
- **60:** No, it only means data was copied to kernel's send buffer, not yet transmitted or received
- **61:** socket() → bind() → listen() → accept()
- **62:** D (accept blocks waiting for clients)
- **63:** Approach B is better - allows simultaneous handling of clients
- **64:** Each process should close descriptors it doesn't use to avoid resource leaks
- **65:** A
- **66:** False - child processes continue running (become orphans, adopted by init)

### Mixed Concepts
- **67:** (1) Unbuffered for immediate writes and avoiding buffer issues with multiple processes (2) Other children unaffected - processes are isolated (3) SIGINT for graceful shutdown
- **68:** (1) Need htons(8080) (2) Need listen() before accept() (3) Using wrong file descriptor - should use return value from accept()
- **69:** exit(0); signal; alarm
- **70:** See detailed solution below

---

## Detailed Solutions for Complex Problems

### Problem 54 - SIGINT Counter
```c
#include <stdio.h>
#include <signal.h>
#include <stdlib.h>

volatile int count = 0;

void sigint_handler(int sig) {
    count++;
    printf("CTRL-C pressed %d time(s)\n", count);
    
    if (count >= 3) {
        printf("Exiting after 3 presses\n");
        exit(0);
    }
}

int main() {
    signal(SIGINT, sigint_handler);
    
    printf("Press CTRL-C three times to exit\n");
    
    while(1) {
        // Do work
    }
    
    return 0;
}
```

### Problem 70 - Complete Server Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <signal.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>

volatile int keep_running = 1;

void sigint_handler(int sig) {
    keep_running = 0;
}

int main() {
    // 1. Create socket
    int listen_fd = socket(AF_INET, SOCK_STREAM, 0);
    
    // 2. Setup address
    struct sockaddr_in addr;
    memset(&addr, 0, sizeof(addr));
    addr.sin_family = AF_INET;
    addr.sin_port = htons(9000);  // Port 9000
    addr.sin_addr.s_addr = INADDR_ANY;
    
    // 3. Bind
    bind(listen_fd, (struct sockaddr*)&addr, sizeof(addr));
    
    // 4. Listen
    listen(listen_fd, 5);
    
    // 5. Install signal handler
    signal(SIGINT, sigint_handler);
    
    printf("Server listening on port 9000...\n");
    
    while (keep_running) {
        // 6. Accept client
        int conn_fd = accept(listen_fd, NULL, NULL);
        if (conn_fd < 0) continue;
        
        // 7. Fork child
        pid_t pid = fork();
        if (pid == 0) {
            // CHILD
            close(listen_fd);  // Don't need listening socket
            
            int num;
            read(conn_fd, &num, sizeof(num));
            num = num * 2;
            write(conn_fd, &num, sizeof(num));
            
            close(conn_fd);
            exit(0);
        } else {
            // PARENT
            close(conn_fd);  // Don't need connection socket
        }
    }
    
    printf("Server shutting down...\n");
    close(listen_fd);
    return 0;
}
```

---

## Study Tips for These Topics

### Buffered vs Unbuffered I/O
- **Key distinction**: 'f' prefix functions (fopen, fgets, fprintf) = buffered
- **Remember**: Unbuffered = direct system calls, Buffered = library wrapper
- **Practice**: Identify which header file each function needs

### Fork Return Values
- **Memorize**: Parent gets child PID, child gets 0, error gets -1
- **Draw it out**: Always draw process trees for fork problems
- **Formula**: n sequential forks = 2^n processes

### Signals
- **Know the big 3**: SIGINT (Ctrl-C, catchable), SIGKILL (force kill, uncatchable), SIGALRM (alarm timer)
- **Handler behavior**: Returns to program unless it calls exit()
- **Common mistake**: Confusing alarm() (sets timer) with sleep() (blocks)

### Socket Programming
- **Server sequence**: socket → bind → listen → accept (S-B-L-A)
- **Client sequence**: socket → connect (S-C)
- **Remember**: Clients don't bind, servers must bind
- **Blocking**: accept() and read() block, write() doesn't

### Multiprocess Servers
- **Parent role**: Accept loop only
- **Child role**: Handle one client, then exit
- **Resource management**: Always close unused file descriptors

Good luck with your continued studying! These problems should help reinforce the concepts you missed.