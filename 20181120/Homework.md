1. 奇约数问题。
```
题目描述：定义函数f(x)为x最大的奇数约数，其中，x为正整数。例如：f(44)=11。现给出整数N，请求出f(1)+f(2)+⋯+f(N)。例如，若N为7，则f(1)+f(2)+f(3)+f(4)+f(5)+f(6)+f(7)=1+1+3+1+5+3+7=21。
```
```
输入：输入一个正整数N(1≤N≤1000000000)。
```
```
输出：输出一个整数，即f(1)+f(2)+⋯+f(N)。
```
```
样例输入：
7
样例输出：
21
```
（注：程序命名为1.c）。

2. 写一个函数，函数声明如下：
```c
int bin_insert(int n, int m, int j, int i);
```
接受两个32位整数n和m，实现将m的二进制数位插入到n的二进制的第j到第i位，其中二进制的位数从低位数到高位且以0开始。返回操作后的数，保证n的第j到第i位均为零，且m的二进制位数小于等于i-j+1。举例来说，当n、m、j、i分别为1024、19、2、6时，返回1100。在主函数中调用该函数，并进行多组测试，以验证你的函数（注：程序命名为2.c）。

3. 写一个函数，函数声明如下：
```c
int sum(int n);
```
接受正整数n，求1+2+3+…+n。要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。在主函数中调用该函数，并进行多组测试，以验证你的函数（注：程序命名为3.c）。

4. 写一个函数，函数声明如下：
```c
int add(int n1, int n2);
```
接受两个整数n1和n2（未必为正整数），求n1和n2之和。要求不得使用`+、-、*、/`四则运算符号。在主函数中调用该函数，并进行多组测试，以验证你的函数（注：程序命名为4.c）。

5. 写一个函数，函数声明如下：
```c
int substr(const char* str, const char* substr);
```
接受两个字符串str和substr，其中，str为主串，substr为子串。返回substr在str中第一次出现的位置（数组下标）；若substr尚未在str中出现，则返回-1。例如，若str为"I dislike C"，substr为"like"，则返回5；若str为"I dislike C"，substr为"love"，则返回-1。在主函数中调用该函数，并进行多组测试，以验证你的函数（注：程序命名为5.c）。

6. 写一个函数，函数声明如下：
```c
int count_substr(const char* str, const char* substr);
```
接受两个字符串str和substr，其中，str为主串，substr为子串。返回substr在str中出现的次数。注意，"hh"在"hhh"中仅出现一次，而非两次；"hh"在"hhhh"中出现两次；"h"在"hhh"中出现三次；"sos"在"sososos"中仅出现两次，而非三次。在主函数中调用该函数，并进行多组测试，以验证你的函数（注：程序命名为6.c）。

排序和查找是程序设计中重要的内容。在上次（20181113）作业中，我们对排序和查找做了一些练习。这次作业，我们继续练习排序和查找。

7. 实现归并排序。函数声明如下：
```c
void MergeSort(int arr[], int left, int right);
```
该函数接受三个参数，实现选择排序的功能（升序排序）。参数的意义及要求同上次（2011113）作业第2题。你可以参阅[百度百科](https://baike.baidu.com/item/%E5%BD%92%E5%B9%B6%E6%8E%92%E5%BA%8F/1639015?fr=aladdin)
或[维基百科](https://en.wikipedia.org/wiki/Merge_sort)
关于归并排序的讲解，看懂排序的过程，并自己实现。建议参阅维基百科，讲解更为详细，且有图解。如果你对英语头大，可切换到中文模式。
（注：程序命名为7.c）。

8. 学会使用库函数qsort。
qsort是定义在头文件stdlib.h中的一个排序函数，它使用快速排序的方式。qsort的命名来自“quick sort”，即快速排序。你现在无须知道快速排序的实现细节，你只需学会使用这个函数即可。你可以参阅[百度百科](https://baike.baidu.com/item/qsort/4747970?fr=aladdin)
或[cppreference](http://en.cppreference.com/w/c/algorithm/qsort)
中关于qsort的讲解。学会使用qsort，并实现以上cppreference链接中的例子。（注：程序命名为8.c）。

9. 学会使用库函数bsearch。
bsearch是定义在头文件stdlib.h中的一个查找函数，它使用二分查找的方式。bsearch的命名来自“binary search”，即二分查找。你已经清楚了二分查找的实现，如果你感兴趣，可以阅读bsearch的实现源码，以加深理解。你可以参阅[百度百科](https://baike.baidu.com/item/bsearch/10931422?fr=aladdin)
或[cppreference](http://en.cppreference.com/w/c/algorithm/bsearch)
中关于bsearch的讲解。学会使用bsearch，并实现以上cppreference链接中的例子。（注：程序命名为9.c）。

10. 学习malloc、ralloc、calloc、free的用法。你可以阅读教材中的内容，也可以上网通过百度、谷歌、知乎等查阅相关的资料与博客，以加深对动态内存分配的理解（注：此题无须写程序）。

做了这么多紧张刺激的编程题，你可能已经感到烦躁了。让我们来几道轻松舒坦的语法练习题换个口味。

语法练习题

要求：

（1）对于以下几道语法练习题，请给出答案，并给出每一题对应的解释，写在一个文本文件中，命名为exercise.md，与c语言代码一起提交。

（2）你应当通过肉眼观察即给出答案，而不能写程序运行以获得结果；当然，在你完成后，你可以写程序运行以验证你的答案。

（3）语法练习题与编程题同样重要，请认真对待，并确保弄懂每一题。

1. 执行C程序代码：
```c
int a = 1;
int b = 0;
int c = 0;
int d = (++a) * (c = 1);
```
a，b，c，d的值分别为（）。

2. 下面程序输出结果为（）。
```c
#include <stdio.h>
#define SUB(X,Y) (X)*Y
int main() {
	int a = 3, b = 4;
	printf("%d", SUB(a++, ++b));
	return 0;
}
```

3. 下列代码的输出结果是（）。
```c
int i = -1;
unsigned j = 1;
if (j > i)
	printf("j > i");
else
	printf("i > j");
```

4. 下列代码的输出结果是（）。
```c
int a[5] = {1, 2, 3, 4, 5};
int* ptr = (int *)(&a + 1);
printf("%d, %d", *(a + 1), *(ptr - 1));
```

5. 下列代码的输出结果是（）。
```c
int arr[][3] = {10, 20, 30, 40, 50, 60};
int (*p)[3];
p = arr;
printf("%d, %d, %d", p[0][0], *(p[0] + 1), (*p)[2]);
```

6. 下列代码的输出结果是（）。
```c
char str[] = "ABCD", *p = str;
printf("%d", *(p + 4));
```

7. 设a、b、c、d、m、n均为int型变量，且a = 5、b = 6、c = 7、d = 8、m = 2、n = 2。则逻辑表达式(m = a > b) && (n = c > d)运算后，n的值为（）。

8. 定义char dog[] = "wang\0miao";那么sizeof(dog)与strlen(dog)分别是多少（）。

9. 下列代码的输出结果是（）。
```c
unsigned char *p1;
unsigned long *p2;
p1 = (unsigned char *)0x801000;
p2 = (unsigned long *)0x810000;
printf("%p, %p", p1 + 5, p2 + 5);
```

10. 如下函数的func(1)值为（）。
```c
int func(int n) {
	static int i = 1;
	if (n >= 5)
		return n;
	n = n + i;
	i++;
	return func(n);
}
```

注：作业提交到自己仓库的`19180xxx/20181120`目录下。截止日期：`2018.11.27-00:00:00`（零点）。
