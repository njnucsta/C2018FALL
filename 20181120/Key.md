1.
```c
#include <stdio.h>
long long sum(long long i) {
	long long cnt;
	if (i & 1)
		cnt = (i + 1) >> 1;
	else {
		cnt = i >> 1;
		--i;
	}
	return (1 + i) * cnt / 2;
}
int main() {
	int n;
	scanf("%d", &n);
	long long res = 0;
	while (n) {
		res += sum(n);
		n >>= 1;
	}
	printf("%lld", res);
	return 0;
}
```
𝑓(x)为x最大的奇数约数，则显然，x为奇数时，𝑓(x)=x；x为偶数时，x最大的两个约数分别为x与𝑥2，故此时，𝑓(x)=𝑥2。那么， 𝑓(1)+𝑓(2)+⋯+𝑓(𝑁)=1+𝑓(1)+3+𝑓(2)+5+𝑓(3)+⋯
可以把上式分为两部分，一部分是奇数值构成的等差数列，这部分可以直接利用求和公式计算出来；另一部分是偶数折半后的最大奇约数，重复同样的过程即可。
代码中的函数sum是完成一次上述的过程。

2.
```c
int bin_insert(int n, int m, int j, int i) {
	m <<= j;
	n |= m;
	return n;
}
```
3.
```c
int sum(int n) {
	n && (n += sum(n - 1));
	return n;
}
```
这里用到了短路求值

4.
```c
int add(int n1, int n2) {
	if (n2 > 0) {
		for (int i = 1; i <= n2; ++i)
			++n1;
	} else if (n2 < 0) {
		for (int i = -1; i >= n2; --i)
			--n1;
	}
	return n1;
}
```
5.
```c
int find(const char* str, const char* substr) {
	int i, j, k;
	for (i = 0; str[i]; ++i) {
		for (k = i, j = 0; str[k] && substr[j]
		        && str[k] == substr[j]; ++k, ++j);
		if (!substr[j])
			return i;
	}
	return -1;
}
```
原题中函数名为substr，与该函数的第二个形参命名相同，虽为发生命名冲突，但这其实不是一个很好的习惯。我在出题时疏忽了，特此将该函数名更正find。即在主串str中查找字串substr，并返回其第一次出现的位置；若为查找到，则返回-1。
这是一道字符串匹配题。我在此处用的是普通的匹配方式，即试探所有的情况。此题另有更好的做法，叫做KMP算法。感兴趣的同学可以参考
[百度百科](https://baike.baidu.com/item/KMP/10158450?fr=aladdin)
或[维基百科](https://en.wikipedia.org/wiki/Knuth%E2%80%93Morris%E2%80%93Pratt_algorithm)

6.
```c
int count_substr(const char* str, const char* substr) {
	int i, j, k;
	int cnt = 0;
	for (i = 0; str[i]; ) {
		for (k = i, j = 0; str[k] && substr[j]
		        && str[k] == substr[j]; ++k, ++j);
		if (!substr[j]) {
			++cnt;
			i = k;
		} else
			++i;
	}
	return cnt;
}
```
可以使用更好的KMP算法

7.
```c
void Merge(int arr[], int left, int mid, int right) {
	int size = right - left + 1;
	int* temparr = (int*)malloc(size * sizeof(int));
	int i = left, j = mid + 1, k = 0;
	while (i <= mid && j <= right) {
		if (arr[i] <= arr[j])
			temparr[k++] = arr[i++];
		else
			temparr[k++] = arr[j++];
	}
	while (i <= mid)
		temparr[k++] = arr[i++];
	while (j <= right)
		temparr[k++] = arr[j++];
	memcpy(arr + left, temparr, size * sizeof(int));
	free(temparr);
}
void MergeSort(int arr[], int left, int right) {
	int mid = left + (right - left) / 2;
	if (left >= right)
		return;
	MergeSort(arr, left, mid);
	MergeSort(arr, mid + 1, right);
	Merge(arr, left, mid, right);
}
```
（非降序）序列，其中arr[left .. mid]与arr[mid + 1 .. right]均已有序（非降序）。
我用到了malloc函数进行动态内存分配。而有些同学在此处，可以会写为：
```c
int temparr[right – left + 1];
```
虽然这个写法在使用gcc编译器进行编译时不会出现编译错误，甚至在运行时也几乎不会出现运行时错误，但我建议还是慎用这种写法。出于以下两点理由：
其一，这个特性叫变长数组。我们知道，C语言在定义数组时，数组的长度应当是一个常量，或者说，编译期常量，即，在编译期就已经确定了其值，也就是说，在编译完成后，编译器须要知道某一数组的具体大小，这样才能在程序运行时为函数栈分配确定的空间。不过，变长数组是C99的一个新特性，也就是说，C语言标准支持这种写法。然而，未必所有的C语言编译器都实现了这个特性，我们目前所使用的gcc的确是支持变长数组，但换一个编译器，就可能出现编译错误。
其中，C99标准是ISO/IEC 9899:1999 - Programming languages -- C的简称，是C语言的官方标准第二版，与1999年发布。你可以了解有关[C99](https://baike.baidu.com/item/c99/7335191?fr=aladdin)
的内容。
其二，这种写法存在一个问题，就是，当该变长数组的长度过大时，在这个例子中，即，当right – left + 1过大时，可能会超出一个栈的最大可分配空间，这样就造成了运行时错误。
所以，慎用变长数组这一特性。使用动态内存分配是一个更安全更妥善的方法。当然，在使用动态分配的内存完毕后，应当使用free来释放内存，否则就造成了内存泄漏。你可以了解有关[内存泄露](https://baike.baidu.com/item/%E5%86%85%E5%AD%98%E6%B3%84%E6%BC%8F/6181425?fr=aladdin)
的内容。
另外，我用到了memcpy函数，实现将数组temparr中的内容拷贝到数组arr中。它在语义逻辑上等价于：
```c
for (i = left, k = 0; i <= right; ++i)
	arr[i++] = temparr[k++];
```
memcpy的使用方法可以参考[百度百科](https://baike.baidu.com/item/memcpy/659918?fr=aladdin)
或[cppreference](http://en.cppreference.com/w/c/string/byte/memcpy)

8.
提供一篇[博客](http://blog.csdn.net/xyt8023y/article/details/47419493)
供参考。
以上三题均较难，我所提供的题解均是用C++语言实现的，不过其大部分的写法同C。另外，解体思路也值得参考。

语法练习题：
1.（2，0，1，2）。
2.（15）。
3.（i > j）。
解释如下：
表达式会包含隐式类型转换，它由编译器自动执行，不需程序员介入。
何时发生隐式类型转换：
（1）在混合类型的表达式中，操作数会被转换为相同类型，如：
```c
int ival;
double dval;
ival >= dval; // ival converted to double
```
（2）条件表达式会被转换为bool类型，如：
```c
int ival;
if (ival) // ival converted to bool
```
条件操作符（? :）中的第一个操作数，逻辑非（!）、逻辑与（&&）、逻辑或（||）的操作数都是条件表达式。if、while、do while、以及for的第2个表达式都是条件表达式。
（3）初始化和赋值，如：
```c
int ival = 3.14 // 3.14 converted to int
int *ip;
ip = 0; // the int 0 converted to a null pointer of type int *
```
（4）在函数调用时，所传递的参数也可能发生隐式类型转换。
如何转换：
（1）算术转换
算术转换保证在执行操作前，将二元操作符的两个操作数转换为同一类型，并使表达式的值也具有相同的类型。
算术转换通常的是做提升（integral promotion），对于所有比int小的整型，包括char、signed char、unsigned char、short和unsigned short，如果该类型的所有可能的值都能包含在int内，它们就会被提升为int，否则被提升为unsigned int。如果将bool值提升为int，则false转换为0，true转换为1。
包含short和int类型的表达式，short转换为int。如果int足以表示所有unsigned short类型的值，则将unsigned short转换为int，否则两个操作数均转换为unsigned int。long和unsigned int的转换也一样。只要机器上的long足够表示unsigned int类型所有的值，就将unsigned int转换为long，否则两个操作数都转换为unsigned long。在32位的机器上，long和int通常用一个字长表示，此时如果表达式包含unsigned int和long，两者都转换为unsigned long。
如果表达式包含signed和unsigned int，signed会被转换为unsigned。如果int 操作数的值恰为负数，其转换为unsigned int可能会变为一个很大的正数（转换结果是该负值对unsigned int的取值个数求模）。所以最好避免对int和unsigned int的两个操作数进行比较。
转换示例：



（2）其他隐式转换
1）数组名转换为指向其第一个元素的指针，如：
```c
int ia[10]; // array of 10 ints
int *ip = ia; // convert ia to pointer to first element
```
另外，任意数据类型的指针都可转换为void *，整形数值常量0可以转换为任意类型指针。
2）指针值可转换为bool
如果指针为0，转换为false，否则转换为true。如：
```c
if (cp) // true if pointer cp is not zero
```
3）算术类型与bool的转换
算术类型转换为bool时，0转换为false，其他值（包括负值）转换为true。将bool转换为算术类型时，true转换为1，false转换为0。
4）转换与枚举类型
枚举类型对象或枚举成员将自动转换为整型，其转换结果可以用于任何需要使用整数值的地方。具体会被转换为哪种整型，依赖于枚举成员的最大值和机器。enum对象或枚举成员至少提升为int，如果int无法表示枚举成员的最大值，则提升到能表示所有枚举成员值的、大于int型的最小类型（unsigned int 、long或unsigned long）。
4.（2, 5）。
解释如下：
数组名就是数组0号元素的地址，即a = &a[0]。
&a是指向一个有5个整型元素的数组的地址。a是一维指针，&a相当于是二维指针。&a+1就是从a向后跳过一个完整的数组所占用的内存空间。整型5个元素的数组占用5*sizeof(int)=5*4=20，所以&a+1应该从a向后跳20字节。正好指到a[4]的后面。ptr是int *，减1就是向前跳4个字节，ptr-1正好指向a[4]。
5.（10, 20, 30）。
解释如下：
int (*p)[3]，这里首先确定：p是一个指针，一个指向数组的指针。
p = &(p[0])，p是二维指针。
p[0] = &(p[0][0])，p[0]是一维指针。
p[0] + 1表示在列上移动。e.g.，p[0] + 1 = &p[0][0] + 1 = &p[0][1]。
p + 1表示在行上移动。e.g.，p + 1 = &(p[0]) + 1 = &p[1]。
因此：
*(p[0]+1) = p[0][1] = 20。
(*p)[2] = p[0][2] = 30。
6.（0）。
解释如下：
char str[] = "ABCD"; 相当于：
str[0] = 'A';
str[1] = 'B';
str[2] = 'C';
str[3] = 'D';
str[4] = '\0';
而*(p + 4) == str[4]，'\0'的ASCII为0，故输出0。
7.（2）。
解释如下：
注意短路求值。逻辑与或者逻辑或的表达式，先是判断一边，若一边可以判断整个表达式为真假时，另一边不再执行。
8.（10，4）。
解释如下：
sizeof返回数组所占的字节数，'wang' 'miao'共占8字节，显式'\0'占1字节，字符串末尾隐式'\0'占1字节，共10字节。
strlen返回字符串的长度，以遇到'\0'结束符为准，因此为4。
另外，对于指针，sizeof操作符返回这个指针占的空间，一般是4个字节；而对于一个数组，sizeof返回这个数组所有元素占的总空间,包括结束符'\0'。char*与char[]容易混淆，一定要分清。
strlen不区分是数组还是指针，就读到'\0'为止返回长度。而且strlen是不把'\0'计入字符串的长度的 。
9.（00801005, 00810014）。
解释如下：
p1指向字符型，一次移动一个字符型，1个字节；p1+5后移5个字节，16进制表示为5；p2指向长整型，一次移动一个长整型，4个字节，p2+5后移20字节，16进制表示为14。
另外，char每次移动1个字节；short移动2个字节 ；int、long、float移动4个字节 ；double移动8个字节。
10.（7）。
解释如下：
该函数为递归调用。
需注意i为静态变量。
f(1)：n=2; i=2;调用f(2)；
f(2)：n=4; i=3;调用f(4)；
f(4)：n=7; i=4;调用f(7)；
f(7)：返回7。
即最终函数返回结果为7。
