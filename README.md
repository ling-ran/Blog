# C语言
一个小白的学习过程  
>打印100到200的素数过程优化  
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
