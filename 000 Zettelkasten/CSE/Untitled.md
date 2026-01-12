# CSE 384: Systems and Network Programming
## Comprehensive Final Exam Study Guide
### Fall 2025 - Professor Reza Zafarani

---

## Table of Contents
1. [Exam Information](#exam-information)
2. [UNIX File I/O](#unix-file-io)
3. [Processes and Process Management](#processes-and-process-management)
4. [Signals](#signals)
5. [Networking and Sockets](#networking-and-sockets)
6. [Bash Programming](#bash-programming)
7. [C Programming Fundamentals](#c-programming-fundamentals)
8. [Practice Problems](#practice-problems)
9. [Quick Reference Tables](#quick-reference-tables)

---

## Exam Information

### Format
- **Similar to midterm** but with 50% more questions (more time allocated)
- **Comprehensive coverage** - all topics with emphasis on post-midterm material
- More focus on **explaining code** than writing it from scratch
- Function **names and formats will be given** - focus on understanding parameters and behavior
- **Pay attention to footnotes** in slides

### What to Study
- All relevant slides (comprehensive)
- In-class exercises
- Homework assignments (HW #3, #4, #5)
- New topics since midterm:
  - File I/O (Unbuffered and Standard I/O)
  - Processes (fork, wait, exit)
  - Signals
  - Network I/O (Sockets)
- Foundation topics (still tested):
  - Bash Programming
  - C Basics and Pointers

### Key Study Strategy
1. **Master homework problems** - understand every problem thoroughly
2. **Work through in-class exercises** - similar format to exam
3. **Practice code tracing** - be able to follow execution step-by-step
4. **Draw diagrams** - especially for fork trees and client-server interactions
5. **Understand concepts over memorization** - know what functions do, not just syntax

---

## UNIX File I/O

### Overview
Two types of file I/O in UNIX:
1. **Unbuffered I/O** - Direct system calls (kernel level)
2. **Buffered I/O** (Standard I/O) - Library functions with internal buffering

---

### Unbuffered I/O (System Calls)

#### Core System Calls
```c
#include <unistd.h>
#include <fcntl.h>

int open(const char *pathname, int flags, mode_t mode);
ssize_t read(int fd, void *buf, size_t count);
ssize_t write(int fd, const void *buf, size_t count);
off_t lseek(int fd, off_t offset, int whence);
int close(int fd);
```

#### What Each Function Does

**`open()`**
- Opens or creates a file
- Returns a file descriptor (integer) or -1 on error
- File descriptor is used for all subsequent operations
- Flags control the behavior

**`read()`**
- Reads data from file descriptor into buffer
- Returns number of bytes read, 0 at EOF, -1 on error
- Blocking operation - waits for data

**`write()`**
- Writes data from buffer to file descriptor
- Returns number of bytes written, -1 on error
- Non-blocking in most cases

**`lseek()`**
- Changes file offset (position) for reading/writing
- Allows random access within files
- Can create sparse files by seeking beyond end

**`close()`**
- Closes file descriptor
- Releases resources
- Always close files when done!

#### File Descriptors

**Standard file descriptors:**
- **0 = stdin** (standard input)
- **1 = stdout** (standard output)
- **2 = stderr** (standard error)

**Key points:**
- File descriptors are small non-negative integers
- Each process has its own file descriptor table
- File descriptors are reused (lowest available number)
- Valid operations: read, write, lseek, close

#### Open Flags (Important!)

**Access modes (mutually exclusive):**
- `O_RDONLY` - Read only
- `O_WRONLY` - Write only
- `O_RDWR` - Read and write

**File creation flags:**
- `O_CREAT` - Create file if it doesn't exist
- `O_TRUNC` - Truncate file to zero length if it exists
- `O_APPEND` - Append to end of file (atomic)
- `O_EXCL` - Used with O_CREAT; fail if file exists

**Common combinations:**
```c
// Open for reading
int fd = open("file.txt", O_RDONLY);

// Open for writing, create if doesn't exist, truncate if exists
int fd = open("file.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);

// Open for appending
int fd = open("file.txt", O_WRONLY | O_CREAT | O_APPEND, 0644);

// Open for read/write, create if doesn't exist
int fd = open("file.txt", O_RDWR | O_CREAT, 0644);
```

#### lseek() Whence Parameters

**Three options for `whence`:**
- `SEEK_SET` - Seek from beginning of file
- `SEEK_CUR` - Seek from current position
- `SEEK_END` - Seek from end of file

**Examples:**
```c
// Go to beginning
lseek(fd, 0, SEEK_SET);

// Go to end (for appending)
lseek(fd, 0, SEEK_END);

// Move forward 100 bytes from current position
lseek(fd, 100, SEEK_CUR);

// Move backward 50 bytes from current position
lseek(fd, -50, SEEK_CUR);
```

#### Sparse Files (Important Concept!)

**What is a sparse file?**
- A file with "holes" - regions of zeros that don't consume disk space
- Created by seeking beyond the end of a file and then writing

**Example:**
```c
int fd = open("sparse.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
lseek(fd, 1024*1024*1024, SEEK_SET);  // Seek 1GB ahead
write(fd, "X", 1);                     // Write 1 byte
close(fd);
```

**Result:**
- `ls -l` shows file size as ~1GB
- `du -h` shows actual disk usage as 4KB (one block)
- `cat` skips the holes - file appears nearly empty
- Holes read as zeros if accessed

**Why use sparse files?**
- Save disk space
- Efficient for databases and virtual machine disk images
- Useful for large files with mostly empty space

#### Appending Data

**Always use O_APPEND flag for appending:**
```c
// CORRECT - atomic append
int fd = open("log.txt", O_WRONLY | O_APPEND);
write(fd, data, len);

// INCORRECT - race condition possible
int fd = open("log.txt", O_WRONLY);
lseek(fd, 0, SEEK_END);  // Not atomic with write!
write(fd, data, len);
```

**Why O_APPEND matters:**
- Ensures atomic operation (seek + write happen together)
- Prevents race conditions in concurrent access
- Multiple processes can safely append simultaneously

---

### Standard I/O (Buffered Streams)

#### Overview
- Higher-level library functions (part of C standard library)
- Built on top of unbuffered I/O
- Provides buffering for efficiency
- Uses `FILE *` pointers instead of file descriptors

#### Core Functions
```c
#include <stdio.h>

FILE *fopen(const char *pathname, const char *mode);
int fclose(FILE *stream);
int fgetc(FILE *stream);
int fputc(int c, FILE *stream);
char *fgets(char *s, int size, FILE *stream);
int fputs(const char *s, FILE *stream);
int fscanf(FILE *stream, const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);
size_t fread(void *ptr, size_t size, size_t nmemb, FILE *stream);
size_t fwrite(const void *ptr, size_t size, size_t nmemb, FILE *stream);
```

#### fopen() Mode Strings (MEMORIZE!)

| Mode | Read | Write | Create | Truncate | Position | Notes |
|------|------|-------|--------|----------|----------|-------|
| `r`  | ✓    | ✗     | ✗      | ✗        | Start    | File must exist |
| `r+` | ✓    | ✓     | ✗      | ✗        | Start    | File must exist |
| `w`  | ✗    | ✓     | ✓      | ✓        | Start    | Truncates existing file |
| `w+` | ✓    | ✓     | ✓      | ✓        | Start    | Truncates existing file |
| `a`  | ✗    | ✓     | ✓      | ✗        | End      | Append mode |
| `a+` | ✓    | ✓     | ✓      | ✗        | End      | Read anywhere, write at end |

**Key differences to remember:**
- **`r+` vs `w+`**: `r+` requires file to exist; `w+` creates or truncates
- **`a` vs `a+`**: `a+` allows reading; both append writes
- **`w` modes**: Always truncate existing files (dangerous!)
- **`a` modes**: Never truncate; safe for logging

**Examples:**
```c
// Read only - file must exist
FILE *fp = fopen("input.txt", "r");

// Write, creating or truncating file
FILE *fp = fopen("output.txt", "w");

// Append to log file
FILE *fp = fopen("log.txt", "a");

// Read and write existing file without truncating
FILE *fp = fopen("data.txt", "r+");

// Read and append (create if doesn't exist)
FILE *fp = fopen("notes.txt", "a+");
```

#### Character I/O

**Reading characters:**
```c
int ch;
while ((ch = fgetc(fp)) != EOF) {
    putchar(ch);
}
```

**Writing characters:**
```c
fputc('A', fp);
fputc('\n', fp);
```

#### Line I/O

**Reading lines:**
```c
char buffer[256];
while (fgets(buffer, sizeof(buffer), fp) != NULL) {
    // buffer contains line including newline
    printf("%s", buffer);
}
```

**Key points about fgets():**
- Reads up to `size-1` characters
- Stops at newline (includes newline in buffer)
- Always null-terminates the string
- Returns NULL on EOF or error

**Writing lines:**
```c
fputs("Hello, World!\n", fp);
// Does NOT automatically add newline - you must include it
```

#### Formatted I/O

**scanf() and fscanf():**
```c
int age;
char name[50];
float gpa;

// From stdin
scanf("%d", &age);  // REQUIRES ADDRESS (&)!

// From file
fscanf(fp, "%s %f", name, &gpa);  // name is already a pointer
```

**CRITICAL: scanf() requires addresses!**
```c
int x;
scanf("%d", &x);    // CORRECT - address of x
scanf("%d", x);     // WRONG - will crash!

char str[50];
scanf("%s", str);   // CORRECT - str is already address
scanf("%s", &str);  // WRONG - address of array, not needed
```

**printf() and fprintf():**
```c
// To stdout
printf("Age: %d\n", age);

// To file
fprintf(fp, "Name: %s, GPA: %.2f\n", name, gpa);

// To string (useful for formatting)
char buffer[100];
sprintf(buffer, "Score: %d", score);
```

**Common format specifiers:**
- `%d` - integer
- `%f` - float/double
- `%s` - string
- `%c` - character
- `%ld` - long
- `%lf` - double (for scanf only)
- `%.2f` - float with 2 decimal places

#### Practical Examples

**Example 1: Copy file using standard I/O**
```c
FILE *src = fopen("input.txt", "r");
FILE *dst = fopen("output.txt", "w");
int ch;

while ((ch = fgetc(src)) != EOF) {
    fputc(ch, dst);
}

fclose(src);
fclose(dst);
```

**Example 2: Read and sum numbers from file**
```c
FILE *fp = fopen("numbers.txt", "r");
int num, sum = 0;

while (fscanf(fp, "%d", &num) == 1) {
    sum += num;
}

printf("Sum: %d\n", sum);
fclose(fp);
```

**Example 3: Append to log file**
```c
FILE *log = fopen("log.txt", "a");
fprintf(log, "[%s] User logged in\n", timestamp);
fclose(log);
```

---

### File Metadata and Types

#### stat() and fstat()

**Purpose:** Get information about a file
```c
#include <sys/stat.h>

int stat(const char *pathname, struct stat *buf);
int fstat(int fd, struct stat *buf);
```

**Key fields in `struct stat`:**
```c
struct stat {
    mode_t    st_mode;     // File type and permissions
    off_t     st_size;     // Total size in bytes
    uid_t     st_uid;      // User ID of owner
    gid_t     st_gid;      // Group ID of owner
    time_t    st_atime;    // Time of last access
    time_t    st_mtime;    // Time of last modification
    time_t    st_ctime;    // Time of last status change
    // ... more fields
};
```

**Example usage:**
```c
struct stat file_info;

// Using stat() with pathname
if (stat("file.txt", &file_info) == 0) {
    printf("File size: %ld bytes\n", file_info.st_size);
}

// Using fstat() with file descriptor
int fd = open("file.txt", O_RDONLY);
if (fstat(fd, &file_info) == 0) {
    printf("File size: %ld bytes\n", file_info.st_size);
}
```

#### File Types

**Extracted from `st_mode` field:**
- **Regular file** - normal data file
- **Directory** - contains directory entries
- **Socket** - network communication endpoint
- **FIFO (named pipe)** - inter-process communication
- **Symbolic link** - pointer to another file
- **Block device** - buffered I/O device (e.g., hard drive)
- **Character device** - unbuffered I/O device (e.g., terminal)

**Checking file type (macros provided):**
```c
if (S_ISREG(file_info.st_mode)) {
    printf("Regular file\n");
}
if (S_ISDIR(file_info.st_mode)) {
    printf("Directory\n");
}
if (S_ISSOCK(file_info.st_mode)) {
    printf("Socket\n");
}
```

#### File Permissions

**Permission bits in `st_mode`:**
```
Owner:  Read (r) Write (w) Execute (x)
Group:  Read (r) Write (w) Execute (x)
Other:  Read (r) Write (w) Execute (x)
```

**Extracting permissions using masks:**
```c
// Check owner permissions
if (file_info.st_mode & S_IRUSR) printf("Owner can read\n");
if (file_info.st_mode & S_IWUSR) printf("Owner can write\n");
if (file_info.st_mode & S_IXUSR) printf("Owner can execute\n");

// Check group permissions
if (file_info.st_mode & S_IRGRP) printf("Group can read\n");
if (file_info.st_mode & S_IWGRP) printf("Group can write\n");
if (file_info.st_mode & S_IXGRP) printf("Group can execute\n");

// Check other permissions
if (file_info.st_mode & S_IROTH) printf("Others can read\n");
if (file_info.st_mode & S_IWOTH) printf("Others can write\n");
if (file_info.st_mode & S_IXOTH) printf("Others can execute\n");
```

**Example: Print three-bit owner permissions**
```c
struct stat file_info;
stat("file.txt", &file_info);

printf("Owner permissions: ");
printf("%c", (file_info.st_mode & S_IRUSR) ? 'r' : '-');
printf("%c", (file_info.st_mode & S_IWUSR) ? 'w' : '-');
printf("%c", (file_info.st_mode & S_IXUSR) ? 'x' : '-');
printf("\n");
// Output example: "rwx" or "rw-" or "r--"
```

---

### Unbuffered vs Buffered I/O

| Feature | Unbuffered I/O | Buffered I/O |
|---------|---------------|--------------|
| **Functions** | open, read, write, lseek, close | fopen, fread, fwrite, fseek, fclose |
| **Handle type** | File descriptor (int) | FILE pointer (FILE *) |
| **Performance** | Every call is a system call | Buffered, fewer system calls |
| **Portability** | POSIX/UNIX specific | ANSI C standard (portable) |
| **Control** | Direct, low-level | Higher-level, easier to use |
| **Use case** | System programming, precise control | General application development |
| **Binary data** | read/write with byte count | fread/fwrite with element size |

**When to use each:**
- **Unbuffered I/O:** Device drivers, network programming, precise control needed
- **Buffered I/O:** Text files, formatted data, general file operations

---

## Processes and Process Management

### Process Basics

**What is a process?**
- A running instance of a program
- Has its own memory space (code, data, stack, heap)
- Has its own process ID (PID)
- Each process runs in isolation (illusion of exclusivity)

**Process creation:**
- Shell runs commands by forking child processes
- Parent process creates child processes
- Child inherits copy of parent's memory

### Key System Calls

#### fork()

**Declaration:**
```c
#include <unistd.h>
pid_t fork(void);
```

**What fork() does:**
1. Creates an exact copy of the calling process
2. Child gets copy of parent's memory, file descriptors, etc.
3. Both processes continue execution after fork()

**Return values (CRITICAL!):**
- **Parent process:** Returns child's PID (positive number)
- **Child process:** Returns 0
- **On error:** Returns -1

**Basic pattern:**
```c
pid_t pid = fork();

if (pid < 0) {
    // Error
    perror("fork failed");
    exit(1);
} else if (pid == 0) {
    // Child process
    printf("I am the child, PID = %d\n", getpid());
} else {
    // Parent process
    printf("I am the parent, child PID = %d\n", pid);
}
```

**Important notes:**
- After fork(), BOTH processes continue execution
- Child gets a COPY of parent's variables (not shared)
- Changes in child don't affect parent and vice versa
- File descriptors are shared (both point to same open file)

#### wait() and waitpid()

**Declaration:**
```c
#include <sys/wait.h>
pid_t wait(int *status);
pid_t waitpid(pid_t pid, int *status, int options);
```

**Purpose:**
- Parent waits for child process to terminate
- Retrieves child's exit status
- Prevents zombie processes

**Basic usage:**
```c
pid_t pid = fork();

if (pid == 0) {
    // Child
    printf("Child running\n");
    exit(0);  // Exit with status 0
} else {
    // Parent
    int status;
    wait(&status);  // Wait for child to finish
    printf("Child finished\n");
}
```

**Why wait() is important:**
- Prevents zombie processes (terminated but not reaped)
- Ensures parent knows when child completes
- Allows parent to get child's exit status

**Waiting for specific child:**
```c
pid_t child_pid = fork();

if (child_pid == 0) {
    // Child
    exit(42);
} else {
    // Parent - wait for specific child
    int status;
    waitpid(child_pid, &status, 0);
    
    if (WIFEXITED(status)) {
        printf("Exit status: %d\n", WEXITSTATUS(status));
    }
}
```

#### exit()

**Declaration:**
```c
#include <stdlib.h>
void exit(int status);
```

**Purpose:**
- Terminates the calling process
- Returns exit status to parent
- Closes all open file descriptors
- Flushes all buffers

**Usage:**
```c
if (error_condition) {
    fprintf(stderr, "Error occurred\n");
    exit(1);  // Exit with error status
}

// Normal termination
exit(0);  // Exit with success status
```

**Exit status convention:**
- **0** = Success
- **Non-zero** = Error (different values can indicate different errors)

### Multiple Forks (EXAM FAVORITE!)

**Key concept:** Each fork() creates one new process

**Pattern 1: Sequential forks**
```c
fork();  // Creates 1 child → 2 total processes
fork();  // Each process forks → 4 total processes
```

**Process tree:**
```
        Parent (P)
         /    \
    Child1    fork()
     /  \
Child2  Child3
```

**Pattern 2: Three forks**
```c
fork();
fork();
fork();
// Total processes = 2^3 = 8
```

**How to count:**
- Start with 1 process (parent)
- Each fork() doubles the number of processes
- Formula: **2^n processes** (where n = number of fork calls)

**Example with conditional logic:**
```c
pid_t pid1 = fork();

if (pid1 == 0) {
    // Only child from first fork
    printf("Child1\n");
    exit(0);
}

// Only parent reaches here
pid_t pid2 = fork();

if (pid2 == 0) {
    // Only child from second fork
    printf("Child2\n");
    exit(0);
}

// Only original parent reaches here
printf("Parent\n");
wait(NULL);  // Wait for first child
wait(NULL);  // Wait for second child
```

**Output:** Exactly 3 processes total (1 parent, 2 children)

**Common exam question:** Count processes created
```c
fork(); fork(); fork();
printf("Hello\n");
```
**Answer:** "Hello" printed 8 times (by 8 different processes)

### Process States

**Common states:**
- **Running (R):** Currently executing on CPU
- **Sleeping (S):** Waiting for event (e.g., I/O)
- **Stopped (T):** Suspended (e.g., by CTRL-Z)
- **Zombie (Z):** Terminated but not yet reaped by parent

**Zombie processes:**
- Child has terminated but parent hasn't called wait()
- Still occupies entry in process table
- Shows as `<defunct>` in ps output
- Prevented by parent calling wait() or waitpid()

### Getting Process Information

**Get current process ID:**
```c
pid_t my_pid = getpid();
printf("My PID: %d\n", my_pid);
```

**Get parent process ID:**
```c
pid_t parent_pid = getppid();
printf("My parent's PID: %d\n", parent_pid);
```

### Linux Process Commands

#### ps (Process Status)

**Basic usage:**
```bash
ps           # Shows your processes in current terminal
ps aux       # Shows all processes for all users
ps -ef       # Alternative format showing all processes
```

**Understanding ps output:**
```
PID   TTY     TIME    CMD
1234  pts/0   0:00    bash
5678  pts/0   0:01    ./myprogram
```
- **PID:** Process ID
- **TTY:** Terminal
- **TIME:** CPU time used
- **CMD:** Command name

#### top (Real-time Process Viewer)
```bash
top          # Interactive, real-time view of processes
```

**Key information shown:**
- CPU usage per process
- Memory usage
- Process priority
- Running time
- Can sort by various criteria

**Useful in top:**
- Press `q` to quit
- Press `k` to kill a process
- Press `M` to sort by memory
- Press `P` to sort by CPU

#### jobs (Background Jobs)
```bash
jobs         # Lists background jobs in current shell
```

**Example output:**
```
[1]+  Running     ./long_process &
[2]-  Stopped     vi myfile.txt
```

### Foreground vs Background

**Running in background:**
```bash
./program &              # Start in background
```

**Job control:**
```bash
CTRL-Z                   # Suspend foreground process
bg                       # Resume suspended job in background
bg %1                    # Resume specific job in background
fg                       # Bring background job to foreground
fg %2                    # Bring specific job to foreground
jobs                     # List background jobs
```

**Example workflow:**
```bash
$ ./long_running_program    # Start in foreground
^Z                          # Press CTRL-Z (suspend)
[1]+  Stopped    ./long_running_program
$ bg                        # Resume in background
[1]+ ./long_running_program &
$ jobs                      # Check status
[1]+  Running    ./long_running_program &
$ fg                        # Bring back to foreground
./long_running_program
```

---

## Signals

### What are Signals?

**Definition:** Software interrupts that notify a process of an event

**Key characteristics:**
- Asynchronous - can arrive at any time
- Process can catch, ignore, or use default action
- Used for process communication and event notification

### Common Signals

| Signal | Number | Default Action | Triggered By | Purpose |
|--------|--------|---------------|--------------|---------|
| SIGINT | 2 | Terminate | CTRL-C | Interrupt from keyboard |
| SIGTERM | 15 | Terminate | kill command | Termination request |
| SIGKILL | 9 | Terminate | kill -9 | Force kill (cannot be caught!) |
| SIGALRM | 14 | Terminate | alarm() | Timer expired |
| SIGUSR1 | 10 | Terminate | User-defined | Custom signal 1 |
| SIGUSR2 | 12 | Terminate | User-defined | Custom signal 2 |
| SIGCHLD | 17 | Ignore | Child process | Child terminated/stopped |
| SIGSTOP | 19 | Stop | CTRL-Z | Stop process (cannot be caught!) |

**Signals that CANNOT be caught:**
- **SIGKILL** (9) - Force kill
- **SIGSTOP** (19) - Force stop

All other signals can be caught with signal handlers.

### Sending Signals

#### From Command Line
```bash
# Send SIGTERM (default)
kill 1234

# Send specific signal by number
kill -9 1234        # SIGKILL (force kill)
kill -2 1234        # SIGINT

# Send specific signal by name
kill -SIGTERM 1234
kill -SIGINT 1234
kill -SIGUSR1 1234

# List all signals
kill -l
```

#### From C Code

**Declaration:**
```c
#include <signal.h>
#include <sys/types.h>

int kill(pid_t pid, int sig);
```

**Usage:**
```c
// Send SIGTERM to process 1234
kill(1234, SIGTERM);

// Send SIGUSR1 to process
kill(child_pid, SIGUSR1);

// Send SIGKILL (force kill)
kill(process_pid, SIGKILL);
```

### Installing Signal Handlers

**Declaration:**
```c
#include <signal.h>

typedef void (*sighandler_t)(int);
sighandler_t signal(int signum, sighandler_t handler);
```

**Basic pattern:**
```c
void my_handler(int sig) {
    printf("Received signal %d\n", sig);
    // Handle the signal
}

int main() {
    // Install handler for SIGINT (CTRL-C)
    signal(SIGINT, my_handler);
    
    // Program continues...
    while (1) {
        // Do work
    }
}
```

**Example: Count SIGUSR1 signals**
```c
#include <stdio.h>
#include <signal.h>
#include <unistd.h>

int signal_count = 0;

void sigusr1_handler(int sig) {
    signal_count++;
    printf("Received SIGUSR1 #%d\n", signal_count);
    
    if (signal_count >= 5) {
        printf("Five signals received.\n");
        exit(0);
    }
}

int main() {
    // Print PID so we can send signals to this process
    printf("My PID: %d\n", getpid());
    
    // Install signal handler
    signal(SIGUSR1, sigusr1_handler);
    
    // Wait for signals
    while (1) {
        pause();  // Sleep until signal arrives
    }
    
    return 0;
}
```

**To test the above program:**
```bash
# Terminal 1
$ ./program
My PID: 12345

# Terminal 2
$ kill -SIGUSR1 12345    # Send first signal
$ kill -SIGUSR1 12345    # Send second signal
# ... (repeat 5 times)
```

### alarm() Function

**Declaration:**
```c
#include <unistd.h>
unsigned int alarm(unsigned int seconds);
```

**Purpose:** Schedule SIGALRM signal after specified seconds

**Usage:**
```c
void alarm_handler(int sig) {
    printf("Time's up!\n");
    exit(0);
}

int main() {
    signal(SIGALRM, alarm_handler);
    alarm(5);  // Set alarm for 5 seconds
    
    printf("Starting work...\n");
    while (1) {
        // Do work
    }
    // After 5 seconds, alarm_handler will be called
}
```

**Important notes:**
- Only one alarm can be set at a time
- Calling alarm() again resets the timer
- alarm(0) cancels the current alarm

### Signal Handler Behavior (CRITICAL!)

**After signal handler executes:**
- Handler **RETURNS** to program (does not terminate)
- Program continues from where it was interrupted
- Unless handler explicitly calls exit()

**Example:**
```c
void handler(int sig) {
    printf("Signal caught\n");
    // Handler returns here - program continues!
}

int main() {
    signal(SIGINT, handler);
    
    for (int i = 0; i < 100; i++) {
        printf("Working... %d\n", i);
        sleep(1);
    }
    // If CTRL-C pressed, handler runs, then loop continues
}
```

**To terminate in handler:**
```c
void handler(int sig) {
    printf("Signal caught, exiting\n");
    exit(0);  // Explicitly exit
}
```

### Signal Safety

**Problem:** Signals are asynchronous - can interrupt anywhere

**Safe practices:**
- Keep signal handlers short and simple
- Don't call complex functions in handlers
- Be careful with global variables
- Use volatile for variables modified in handlers

**Example with global variable:**
```c
volatile int keep_running = 1;

void sigint_handler(int sig) {
    keep_running = 0;  // Set flag
}

int main() {
    signal(SIGINT, sigint_handler);
    
    while (keep_running) {
        // Do work
    }
    
    printf("Shutting down gracefully\n");
}
```

---

## Networking and Sockets

### Network Programming Overview

**Client-Server Model:**
- **Server:** Waits for connections, provides service
- **Client:** Initiates connection, requests service
- Communication happens over sockets

**Sockets:**
- Similar to file descriptors
- Can read/write like files
- Provide network communication endpoint

### DNS and IP Basics

#### IP Addresses

**IPv4 addresses:**
- 32-bit number
- Usually written as dotted decimal: `192.168.1.1`
- Split into network and host portions

**Byte order matters!**
- **Host byte order:** CPU's native byte order (may be little-endian or big-endian)
- **Network byte order:** Always big-endian (most significant byte first)
- Must convert between host and network byte order

#### IP Address Conversion Functions

**String ↔ Binary conversions:**
```c
#include <arpa/inet.h>

// ASCII to Network (string → binary)
int inet_aton(const char *cp, struct in_addr *inp);

// Network to ASCII (binary → string)
char *inet_ntoa(struct in_addr in);
```

**Examples:**
```c
// Convert string to binary
struct in_addr addr;
inet_aton("192.168.1.1", &addr);

// Convert binary to string
char *ip_string = inet_ntoa(addr);
printf("IP: %s\n", ip_string);  // Prints: IP: 192.168.1.1
```

**Special IP addresses:**
- `127.0.0.1` - Localhost (loopback)
- `0.0.0.0` - Any address (bind to all interfaces)
- `255.255.255.255` - Broadcast

#### DNS Lookup Functions

**Hostname → IP address:**
```c
#include <netdb.h>

struct hostent *gethostbyname(const char *name);
```

**Usage:**
```c
struct hostent *host = gethostbyname("www.google.com");
if (host != NULL) {
    struct in_addr **addr_list = (struct in_addr **)host->h_addr_list;
    for (int i = 0; addr_list[i] != NULL; i++) {
        printf("IP: %s\n", inet_ntoa(*addr_list[i]));
    }
}
```

**IP address → Hostname:**
```c
struct hostent *gethostbyaddr(const void *addr, socklen_t len, int type);
```

**Example: Resolve ecs.syracuse.edu**
```c
#include <stdio.h>
#include <netdb.h>
#include <arpa/inet.h>

int main() {
    struct hostent *host = gethostbyname("ecs.syracuse.edu");
    
    if (host == NULL) {
        printf("DNS lookup failed\n");
        return 1;
    }
    
    printf("Hostname: %s\n", host->h_name);
    printf("IP addresses:\n");
    
    struct in_addr **addr_list = (struct in_addr **)host->h_addr_list;
    for (int i = 0; addr_list[i] != NULL; i++) {
        printf("  %s\n", inet_ntoa(*addr_list[i]));
    }
    
    return 0;
}
```

### Network Byte Order

**Why byte order matters:**
- Different CPUs store multi-byte integers differently
- Network protocols require consistent byte order
- Always use network byte order for transmission

**Conversion functions:**
```c
#include <arpa/inet.h>

// Host to Network
uint16_t htons(uint16_t hostshort);   // 16-bit (ports)
uint32_t htonl(uint32_t hostlong);    // 32-bit (IP addresses)

// Network to Host
uint16_t ntohs(uint16_t netshort);    // 16-bit
uint32_t ntohl(uint32_t netlong);     // 32-bit
```

**When to use:**
- **htons():** Port numbers before sending
- **htonl():** IP addresses before sending
- **ntohs():** Port numbers after receiving
- **ntohl():** IP addresses after receiving

**Example:**
```c
// Convert port to network byte order
uint16_t port = 8080;
uint16_t network_port = htons(port);

// Convert IP to network byte order
struct in_addr addr;
inet_aton("192.168.1.1", &addr);
// addr.s_addr is already in network byte order after inet_aton
```

### Socket Programming

#### Creating a Socket

**Declaration:**
```c
#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

**Common usage for TCP:**
```c
int sockfd = socket(AF_INET, SOCK_STREAM, 0);
if (sockfd < 0) {
    perror("socket creation failed");
    exit(1);
}
```

**Parameters:**
- `AF_INET` - IPv4 address family
- `SOCK_STREAM` - TCP (reliable, connection-oriented)
- `SOCK_DGRAM` - UDP (unreliable, connectionless)
- `0` - Default protocol for the type

**Return value:**
- Socket file descriptor on success
- -1 on error

#### Socket Address Structure

**Definition:**
```c
#include <netinet/in.h>

struct sockaddr_in {
    short            sin_family;   // AF_INET
    unsigned short   sin_port;     // Port (network byte order!)
    struct in_addr   sin_addr;     // IP address
    char             sin_zero[8];  // Padding
};

struct in_addr {
    unsigned long s_addr;  // IP address (network byte order!)
};
```

**Setting up address structure:**
```c
struct sockaddr_in server_addr;

// Clear structure
memset(&server_addr, 0, sizeof(server_addr));

// Set address family
server_addr.sin_family = AF_INET;

// Set port (convert to network byte order!)
server_addr.sin_port = htons(8080);

// Set IP address
inet_aton("127.0.0.1", &server_addr.sin_addr);
// OR for any address:
server_addr.sin_addr.s_addr = INADDR_ANY;
```

**What's stored in sockaddr_in:**
- ✓ IP address
- ✓ Port number
- ✗ FILE pointer (not stored)
- ✗ URL (not stored)

### Client-Side Socket Programming

**Client workflow:**
1. Create socket with `socket()`
2. Connect to server with `connect()`
3. Send/receive data with `write()`/`read()`
4. Close socket with `close()`

**Complete client example:**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    // 1. Create socket
    int sockfd = socket(AF_INET, SOCK_STREAM, 0);
    if (sockfd < 0) {
        perror("socket");
        exit(1);
    }
    
    // 2. Set up server address
    struct sockaddr_in server_addr;
    memset(&server_addr, 0, sizeof(server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(8080);
    inet_aton("127.0.0.1", &server_addr.sin_addr);
    
    // 3. Connect to server
    if (connect(sockfd, (struct sockaddr*)&server_addr, 
                sizeof(server_addr)) < 0) {
        perror("connect");
        exit(1);
    }
    
    printf("Connected to server\n");
    
    // 4. Send data
    char *message = "Hello from client!";
    write(sockfd, message, strlen(message));
    
    // 5. Receive response
    char buffer[1024];
    int n = read(sockfd, buffer, sizeof(buffer)-1);
    buffer[n] = '\0';
    printf("Server response: %s\n", buffer);
    
    // 6. Close socket
    close(sockfd);
    
    return 0;
}
```

**Functions client calls (in order):**
1. `socket()` - Create socket
2. `connect()` - Connect to server
3. `read()`/`write()` - Communicate
4. `close()` - Clean up

### Server-Side Socket Programming

**Server workflow:**
1. Create socket with `socket()`
2. Bind to address/port with `bind()`
3. Mark as listening with `listen()`
4. Accept connections with `accept()`
5. Send/receive data with `write()`/`read()`
6. Close sockets with `close()`

**Complete server example:**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <arpa/inet.h>

int main() {
    // 1. Create socket
    int listen_fd = socket(AF_INET, SOCK_STREAM, 0);
    if (listen_fd < 0) {
        perror("socket");
        exit(1);
    }
    
    // 2. Set up server address
    struct sockaddr_in server_addr;
    memset(&server_addr, 0, sizeof(server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_port = htons(8080);
    server_addr.sin_addr.s_addr = INADDR_ANY;  // Any interface
    
    // 3. Bind socket to address
    if (bind(listen_fd, (struct sockaddr*)&server_addr,
             sizeof(server_addr)) < 0) {
        perror("bind");
        exit(1);
    }
    
    // 4. Mark socket as passive (ready to accept)
    if (listen(listen_fd, 5) < 0) {  // Backlog of 5
        perror("listen");
        exit(1);
    }
    
    printf("Server listening on port 8080...\n");
    
    // 5. Accept connection
    struct sockaddr_in client_addr;
    socklen_t client_len = sizeof(client_addr);
    int conn_fd = accept(listen_fd, (struct sockaddr*)&client_addr,
                         &client_len);
    if (conn_fd < 0) {
        perror("accept");
        exit(1);
    }
    
    printf("Client connected: %s\n", 
           inet_ntoa(client_addr.sin_addr));
    
    // 6. Receive data
    char buffer[1024];
    int n = read(conn_fd, buffer, sizeof(buffer)-1);
    buffer[n] = '\0';
    printf("Client message: %s\n", buffer);
    
    // 7. Send response
    char *response = "Hello from server!";
    write(conn_fd, response, strlen(response));
    
    // 8. Close sockets
    close(conn_fd);
    close(listen_fd);
    
    return 0;
}
```

**Functions server calls (in order):**
1. `socket()` - Create socket
2. `bind()` - Bind to address/port
3. `listen()` - Mark as listening
4. `accept()` - Accept connection (blocks)
5. `read()`/`write()` - Communicate
6. `close()` - Clean up

**Key server functions explained:**

**bind()** - Associates socket with specific IP/port
```c
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

**listen()** - Marks socket as passive (accepting connections)
```c
int listen(int sockfd, int backlog);
// backlog: max number of pending connections
```

**accept()** - Accepts incoming connection (BLOCKING!)
```c
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
// Returns NEW socket for communication with client
// Original socket continues listening
```

### Socket I/O Behavior (IMPORTANT!)

**write() on socket:**
- **Non-blocking** (usually)
- Returns immediately after copying data to kernel buffer
- Does NOT wait for data to be transmitted

**read() on socket:**
- **Blocking** (by default)
- Waits for data to arrive
- Similar to reading from stdin

**Example:**
```c
// write returns immediately
write(sockfd, data, len);  // Returns after copying to buffer

// read waits for data
int n = read(sockfd, buffer, sizeof(buffer));  // Blocks until data arrives
```

**Which functions can block?**
- ✓ `accept()` - Waits for client connection
- ✓ `read()` - Waits for data
- ✓ `connect()` - Can block (establishing connection)
- ✗ `socket()` - Does not block
- ✗ `bind()` - Does not block
- ✗ `listen()` - Does not block

### Multiprocess Server

**Problem:** Single-process server handles one client at a time

**Solution:** Fork a child process for each client

**Pattern:**
```c
int listen_fd = socket(...);
bind(listen_fd, ...);
listen(listen_fd, 5);

while (1) {
    // Accept connection (blocks waiting for client)
    int conn_fd = accept(listen_fd, ...);
    
    // Fork child to handle client
    pid_t pid = fork();
    
    if (pid == 0) {
        // CHILD PROCESS
        close(listen_fd);  // Child doesn't need listen socket
        
        // Handle client
        handle_client(conn_fd);
        
        close(conn_fd);
        exit(0);  // Child exits
        
    } else {
        // PARENT PROCESS
        close(conn_fd);  // Parent doesn't need connection socket
        
        // Immediately loops back to accept() for next client
        // Multiple children can run simultaneously!
    }
}
```

**Key points:**
- **Parent process:** Runs accept loop, creates children
- **Child process:** Handles one client, then exits
- **Parent immediately returns to accept():** Can serve multiple clients
- **Close unused descriptors:** Parent closes conn_fd, child closes listen_fd

**Example: Two-client addition server**
```c
int listen_fd = socket(...);
bind(listen_fd, ...);
listen(listen_fd, 2);

int num1, num2;

// Accept first client
int conn1 = accept(listen_fd, ...);
read(conn1, &num1, sizeof(num1));
close(conn1);

// Accept second client
int conn2 = accept(listen_fd, ...);
read(conn2, &num2, sizeof(num2));
close(conn2);

// Compute and print
printf("Sum: %d\n", num1 + num2);

close(listen_fd);
```

---

## Bash Programming

### Output Redirection

**Basic redirection:**
```bash
command > file           # Redirect stdout to file (overwrite)
command >> file          # Redirect stdout to file (append)
command 2> file          # Redirect stderr to file
command &> file          # Redirect both stdout and stderr
command > file 2>&1      # Redirect stderr to stdout, then to file
```

**File descriptor numbers:**
- **0** = stdin (standard input)
- **1** = stdout (standard output)
- **2** = stderr (standard error)

**Explicit redirection:**
```bash
command 1> stdout.txt    # Same as command > stdout.txt
command 2> stderr.txt    # Redirect errors only
command 1> out.txt 2> err.txt  # Separate files for stdout and stderr
```

**Silencing output:**
```bash
command > /dev/null      # Silence stdout
command 2> /dev/null     # Silence stderr
command &> /dev/null     # Silence both
command > /dev/null 2>&1 # Alternative for both
```

**Examples:**
```bash
# Save output, discard errors
ls -l > files.txt 2> /dev/null

# Append to log file
echo "Error occurred" >> error.log

# Combine stdout and stderr
./program > output.txt 2>&1
```

### Command History

**Using history:**
```bash
history              # Show command history
!!                   # Repeat last command
!n                   # Repeat command number n
!string              # Repeat last command starting with "string"
!?string             # Repeat last command containing "string"
```

**Examples:**
```bash
!ls                  # Repeat last command starting with "ls"
!-2                  # Repeat command 2 lines back
history | grep gcc   # Search history for gcc commands
```

### Process Control (Review)

**Background execution:**
```bash
command &            # Run in background
```

**Job control:**
```bash
jobs                 # List background jobs
fg                   # Bring last background job to foreground
fg %1                # Bring job 1 to foreground
bg                   # Resume suspended job in background
bg %2                # Resume job 2 in background
```

**Process management:**
```bash
ps                   # Show your processes
ps aux               # Show all processes
top                  # Interactive process viewer
kill PID             # Send SIGTERM to process
kill -9 PID          # Send SIGKILL (force kill)
kill -SIGINT PID     # Send SIGINT
```

### File Permissions

**Permission format:**
```
-rwxr-xr--
```
- First character: file type (- = regular, d = directory, l = link)
- Next 3: owner permissions (rwx)
- Next 3: group permissions (r-x)
- Next 3: other permissions (r--)

**Permission meanings:**
- **r (read):** Can read file contents / list directory
- **w (write):** Can modify file / add/remove files in directory
- **x (execute):** Can execute file / enter directory

**Changing permissions:**
```bash
chmod 755 file       # rwxr-xr-x
chmod 644 file       # rw-r--r--
chmod u+x file       # Add execute for owner
chmod g-w file       # Remove write for group
chmod a+r file       # Add read for all
```

### Find and Grep

**find command:**
```bash
find /path -name "pattern"           # Find by name
find /path -type f                   # Find files only
find /path -type d                   # Find directories only
find /path -size +1M                 # Find files larger than 1MB
find /path -mtime -7                 # Modified in last 7 days
find /path -name "*.txt" -exec rm {} \;  # Execute command on results
```

**grep command:**
```bash
grep "pattern" file                  # Search for pattern in file
grep -r "pattern" /path              # Recursive search
grep -i "pattern" file               # Case-insensitive
grep -n "pattern" file               # Show line numbers
grep -v "pattern" file               # Invert match (show non-matching)
```

**Combining find and grep:**
```bash
find /path -name "*.c" -exec grep -H "main" {} \;
```

---

## C Programming Fundamentals

### Pointers (Critical Review)

**Pointer basics:**
```c
int x = 42;
int *ptr = &x;      // ptr holds address of x

printf("%d\n", x);     // Prints: 42
printf("%d\n", *ptr);  // Prints: 42 (dereference)
printf("%p\n", ptr);   // Prints: address of x
```

**Key operators:**
- `&` - Address-of operator (gets address)
- `*` - Dereference operator (gets value at address)

**Common patterns:**
```c
// Declare pointer
int *ptr;

// Get address
ptr = &variable;

// Dereference (get value)
int value = *ptr;

// Modify through pointer
*ptr = 100;
```

**Pointers with functions:**
```c
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

int main() {
    int x = 1, y = 2;
    swap(&x, &y);  // Pass addresses
    printf("x=%d, y=%d\n", x, y);  // Prints: x=2, y=1
}
```

### Arrays and Pointers

**Array name is pointer to first element:**
```c
int arr[5] = {1, 2, 3, 4, 5};
int *ptr = arr;  // No & needed! arr is already address

printf("%d\n", arr[0]);   // Prints: 1
printf("%d\n", *ptr);     // Prints: 1 (same)
printf("%d\n", *(ptr+1)); // Prints: 2
```

**Pointer arithmetic:**
```c
int arr[5] = {10, 20, 30, 40, 50};
int *ptr = arr;

ptr++;        // Points to arr[1]
ptr += 2;     // Points to arr[3]
ptr--;        // Points to arr[2]
```

### String Handling

**Strings are char arrays:**
```c
char str1[] = "Hello";      // Array with size 6 (includes \0)
char *str2 = "World";       // Pointer to string literal

printf("%s\n", str1);       // Prints: Hello
printf("%c\n", str1[0]);    // Prints: H
```

**String functions:**
```c
#include <string.h>

strlen(str);              // Length of string
strcpy(dest, src);        // Copy string
strncpy(dest, src, n);    // Copy at most n characters
strcmp(s1, s2);           // Compare strings
strcat(dest, src);        // Concatenate strings
```

### Memory Allocation

**Dynamic memory:**
```c
#include <stdlib.h>

// Allocate memory
int *ptr = (int *)malloc(sizeof(int) * 10);  // Array of 10 ints
if (ptr == NULL) {
    printf("Allocation failed\n");
    exit(1);
}

// Use memory
ptr[0] = 42;

// Free memory
free(ptr);
ptr = NULL;  // Good practice
```

### Common C Pitfalls

**1. Uninitialized variables:**
```c
int x;          // WRONG - contains garbage
int y = 0;      // CORRECT
```

**2. Array bounds:**
```c
int arr[5];
arr[5] = 10;    // WRONG - out of bounds (index 0-4 only)
arr[4] = 10;    // CORRECT
```

**3. Pointer dereferencing:**
```c
int *ptr;
*ptr = 10;      // WRONG - ptr not initialized!

int *ptr = malloc(sizeof(int));
*ptr = 10;      // CORRECT
```

**4. String termination:**
```c
char str[5];
strcpy(str, "Hello");  // WRONG - needs 6 bytes for \0

char str[6];
strcpy(str, "Hello");  // CORRECT
```

**5. scanf with addresses:**
```c
int x;
scanf("%d", x);     // WRONG - needs address
scanf("%d", &x);    // CORRECT

char str[50];
scanf("%s", str);   // CORRECT - str is already address
```

---

## Practice Problems

### File I/O Problems

**Problem 1:** Write a program to copy one file to another using unbuffered I/O.

**Problem 2:** Write a program that opens a file for reading and writing without truncating it. If the file doesn't exist, create it.

**Problem 3:** Write a program that creates a sparse file of 1GB with one byte at the end.

**Problem 4:** Write a program that reads a file and counts the number of lines.

**Problem 5:** Write a program that reads numbers from a file and prints their average.

### Process Problems

**Problem 6:** Draw the process tree and count total processes:
```c
fork();
fork();
if (fork() == 0) {
    fork();
}
```

**Problem 7:** What is the output of this program?
```c
int main() {
    int x = 5;
    pid_t pid = fork();
    
    if (pid == 0) {
        x = 10;
        printf("Child: x = %d\n", x);
    } else {
        wait(NULL);
        printf("Parent: x = %d\n", x);
    }
}
```

**Problem 8:** Write a program that creates 3 child processes and waits for all of them.

### Signal Problems

**Problem 9:** Write a program that counts SIGUSR1 signals and exits after 3 signals.

**Problem 10:** Write a program that uses alarm() to timeout after 5 seconds.

**Problem 11:** Explain what happens when a signal handler doesn't call exit().

### Socket Problems

**Problem 12:** Put these server operations in order: accept, bind, listen, socket

**Problem 13:** What's stored in `struct sockaddr_in`?

**Problem 14:** Write a client that connects to localhost:8080 and sends "Hello".

**Problem 15:** Explain the difference between the listening socket and connection socket in a server.

**Problem 16:** In a multiprocess server, what does the parent do? What does the child do?

---

## Quick Reference Tables

### System Call Quick Reference

| Function | Purpose | Return Value |
|----------|---------|--------------|
| `open()` | Open/create file | File descriptor or -1 |
| `read()` | Read data | Bytes read, 0 at EOF, -1 error |
| `write()` | Write data | Bytes written, -1 error |
| `close()` | Close descriptor | 0 success, -1 error |
| `fork()` | Create process | Child PID (parent), 0 (child), -1 error |
| `wait()` | Wait for child | Child PID or -1 |
| `exit()` | Terminate | Does not return |
| `socket()` | Create socket | Socket descriptor or -1 |
| `bind()` | Bind address | 0 success, -1 error |
| `listen()` | Mark listening | 0 success, -1 error |
| `accept()` | Accept connection | Connection descriptor or -1 |
| `connect()` | Connect to server | 0 success, -1 error |

### Flag Quick Reference

**open() flags:**
- `O_RDONLY` - Read only
- `O_WRONLY` - Write only
- `O_RDWR` - Read and write
- `O_CREAT` - Create if doesn't exist
- `O_TRUNC` - Truncate to zero
- `O_APPEND` - Append (atomic)

**fopen() modes:**
- `r` - Read (must exist)
- `r+` - Read/write (must exist)
- `w` - Write (truncate)
- `w+` - Read/write (truncate)
- `a` - Append
- `a+` - Read/append

### Signal Quick Reference

| Signal | Number | Meaning | Can Catch? |
|--------|--------|---------|------------|
| SIGINT | 2 | Interrupt (Ctrl-C) | Yes |
| SIGTERM | 15 | Termination | Yes |
| SIGKILL | 9 | Force kill | No |
| SIGALRM | 14 | Alarm timer | Yes |
| SIGUSR1 | 10 | User-defined 1 | Yes |
| SIGUSR2 | 12 | User-defined 2 | Yes |

### Byte Order Functions

| Function | Purpose |
|----------|---------|
| `htons()` | Host to Network Short (16-bit port) |
| `htonl()` | Host to Network Long (32-bit IP) |
| `ntohs()` | Network to Host Short |
| `ntohl()` | Network to Host Long |

### Common Mistakes to Avoid

1. **Forgetting & in scanf:** `scanf("%d", &x)` not `scanf("%d", x)`
2. **Not checking return values:** Always check for errors
3. **Forgetting to close files/sockets:** Resource leaks
4. **Wrong byte order:** Always use htons/htonl for network
5. **Not waiting for children:** Creates zombie processes
6. **Confusing O_APPEND and lseek:** Use O_APPEND for atomic append
7. **Wrong fopen mode:** r+ vs w+ vs a+
8. **Forgetting null terminator:** Strings need \0
9. **Array out of bounds:** Valid indices 0 to n-1
10. **Dereference before initialization:** Initialize pointers first

---

## Final Exam Checklist

### Before the Exam

- ✓ Review all homework problems (HW #3, #4, #5)
- ✓ Work through practice problems above
- ✓ Understand fork() process trees
- ✓ Memorize fopen() mode strings
- ✓ Know socket sequences (client and server)
- ✓ Understand signal handler behavior
- ✓ Practice code tracing by hand
- ✓ Review blocking vs non-blocking operations

### During the Exam

- Read each question carefully
- Draw diagrams for fork problems
- Trace through code step by step
- Check for off-by-one errors
- Remember: function formats are given
- Focus on understanding, not memorization
- Manage your time - don't get stuck
- Double-check your answers

### Key Concepts to Master

1. **File descriptors** vs **FILE pointers**
2. **fork() return values** - Parent gets PID, child gets 0
3. **Signal handlers** - They return, don't terminate
4. **Socket sequences** - Server: socket→bind→listen→accept
5. **Byte order** - Always convert for network
6. **Blocking operations** - accept(), read() block
7. **Process counting** - 2^n processes for n forks
8. **Sparse files** - Size vs disk usage

---

## Additional Resources

**Man pages (command line):**
```bash
man 2 open      # System calls (section 2)
man 3 fopen     # Library functions (section 3)
man 7 signal    # Overview pages (section 7)
```

**Useful commands:**
```bash
man -k keyword  # Search man pages
info gcc        # GCC documentation
```

**Online resources:**
- Beej's Guide to Network Programming
- Advanced Programming in the UNIX Environment (APUE)
- Linux man pages online

---

## Good Luck!

**Remember:**
- Stay calm and focused
- You've prepared well
- Trust your understanding
- Show your work
- You've got this! 🎓

---

*End of Study Guide*