
## Problem 1:
#include <unistd.h>
#include <fcntl.h>
#include <stdio.h>

int main() {
    int fd;
    fd = open("f.txt", O_WRONLY | O_TRUNC);
    if (fd == -1) {
        write(1, "Error: f.txt does not exist\n", 29);
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

## Problem 4
#include <stdio.h>

int main(void) {
    FILE \*fp;
    char buf[100];
    fp = fopen("file1.txt", "a");
    fclose(fp);
    fp = fopen("file1.txt", "a");
    fprintf(fp, "Alice\n");
    fclose(fp);
    fp = fopen("file1.txt", "r");
    while (fgets(buf, sizeof(buf), fp) != NULL)
        printf("%s", buf);
    fclose(fp);
    return 0;
}

## Problem 5
#include <stdio.h>

int main(int argc, char \*argv[]) {
    FILE \*fp = fopen(argv[1], "r");
    int x, i;
    float num, sum = 0.0;
    fscanf(fp, "%d", &x);
    for (i = 0; i < x; i++) {
        fscanf(fp, "%f", &num);
        sum += num;
    }
    printf("%.2f\n", sum);
    fclose(fp);
    return 0;
}

## Problem 6
#include <stdio.h>

int main(void) {
    FILE \*fp = fopen("db.txt", "r");
    char first[50], last[50];
    int salary, count = 0, sum = 0;
    while (fscanf(fp, "%s %s %d", first, last, &salary) == 3) {
        sum += salary;
        count++;
    }
    printf("Average salary: %.2f\n", (float)sum / count);
    fclose(fp);
    return 0;
}

## Problem 7
