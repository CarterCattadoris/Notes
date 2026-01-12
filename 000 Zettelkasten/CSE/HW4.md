## Problem 1

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/stat.h>

int main(int argc, char *argv[]){
    struct stat file_stat;
    stat(argv[1], &file_stat); 
    printf("Owner permissions: ");
    printf("%c", (file_stat.st_mode & S_IRUSR) ? 'r' : '-');
    printf("%c", (file_stat.st_mode & S_IWUSR) ? 'w' : '-');
    printf("%c", (file_stat.st_mode & S_IXUSR) ? 'x' : '-');
    printf("\n");
    return 0;
}
```
## Problem 2
There are 2 options using fg for bringing vi to the foreground. Since it was the third job, fg %3 would work. Since it was the only vi command, fg %vi would also work.

## Problem 3
```
#include <stdio.h>
#include <stdlib.h>
#include <signal.h>
#include <unistd.h>

int signal_count = 0;

void handler(int sig){
    signal_count++;
    printf("Signal %d received (Total: %d/5)\n", sig, signal_count);
    
    if(signal_count >= 5){
        printf("Five signals received.\n");
        exit(0);
    }
}

int main(){
    printf("Process PID: %d\n", getpid());
    printf("Waiting for 5 SIGUSR1 signals...\n");
    
    if(signal(SIGUSR1, handler) == SIG_ERR){
        printf("fail to install handler\n");
        return 1;
    }
    
    while(1){
        pause();
    }
    
    return 0;
}
```
