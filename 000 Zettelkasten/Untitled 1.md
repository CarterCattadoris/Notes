# CSE 384: Systems and Network Programming - Final Exam Study Guide

## File I/O - Core Concepts

### The Five Core Functions (Unbuffered I/O)
- **open()** - Opens/creates file, returns lowest unused file descriptor
- **read()** - Reads bytes into buffer, moves offset forward, returns bytes read (0 at EOF)
- **write()** - Writes bytes from buffer, starts at current offset, returns bytes written
- **lseek()** - Changes file offset for random access
- **close()** - Closes file descriptor

### File Descriptors (MEMORIZE)
- **0 = stdin** (keyboard input)
- **1 = stdout** (normal output)
- **2 = stderr** (error output)

### Open Flags - What They DO

**Mandatory (pick one):**
- **O_RDONLY** - Read only
- **O_WRONLY** - Write only
- **O_RDWR** - Read and write

**Optional (combine with |):**
- **O_CREAT** - Create if doesn't exist
- **O_TRUNC** - Truncate to zero if exists
- **O_APPEND** - Append atomically (SAFE for shared files)

### lseek() - The whence Parameter
- **SEEK_SET** - offset from beginning
- **SEEK_CUR** - offset from current position
- **SEEK_END** - offset from end (often negative)

### Sparse Files (IMPORTANT!)
- Created by: write data → large lseek → write more data
- **`ls -l`** - Shows full size
- **`ls -ls`** - Shows actual disk usage (much smaller)
- **`cat`** - Skips holes, shows only actual data

### File Appending
❌ **Wrong (NOT SAFE):** `lseek(fd, 0, SEEK_END); write(fd, data, len);`

✅ **Right (SAFE):** Use `O_APPEND` flag - atomic operation

---

## Standard I/O (Buffered)

### fopen() Modes (MEMORIZE!)

| Mode | Must Exist? | Truncates? | Read? | Write? |
|------|-------------|------------|-------|--------|
| r | YES | No | Yes | No |
| r+ | YES | No | Yes | Yes |
| w | No | YES | No | Yes |
| w+ | No | YES | Yes | Yes |
| a | No | No | No | Yes (append) |
| a+ | No | No | Yes | Yes (append) |

**Key differences:**
- **r** - File must exist, read only
- **r+** - File must exist, read and write
- **w** - Creates/truncates file, write only
- **w+** - Creates/truncates file, read and write

### Character & Line I/O
- `fgetc(FILE *fp)` - Read char, returns EOF at end
- `fputc(int c, FILE *fp)` - Write char
- `fgets(char *buf, int n, FILE *fp)` - Read line (INCLUDES \n)
- `fputs(const char *str, FILE *fp)` - Write string (NO \n added)

### Formatted I/O
- `fscanf(FILE *fp, format, ...)` - Read formatted input from file
- `fprintf(FILE *fp, format, ...)` - Write formatted output to file
- **CRITICAL: scanf/fscanf require addresses (&)!**
```c
int x;
float y;
fscanf(fp, "%d %f", &x, &y);  // CORRECT - need &
scanf("%d", x);                // WRONG - crashes!
```

### stdin Blocking Behavior
- `fgets(..., stdin)` **BLOCKS** - waits until user presses Enter

---

## File Metadata (stat)

### File Types (Know All)
- Regular file - `S_ISREG(mode)`
- Directory - `S_ISDIR(mode)`
- Socket - `S_ISSOCK(mode)`
- FIFO - `S_ISFIFO(mode)`
- Symbolic link - `S_ISLNK(mode)`

### Permission Bitmasks
```c
// Owner permissions
S_IRUSR  // Read
S_IWUSR  // Write
S_IXUSR  // Execute

// Group permissions
S_IRGRP, S_IWGRP, S_IXGRP

// Other permissions
S_IROTH, S_IWOTH, S_IXOTH
```

**Check permissions:**
```c
if (info.st_mode & S_IRUSR) {
    printf("Owner can read\n");
}
```

**Print three-bit owner permissions:**
```c
// Extract owner bits: (mode >> 6) & 0x7
printf("%d%d%d", 
    (mode & S_IRUSR) ? 1 : 0,
    (mode & S_IWUSR) ? 1 : 0,
    (mode & S_IXUSR) ? 1 : 0);
```

---

## Bash Output Redirection

### The Three Cases (1 vs 2 vs &)

**1 = stdout only:**
```bash
command > file
command 1> file
```

**2 = stderr only:**
```bash
command 2> file
```

**& = both:**
```bash
command &> file
```

### Silencing Output
```bash
command > /dev/null      # Silence stdout
command 2> /dev/null     # Silence stderr
command &> /dev/null     # Silence both
```

---

## Processes, Signals, Fork, Wait

### Process Basics
- Each program runs in its own **process** (illusion of exclusivity)
- Shell runs commands by **forking** a child process
- **Foreground/background:** CTRL-Z, bg, fg, jobs
- Process provides illusion that your program is the only thing running
- In reality, multiple programs share CPU, memory, I/O devices

### Key System Calls
- **fork()** → parent gets child PID, child gets 0
  - Child process's code is a clone of parent's code
- **wait() / waitpid()** → parent waits for child exit
  - `wait(NULL)` blocks current process until child terminates
  - `WIFEXITED(wstatus)` returns true if child terminated normally
- **exit(status)** → terminates process
- **getpid()** → returns caller's PID

### Process Management Commands
- **top** - Show all active OS processes (global, for performance monitoring)
- **jobs** - Show all children processes created by current process
- **ps** - Show processes attached (foreground) to terminal
- **ps aux** - Show all processes (similar to top)

### Signals (IMPORTANT!)
- **Send:** `kill(pid, sig)` or `kill -SIGNAME pid`
- **Install handler:** `signal(signum, handler)`
- **Common signals:** 
  - SIGINT (Ctrl-C, signal #2)
  - SIGTERM (signal #15, "nice" termination)
  - SIGKILL (signal #9, force-kill, **cannot be caught**)
  - SIGALRM (from alarm() function, signal #14)
  - SIGUSR1 (signal #10), SIGUSR2 (signal #12) - user-defined signals
- **alarm(seconds)** triggers SIGALRM - process sends signal to itself
- **Signal handler** - function that processes received signals
  - Returns to program unless explicitly exiting
  - Can modify behavior of process when signal received
- **kill -l** - List all signals and their numbers

### Process Execution & Return Codes
- **$?** - Returns exit status of previous command (0 = success, non-zero = error)
- **exit(status)** - Used in C programs to return status code

### Foreground/Background Process Control
- Run in foreground: `command`
- Run in background: `command &`
- **CTRL-Z** - Put process to background (suspend)
- **fg** - Bring most recent background process to foreground
- **fg %N** - Bring job number N to foreground
- **jobs** - List all background processes spawned from current shell

### Important Patterns
- Multiple forks → exponential processes
- Example: `fork(); fork();` → **4 processes**
- Signal handler returns to program unless explicitly exiting

### Signal Handler Example Pattern
```c
void handler(int sig) {
    printf("Caught signal!\n");
    // exit(0); // optional - terminates process
}

int main(void) {
    signal(SIGINT, handler);  // Register handler
    while(1) {}  // Handler returns control here
}
```

### Counting Signals Example
```c
int count = 0;
void handler(int sig) {
    count++;
    if (count >= 5) {
        printf("Five signals received.\n");
        exit(0);
    }
}
```

---

## Networking & Sockets

### DNS & IP Basics
- **IP:** 32-bit unsigned integer, network byte order (big-endian) vs host byte order (little-endian)
- **Conversions:** 
  - `inet_aton(char *str, struct in_addr *addr)` - string → binary
  - `inet_ntoa(struct in_addr addr)` - binary → string
- **DNS lookup:** 
  - `gethostbyname(domain)` - domain name → IP address(es)
  - `gethostbyaddr(IP)` - IP address → domain name
- **Network byte order examples:**
  - 127 → 127.0.0.0
  - 257 → 1.1.0.0
  - 1025 → 1.4.0.0
  - -1 → 255.255.255.255

### Socket Address Structure
```c
struct sockaddr_in {
    uint16_t sin_family;    // AF_INET
    uint16_t sin_port;      // Port (network byte order)
    struct in_addr sin_addr; // IP address (network byte order)
};
```

**What's stored in sockaddr_in:**
- IP address (✓)
- Port number (✓)
- NOT: FILE pointer, URL

### Socket Workflow

**Client:**
1. `socket(AF_INET, SOCK_STREAM, 0)` - Create socket
2. `connect(clientfd, server_addr, addrlen)` - Connect to server

**Server (Listen Socket):**
1. `socket(AF_INET, SOCK_STREAM, 0)` - Create socket
2. `bind(serverfd, server_addr, addrlen)` - Bind to address/port
3. `listen(serverfd, backlog)` - Convert to passive socket (marks socket as listening)
4. `accept(serverfd, client_addr, &addrlen)` - Wait for connection (BLOCKING, returns new socket)

### Socket I/O
- **Basic file I/O works with socket descriptors:** read(), write(), close()
- **write()** = **non-blocking** (sends immediately)
- **read()** = **BLOCKING** (waits for data, like stdin)
- **Cannot use Standard I/O (FILE*)** directly with sockets without fdopen()

### Network Byte Order Functions
- **htons()** - host to network short (port numbers)
- **htonl()** - host to network long (IP addresses)
- **ntohs()** - network to host short
- **ntohl()** - network to host long

### Blocking Functions (EXAM IMPORTANT!)
- **accept()** - BLOCKS waiting for client connection
- **read()** - BLOCKS waiting for data
- **connect()** - Can block (waiting for server response)
- **NOT blocking:** socket(), bind(), listen(), write()

### Concurrency Problem & Solution
**Problem:** Single-process server blocks on one client
- Server stuck in `read()` loop with Client C1
- Can't handle new connection from Client C2

**Solution:** Multi-process server using `fork()`
```c
while (1) {
    connfd = accept(listenfd, ...);  // Parent accepts
    if (fork() == 0) {               // Child process
        // Handle client
        while (read(connfd, buf, 10) > 0) {
            printf("%s", buf);
        }
        close(connfd);
        exit(0);
    }
    close(connfd); // Parent closes its copy
}
```

---

## Common Exam Questions

1. **Sparse file size vs disk usage** - ls -l vs ls -ls
2. **fopen mode selection** - r+ vs w+ vs a+
3. **lseek offset calculations** - with SEEK_SET/CUR/END
4. **scanf & requirement** - when needed vs not
5. **File type identification** - using S_ISREG, S_ISDIR, etc.
6. **Permission checking** - using bitmasks and extracting owner permissions
7. **O_APPEND vs lseek+write** - which is safe?
8. **I/O redirection** - 1> vs 2> vs &>
9. **Fork patterns** - counting processes (exponential growth)
10. **Socket workflow** - client vs server steps
11. **Blocking vs non-blocking I/O** - accept() and read() block, write() doesn't
12. **Signal handling** - installing handlers, signal numbers, kill -l
13. **Process return codes** - using $? and exit()
14. **Foreground/background control** - fg %N to bring job N to foreground
15. **What's in sockaddr_in** - IP and port (not URL or FILE*)
16. **Which I/O works with sockets** - Basic file I/O (read/write)
17. **Network byte order conversions** - htons/htonl for sending, ntohs/ntohl for receiving
18. **IP address conversions** - inet_aton (string→binary), inet_ntoa (binary→string)

---

## Study Tips
- Practice lseek offset calculations by hand
- Work through in-class exercises + homeworks (especially HW3, HW4, HW5)
- Understand when to use unbuffered vs buffered I/O
- Know the difference between single-process vs multi-process servers
- Remember: scanf needs &, printf doesn't!
- Understand fork() creates exponential processes
- Know socket workflow for both client and server
- **Know which socket functions are blocking: accept(), read(), connect()**
- **Memorize what goes in sockaddr_in: IP address and port number**
- **Remember: Basic file I/O (read/write) works with socket descriptors**
- **Practice signal handling with counters and multiple signal types**
- **Exam is comprehensive** - covers all topics including Bash programming and C basics
- Be able to solve in-class exercises and homework problems
- New topics since midterm: File I/O, Processes, Network I/O