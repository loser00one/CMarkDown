
# Binary Search
## code
```c
#include<stdio.h>
typedef double arrType;

void initialArr(arrType* arr, int* length);
void showArr(arrType* arr, int length);
int binarySearch(arrType* arr, int length, int targetNum);

int main() {
	int length = 0;
	double targetNum;
	arrType arr[1000];
	initialArr(arr, &length);
	printf("Enter the element you want to find：");
	scanf("%lf", &targetNum);
	int result = binarySearch(arr, length, targetNum);
	if(result!=-1)
		printf("The subscript of the element you're looking for is:%d", result);
	else {
		printf("This element does not exist\n");
	}
	return 0;
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

int binarySearch(arrType* arr, int length, int targetNum){
	int left = 0;
	int right = length - 1;
	int middle;
	while (left<=right) {
		middle = left + (right - left) / 2;
		if (arr[middle] == targetNum)
			return middle;
		else if (arr[middle] > targetNum)
			right = middle - 1;
		else
			left = middle + 1;
	}
	return -1;
}
```

## test
test1:
输入：
```
1 2 3 4
1
```
输出：
```
0
```
test2:
输入：
```
2 5 7 8 9
9
```
输出：
```
4
```
test3:
输入：
```
1 4 7 9 10
6
```
输出：
```
This element does not exist
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbODE2MDcyMzY1XX0=
-->