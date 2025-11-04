
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
#include <stdio.h>

int main(int argc, char \*argv[]) {
    FILE \*src, \*dest;
    int ch;
    src = fopen(argv[1], "r");
    dest = fopen(argv[2], "w");
    while ((ch = fgetc(src)) != EOF) {
        fputc(ch, dest);
    }
    fclose(src);
    fclose(dest);
    return 0;
}

## Problem 3
#include <stdio.h>

int main(void) {
    FILE \*fp;
    fp = fopen("f.txt", "w");
    if (fp == NULL) {
        printf("Error: f.txt does not exist\n");
        return 1;
    }
    printf("File truncated successfully\n");
    fclose(fp);
    return 0;
}
