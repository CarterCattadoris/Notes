cumulative

name/format of the function is given. have to know params
more on explaining code then writing it
look at footnotes
## File IO

5 basic: open, read, write, lseek, close
- what they do not syntax
- unbuffered vs buffered

### important
create file with empty space example
cat ignores empty space, size doesn't

file descriptors, FD0,1,2
stdout, in, err

don't need to memorize flags they will be given, but need to know what each does

### stdio

memorize fopen syntax, ex: difference between r/r+
know about reading file metadata
know types of files
bash:
silencing output
1 vs 2 vs &

### process management
linux part:
know how programs run inside the shell
repeat same command: history, !ls
know top, jobs, ps, ps aux. what they provide and when to use
killing processes, and what parameters passing to kill mean
ctrl-c maps to SIGINT, kills foreground process
move a process between fore/background, stop running and keep running
ctrl-z puts process to backgound

C part:
getting pid, killing pid
kill function, pass a PID and a signal
signal handlers
forks, understand how they work
- return value = 0 is in child, not zero is in parent
wait and exit, waiting for child process

## network programming

understand server/client relationships, idea of a DNS
understand how IPs are stored
know usage of aton, ntoa
sockets are like file descriptors
socket process, what server/client do and how they are connected
blocking vs non blocking
client/server diagram slide is important
know multi process servers