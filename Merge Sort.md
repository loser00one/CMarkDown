# Merge Sort
## code
```c
#include<stdio.h>
typedef double arrType;

void initialArr(arrType* arr, int* length);
void showArr(arrType* arr, int length);
void merge(arrType* arr, int left, int mid, int right);
void merge_Sort(arrType* arr, int left, int right);

int main() {
	int length = 0;
	arrType arr[1000];
	initialArr(arr, &length);
	printf("The array before sorting:");
	showArr(arr, length);
    merge_Sort(arr, 0, length - 1);
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

void merge(arrType* arr, int left, int mid, int right) {
    int i, j, k;
    int n1 = mid - left + 1;
    int n2 = right - mid;
    arrType* L = (arrType*)malloc(n1 * sizeof(arrType));
    arrType* R = (arrType*)malloc(n2 * sizeof(arrType));
    for (i = 0; i < n1; i++)
        L[i] = arr[left + i];
    for (j = 0; j < n2; j++)
        R[j] = arr[mid + 1 + j];
    i = 0;
    j = 0;
    k = left;
    while (i < n1 && j < n2) {
        if (L[i] <= R[j])
            arr[k++] = L[i++];
        else
            arr[k++] = R[j++];
    }
    while (i < n1)
        arr[k++] = L[i++];
    while (j < n2)
        arr[k++] = R[j++];
    free(L);
    free(R);
}

void merge_Sort(arrType* arr, int left, int right) {
    if (left < right) {
        int mid = left + (right - left) / 2;
        merge_Sort(arr, left, mid);
        merge_Sort(arr, mid + 1, right);
        merge(arr, left, mid, right);
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
eyJoaXN0b3J5IjpbNzc2Mzk2NzU1XX0=
-->