# C语言基本知识

## vscode调试快捷键

```
F9：创建断点，打上断点可以使得程序执行到想要的位置暂定执行，然后配合F10，F11观察代码执行细节

条件断点：满足这个条件才触发断点

F5：启动调试，经常用来跳到下一个断点处，配合F9使用

F10：逐过程，通常用来处理一个过程，可以是一次函数调用，或者一条语句

F11：逐语句，就每次都执行一条语句，但这个快捷键可以使我们的执行逻辑进入函数内部，在函数调用的地方想进入函数观察细节就需要使用F11，如果使用F10，直接完成函数调用

crtl+F5:开始执行不调试
```

### 中文识别问题

`system()` 是 C 标准库 `<stdlib.h>` 中提供的一个函数。

> **Change Code Page（修改代码页）**
>
> Windows 的 CMD 使用**代码页(Code Page)**决定字符编码

65001  -> UTF-8

```
启动 cmd.exe

↓

执行

chcp 65001 > nul

↓

把控制台编码改成 UTF-8

↓

输出信息被丢进 nul

↓

返回程序
```

## main函数是什么？

**概念定义**

1. 程序的入口
2. 有且仅有一个
3. 多个.c文件中只能有一个main函数（程序入口只能有一个）

main函数的多种写法?

```C
//写法一
int main(){
    return 0;
}
//写法二
int main(void){
    //void表示main函数不接收任何参数
    return 0;
}
//写法三
int main(int argc,char*argv[]){
    return 0;
}

```

)

## 库函数和printf

定义：库函数是为了方便程序员写代码，简单来说就是编译器厂商提供

在线查看

[Reference - C++ Reference](https://legacy.cplusplus.com/reference/)

```c
printf(格式控制，输出列表);
/*
1、格式字符：用双撇号括起来的一个字符串，作用是将输出的数据转换成指定的格式后输出，格式声明总是由"%"开始
2、普通字符：即需要在输出时原样输出的字符
3、输出列表：程序需要输出的一些数据，可以是常量、变量或表达式*/
```

### 格式字符

1）d格式字符，用来输出一个有符号的十进制整数，可以在格式声明指定输出数据的域宽（所占的列数），如"%5d"指定输出数据占5列

2）c格式字符，用来输出一个字符也可以指定域宽

3）s格式字符，用来输出一个字符串

```c
printf("%s","china");
//输出：china
```

4）f格式字符

1. 基本型，用%f（不指定输出数据长度，系统处理一般是：实数中整数全部输出，小数部分占6位）
2. 指定数据宽度和小数位数%m.nf

## 数据类型

### 1、基本数据类型

```C
//短整型
short [int]
[signed] short [int]
unsigned short [int] 

//整型
int 
[signed] int
unsigned int 

//长整型
long [int]
[signed] long [int]
unsigned long [int]

//更长的整型
long long [int]
[signed] long long [int]
unsigned long long [int]


//浮点型
float(单精度)
double(双精度)
long double

//字符（所有的字符ASCII代码最多7个二进制就可以表示，所以在C语言中指定一个字节存储一个字符）
char

//布尔类型
//表示真假
//使用需要包含<stdbool.h>这个头文件
//取值为true or false
_Bool
```

### 2、枚举类型

### 3、void类型

### 4、派生类型

## 占位符

## 字符和ASCII码

A~Z：65-90 

a~z：97-122

0~9：48-57

\n:10

## 表达式属性

值属性：

类型属性：



## 变量

```c
//基本语法
类型名 变量名;
```

**变量名要求**

- 只能由字母（大小写都可以）、**数字（不能用于开头）**、和下划线组成
- 长度不能超过63个字符
- 变量名区分大小写
- 变量名不能使用关键字 

**局部变量**

局部变量进入函数创建，出了函数销毁，下一次调用函数重新创建

**全局变量**

**初始化**

在创建变量的同时给一个确定的值，这叫做变量的初始化

```c
int age=19;
```

## getchar和putchar

getchar()函数返回用户从建盘上输入一个字符，使用时不带有任何参数

程序运行到这个命令就会暂停，等待用户从键盘输入，等同于scanf（）读取一个字符

原型定义在头文件stdio.h

不会跳过任何字符

如果读取失败会返回EOF  -1

```c
//跳过空格
#include<stdio.h>
int main() {
	int ch = 0;
	while ((ch = getchar()) == ' ') {
		;
	}
	printf("%c\n", ch);
	return 0;
}
```

putchar

putchar（）函数将他的参数字符输出到屏幕，等同于printf（)输出一个**字符**

原型定义在头文件stdio.h

如果读取失败会返回EOF  -1

## 块作用和文件作用域？这是什么呢

**程序块（复合语句）**{}里面的就叫做

**作用域**scope（变量生效范围）

1. 文件作用域（函数外部声明的变量（全局变量（具有文件作用域））
2. 块作用域（单独作用的区域）

代码块是可以嵌套的

### 局部优先

```c
#include<stdio.h>
int main() {
	int i = 20;
	{
		int i = 8;
		printf("a=%d\n", i);
	}
	return 0;
}
a=8
```

for循环也是块作用域（函数内部声明的变量只能在函数内使用）

## 关键字（保留字）

关键字查找链接

[C语言关键字大全（44个，附带详细解释） - C语言中文网](https://c.biancheng.net/view/60bjy80.html)

定义：一批保留名字的符号如int if return

注意：创建标识符的时候不能和关键字重复

### 1、存储类型

#### auto

#### **static**

1、static修饰局部变量

​    改变了变量的存储类型

​    普通的局部变量是存储在栈区

​    被static修饰的局部变量是存储在**静态区**的

2、static修饰全局变量

**作用**：static修饰的全局变量只能在自己所在的源文件内部使用，不让其他源文件使用就可以用static修饰全局变量

**原理**：全局变量本来是具有外部链接属性的，而被static修饰后外部链接属性就变成了内部链接属性

3、static修饰函数

作用：与修饰全局变量效果相同

原理：函数也具有外部链接属性

#### register

#### **extern**

1、声明来自外部的全局变量

2、不过，由于**函数声明**原型默认就是extern,所以这里不加extern，效果是一样的

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260201171450968.png)

### 2、数据类型相关

### 3、控制语句相关

```c
if 
    
else
    
switch

case

default

for 

while

do

break

continue

goto

return
```

### 4、说明符

const

volatile

### 5、**sizeof关键字**:

sizeof 的作用：返回某种数据类型或者某个值占用的字节数量

参数可以是数据类型（关键字）、变量名、具体的值

计算内置类型、数组、自定义类型大小都可以

占位符%zd或%zu

```c
sizeof(类型)
sizeof 表达式
```

```c
#include<stdio.h>
int main() {
	int a = 10;
	printf("%zd\n", sizeof(int));
	printf("%zd\n", sizeof a);
	printf("%zd\n", sizeof(a));
	return 0;
}
```

sizeof的返回类型

创建了一个类型别名size_t，用来同意表示sizeof的返回值类型

别名定义再stddef.h（不一定）头文件（引入stdio.h时自动引入）里面，对应当前系统的sizeof的返回值类型，可能时unsigned int，也可能时unsigned long。

### 6、signed（含正负）和unsigned（没有负号）

用来修饰char、short等整型

signed int的取值范围可以看limits.h

unsigned打印应该用%u占位符

## 注释

注意不要放在“ ”内不然会取消注释

/**/

//这是一行注释   

## c语言的操作符

### 算术操作符

+

-

*

```c
#include<stdio.h>
int main() {
	int num1 = 5;
	printf("%d\n", num1 * num1);
	return 0;
}
```

/

➗两端如果都是整数就比较简单



```c
#include<stdio.h>
int main() {
	int a = 6 / 4;
	float f = 4.0 / 2.0;
	printf("f=%f\n", f);
	printf("a=%d\n", a);
	return 0;
}
```

%（两端只能是整数类型的值）

取余运算

```c
#include<stdio.h>
int main() {
	int a = 8 % 3;
	printf("a=%d\n", a);
	return 0;
}
```

**负数取模**

结果是由第一个运算数的正负号决定的

```c
#include<stdio.h>
int main() {
	int a = -8 % 3;
	printf("a=%d\n", a);
	return 0;
}
```

### ++和--运算

**单目操作符**

操作对象之一一个

++（自增）分为前置（先++再运算）和后置（先运算再++）

### 赋值操作符（=）

作用：给变量一个值

注意：==作用是判断值是否相等

### 复合赋值符

+=

-=

*=

/=

%=

### 连续赋值

从右往左依次赋值的（c语言虽然理解但是不建议）拆开来写更好

### 移位操作符

<< (左移) >>（右移运算符）

移动的是二进制的位

### 单目操作符

**只有一个操作数**

```
!  逻辑反操作
-   负值
+   正值
&   取地址
sizeof  操作数的类型长度
~    对一个数的二进制按位取反
--   前置 后置--
++   前置 后置++
*     间接访问操作符（解引用操作符）
(类型)  强制类型转换
```

### 关系操作符

```
> >= < <= != ==
```

### 逻辑操作符

```
! (假变成真，真变成假)  
&&
||
```

### 条件操作符(三目操作符)

```c
exp1?exp2:exp3
```



```
?  : , 例如 x？y:z
如果x成立就y否则z
```

### 逗号操作符

```
a,b,c
```

### 下标引用

```
[]
```

### 函数调用

```c
()
eg
fun()
```

### 结构成员

```c
.   ->
a.b   a->b
```

## 操作符的优先级和结合性，哪个厉害呢？

### 优先级

基本的几个

- 圆括号()
- ++ --
- 一元运算符（+和 -）
- 乘法(*)除法(/)
- 加法（+）减法（-）
- 关系运算符（<  >等）
- 赋值运算符（=）

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/2668179ee2bbf668e62360f56eec6749.png)

### 结合性

当优先级不起作用时

看是**左结合**还是**右结合**

## c语言语句分类

- 空语句

  ```c
  #include<stdio.h>
  int main() {
  	;//空语句
  	return 0;
  }
  ```

- 表达式语句

  表达式的后面加上分号

- 函数调用语句

  ```c
  #include<stdio.h>
  int ADD(int x, int y) {
  	return x + y;
  }
  int main() {
  	int a, b;
  	printf("请输入a和b\n");
  	scanf("%d %d", &a, &b);
  	printf("%d\n",ADD(a, b));
  	return 0;
  }
  ```

- 复合语句

- 控制语句

C语言支持三种结构：顺序结构，选择结构，循环结构

九种控制语句

1. 条件判断语句（分支语句）if语句，switch语句
2. 循环执行语句 do while语句、while语句、for语句
3. 转向语句：break语句、goto语句、continue语句、return语句

## 选择结构

### 1、if语句语法形式

```c
if(表达式)
    语句
```

表达式的值为真（1），则运行语句，表达式不成立（0），则语句不执行

if和else语法

```c
if(条件)
    语句 
else
    语句

```

if--else语句中可以包含多条语句但必须加上大括号{}

因为if语句默认只能控制一条语句

### 2、if的嵌套

if嵌套if--else的话用大括号

### 3、悬空else问题

如果有多个if和else，else总是和最接近的if匹配

else嵌套可以用else if

### 4、switch语句haha

**用于判断条件有多个结果的情况**

- switch后的expression是**整型表达式**
- case后的值，必须是整型**常量表达式**
- case和后面的数字之间要有空格
- 每一个case语句代码执行后要加break，才能跳出switch

```c
switch(expression){
case value1:statement
case value2:statement
default:statement//跟表达不同的值就执行default
}



#include<stdio.h>
int main() {
	int num=0;
	printf("输入一个数");
	scanf("%d",&num);
	switch (num % 3) {
	case 0:
		printf("余数是0");
		break;
	case 1:
		printf("余数是1");
		break;
	case 2:
		printf("余数是2");
		break;
	}
	return 0;
}
```

#### break

1. 看情况考虑需不需要加break

#### default

- switch后的表达式无法匹配case语句，1、不做处理  2、加入default

- default和case够的顺序没有要求习惯把default放后面

## 循环结构

#### 1、for循环

- for循环中的continue跳过的是本次循环后面的代码，还是可以到达循环调整部分

```c
for(条件一;条件二;条件三)
    语句;//如果多条语句需要大括号


//表达式1：用于变量初始化
//表达式2：用于循环结束的判断
//表达式3：用于循环变量调整
```

#### 2、while循环

如果需要包含多条语句，需要加上大括号

```c
while(表达式)//表达式的值为真：非0值  为假：0
    语句;
```

#### 3、break

作用：终止循环，只要执行到break，后续的循环都会终止（只会跳出自己所在的循环）

```c
#include<stdio.h>
int main() {
	int i = 0;
	while (i <= 10) {
		if (i == 5)
			break;
		printf("%d ", i);
		i++;
		
	}
	return 0;
}

```

#### 4、continue

作用：在循环中的作用就是**跳过本次循环中continue后边的代码**，继续进行下一次的判断

```c
#include<stdio.h>
int main() {
	int i = 0;
	while (i <= 10) {
		if (i == 5)
			continue;
		printf("%d ", i);
		i++;
	}
	return 0;
}
//0 1 2 3 4
```

> 连续输入字符，只打印数字字符，其他字符跳过

```c
#include<stdio.h>
int main() {
	int ch =0;
	while ((ch = getchar())!=EOF) {
		
		if (ch>'9' || ch<'0')
			continue;
		putchar(ch);   
	}
	return 0;
}

```

#### 5、do~while循环

```c
do
    语句;
while(表达式);



do{
    语句;//多条语句的时候，加上大括号{}
}while(表达式);
```

### 循环嵌套

练习1

找出100-200之间的素数，并打印

```c
#include<stdio.h>
#include<math.h>
int main() {
	
	for (int i = 101; i <= 200; i+=2) {
		
		int flag = 1;
		for (int j = 2; j <= sqrt(i); j++) {
			//还可以优化范围到根号sqrt(i)需要引用math.h这个头文件
			if (i % j == 0) {
				flag = 0;
				break;
			}
		}
		if (flag == 1) {
			printf("%d ", i);
		}
	}
	
	return 0;
}
```

## go end

多重循环语句想要跳出的时候可以用

## 指针

### 1、内存和地址

CPU通过地址提取内存空间

内存单元的编号==地址==指针

CPU->(地址总线)->内存

--------------------------------------------------------------------------------

### 2、指针变量和地址

**指针变量**：也是一种变量作用就是用来存放地址

```c
int a=10;
int* pa=&a;//pa就是指针变量，把a的地址赋值给pa，pa存的是a的地址
```

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260117214748273.png)

| 符号 | 含义                 | 记忆                       |
| ---- | -------------------- | -------------------------- |
| &a   | 获取变量 a 的地址    | "a 住在哪"                 |
| *pa  | 解引用：取地址里的值 | "去这个地址看看里面有什么" |

### **3、指针变量的大小** 

**大小**：在32位平台下都是4字节，64位平台下都是8字节，与类型无关

```c
	int a = 10;//向内存空间索要4字节空间
	int* pa = &a;
	printf("%d\n",sizeof(pa));
```

指针存储的是另一个变量的地址

取地址运算符 **&**

取值运算符 *****

*取值运算符：取到*****后面那个地址所保存的变量

*地址->地址由变量指针保存， *p = a

​          ->地址就是地址 *（&a）= a 

```c
int a =10;
//a的地址1000，第一个小格的位置 &a->1000
int *p = &a;//指针变量
int *p = 1000
//p保存的就是a的地址1000
*p = 10;//取值运算
```

对于一个函数，调用函数的时候，都不会将这个值直接传入，而是将这个变量的值拷贝一份，将变量的副本传入到这个函数中

```c
void swap(int *pa,int *pb){
    //定义两个指针变量来存储a、b的地址jie
    int temp = *pa;
    *pa=*pb;
    *pb=temp;
    //*pa:pa存储的是a的地址即*pa=*（&a）
    //*pb:pb存储的是b的地址即*pb=*（&b） 
}
```

### 4、**指针变量类型的意义**

决定了解引用的权限（依次能操作几个字节）

### 5、指针加减

***强制类型转化

```c
int n=10;
char* pc=(char*)&n;
int *pi=&n;
```

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260117233928713.png)

指针的类型决定了指针向前或向后走一步有多大（距离）

### 6、void*指针

优点：接受任意类型地址

缺点：不能进行指针的+-和解引用



### 7、指针和数组

1. 数组在内存中是怎么存储的
2. 如何利用指针操作数组

 通过指针

int *pb =&b[0];

int *pb = b;

两种操作 pb++ 

​                 pb--

```c
int main(){
    int a[5]={1,2,3,4,5};
    int *pa = a;//a就是数组的地址，也就是&a[0]的地址
}
```

```c
int arr[] = {10, 20, 30, 40, 50};
int *p = arr;          // 等价于 int *p = &arr[0];

// 以下三种写法完全等价：
printf("%d\n", arr[2]);   // 30
printf("%d\n", *(arr+2)); // 30
printf("%d\n", *(p+2));   // 30

//指针算术：p + n 不是加 n 个字节，而是加 n * sizeof(类型) 个字节，所以 p + 2 自动跳到第 3 个 int。

// 用指针遍历数组
for (int i = 0; i < 5; i++) {
    printf("%d ", *(p + i));  // 等价于 p[i]，反过来数组也能当指针用
}
```

### 8、指针与函数

## 数组

`概念`

一组相同元素的集合

- 数组中存放的是一个或者多个数据
- 数组中存放的数据，类型是相同的

### 一维数组的创建和初始化

数组类型就是数组去掉数组名比如int [10]

创建

```c
type arr_name[常量表达式];
```

type是存放类型可以是int char float等

arr_name是数组名，有意义就行

[]中的常量值是用来指定数组大小的，这个数组的大小是根据实际的需求指定的

`初始化`

给定一些初始的值一般使用大括号{}将数据放在大括号里面

```c
int a[10]={0,1,2,3,4,5,6,7,8,9}//10可以不写，因为初始化时已经规定了长度
int a[10]={0,1,2,3,4,5} //后面的都是0
int a[10]={0}//未赋值的部分元素自动设定为0
```



### 一维数组怎么使用啊？easy

```c
数组名[下标]
```

##### 数组下标

数组下标 n个元素的数组下标是0~n-1

**在c语言中数组的访问提供了一个操作符[]（下标引用操作符）**

##### 数组元素的打印

```c
#include<stdio.h>
int main() {
	int math[10];
	int arr[5] = { 1,3,4,5,6 };
	double score[10];
	char ch[5];
	/*printf("%d\n", arr[3]);*/
	for (int i = 0; i < 5; i++) {
		printf("%d\n", arr[i]);
	}
	return 0;
}
```

##### 数组的输入

```c
#include<stdio.h>
int main() {
	int math[10];
	int arr[5] = { 1,3,4,5,6 };
	double score[10];
	char ch[5];
	/*printf("%d\n", arr[3]);*/
	for (int i = 0; i < 5; i++) {
		scanf("%d", &arr[i]);
	}
	for (int i = 0; i < 5; i++) {
		printf("%d\n", arr[i]);
	}
	return 0;
}
```

#### 打印数组元素的地址

#### （数组在内存中是连续存储的

#### 随着下标的增长地址由小到大变化）

```c
#include<stdio.h>
int main() {
	int arr[10] = { 1,3,4,5,4,6,6,3,5 };
	int i = 0;
	for (i = 0; i < 10; i++) {
		printf("&arr[%d]=%p\n",i, &arr[i]);
	}
	return 0;
}
```

#### sizeof计算求数组元素个数怎么做呢？

```c
#include<stdio.h>
int main() {
	int arr[10] = { 0 };
	printf("%zd\n", sizeof(arr));//计算数组总大小，单位为字节
	return 0;
}
```

打印元素

```c
#include<stdio.h>
int main() {
	int arr[] = {0,1,1,2,3,5};
	printf("%zd\n", sizeof(arr));
	int sz = sizeof(arr)/sizeof(arr[0]);
	printf("%d\n", sz);
	for (int i = 0; i < sz; i++) {
		printf("%d ", arr[i]);
	}
	return 0;
}
```

**一维数组**

```c
int a[3];
int i;
for(i=0;i<3;i++){
    ......
}
```

### **二维数组创建和初始化**

把一维数组作为数组元素组件二维数组

```c
type arr_name[常量值1][常量值2];

int arr[3][5]
double data[2][7]
```

不完全初始化

完全初始化

按行初始化

```c
int arr[2][5] = { {1,2,43,32,3} , {334,4,32,32,3} };
```

初始化时省略行，但不能省略列

```c
int arr[][5] = { {1,2,43,32,3} , {334,4,32,32,3} };
```

### 二维数组的使用

**下标**

```c
int arr[3][5]={1,2,3,4,5,2,3,4,5,6,3,4,5,6,7}
```

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260107125631737.png)

### 二维数组输入和输出

```c
#include<stdio.h>
int main() {
	int arr[3][4] = {0};
	int i = 0;
	int j = 0;
	for (i = 0; i <=2; i++) {
		for (j = 0; j<= 3; j++) {
			scanf("%d",&arr[i][j]);
		}

	}
	for (i = 0; i <= 2; i++) {
		for (j = 0; j <= 3; j++) {
			printf("%d ",arr[i][j]);
		}
	}
	return 0;

}
```

### 二维数组在内存中的存储

二维数组的每个元素都是连续存放的

### 字符数组创建和初始化

因为字符型数据是以整数形式（ASCII代码）存放的，所以也可以用整型数组来存放字符数据，但是有点浪费空间

```c
char c[10]={'a','b','b','b','b','b','b','b','b','b'};
```

字符串以'\0'为结束标志

### 字符串数组的输入和输出

1. 逐个字符输入输出。用格式符"%c"输入或输出一个字符
2. 将整个字符串一次输入或输出。用"%s"格式符

```c
char c[]={"china"};
printf("%s\n",c);
//在内存在数组c存储情况为
|c|h|i|n|a|\0|
```

### 字符串处理函数

> 注意：要引入string.h这个头文件

puts函数

```c
put(字符数组)；
```

作用：输出字符串的函数

```c
char str[]={"china\nBeiJing"};
puts(str);
```

gets函数

```c
get(字符数组)；
```

作用：输入字符串的函数

```c
gets(str);
```

两者只能输入或输出一个字符串

eg:

输入单词以空格为分界线,计算单词数.

```c
#include <stdio.h>
#include <string.h>
int main()
{
    char str[81];
    int i, n = 0, w = 0;
    char c;
    gets(str);
    for (i = 0; (c = str[i]) != '\0'; i++)
    {
        if (c == ' ')
        {
            w = 0;
        }
        else if (w == 0)
        {
            w = 1;
            n++;
        }
    }
    printf("单词数=%d\n", n);
    return 0;
}
```

## 函数

### 函数设计原则

> 函数就是功能。每一个函数用来实现一个特定的功能（函数名反应其代表的功能）

1、函数名有意义

2、函数的功能尽量独立单一

3、函数参数尽量少

4、规模不要太大

5、函数中尽量不要使用全局变量，降低函数对外部变量依赖

6、如果函数不需要返回值，返回类型位void，如果不写，函数就默认返回int类型

> 从用户的角度来看，函数有两种1、库函数，2、用户自定义函数（满足自身需求）
>
> 从函数形式来看，函数分为两种1、无参函数，2、有参函数

### 库函数

C语言库函数是指在C语言标准库中预先定义好的函数，这些函数包含在相应的头文件里，每个函数都有其函数名、返回值类型和函数参数；这些函数用于执行常见的任务，例如输入输出、字符串处理、内存操作等。

```c
strlen();函数
```

```c
char dest[10] = "Hello";
strcat(dest, " World!"); // 缓冲区溢出！可能导致程序崩溃
//把10改为20就可以了
```

**使用**

要在C程序中使用库函数，首先需要包含相应的头文件

### 自定义函数

#### 函数声明

（照搬函数定义第一行，然后加个分号）

返回值类型：整型、字符型、各种指针类型；如果不返回任何值可以用void

函数名：用于调用

> 形参名可以省略不写，只写类型也可以。（编译系统只关心参数个数和参数类型）

```c
//形式1
函数类型 函数名(参数类型1 参数名1，参数类型2 参数2，...,参数类型n 参数名n);
//形式2
函数类型 函数名(参数名1，参数2，...,参数名n);
```

#### **函数的定义**

```c
//1、定义无参函数
类型名 函数名(void){
    函数体;
}
类型名 函数名(){
    函数体;
}
```

> 函数体包括声明部分和语句部分

```c
//2、定义有参函数
//记录一个语句（z=x>y?x:y）表示z为x，y中较大一个
类型名 函数名(形参表列){
    函数体;
}
//3、定义空函数
void dummy(){}
//空函数本质没起什么作用，主要是在未来准备扩充功能的地方写上一个空函数
```

> **三目运算符（条件运算符 `?:`）**，它的作用是：**比较 `x` 和 `y`，把较大的那个值赋给 `z`**

```c
//结构
条件 ? 表达式1 : 表达式2
```

#### 调用函数

```c
//一般形式
函数名(实参表列);
//如果是无参函数实参列表可省略括号不能。
```

> 函数调用方式主要三类：
>
> 1. 函数调用语句（单独作为一个语句）
> 2. 函数表达式（函数带回一个确定的值参加表达式运算）
> 3. 函数参数（作为另一个函数调用的参数）

当程序调用函数时，程序控制权会**转移**给被调用的函数。被调用的函数执行已定义的任务，当函数的**返回语句**被执行时，或到达函数的结束括号时，会把程序控制权交**还给**主程序。

```c
int sum = add(3, 5); // 调用add函数，并将返回值赋给sum变量
```

```c
//完整调用
#include <stdio.h>
 
// 函数声明
int add(int a, int b);
 
// 函数定义
int add(int a, int b)
{
    int sum = a + b;
    return sum;
}
 
int main() 
{
    int result = add(10, 20); // 函数调用
    printf("Result: %d\n", result);//输出30
    return 0;
}
 
```

#### 函数调用的数据传递

##### 形参和实参:

`实参`（**主调函数中调用一个函数时**）：真正传给函数的参数（可以是常量，变量，表达式，函数等）

`形参`（**函数定义时**）：

- 形式参数是指函数名后括号中的变量，因为形式参数只有在函数被调用的过程中才实例化（分配内存单元），所以叫形式参数。

- 形式参数当函数调用完成之后就自动销毁了，因此形式参数只在函数中有效。

- 在函数定义时，形参由它们的类型和名称组成

  ```c
  void printMessage(int age, char* name) {
      printf("Name: %s, Age: %d\n", name, age);
  }
  //形参与实参的匹配否则会报错（数量对应，类型对应）
  ```


>调用函数过程中发生的实参和形参间的数据传递称为“虚实结合”

#### 函数的返回

`return`语句：

**return**语句将从被调用函数中的一个确定值带回到主调函数中去（如果需要从被调用函数带回一个函数值，被调用函数必须包含return语句）

```c
return z;
//等价
return(z);
//后面也可以是一个表达式
```

**函数值的类型**：

定义函数时指定函数值的类型。

#### 函数的嵌套

<img src="https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/微信图片_20260729212514_460_3.jpg" style="zoom: 33%;" />

> main函数进入，执行main函数遇到调用语句调用函数a，流程转到a函数，执行a函数遇到函数调用语句，调用函数b，流程转去函数b，执行b函数（如果没有其它嵌套函数，完成b的全部操作），返回a中调用b函数的位置，继续执行a函数中尚未执行的部分，直到a函数结束，返回main函数中调用a函数位置执行完main函数剩余部分直到结束

##### **嵌套调用**

可以嵌套调用不能嵌套定义

```c
#include<stdio.h>
void new_line(){
    printf("hehe\n");
}

void three_line(){
    int i=0;
    for(i=0;i<3;i++){
        //继续调用
        new_line();
    }
}

int mian(){
    three_line();
    return 0;
}
```

##### **链接式访问**

是把一个函数的返回值作为另一个函数的参数来调用

```c
#include<stdio.h>
#include<string.h>

int main(){
    char arr[20]="hello";
    int ret=strlen(strcat(arr,"bit"));//求字符串长度
    //strcat用于拼接两个字符串
    printf("%d\n",ret);
}
//8
```

#### 函数的递归

：程序**间接或者直接调用自身**的编程技巧称为递归；函数递归是指函数再执行过程中**调用自身**的一种技术

**必要条件**

1. ⭕递归函数通常包含两部分：基线条件和递归条件；

2. ⭕基线条件是递归函数**停止递归**的条件(比如:可以用if语句来控制)，而递归条件是递归函数**继续调用自身**的条件。递归是一种强大的编程技术，它可以使代码更简洁、更优雅，但需要小心使用，以避免无限递归导致的栈溢出等问题。

3. 递归的限制条件，满足这个限制条件的时候递归不再继续，

   每次递归调用后越来越接近这个条件

**原理**

递归函数通过反复调用自身来解决问题，每次调用时问题规模都会减小，**直到达到基线条件，递归停止**。递归函数在调用自身时，会创建一个新的函数栈帧，用于存储局部变量和参数。当递归结束时，这些栈帧会依次弹出，恢复到最初的调用状态。

最简单的递归

```c
#include<stdio.h>
int main() {
	printf("hehe\n");
	main();
	return 0;
}
//直到栈溢出才停
```

求n的阶乘

```c
//计算阶乘
#include<stdio.h>

//递归函数，计算阶乘
int factorial(int n){
    //基线条件
    if(n==0){
        return 1;
    }else{
        //递归条件
        return n*factorial(n-1);
    }
}
int main(){
    int num=5;
    int ret=factorial(num);
    printf("%d!=%d\n",num,ret);
    return 0;
}
```

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260205000506656.png)

> 递推有一个很好的例子斐波那契数列:
>
> 定义:当前项=前两项之和

![image-20260802180225931](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260802180225931.png)

求第n项斐波那契数列值:

```c
//法一:递推
#include<stdio.h>
int Fib(int n) {
	if (n <= 2)
		return 1;//Fib(0)=0,Fib(1)=Fib(2)都为1
	else
		return Fib(n - 1) + Fib(n - 2);
}
int main() {
	int n;
	scanf("%d", &n);
	int ret = Fib(n);
	printf("%d\n", ret);
	return 0;

}
```

流程图:

![image-20260802180550765](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260802180550765.png)

```c

//法二:迭代
int Fib(int n) {
	int a = 1;
	int b = 1;
	int c = 0;
	while (n >= 3) {
        //因为前三项已经有了所以计算从第3项开始
		c = a + b;
		a = b;
		b = c;
		n--;
		
	}
	return c;
}
int main() {
	int n;
	scanf("%d", &n);
	int ret = Fib(n);
	printf("%d\n", ret);
	return 0;

}
```

> 补充:有一个汉诺塔问题也很经典.

## 结构体

自定义的数据类型

**结构**：是一些值的集合，这些值称为成员变量，结构的每个成员可以是**不同**类型，如标量、数组、指针甚至其他结构体

（数组是一组**相同类型元素**的集合）

### 1、结构体的声明

```c
struct tag{             //tag是自定义标签
    member-list         //成员一个或者多个
}variable-list;
```

### 2、结构体的定义和初始化

eg：创建一个类型描述学士

姓名+年龄+性别+学号

```c
struct Student{
    char name[20];
    int age;
    char sex[6];
    char id[13];
};
int main(){
    struct Student stu1={"张三"，20,"男","2222222222211"}
}

```

嵌套使用结构体

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260118105341100.png)

### 3、结构体的访问操作符

**结构体成员访问操作符**

1、结构体成员的直接访问    .            (结构体变量.结构体成员)

```c
struct Point{
    int x;
    int y;
};
int main(){
    struct Point p={1,4};
    printf("x=%d y=%d",p.x,p.y);
    //输入值
    scanf("%d %d",&(p.x),&(p.y));
    printf("x=%d y=%d",p.x,p.y);
    return 0;
}
```

2、结构体成员的间接访问    ->            (结构体指针->结构体成员)

得到的不是结构体变量，而是得到了一个指向结构体的指针

```c
struct Point{
    int x;
    int y;
};
void SetPoint(struct Point *ptr){
    //scanf("%d %d",&((*ptr).x),&((*ptr).y));
    scanf("%d %d",&(ptr->x),&(ptr->y));
}
int main(){
    struct Point p={0,0};
    //设置坐标的值
    SetPoint(&p);
}
```

eg：

```c
struct Point p = {10, 20};
struct Point *ptr = &p;

p.x      // 10  —— 变量直接用 .
ptr->x   // 10  —— 指针用 ->（帮你偷偷 * 了一下）
(*ptr).x // 10  —— 手写等价形式：先解引用，再 .
```

### 位段

> 1. 位段的成员必须是int、unsigned int、signed int
> 2. 位段的成员名后便有一个冒号和一个数字
> 3. 位段的位是二进制的位

```c
struct A{
    int _q:2;
}
```

A就是一个位段类型

```c
printf("%zd\n",sizeof(struct A));
```

### 位段的跨平台问题

## 联合体/共用体 

编译器**只为最大的成员分配足够的内存空间**。联合体的特点是所有成员共用一块内存空间

```c
//联合体结构声明
union Un{
    char c;
    int i;
};
int main(){
    printf("%zd\n",sizeof(union Un));
    union Un u={0};
    printf("&u=%p\n",&u);
    printf("&(u.c)=%p\n",&(u.c));
    return 0;
}
```

联合体大小的计算

- 联合体大小至少是最大成员的大小
- 当最大成员大小不是最大对齐数的整数倍是，就要对齐到最大对齐数的整数倍

# 内存分配

1、栈空间上开辟

2、数组在栈空间开辟

特点：开辟空间大小固定。数组申明时必须指定数组长度，数组空间大小确定不能调整

3、动态内存开辟（灵活）（malloc和free都声明在stdlib.h头文件中）

**申请  malloc**

```c
void*malloc(size_t size);
```

malloc函数向内存申请一块连续可用的空间，并返回指向这块空间的指针

开辟成功，会返回一个指向开辟好空间的指针。

开辟失败，则返回一个NULL指针。

返回值类型void*，具体使用决定

如果size为0，malloc的行为时标准时未定义的，取决于编译器

```c
#include<stdio.h>
#include<stdlib.h>
int main() {
	int* p = (int*)malloc(20);
	if (p == NULL) {
		printf("返回值无效");
		return 1;
	}
	int i = 0;
	for (i = 0; i < 5; i++) {
		*(p+i) = i + 1;
		
	}
	for (i = 0; i < 5; i++) {
		printf("%d", *(p + i));
	}
    free(p);//释放完p是野指针
    p=NULL;
    return 0;

}
```

**释放  free**

```c
void free(void*ptr);
//传过去是要释放的空间的其实地址 
```

如果参数ptr指向的空间不是动态开辟的，那free函数的行为是未定义的

如果参数ptr是NULL指针，则函数什么都不做

**calloc**

```c
void*calloc(size_t num,size_t size);
```

为num个大小为size的元素开辟一块空间，并把空间的每个字节初始化为0；

与malloc区别在于calloc会在返回地址之前把空间每个字节初始化为0；

**realloc**

```c
void* realloc(void*ptr,size_t size);
```

ptr:需要调整的内存空间的起始地址

size调整之后新大小

返回值为调整之后

返回值为调整之后的内存空间的其实位置。

这个函数调整**原内存空间大小的基础上**，还会将原来内存中的数据移动到新的空间。 

realloc的两种情况

1、原有空间之后有足够大的空间

2、原有空间之后没有足够大的空间

（realloc会在堆区找到一个新的满足大小空间，把旧的空间中的数据全部复制到新的空间，把旧的空间释放，返回新空间起始值）

![](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260228135812656.png)

失败：当realloc函数无法调整产生新的空间是调整失败的时候，会返回NULL

### **常见动态内存错误**

#### 对NULL指针的解引用操作

```c
void test(){
    int*p=(int*)malloc(INT_MAX);
    *p=20;//如果p的值是NULL，就会有问题
    free(p);
}
```

#### 对动态开辟空间的越界访问

#### 对非动态开辟空间进行释放

#### 使用free释放一块动态开辟内存的一部分

```c
void test(){
    int*p=(int*)malloc(100);
    p++;
    free(p);//p不再指向动态内存的起始位置，只有p指向起始位置才能使用free（）释放
}
```

#### 对同一块空间多次释放

#### 动态开辟的内存忘记释放

## 枚举

```c
enum SEX{
    MALE,
    FEMALE,
    SECRET
};
int main(){
    enum SEX sex=MALE;
    return 0;
}
```

优点（相比于#define定义常量）

1. 代码可读性和可维护性
2. 更严谨
3. 便于调试
4. 一次可定义多个常量
5. 枚举遵从作用域规则，枚举声明在函数内只能再函数内使用

(细水长流，慢慢补充)