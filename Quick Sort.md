# Quick Sort
## code
```c
#include<stdio.h>
typedef double arrType;

void initialArr(arrType* arr, int* length);
void showArr(arrType* arr, int length);
void swap(arrType* a, arrType* b);
int partition(arrType* arr, int low, int high);
void quickSort(arrType* arr, int low, int high);

int main() {
	int length = 0;
	arrType arr[1000];
	initialArr(arr, &length);
	printf("The array before sorting:");
	showArr(arr, length);
    quickSort(arr, 0, length-1);
	printf("The sorted array:");
	showArr(arr, length);
}

void initialArr(arrType* arr, int* length) {
	double val;
	printf("Enter the elements of the array strictly in descending order：");
	while (scanf("%lf", &val) != EOF) {
		arr[(*length)++] = val;
	}
}

void showArr(arrType* arr, int length) {
	for (int i = 0; i < length; i++) {
		printf("%g ", arr[i]);
	}
	printf("\n");
}

void swap(arrType* a, arrType* b) {
    arrType temp = *a;
    *a = *b;
    *b = temp;
}

int partition(arrType* arr, int low, int high) {
    arrType pivot = arr[high];
    int i = low - 1;
    for (int j = low; j <= high - 1; j++) {
        if (arr[j] <= pivot) {
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}

void quickSort(arrType* arr, int low, int high) {
    if (low < high) {
        int pi = partition(arr, low, high);
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

## test
test1:
输入：
```
99.99 98.76 98.75 95.6 95.6 93.2 90.2
```
输出：
```
The array before sorting:99.99 98.76 98.75 95.6 95.6 93.2 90.2
The sorted array:90.2 93.2 95.6 95.6 98.75 98.76 99.99
```
test2:
输入：
```
4 3 2 1
```
输出：
```
The array before sorting:4 3 2 1
The sorted array:1 2 3 4
```
test3:
输入：
```
10 9 8 7 6 5 4 3 2 1
```
输出：
```
The array before sorting:10 9 8 7 6 5 4 3 2 1
The sorted array:1 2 3 4 5 6 7 8 9 10
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEwMzcxNzE0NzVdfQ==
-->