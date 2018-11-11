8.
```c
#include <stdio.h>
int main()
{
    int n = 10;
    int flag = n & 1;
    printf("%d\n", flag);
    return 0;
}
```


10.
```c
#include <stdio.h>
int main()
{
    int a, b;
    scanf("%d%d", &a, &b);
    printf("a = %d, b = %d\n", a, b);
    //第1种方法
    int temp = a;
    a = b;
    b = temp;
    printf("a = %d, b = %d\n", a, b);
    //第2种方法
    a = a ^ b;
    b = a ^ b;
    a = a ^ b;
    printf("a = %d, b = %d\n", a, b);
    return 0;
}
```
