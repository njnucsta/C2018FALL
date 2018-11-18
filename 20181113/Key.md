1.
```c
int is_sorted(int arr[], int left, int right) {
	for ( ; left < right; ++left)
		if (arr[left] > arr[left + 1])
			return -1; // not sorted
	return 0; // sorted
}
```
注意是非降序

2.
```c
void swap(int arr[], int i, int j) {
	int temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}//交换数组中两个元素的值
void BubbleSort(int arr[], int left, int right) {
	int i, j;
	for (i = 1; i <= right - left; ++i) {
		for (j = left; j <= right - i; ++j) {
			if (arr[j] > arr[j + 1])
				swap(arr, j, j + 1);
		}
	}
}
```

3.
递归版本
```c
int binary_search_recursive(int arr[], int left, int right, int query) {
	int mid;
	if (left > right)
		return -1;
	mid = left + (right - left) / 2;
	if (arr[mid] == query)
		return mid;
	if (arr[mid] > query)
		return binary_search_recursive(arr, left, mid - 1, query);
	return binary_search_recursive(arr, mid + 1, right, query);
}
```
迭代版本
```c
int binary_search_iterative(int arr[], int left, int right, int query) {
	int mid;
	while (left <= right) {
		mid = left + (right - left) / 2;
		if (arr[mid] == query)
			return mid;
		if (arr[mid] > query)
			right = mid - 1;
		else
			left = mid + 1;
	}
	return -1;
}
```
需注意递归版本的递归终止条件，循环版本的循环判断条件。
另外，在对mid的计算时，我使用的是：
`mid = left + (right - left) / 2;`
而非：
`mid = (left + right) / 2;`
这样做是为了避免left + right的整型溢出风险。
另外，须注意，这种二分查找的实现仅适用于当数组arr是严格升序时的情形。

4.
```c
void InsertionSort(int arr[], int left, int right) {
	int i, j, temp;
	for (i = left + 1; i <= right; ++i) {
		temp = arr[i];
		for (j = i - 1; j >= left && temp < arr[j]; --j)
			arr[j + 1] = arr[j];
		arr[j + 1] = temp;
	}
}
```
注意，这种插入排序的实现，在寻找插入位置时是线性查找。所以，我们也可以使用二分查找的方法来寻找插入位置，这是对插入排序的一个优化方式。

5.
```c
void SelectionSort(int arr[], int left, int right) {
	int i, j, minIdx;
	for (i = left; i < right; ++i) {
		minIdx = i;
		for (j = i + 1; j <= right; ++j)
			if (arr[j] < arr[minIdx])
				minIdx = j;
		swap(arr, i, minIdx);
	}
}
```
swap同第2题。

6.
```c
void k_reverse(char* str, int k) {
	int len = strlen(str);
	int i, left, right;
	char temp;
	for (i = 0; i + k <= len; i += k) {
		for (left = i, right = left + k - 1;
		        left < right; ++left, --right) {
			temp = str[left];
			str[left] = str[right];
			str[right] = temp;
		}
	}
}
```
最后不足 k 个的字符不用反转

7.
```c
#include <stdio.h>
#include <string.h>
#define N 100000
void add(int num1[], int len1, int num2[], int len2, int sum[], int* len) {
	int i = 0, mod = 0, temp;
	while (i < len1 && i < len2) {
		temp = num1[i] + num2[i] + mod;
		sum[i++] = temp % 10;
		mod = temp / 10;
	}
	while (i < len1) {
		temp = num1[i] + mod;
		sum[i++] = temp % 10;
		mod = temp / 10;
	}
	while (i < len2) {
		temp = num2[i] + mod;
		sum[i++] = temp % 10;
		mod = temp / 10;
	}
	if (mod > 0)
		sum[i++] = mod;
	*len = i;
}
void to_arr(const char* str, int arr[], int len) {
	int i;
	for (i = 0, --len; len >= 0; ++i, --len)
		arr[i] = str[len] - '0';
}
int main() {
	char str1[N], str2[N];
	int num1[N], num2[N], sum[N];
	int len1, len2, len;
	scanf("%s%s", str1, str2);
	len1 = strlen(str1);
	len2 = strlen(str2);
	to_arr(str1, num1, len1);
	to_arr(str2, num2, len2);
	add(num1, len1, num2, len2, sum, &len);
	return 0;
}
```

8.
```c
#include <stdio.h>
#define N 25
int main() {
	int spiral_matrix[N][N];
	int n, i;
	int row = 1, col = 1, val = 1;
	scanf("%d", &n);
	for (i = 1; i <= (n + 1) / 2; ++i) {
		while (col <= n - i + 1)
			spiral_matrix[row][col++] = val++;
		--col;
		while (row <= n - i)
			spiral_matrix[++row][col] = val++;
		while (col > i)
			spiral_matrix[row][--col] = val++;
		while (row > i + 1)
			spiral_matrix[--row][col] = val++;
		++col;
	}
	return 0;
}
```
for循环的每一次迭代填充矩阵的一整圈，其中，i用来控制圈数。

10.
```c
int my_strlen(const char* str) {
	if (str == NULL)
		return 0;
	int len;
	for (len = 0; str[len]; ++len);
	return len;
}
```

11.
```c
void my_strcpy(char* dest, const char* src) {
	assert(dest != NULL);
	assert(src != NULL);
	while (*src)
		*dest++ = *src++;
	*dest = 0;
}
```

12.
```c
int my_strcmp(const char* str1, const char* str2) {
	assert(str1 != NULL);
	assert(str2 != NULL);
	while (*str1 && *str2) {
		if (*str1 == *str2) {
			++str1;
			++str2;
		} else
			return *str1 > *str2 ? 1 : -1;
	}
	return *str1 ? 1: (*str2 ? -1 : 0);
}
```

15.
```c
#include <stdio.h>
int main(int argc, char* argv[]) {
	FILE* fp;
	int ch;
	if (argc != 2) {
		printf("Error in format. Usage: show file\n");
		return 1;
	}
	if ((fp = fopen(argv[1], "r")) == NULL) {
		printf("The file <%s> can not be opened.\n", argv[1]);
		return 2;
	}
	ch = fgetc(fp);
	while (ch != EOF) {
		putchar(ch);
		ch = fgetc(fp);
	}
	fclose(fp);
	return 0;
}
```

16.
```c
#include <stdio.h>
int main(int argc, char* argv[]) {
	int ch;
	FILE* srcfp, *destfp;
	if (argc != 3) {
		printf("Error in format. Usage: copy source destination\n");
		return 1;
	}
	if ((srcfp = fopen(argv[1], "r")) == NULL) {
		printf("The file <%s> can not be opened.\n", argv[1]);
		return 2;
	}
	if ((destfp = fopen(argv[2], "w")) == NULL) {
		printf("The file <%s> can not be opened.\n", argv[2]);
		return 2;
	}
	ch = fgetc(srcfp);
	while (ch != EOF) {
		fputc(ch, destfp);
		ch = fgetc(srcfp);
	}
	fclose(srcfp);
	fclose(destfp);
	return 0;
}
```
