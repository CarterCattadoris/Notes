# CSE 384: Systems and Network Programming - Final Exam Practice Problems

Based on the course material and professor's guidance, here are practice problems covering all topics:

---

## UNIX File I/O (Unbuffered + Standard I/O)

### Problem 1 [5 points]
Which system call is used to create a file with empty space (sparse file)?
- A. `open()` with `O_CREAT` flag
- **B**. `lseek()` with a large offset
- C. `write()` with null bytes
- D. `fseek()` with `SEEK_END`

### Problem 2 [5 points]
What are the standard file descriptors? Choose all that apply.
- **A. FD 0 = stdin**
- **B. FD 1 = stdout**
- **C. FD 2 = stderr**
- D. FD 3 = stdlog

### Problem 3 [5 points]
Which flag for `open()` ensures that writes always append to the end of the file atomically?
- A. `O_TRUNC`
- **B. `O_APPEND`**
- C. `SEEK_END`
- D. `O_WRONLY`

### Problem 4 [5 points]
What is the difference between `r+` and `w+` modes in `fopen()`?
- **A**. `r+` requires file to exist, `w+` truncates or creates
- B. `r+` is read-only, `w+` is write-only
- C. `r+` appends, `w+` overwrites
- D. No difference

### Problem 5 [5 points]
Which of the following uses buffered I/O? Choose all that apply.
- **A**. `read()`
- B. `fgets()`
- **C**. `write()`
- D. `fprintf()`
- **E.** `lseek()`

### Problem 6 [10 points]
**Short Answer**: Explain what happens when you create a sparse file using `lseek()` to seek 1GB past the end of an empty file, then write one byte. How does the file size differ from the actual disk space used?

**Answer:**
_______________________________________________________________________________
The file size will be 1 GB but it only uses a small amount of disk space due to there being a lot of whitespace
_______________________________________________________________________________

_______________________________________________________________________________

### Problem 7 [5 points]
What information can be retrieved using `stat()` or `fstat()`? Choose all that apply.
- **A. File size**
- **B. File permissions**
- **C. File type (regular, directory, socket, etc.)**
- D. File contents
- **E. Owner UID/GID**

### Problem 8 [5 points]
Which file types can be identified using `stat()`? Choose all that apply.
- **A. Regular file**
- **B. Directory**
- **C. Socket**
- **D. FIFO (named pipe)**
- E. Symbolic link
- F. Compressed file

---

## Processes, Signals, Fork, Wait

### Problem 9 [10 points]
**Code Analysis**: How many total processes are created by the following code (including the original parent)?
```c
fork();
fork();
fork();
```
- A. 3
- B. 4
- C. 6
- **D. 8**
Isnt there 15? 1 -> 2 (first fork) -> 4 (second fork) -> 8 (third fork)

### Problem 10 [5 points]
What is the return value of `fork()` in the child process?
- A. The child's PID
- B. The parent's PID
- **C. 0**
- D. -1

### Problem 11 [5 points]
What is the return value of `fork()` in the parent process?
- A. The child's PID
- B. The parent's PID
- C. 0
- **D. -1**

### Problem 12 [5 points]
Which Linux commands can be used to view running processes? Choose all that apply.
- **A. `top`**
- **B. `jobs`**
- C. `ps`
- **D. `ps aux`**
- E. `ls -l`

### Problem 13 [5 points]
What does `CTRL-Z` do to a foreground process?
- A. Kills it immediately
- **B. Suspends it and puts it in the background**
- C. Sends SIGINT
- D. Brings it to foreground

### Problem 14 [5 points]
Which signal is sent when you press `CTRL-C`?
- A. SIGTERM
- **B. SIGKILL**
- C. SIGINT
- D. SIGALRM

### Problem 15 [5 points]
Which signal CANNOT be caught or handled by a signal handler?
- A. SIGINT
- B. SIGTERM
- C. SIGKILL (signal -9)
- D. SIGALRM

i dont know

### Problem 16 [5 points]
What system call does a parent use to wait for a child process to terminate?
- A. `fork()`
- **B. `wait()` or `waitpid()`**
- C. `exit()`
- D. `kill()`

### Problem 17 [10 points]
**Short Answer**: Explain what happens after a signal handler function executes. Does the program terminate or continue execution? Under what circumstances would it terminate?

**Answer:**
_______________________________________________________________________________
It depends on the purpose of the signal handler. If it is just meant to display something when passed a signal it will do that, or it will terminate if you pass it a signal meant to kill it
_______________________________________________________________________________

_______________________________________________________________________________

### Problem 18 [5 points]
What function is used to schedule a SIGALRM signal after a specified number of seconds?
- A. `timer()`
- B. `alarm()`
- **C. `sleep()`**
- D. `signal()`

### Problem 19 [10 points]
**Code Analysis**: Given the following code, which processes will print "Hello"?
```c
pid_t pid = fork();
if (pid == 0) {
    printf("Hello\n");
}
```
- A. Only the parent
- **B. Only the child**
- C. Both parent and child
- D. Neither

---

## Bash Programming & Process Management

### Problem 20 [5 points]
How do you silence stdout (standard output) in bash?
- **A. `command 1> /dev/null`**
- B. `command 2> /dev/null`
- C. `command &> /dev/null`
- D. `command > /dev/null`

### Problem 21 [5 points]
How do you silence stderr (standard error) in bash?
- A. `command 1> /dev/null`
- **B. `command 2> /dev/null`**
- C. `command &> /dev/null`
- D. `command > /dev/null`

### Problem 22 [5 points]
How do you silence both stdout and stderr in bash?
- A. `command 1> /dev/null`
- B. `command 2> /dev/null`
- C. `command &> /dev/null`
- D. `command > /dev/null 2> /dev/null`
- **E. Both C and D**

### Problem 23 [5 points]
Which bash command repeats the last command that started with "ls"?
- **A. `!ls`**
- B. `!!`
- C. `history ls`
- D. `repeat ls`

### Problem 24 [5 points]
Which commands can move a background process to the foreground? Choose all that apply.
- **A. `fg`**
- **B. `fg %1` (where 1 is the job number)**
- C. `bg`
- D. `jobs`

---

## Networking & Sockets

### Problem 25 [5 points]
What file I/O can be used to interact with socket descriptors?
- A. Basic file I/O (read, write, close)
- B. Streaming I/O
- C. Standard I/O (fopen, fread, fwrite)
- D. Formatted I/O
i dont know
### Problem 26 [5 points]
What is stored in `struct sockaddr_in`? Choose all that apply.
- **A. IP address**
- B. A FILE pointer
- **C. Port number**
- D. URL

### Problem 27 [5 points]
What functions does a server call to create a listen socket? Choose all that apply.
- **A. `socket()`**
- B. `bind()`
- C. `connect()`
- **D. `accept()`**
- **E. `listen()`**

### Problem 28 [5 points]
What functions does a client call to create a socket and connect to a server? Choose all that apply.
- **A. `socket()`**
- **B. `bind()**`**
- **C. `connect()`**
- D. `accept()`
- E. `listen()`

### Problem 29 [5 points]
Which of the following functions can be blocking? Choose all that apply.
- A. `socket()`
- **B. `bind()`**
- **C. `connect()`**
- **D. `accept()`**
- **E. `listen()`**
- **F. `read()`**

### Problem 30 [5 points]
What is the behavior of `write()` on a socket?
- **A. Blocking**
- B. Non-blocking
- C. Depends on socket flags
- D. Always fails

### Problem 31 [5 points]
What is the behavior of `read()` on a socket?
- **A. Blocking (waits for data)**
- B. Non-blocking
- C. Depends on socket flags
- D. Always fails

### Problem 32 [5 points]
Which functions convert between host and network byte order? Choose all that apply.
- **A. `htons()`**
- **B. `htonl()`**
- **C. `ntohs()`**
- **D. `ntohl()`**

### Problem 33 [5 points]
What does `htons()` do?
- **A. Host to Network Short (16-bit)**
- B. Host to Network Long (32-bit)
- C. Network to Host Short
- D. Network to Host Long

### Problem 34 [5 points]
Which DNS lookup function converts a hostname (like "www.google.com") to an IP address?
- **A. `gethostbyname()`**
- B. `gethostbyaddr()`
- C. `inet_aton()`
- D. `inet_ntoa()`

### Problem 35 [5 points]
Which function converts an IP address string (like "192.168.1.1") to binary network format?
- **A. `inet_aton()`**
- B. `inet_ntoa()`
- C. `gethostbyname()`
- D. `gethostbyaddr()`

### Problem 36 [10 points]
**Short Answer**: In a multiprocess server, explain the role of the parent process versus the child processes. What does the parent do after forking? What does the child do?

**Answer:**
_______________________________________________________________________________
i dont know
_______________________________________________________________________________

_______________________________________________________________________________

### Problem 37 [10 points]
**Code Analysis**: Put the following server socket operations in the correct order:
1. `bind()`
2. `accept()`
3. `socket()`
4. `listen()`

**Answer:** ____________________ socket, accept, bind, listen

### Problem 38 [10 points]
**Code Analysis**: Put the following client socket operations in the correct order:
1. `connect()`
2. `socket()`
3. `read()`/`write()`

**Answer:** ____________________socket, connect , read/write

---

## Advanced Scenarios

### Problem 39 [15 points]
**Code Tracing**: Trace through the following code and determine what will be printed:
```c
int main() {
    pid_t pid1, pid2;
    
    pid1 = fork();
    if (pid1 == 0) {
        printf("Child1\n");
        exit(0);
    }
    
    pid2 = fork();
    if (pid2 == 0) {
        printf("Child2\n");
        exit(0);
    }
    
    printf("Parent\n");
    wait(NULL);
    wait(NULL);
    return 0;
}
```

**Question**: How many times total will something be printed? What are all the possible outputs?

**Answer:**
_______________________________________________________________________________
5 prints, the children created by the forks will all be exited after printing child1 or child2, and then the parent will print out parent
_______________________________________________________________________________

_______________________________________________________________________________

_______________________________________________________________________________

### Problem 40 [15 points]
**Scenario**: You need to write a program that:
1. Opens a file for reading and writing
2. If the file doesn't exist, creates it
3. If the file exists, doesn't truncate it
4. Allows both reading and writing

Which `fopen()` mode string should you use?
- A. `r+`
- B. `w+`
- **C. `a+`**
- D. `r`
- E. None of the above will work

**Explain your answer:**
_______________________________________________________________________________
a+ will create a file, but not truncate a file if it already exists (it appends). a+ also sets it up for reading and writing  
_______________________________________________________________________________

_______________________________________________________________________________

---

## Answer Key

### Multiple Choice Answers

| Problem | Answer(s) | Problem | Answer(s) | Problem | Answer(s) |
|---------|-----------|---------|-----------|---------|-----------|
| 1       | B         | 15      | C         | 29      | C,D,F     |
| 2       | A,B,C     | 16      | B         | 30      | B         |
| 3       | B         | 18      | B         | 31      | A         |
| 4       | A         | 19      | B         | 32      | A,B,C,D   |
| 5       | B,D       | 20      | A,D       | 33      | A         |
| 7       | A,B,C,E   | 21      | B         | 34      | A         |
| 8       | A,B,C,D,E | 22      | E         | 35      | A         |
| 9       | D         | 23      | A         | 37      | 3,1,4,2   |
| 10      | C         | 24      | A,B       | 38      | 2,1,3     |
| 11      | A         | 25      | A         | 40      | C         |
| 12      | A,B,C,D   | 26      | A,C       |         |           |
| 13      | B         | 27      | A,B,D,E   |         |           |
| 14      | C         | 28      | A,C       |         |           |

### Short Answer Guidance

**Problem 6**: The file will show a size of 1GB + 1 byte using `ls -l`, but `du` (disk usage) will show it only uses one block (typically 4KB) on disk. The space in between is "holes" that aren't actually allocated. `cat` will skip these holes, making it appear the file is only 1 byte.

**Problem 17**: After a signal handler executes, it returns control to the program, which continues from where it was interrupted. The program only terminates if: (1) the handler explicitly calls `exit()`, (2) the handler doesn't catch the signal and the default action is termination, or (3) the signal is SIGKILL which cannot be caught.

**Problem 36**: In a multiprocess server, the **parent process** runs an infinite loop calling `accept()` to wait for new client connections. When a client connects, the parent calls `fork()` to create a child, then immediately returns to `accept()` to wait for the next client. The **child process** handles all communication with the connected client (reading requests, processing, sending responses), then exits when done. This allows multiple clients to be served simultaneously.

**Problem 39**: Three things will be printed total. The outputs are:
- "Child1" (from first child)
- "Child2" (from second child)  
- "Parent" (from original parent)

Order may vary due to process scheduling, but all three will appear exactly once.

**Problem 40**: Answer is **C** (`a+`). The `a+` mode opens for reading and appending. It creates the file if it doesn't exist, doesn't truncate if it does exist, and allows both reading and writing. The file pointer starts at the end for writing, but can be repositioned for reading.

---

## Study Tips

1. **Practice drawing fork trees** to visualize process creation
2. **Trace through code by hand** - especially fork, signal handlers, and socket sequences
3. **Know the difference** between unbuffered (system calls) and buffered (standard I/O)
4. **Memorize standard file descriptors**: 0=stdin, 1=stdout, 2=stderr
5. **Remember socket sequences**: 
   - Server: socket → bind → listen → accept
   - Client: socket → connect
6. **Understand blocking vs non-blocking**: `read()` blocks, `write()` doesn't
7. **Practice byte order conversions**: Always convert to network byte order before sending
8. **Review homework problems** - similar format to exam questions

**Good luck on your final exam!**