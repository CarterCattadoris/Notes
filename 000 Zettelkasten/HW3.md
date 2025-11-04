
## Problem 1:
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd;
    fd = open("f.txt", O_WRONLY | O_TRUNC);
    if (fd == -1) {
        printf("Error: File f.txt does not exist or cannot be opened\n");
        return 1;
    }
    close(fd);
    return 0;
}

## Problem 2
#include <unistd.h>
#include <fcntl.h>

#define BUFFER_SIZE 4096

int main(int argc, char \*argv[]) {
    int fd_src, fd_dest;
    char buffer[BUFFER_SIZE];
    ssize_t bytes_read;
    fd_src = open(argv[1], O_RDONLY);
    fd_dest = open(argv[2], O_WRONLY | O_CREAT | O_TRUNC, 0644);
    while ((bytes_read = read(fd_src, buffer, BUFFER_SIZE)) > 0) {
        write(fd_dest, buffer, bytes_read);
    }
    close(fd_src);
    close(fd_dest);
    return 0;
}