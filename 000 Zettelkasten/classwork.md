

#include <stdio.h>

int main(void) {
	char str[5] = {'h', 'e', 'l', 'l', 'o'};
	printf("%s\n", str);
	return 0;
}

#include <stdio.h>

int main(void) {
	int a[] = {1,2,3};
	int b[] = {4,5,6};
	int c = a[0]*b[0] + a[1]*b[1] + a[2]*b[2];
	printf("%d\n", c);
	return 0;
}

#include <stdio.h>

struct hrdb {
	char name[20];
	int age;
	int salary;
};
int main(void) {
	struct hrdb employees[2] = {{"Alice", 32, 2000}, {"Bob", 23, 1800}};
	return 0;
}