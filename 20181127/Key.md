1. 
```c
struct Node* construct(int arr[], int size) {
	int i;
	struct Node head;
	struct Node *prev, *p;
	head.next = NULL;
	prev = &head;
	for (i = 0; i < size; ++i) {
		p = (struct Node* )malloc(sizeof(struct Node));
		p->val = arr[i];
		p->next = NULL;
		prev->next = p;
		prev = p;
	}
	return head.next;
}
```
***
2. 
```c
struct Node* insert_to_head(struct Node* head, int val) {
	struct Node* newhead = (struct Node* )malloc(sizeof(struct Node));
	newhead->val = val;
	newhead->next = head;
	return newhead;
}
```
***
3.
```c
struct Node* insert_to_tail(struct Node* head, int val) {
	struct Node* tail = (struct Node* )malloc(sizeof(struct Node));
	struct Node* p;
	tail->val = val;
	tail->next = NULL;
	if (head == NULL)
		return tail;
	for (p = head; p->next; p = p->next);
	p->next = tail;
	return head;
}
```
***
4.
```c
struct Node* insert(struct Node* head, int val) {
	struct Node* node = (struct Node* )malloc(sizeof(struct Node));
	struct Node* prev = NULL;
	struct Node* p = head;
	node->val = val;
	node->next = NULL;
	while (p && p->val <= val) {
		prev = p;
		p = p->next;
	}
	if (prev == NULL) {
		node->next = head;
		return node;
	}
	prev->next = node;
	node->next = p;
	return head;
}
```
***
5. 
```c
struct Node* delete_node(struct Node* head, struct Node* target) {
	struct Node* prev = NULL;
	struct Node* p = head;
	struct Node* post;
	while (p) {
		post = p->next;
		if (p == target) {
			if (prev == NULL) {
				free(p);
				return post;
			}
			prev->next = post;
			free(p);
			return head;
		}
		prev = p;
		p = post;
	}
	return head;
}
```
***
6.
```c
struct Node* delete_val(struct Node* head, int val) {
	struct Node* prev = NULL;
	struct Node* p = head;
	struct Node* post;
	while (p) {
		post = p->next;
		if (p->val == val) {
			if (prev == NULL) {
				head = post;
				free(p);
			} else {
				prev->next = post;
				free(p);
			}
			p = post;
		} else {
			prev = p;
			p = post;
		}
	}
	return head;
}
```
***
7.
```c
struct Node* reverse(struct Node* head) {
	struct Node* prev = NULL;
	struct Node* p = head;
	struct Node* post;
	while (p) {
		post = p->next;
		p->next = prev;
		prev = p;
		p = post;
	}
	return prev;
}
```
***
8.
```c
struct Node* merge(struct Node* head1, struct Node* head2) {
	struct Node *p1 = head1, *p2 = head2;
	struct Node head;
	struct Node *prev, *p;
	head.next = NULL;
	prev = &head;
	while (p1 && p2) {
		p = (struct Node* )malloc(sizeof(struct Node));
		p->next = NULL;
		if (p1->val <= p2->val) {
			p->val = p1->val;
			p1 = p1->next;
		} else {
			p->val = p2->val;
			p2 = p2->next;
		}
		prev->next = p;
		prev = p;
	}
	while (p1) {
		p = (struct Node* )malloc(sizeof(struct Node));
		p->next = NULL;
		p->val = p1->val;
		p1 = p1->next;
		prev->next = p;
		prev = p;
	}
	while (p2) {
		p = (struct Node* )malloc(sizeof(struct Node));
		p->next = NULL;
		p->val = p2->val;
		p2 = p2->next;
		prev->next = p;
		prev = p;
	}
	return head.next;
}
```
***
9.
```c
void clear(struct Node* head) {
	struct Node* p;
	while (head) {
		p = head;
		head = head->next;
		free(p);
	}
}
```
***
10.
```c
int Merge(int arr[], int left, int mid, int right) {
	int size = right - left + 1;
	int* temparr = (int*)malloc(size * sizeof(int));
	int i = left, j = mid + 1, k = 0;
	int cnt = 0;
	while (i <= mid && j <= right) {
		if (arr[i] <= arr[j])
			temparr[k++] = arr[i++];
		else {
			temparr[k++] = arr[j++];
			cnt += mid - i + 1;
		}
	}
	while (i <= mid)
		temparr[k++] = arr[i++];
	while (j <= right)
		temparr[k++] = arr[j++];
	memcpy(arr + left, temparr, size * sizeof(int));
	free(temparr);
	return cnt;
}
int MergeSort(int arr[], int left, int right) {
	int mid = left + (right - left) / 2;
	int cnt = 0;
	if (left >= right)
		return cnt;
	cnt += MergeSort(arr, left, mid);
	cnt += MergeSort(arr, mid + 1, right);
	cnt += Merge(arr, left, mid, right);
	return cnt;
}
```
在归并排序的基础上稍作修改即可，函数MergeSort 的返回值即为数组arr 逆序对的个数
***
语法练习题：
1. （0）。
***
2. （0，1）。
***
3. （D）。

解释：

++的优先级比*高，所以D 中p++先执行，p 指向的地址改变了，所以year 的内容没有变化。
***
4. （9）。
***
5. （C）。

解释：

* 知识点1：函数指针变量。

函数指针变量的声明方法为：返回值类型 ( * 指针变量名) ([形参列表]);

根据定义，
```c
int (*pf)(float);
int (*p)(float) = &f1;
```
pf，p 都是函数指针变量。

* 知识点2：函数地址。

C 在编译时，每一个函数都有一个入口地址，该入口地址就是函数指针所指向的地址。

函数地址的获取，可以是函数名，也可以在函数名前加取地址符&。

（C） 错误是因为函数形参类型不匹配。
***
6. （Bejing）。
***
7. （D）。

解释：

str 为一个指针，但实际上为int 类型，传入函数内部并不会发生任何改变。

GetMemory 函数执行完成后，str 仍然指向NULL，所以赋值时会奔溃。

正确的做法应该使用双指针，如下：
```c
void GetMemeory(char **p) {
	*p = (char *)malloc(100);
}
void Test() {
	char *str = NULL;
	GetMemeory(&str);
	strcpy(str, "Thunder");
	strcat(str + 2, "Downloader");
	printf("%s", str);
}
```
***
8. （B）。

解释：
```c
typedef char T[10] ;
T * a ;
```
这里T 是什么类型呢，把名字抹去不就是类型了吗？char [10]，T 为一个char 数组。

那么T * a 中a是什么类型呢，T * ，T 为数组，是一个整体，a 为指向这个数组的一个指针喽。也就是a 为指向一个10个元素的数组的指针。

首先，a是指针，不是数组，而且a是指向数组的指针，不仅仅是指针。所以A，C 排除了。那么剩下两项B，D.
```c
char (*a) [10] ;
char *a [10] ;
```

这里就是一个优先级的问题了，[]优先级要高于解引用运算符。所以第一个a 为指针，指向具有十个char 元素的指针。第二个为数组，每个元素都是指针，每个指针指向一个char 变量。

这就是函数指针和函数也有类似的问题。分析优先级即可游刃而解。
***
9. （14）。

解释：

X & (X - 1); 统计X 的二进制中1 的个数；

X | (X + 1); 统计X 的二进制中0 的个数；
***
10. （AB）。

解释：

C 编译器不做数组越界检查。

MAX 为255。

数组A 的下标范围为：0..MAX-1,这是其一。

其二，当i 循环到255 时,循环内执行：A[255] = 255;
这句本身没有问题。但是返回for (i = 0; i<= MAX; ++i)语句时,

由于unsigned char 的取值范围在[0, 255]，++i 以后i 又为0 了。无限循环下去。
