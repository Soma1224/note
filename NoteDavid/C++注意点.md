# C++注意点

## int*

- int*表示定义一个int*类型的变量，即int型的指针变量；
- int表示基本的数据类型（整型）;

```c++
int a[]={1,2,3,4,5};   // 定义一个int类型的数组，包含5个元素
int* p2=a;             // 定义一个int类型的指针变量p1，指向数组a的首地址
int* p2=(int*)malloc(sizeof(int));  // 定义一个int类型的指针变量p2，指向内存中一块连续4个字节的地址单元
```



## 两个int*相减

==利用两个指向同一数组的指针相减得到两个指针之间元素的个数==

## 数组作为函数参数传入

数组作为函数参数，作用类似指针。 函数只传递一个4字节的地址，而没有其大小信息。

```c++
int length(int ar[])
{
  sizeof ar; // 永远是4（当然，在16位编译器下是2 )
}
```

C++规定，数组作为形参的时候，a代表数组首地址。
他的底层意义是： a 退化为了一个4字节的指针，没有任何变量表示数组的大小会“自动”被传递进来。

我们看看这个时候 sizeof a是什么：

```c++
sizeof( 函数形参的a[] )  = sizeof( int* const ) = 4  // 当然a[]不是合法的C++类型
```





# C++中如何在数组作为函数形参后，如何获取数组长度?

数组作为形参传入函数后，传入的就是单纯的指针了，没法利用sizeof计算，只能通过手动再传入一个n作为数组长度





## int和int*和int**的大小

```c++
//查看int和int一级指针和int二级指针的大小
	cout << "int大小：" << sizeof(int) << endl;     //4
	cout << "int一级指针的大小：" << sizeof(int*) << endl;          //4
	cout << "int二级指针的大小：" << sizeof(int**) << endl;         //4
```



## 有符号数和无符号数

- 无符号数：不存在正负之分，所有位都用来表示数的本身。
- 有符号数：最高位用来表示数的正负，最高位为1则表示负数，最高位为0则表示正数



## int的取值范围

==C语言中int的取值范围为：-2147483648 ~ 2147483647==

解释如下：
int类型在C语言中占4个字节，即32个二进制位。

当表示正数时，最高位为符号位（符号位为0），最大的正数是 0111 1111 1111 1111 1111 1111 1111 1111 即$2^{31} -1$ = 2147483647
当表示负数时，最高位为符号位（符号位为1），最小的负数是 1000 0000 0000 0000 0000 0000 0000 0000 而在计算机中是以补码的形式存储的，C语言规定 1000 0000 0000 0000 0000 0000 0000 0000 的补码为-2147483648
所以C语言中int的取值范围为：-2147483648 ~ 2147483647  



## 指针相等（重要的理解！！）

![1541596803988](.\picture\%5CUsers%5Clenovo%5CAppData%5CRoaming%5CTypora%5Ctypora-user-images%5C1541596803988.png)



