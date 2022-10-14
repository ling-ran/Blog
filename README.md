# C语言
## 关键字
关键字 |   - |   -   |     -   | -       |    -   |     -    |    -    |
------- | ----- |----- | ------ | ------ |------|---------|--------|
char| short| int| long |float |double| if |else|
return | do| while | for | switch | case | break| continue |
default | goto| sizeof | auto | register | static | extern | unsigned |
signed | typedef| struct | enum | union | void | const | volatile |
-------------------------------------------------------------------------------------------------- 
 -  **register**大量频繁使用的数据，放在寄存器中，提升效率，在数据前加register(可以不加编译器可以识别）
 - **struct**结构体
 - **union**联合体（共用体）
 - **define include**是预处理指令，不是关键词
 - **typedef**
 ```c
 typedef unsigned int un_it
//typedef 顾名思义是类型定义，这里应该理解为类型重命名。
int main()
{
 unsigned int num1 = 1;
 un_it num2 = 1;
 //观察num1和num2,这两个变量的类型是一样的
 return 0;
｝
```
>**static**用来修饰变量和函数的 
> 
1.修饰局部变量   称为静态局部将变量改变局部变量的生命周期，本质上是改变了变量的存储类型。
![static](https://img-blog.csdnimg.cn/a20b1a8782c6457fbdac63ef53e42710.jpeg#pic_center)
```c
//代码1
#include <stdio.h>
void test()
{
    int i = 0;
    i++;
    printf("%d ", i);
}
int main()
{
 int i = 0;
    for(i=0; i<10; i++)
   {
        test();
   }
    return 0;
}
```

2.static修饰局部变量改变了变量的生命周期，让静态局部变量出了作用域依然存在，到程序结束生命周期才结束。
```c
//代码二
 void test()
{
 static修饰局部变量
 static int i = 0;
 i++; 
 printf("%d\n", i);
}
int main()
{
 int i = 0;
 for (i = 0; i < 10; i++)
 {
  test();
 }
 return 0;
}
```
3.修饰函数-称为静态函数
```c
三.//代码1
int g_val = 2018;
//test.c
int main()
{
    printf("%d\n", g_val);
    return 0;
}
//代码2
static int g_val = 2018;
//test.c
int main()
{
    printf("%d\n", g_val);
    return 0;
}
```
>代码1正常，代码2在编译的时候会出现连接性错误。
结论：
一个全局变量被static修饰，使得这个全局变量只能在本源文件内使用，不能在其他源文件内使用

 ## 数据类型
- C语言中有四大数据类型，分为基本类型、构造类型、指针类型、空类型
       
>**整型常量** 
- 十进制的整数
- 八进制的整数，以0开头。例如：0123也就是十进制83
- 十六进制整数，以0x开头。例如：0x123就是10进制291
- 二进制整数，0b开头。例如：0b0010就是10进制2
>**实型常量**

1.小数形式
- 单精度小数，以字母f或F结尾。例如：1.0f、1.01f
- 双精度小数，十进制小数形式，3.14
- 默认双精度
- 可以没有整数位只有小数位。例如：.3、6f
--------------------------------------------------------------------------------------------
2.指数形式
- 以幂的形式表示 ，以字母E或e后跟一个10为底的指数
- 1.23×10^5用C语言表示就是1.23e5或1.23E5
- 字母E后面必须为整数
- 字母E前后必须要有数字
- E前后不能有空格
>字符常量
- 用单引号括起来'a'  'b'  'c'
- 字符常量的单引号中只能有一个字符
- 特殊情况：如果是转义字符，单引号中可以有两个字符。'\n'、'\t'
>字符串常量
- 字符型常量都是用双引号括起来的。例如:"a"、"abc"、"lnj"






>打印100到200的素数过程优化  
>首先偶数都可以省去，每次加2
>不必把从2到i的数全部试一遍，只需到\sqrt{2}就可以
```c
#include"stdio.h"
#include"math.h"
int main()//100到200的素数
{
	int i = 0;
	int count = 0;
	for (i = 100; i <= 200; i++)//因为每个偶数都可以省去，可以优化为i+=2
	{
		int n = 0;
		for (n = 2; n <= i ; n++)//n<=sqrt(i)开平方函数
		{
			if (i % n == 0)
				break;
		}
		if (i == n)
		{
			printf("%d ", i);
			count++;
		}
	}
	printf("\n%d", count);
	return 0;
}
```

>用二分法查找数组里的值
```c
#include"stdio.h"
int main()
{
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int k = 7;//要查找的数字，在数组中找k（7）的值
	int sz = sizeof(arr) / sizeof(arr[0]);//算数组的元素个数

	int left = 0;
	int right = sz - 1;

	while (left <= right)//二分法
	{
		int mid = (left + right) / 2;
		if (arr[mid] < k)
		{
			left = mid + 1;
		}
		else if (arr[mid] > k)
		{
			right = mid - 1;
		}
		else
		{
			printf("找到，下标为：%d\n", mid);
			break;
		}
	}
	if (left > right)
	{
		printf("找不到\n");
	}
	return 0;
}
```
