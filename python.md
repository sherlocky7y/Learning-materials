## 基本语法

### 保留关键字

逻辑值 

True

False

逻辑运算

and

or

not

条件控制

if 

elif

else

循环控制

for

while

break

continue

异常处理

try  尝试执行代码异常

except  捕获异常

finally  无论是否发生都会执行的代码块

raise  抛出异常

**函数定义**

def

return 

lambda

类与对象

class

del 删除对象引用

模块导入

import

from   从模块导入特定部分

as  为导入的模块或者对象创建别名

作用域

global

nonlocal

异步编程

async  声明异步函数

await 等待异步操作完成

其他

assert  断言

in

is 

pass

with

yield

### 等待用户输入

input()

### import 与 from...import

在 python 用 **import** 或者 **from...import** 来导入相应的模块。

将整个模块(somemodule)导入，格式为： **import somemodule**

从某个模块中导入某个函数,格式为： **from somemodule import somefunction**

从某个模块中导入多个函数,格式为： **from somemodule import firstfunc, secondfunc, thirdfunc**

将某个模块中的全部函数导入，格式为： **from somemodule import \***

## 标识符

- 第一个字母必须是字母或者下划线_
- 其他部分由字母、数字和下划线组成

## 变量

（字母数字下划线，但不能用）

变量赋值、调用

### 作用域（id（）函数）

变量被访问的范围

##### 局部作用域

局部变量

**全局作用域**global语句：在函数内部修改同名的全局变量的值

##### legb规则

l：local局部作用域

e：enclosed嵌套函数外层函数作用域

g：global

b;build in内置作用域（）局部作用域与全局作用域发生冲突时

## 基本数据类型

#### String（字符串）和编码

Unicode字符集

把所有语言统一到一套编码里

**ASCII编码和Unicode编码的区别**

字母`A`用ASCII编码是十进制的`65`，二进制的`01000001`；

字符`0`用ASCII编码是十进制的`48`，二进制的`00110000`，注意字符`'0'`和整数`0`是不同的；

汉字`中`已经超出了ASCII编码的范围，用Unicode编码是十进制的`20013`，二进制的`01001110 00101101`。

为了解决资源浪费提出`utf-8`



**python的字符串**

ord()函数获取字符的整数表示

chr()函数把编码转换为对应的字符





由于Python的字符串类型是`str`，在内存中以Unicode表示，一个字符对应若干个字节。如果要在网络上传输，或者保存到磁盘上，就需要把`str`变为以字节为单位的`bytes`。

`bytes`类型的数据用带`b`的前缀的单引号or双引号表示

```python
x=b'ABC' #bytes每个字节占一个字符
```

以Unicode表示的`str`通过`encode()`方法可以编码为指定的`bytes`

```python
>>> 'ABC'.encode('ascii')
b'ABC'
>>> '中文'.encode('utf-8')
b'\xe4\xb8\xad\xe6\x96\x87'
>>> '中文'.encode('ascii')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
UnicodeEncodeError: 'ascii' codec can't encode characters in position 0-1: ordinal not in range(128)

```

纯英文的`str`可以用`ASCII`编码为`bytes`，内容是一样的，含有中文的`str`可以用`UTF-8`编码为`bytes`。含有中文的`str`无法用`ASCII`编码，因为中文编码的范围超过了`ASCII`编码的范围，Python会报错。



在`bytes`中，无法显示为ASCII字符的字节，用`\x##`显示

如果读到这种字节流可以知道数据为`bytes`

要把`bytes`变为`str`，就需要用`decode()`方法

```python
>>> b'ABC'.decode('ascii')
'ABC'
>>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
'中文'

```

小技巧

如果`bytes`中只有一小部分无效的字节，可以传入`errors='ignore'`忽略错误的字节



```python
b'\xe4\xb8\xad\xff'.decode('utf-8',errors='ignore')
'中
```

计算`str`包含字节数用`len()`函数：

```python
len('ABC')
3
len('中文')
2
```

`len()`函数计算的是`str`的字符数，如果换成`bytes`，`len()`函数就计算字节数：

```python
>>> len(b'ABC')
3
>>> len(b'\xe4\xb8\xad\xe6\x96\x87')
6
>>> len('中文'.encode('utf-8'))
6

```

由于Python源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为UTF-8编码。当Python解释器读取源代码时，为了让它按UTF-8编码读取，我们通常在文件开头写上这两行：

```python
#!/user/bin/env python3  
第一行注释是为了告诉Linux/OS X系统，这是一个Python可执行程序，Windows系统会忽略这个注释
#_*_coding:utf-8_*_
第二行注释是为了告诉Python解释器，按照UTF-8编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。
```



%占位

| 占位符 | 替换内容     |
| ------ | ------------ |
| %d     | 整数         |
| %f     | 浮点数       |
| %s     | 字符串       |
| %x     | 十六进制整数 |





format()

利用传入的参数替代占位符{0},{1}.....

f-string

以`f`开头的字符串，称为`f-string`，字符串如果包含{xxx}，就会以对应的变量替换

```python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```







用 *‘* 或者 *“* 括起来

![image-20251026215744563](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251026215744563.png)

```python
#!/usr/bin/python3
#字符串截取  变量[头下标，尾下标]

str = 'Runoob'  # 定义一个字符串变量

print(str)           # 打印整个字符串
print(str[0:-1])     # 打印字符串第一个到倒数第二个字符（不包含倒数第一个字符）
print(str[0])        # 打印字符串的第一个字符
print(str[2:5])      # 打印字符串第三到第五个字符（不包含索引为 5 的字符）
print(str[2:])       # 打印字符串从第三个字符开始到末尾
print(str * 2)       # 打印字符串两次
print(str + "TEST")  # 打印字符串和"TEST"拼接在一起
#结果
Runoob
Runoo
R
noo
noob
RunoobRunoob
RunoobTEST
```

注意：反斜杠可以用来转义，使用r可以让反斜杠不发生转义

.upper()将字符串转化为大写

#### Number（数字）

int

float

complex：comlex（a，b）

#### bool（布尔类型）

> **注意：**Python3 中，bool 是 int 的子类，True 和 False 可以和数字相加， **True==1、False==0** *会返回* **True**，但可以通过**is** *来判断类型。*

> **注意:** 在 Python 中，所有非零的数字和非空的字符串、列表、元组等数据类型都被视为 True，**只有 0、空字符串、空列表、空元组等被视为 False。**因此，在进行布尔类型转换时，需要注意数据类型的真假性。

#### List（列表）

![image-20251026220224239](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251026220224239.png)

![image-20251207231845993](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251207231845993.png)

![image-20251207231904460](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251207231904460.png)

##### 列表嵌套

![image-20251207231931140](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251207231931140.png)

```python
matrix=[[1,2,3,4],
       [5,6,7,8],
       [9,10,11,12],
       ]
```

1、

```python
[[row[i] for row in matrix]for i in range(4)]
#row 是循环变量，代表矩阵的每一行
```

2、

```python
transposed=[]
for i in range(4):
    transposed.append(row[i] for row in matrix)
```

3、

```python
transposed=[]
for i in range(4):
    transposed_row=[]
    for row in matrix:
        transposed_row.append(row[i])
    transposed.append(transposed_row)
```



##### 数据结构

![image-20251207232053667](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251207232053667.png)

- [ list.append(obj)](https://www.runoob.com/python3/python3-att-list-append.html)

  在列表末尾添加新的元素对象

- [ list.count(obj)](https://www.runoob.com/python3/python3-att-list-count.html)

  统计某个元素在列表中出现的次数

- [list.extend(seq)](https://www.runoob.com/python3/python3-att-list-extend.html)

  在列表末尾一次性追加另一个序列中的多个值（用新列表扩展原来的列表）

- [ list.index(obj)](https://www.runoob.com/python3/python3-att-list-index.html)

  从列表中找出某个值第一个匹配项的索引位置

- [ list.insert(index, obj)](https://www.runoob.com/python3/python3-att-list-insert.html)

  将对象插入列表

- [ list.pop([index=-1\])](https://www.runoob.com/python3/python3-att-list-pop.html)

  移除列表中的一个元素（默认最后一个元素），并且返回该元素的值

- [list.remove(obj)](https://www.runoob.com/python3/python3-att-list-remove.html)

  移除列表中某个值的第一个匹配项

- [list.reverse()](https://www.runoob.com/python3/python3-att-list-reverse.html)

  反向列表中元素

- [ list.sort( key=None, reverse=False)](https://www.runoob.com/python3/python3-att-list-sort.html)

  对原列表进行排序

- [ list.clear()](https://www.runoob.com/python3/python3-att-list-clear.html)

  清空列表

- [ list.copy()](https://www.runoob.com/python3/python3-att-list-copy.html)

  复制列表





```python
a=[66.25,444,555,333,1,1234]
print(a.count(333),a.count(66.25))
```

###### 列表推导式

```python
vec=[2,4,6]
[3*x for x in vec]
#[6,12,18]
```



#### Tuple（元组）

具有打包和解包的能力

1. 元组中的元素不能修改。元组写在小括号（）内

2. 索引和列表一样，也可以截取

3. > tup1 = ()    # 空元组
   > tup2 = (20,) # 一个元素，需要在元素后添加逗号

```python
#!/usr/bin/python3

tuple = ( 'abcd', 786 , 2.23, 'runoob', 70.2  )
tinytuple = (123, 'runoob')

print (tuple)             # 输出完整元组
print (tuple[0])          # 输出元组的第一个元素
print (tuple[1:3])        # 输出从第二个元素开始到第三个元素
print (tuple[2:])         # 输出从第三个元素开始的所有元素
print (tinytuple * 2)     # 输出两次元组
print (tuple + tinytuple) # 连接元组
#结果
('abcd', 786, 2.23, 'runoob', 70.2)
abcd
(786, 2.23)
(2.23, 'runoob', 70.2)
(123, 'runoob', 123, 'runoob')
('abcd', 786, 2.23, 'runoob', 70.2, 123, 'runoob')

```

格式：

parame = {value01,value02,...}或者set(value)

#### Set（集合）

Python 中的集合（Set）是一种无序、可变的数据类型，用于存储唯一的元素。

集合中的元素不会重复，并且可以进行交集、并集、差集等常见的集合操作。

在 Python 中，集合使用大括号 **{}** 表示，元素之间用逗号 **,** 分隔。

另外，也可以使用 **set()** 函数创建集合。

**注意：**创建一个空集合必须用 **set()** 而不是 **{ }**，因为 **{ }** 是用来创建一个空字典。

```python
#!/usr/bin/python3

sites = {'Google', 'Taobao', 'Runoob', 'Facebook', 'Zhihu', 'Baidu'}

print(sites)   # 输出集合，重复的元素被自动去掉

# 成员测试
if 'Runoob' in sites :
    print('Runoob 在集合中')
else :
    print('Runoob 不在集合中')


# set可以进行集合运算
a = set('abracadabra')
b = set('alacazam')

print(a)

print(a - b)     # a 和 b 的差集

print(a | b)     # a 和 b 的并集

print(a & b)     # a 和 b 的交集

print(a ^ b)     # a 和 b 中不同时存在的元素
#结果
{'Zhihu', 'Baidu', 'Taobao', 'Runoob', 'Google', 'Facebook'}
Runoob 在集合中
{'b', 'c', 'a', 'r', 'd'}
{'r', 'b', 'd'}
{'b', 'c', 'a', 'z', 'm', 'r', 'l', 'd'}
{'c', 'a'}
{'z', 'b', 'm', 'r', 'l', 'd'}
```

#### Dictionary（字典）

1. 无需对象的集合
2. 字典是一种映射类型，字典用 **{ }** 标识，它是一个无序的 **键(key) : 值(value)** 的集合。键（key）必须使用不可变类型
3. 在同一个字典中键（key）必须唯一

```python
#!/usr/bin/python3

dict = {}
dict['one'] = "1 - 菜鸟教程"
dict[2]     = "2 - 菜鸟工具"

tinydict = {'name': 'runoob','code':1, 'site': 'www.runoob.com'}


print (dict['one'])       # 输出键为 'one' 的值
print (dict[2])           # 输出键为 2 的值
print (tinydict)          # 输出完整的字典
print (tinydict.keys())   # 输出所有键
print (tinydict.values()) # 输出所有值
#结果
1 - 菜鸟教程
2 - 菜鸟工具
{'name': 'runoob', 'code': 1, 'site': 'www.runoob.com'}
dict_keys(['name', 'code', 'site'])
dict_values(['runoob', 1, 'www.runoob.com'])

```

构造dict（）函数

```python
>>> dict([('Runoob', 1), ('Google', 2), ('Taobao', 3)])
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
>>> {x: x**2 for x in (2, 4, 6)}
{2: 4, 4: 16, 6: 36}
>>> dict(Runoob=1, Google=2, Taobao=3)
{'Runoob': 1, 'Google': 2, 'Taobao': 3}
```

#### bytes类型

- 不可变的二进制序列（元素在0~255间的整数）

- 创建 bytes 对象的方式有多种，最常见的方式是使用 b 前缀：

```python
x = b"hello"
if x[0] == ord("h"):
    print("The first element is 'h'")
```

此外，也可以使用 bytes() 函数将其他类型的对象转换为 bytes 类型。bytes() 函数的第一个参数是要转换的对象，第二个参数是编码方式，如果省略第二个参数，则默认使用 UTF-8 编码：

> x = bytes("hello", encoding="utf-8")

## 运算符

### 算数运算符

### 比较运算符

![image-20251203171316550](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251203171316550.png)

### 赋值运算符

![image-20251203171414182](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251203171414182.png)

### 位运算符

![image-20251203171444286](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251203171444286.png)

### 逻辑运输符

![image-20251203171514421](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251203171514421.png)

### 运算符比较级

![image-20251203171551482](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251203171551482.png)

## 条件控制

`input()`返回的数据类型是`str`，`str`不能直接和整数比较，必须先把`str`转换成整数。Python提供了`int()`函数来完成这件事情

#### if-elif-else语句

![image-20251027141731317](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251027141731317.png)

Python 中用 **elif** 代替了 **else if**，所以if语句的关键字为：**if – elif – else**

**注意：**

- 1、每个条件后面要使用冒号 **:**，表示接下来是满足条件后要执行的语句块。
- 2、使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。

```python
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
    
    
    
```



#### if嵌套

if 表达式1:
    语句
    if 表达式2:
        语句
    elif 表达式3:
        语句
    else:
        语句
elif 表达式4:
    语句
else:
    语句

```python
# !/usr/bin/python3
 
num=int(input("输入一个数字："))
if num%2==0:
    if num%3==0:
        print ("你输入的数字可以整除 2 和 3")
    else:
        print ("你输入的数字可以整除 2，但不能整除 3")
else:
    if num%3==0:
        print ("你输入的数字可以整除 3，但不能整除 2")
    else:
        print  ("你输入的数字不能整除 2 和 3")
#结果
$ python3 test.py 
输入一个数字：6
你输入的数字可以整除 2 和 3
```

### 模式匹配

#### match-case语句

使用`match`语句时，我们依次用`case xxx`匹配，并且可以在最后（且仅能在最后）加一个`case _`表示“任意值”，代码较`if ... elif ... else ...`更易读。

```python
match subject:
    case <pattern_1>:
        <action_1>
    case <pattern_2>:
        <action_2>
    case <pattern_3>:
        <action_3>
    case _:
        <action_wildcard>
```

复杂匹配

`match`语句除了可以匹配简单的单个值外，还可以匹配多个值、匹配一定范围，并且把匹配后的值绑定到变量：

匹配列表

`match`语句还可以匹配列表，功能非常强大。

我们假设用户输入了一个命令，用`args = ['gcc', 'hello.c']`存储，下面的代码演示了如何用`match`匹配来解析这个列表：

```python
args = ['gcc', 'hello.c', 'world.c']
# args = ['clean']
# args = ['gcc']

match args:
    # 如果仅出现gcc，报错:
    case ['gcc']:
        print('gcc: missing source file(s).')
    # 出现gcc，且至少指定了一个文件:
    case ['gcc', file1, *files]:
        print('gcc compile: ' + file1 + ', ' + ', '.join(files))
    # 仅出现clean:
    case ['clean']:
        print('clean')
    case _:
        print('invalid command.')

```









## 循环语句

![image-20251027234106212](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251027234106212.png)

#### while循环

```python
while 判断条件(condition)：
    执行语句(statements)……
```

#### 无限循环

表达式永远不为false实现

```python
#!/usr/bin/python3
 
var = 1
while var == 1 :  # 表达式永远为 true
   num = int(input("输入一个数字  :"))
   print ("你输入的数字是: ", num)
 
print ("Good bye!")
#结果
输入一个数字  :5
你输入的数字是:  5
输入一个数字  :
```

#### while循环使用else语句







#### for语句

Python的循环有两种，一种是for...in循环，依次把list或tuple中的每个元素迭代出来

> ```python
> for <variable> in <sequence>:
>  <statements>
> else:
>  <statements>
> ```

```python
#!/usr/bin/python3
 
sites = ["Baidu", "Google","Runoob","Taobao"]
for site in sites:
    print(site)
#结果
Baidu
Google
Runoob
Taobao
```

#### break

提前退出循环

#### continue

跳过当前这次循环，执行开始下一次循环





**整数范围值可以配合 range() 函数使用：**

#### range函数

```python
for _ in range(128)：循环执行128次
```

- 需要遍历数字序列，可以使用内置range（）函数
- 可以使用 range() 指定区间的值：
- 可以使 range() 以指定数字开始并指定不同的增量(甚至可以是负数，有时这也叫做'步长'):





`range()` 用于生成一个**整数序列**，常配合 `for` 循环使用。

range(stop)              # 从 0 开始
range(start, stop)       # 指定起止
range(start, stop, step) # 指定步长

## 三种用法

python

```python
range(stop)              # 从 0 开始
range(start, stop)       # 指定起止
range(start, stop, step) # 指定步长
```

## 迭代器

可以访问集合元素

迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退

迭代器有两个基本的方法：**iter()** 和 **next()**

创建一个迭代器：

需要在类中实现两个方法__ iter __ () 与 __  next __()

## 面对对象

- **类(Class):** 用来描述具有相同的属性和方法的对象的集合。它定义了该集合中每个对象所共有的属性和方法。对象是类的实例。
- **方法：**类中定义的函数。
- **类变量：**类变量在整个实例化的对象中是公用的。类变量定义在类中且在函数体之外。类变量通常不作为实例变量使用。
- **数据成员：**类变量或者实例变量用于处理类及其实例对象的相关的数据。
- **方法重写：**如果从父类继承的方法不能满足子类的需求，可以对其进行改写，这个过程叫方法的覆盖（override），也称为方法的重写。
- **局部变量：**定义在方法中的变量，只作用于当前实例的类。
- **实例变量：**在类的声明中，属性是用变量来表示的，这种变量就称为实例变量，实例变量就是一个用 self 修饰的变量。
- **继承：**即一个派生类（derived class）继承基类（base class）的字段和方法。继承也允许把一个派生类的对象作为一个基类对象对待。例如，有这样一个设计：一个Dog类型的对象派生自Animal类，这是模拟"是一个（is-a）"关系（例图，Dog是一个Animal）。
- **实例化：**创建一个类的实例，类的具体对象。
- **对象：**通过类定义的数据结构实例。对象包括两个数据成员（类变量和实例变量）和方法。

## 函数

将函数作为返回值或者参数只需要写名字即可

**定义一个函数**

- 函数代码块由def关键词开头，后接函数标识符名称和圆括号（）
- 任何传入参数和自变量必须放在圆括号中间，圆括号之间可以用于定义参数。
- 函数的第一行语句可以选择性地使用文档字符串—用于存放函数说明。
- 函数内容以冒号 **:** 起始，并且缩进。
- **return [表达式]** 结束函数，选择性地返回一个值给调用方，不带表达式的 return 相当于返回 None。

![image-20251031112018911](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20251031112018911.png)

#### 函数的参数

形式参数

实际参数

**位置参数**：实参是根据形参的定义顺序进行传递

关键字参数（参数多的函数）：指定实参对应位置

默认参数：不传递指定参数使用默认值，若传递则覆盖默认值



/ 左侧不能使用关键字参数，只能使用位置参数

```python
def abc(a,/,b,c):
    print(a,b,c)
  
abc(1,2,3)
#输出1，2，3
abc(a=1,2,3)
#error
```



**收集参数**

*：元组

**：字典

**解包参数**

#### 函数返回值

return 

例子计算面积

```python
#!/usr/bin/python3
 
# 计算面积函数
def area(width, height):
    return width * height
 
def print_welcome(name):
    print("Welcome", name)
 
print_welcome("Runoob")
w = 4
h = 5
print("width =", w, " height =", h, " area =", area(w, h))
#结果
Welcome Runoob
width = 4  height = 5  area = 20
```

#### 函数的调用

函数的基本结构完成以后，你可以通过另一个函数调用执行

#### 内置函数

zip()

用于将多个可迭代对象的元素**并行组合成元组**

```python
list(zip([1, 2, 3], ['a', 'b', 'c']))
# 输出: [(1, 'a'), (2, 'b'), (3, 'c')]
```

#### 嵌套函数

对于嵌套函数来所外层函数的作用域是会通过某种形式保存下来的



nonlocal语句

非要在内部函数去修改外部语句



#### 闭包（工厂函数）

利用嵌套函数来实现

1. 利用嵌套函数的外层作用域具有记忆能力的特性，让数据保存在外层函数的参数或变量中
2. 将内层函数作为返回值给返回

```python
def funA():
    x=880
    def funB():
        print(x)
    return funB
```

现在要求不通过funA()函数来调用funB()

:先调用funA函数并把结果赋值给一个变量

```python
funny=funA()
funny()
#880
```



eg

```python
def power(exp):
    def exp_of(base):
        return bse**exp
    return exp_of
```

```python
squre=power(2)
cube=power(3)
```

squre指向exp_of时记住了外层函数作用域的exp参数



```python
def outer():
    x=0
    y=0
    def inner(x1,y1):
        nonlocal x,y
        x+=x1
        y+=y1
        print(f"x={x},y={y}")
    return inner

move=outer()
move(1,2)
#x=1,y=2
move(-2,2)
#x=-1,y=4(因为nonlocal导致x，y的值发生改变)
```



#### 递归函数

定义简单

使用递归函数要注意防止栈溢出，

**`方法`**

尾递归优化，再函数返回的时候，调用`自身`本身，并且，return语句不能包含表达式。编译器或者解释器就可以把尾递归做优化，使递归本身无论调用多少次，都只占用一个栈帧，不会出现栈溢出的情况。

```python
def fact(n):
    return fact_iter(n,1)

def fact_iter(num,product):
    if num==1:
        return product
    return fact_iter(num-1,num*product)

#return fact_iter(num - 1, num * product)仅返回递归函数本身，num - 1和num * product在函数调用前就会被计算，不影响函数调用


fact(5)对应的fact_iter(5, 1)的调用如下：

=> fact_iter(5, 1)
=> fact_iter(4, 5)
=> fact_iter(3, 20)
=> fact_iter(2, 60)
=> fact_iter(1, 120)
=> 120
```



汉诺塔

```python
def hannoi(n,x,y,z):
    if n==1:
        print(x,'->',z)
    else:
        hannoi(n-1,x,z,y) #n-1层的金片移到y # x为起始点，z为中间点，y为终点
        print(x,'->',z)
        hannoi(n-1,y,x,z)  #同理

n=int(input(print("请输入n")))
hannoi(n,'a','b','c')
```



## 高级特性

### 切片操作

创建一个0-99的数列

```
>>> L = list(range(100))
>>> L
[0, 1, 2, 3, ..., 99]

```

前10个数，每两个取一个：

```
>>> L[:10:2]
[0, 2, 4, 6, 8]
```

mask[:]

```python
mask[i*8:(i+1)*8]
'''
当 i=0: mask[0:8] → 前8位
当 i=1: mask[8:16] → 接下来的8位
...
当 i=15: mask[120:128] → 最后8位
'''
```

### 切片逆序

语法：`字符串/列表[start:stop:step]`，步长为 `-1` 即可逆序

### 连接操作

分隔符.join(字符串序列)

```python
words = ['hello', 'world']

print('-'.join'.join(words))    # 输出: "hello-world"
print(' '.join(words))    # 输出: "hello world"  
print(', '.join(words))   # 输出: "hello, world"
print(''.join(words))     # 输出: "helloworld"
```

### 迭代操作

判断一个对象是可迭代对象通过`collection.abc`模块的`Iterable`类型判断：

```python
from collection.abc import Iterable
isinstance('abc',Iterable)#str是否可迭代
>>>True
```

最后一个小问题，如果要对`list`实现类似Java那样的下标循环怎么办？Python内置的`enumerate`函数可以把一个`list`变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身：

```python
for i,val in enumerate(['A','B','C']):
    print(i,val)
   
...
0 A
1 B
2 C
```





给定一个`list`或`tuple`,我们可以用for循环来遍历`list`和`tuple`,称为迭代

有没有下标都可以迭代





迭代dict

`dict`迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。



```python
>>> d = {'a': 1, 'b': 2, 'c': 3}
>>> for key in d:
...     print(key)
...
a
c
b

```

由于字符串也是可迭代对象，因此，也可以作用于`for`循环



### 迭代器

使用`isinstance()`判断一个对象是否是`Iterable`对象：

```python
from collections.abc import Iterable
```

生成器都是`Iterator`对象，但`list`、`dict`、`str`虽然是`Iterable`，却不是`Iterator`。

把`list`、`dict`、`str`等`Iterable`变成`Iterator`可以使用`iter()`函数：

```python
>>> isinstance(iter([]), Iterator)
True
>>> isinstance(iter('abc'), Iterator)
True

```











### 列表生成式（List Comprehensions）

创建`list`的生成式

eg

```python
list(range(1,11))
[1,2,3,4,5,6,7,8,9,10]
```

但如果要生成`[1x1, 2x2, 3x3, ..., 10x10]`怎么做？方法一是循环：

```python
>>> L = []
>>> for x in range(1, 11):
...    L.append(x * x)
...
>>> L
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

```

但是循环太繁琐，而列表生成式则可以用一行语句代替循环生成上面的list

```python
[x*x for x in range(1,11)]
[1,4,9,16,25,36,49,64,81,100]

写列表生成式时，把要生成的元素x * x放到前面，后面跟for循环，就可以把list创建出来，


for循环后面还可以加上if判断，这样我们就可以筛选出仅偶数的平方：
[x*x for i in range (1,11) if x%2==0]
[4,16,36,64,100]


双层循环
[m+n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

`for`循环可以同时使用两个甚至多个变量

```python
>>> d = {'x': 'A', 'y': 'B', 'z': 'C' }
>>> for k, v in d.items():
...     print(k, '=', v)
...
y = B
x = A
z = C

```

if....else

最后的if后面不能加else

if写在for前面后面必须加else

### 生成器（generator）

##### 法1

```python
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

只要把一个列表生成式的[]改成()，就创建了一个generator

>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>


可以用for循环去迭代
for n in g:
    print(n)
  

0
1
4
9
16
25
36
49
64
81
```

斐波那契数列（Fibonacci）

`函数表示`

```python
def fib(max):
    n,a,b=0,0,1
    while n<max:
        print(b)
        a,b=b,a+b
        n=n+1
       
    return 'done'


#赋值语句
a,b=b,a+b

#等于
t=(b,a+b)   #t是一个元组
a=t[0]
b=t[1]
```

`生成器generator`

只需要把print(b)修改为yield b就可以了

##### 法2：

如果一个函数定义中包含`yield`关键字，那么这个函数就是一个generator函数

generator的函数，在每次调用`next()`的时候执行，遇到`yield`语句返回，再次执行时从上次返回的`yield`语句处继续执行

> 注意
>
> 调用generator函数会创建一个generator对象，多次调用generator函数会创建多个相互独立的generator。



用`for`循环

但是用`for`循环调用generator时，发现拿不到generator的`return`语句的返回值。如果想要拿到返回值，必须捕获`StopIteration`错误，返回值包含在`StopIteration`的`value`中：

```python
>>> g = fib(6)
>>> while True:
...     try:
...         x = next(g)
...         print('g:', x)
...     except StopIteration as e:
...         print('Generator return value:', e.value)
...         break
...
g: 1
g: 1
g: 2
g: 3
g: 5
g: 8
Generator return value: done

```











## 编程

**斐波那契数列**

```python
a,b=0,1
while b<1000:
    print(b)
    a,b=b,a+b
```

```python
a,b=0,1
n=10
for i in range(n):
    print(b)
    a,b=b,a+b
```

#### end关键字

用于将结果输出到同一行，或着在输出的末尾添加不同的字符

```python
a,b=0,1
while b<1000:
    print(b,end=',')
    a,b=b,a+b
```

## with关键字

上下文管理协议

1. 自动资源释放

2. 代码简洁

3. 异常安全

4. 可读性强

   **基本用法**

```python
with expression [as variable]:
    #代码块
```

- `expression` 返回一个支持上下文管理协议的对象

- `as variable` 是可选的，用于将表达式结果赋值给变量

- 代码块执行完毕后，自动调用清理方法

  ```python
  with open('example.txt','r')as file:
      content=file.read()
      print(content)
  ```

  | 模式   | 含义       |
  | ------ | ---------- |
  | `'r'`  | 读（默认） |
  | `'w'`  | 写（覆盖） |
  | `'a'`  | 追加       |
  | `'r+'` | 读写       |
  | `'rb'` | 二进制读   |
  | `'wb'` | 二进制写   |
  
  ```python
  # 读取（默认）
  with open('file.txt', 'r') as f:
      content = f.read()
  
  # 写入（覆盖）
  with open('file.txt', 'w') as f:
      f.write('Hello')
  
  # 追加
  with open('file.txt', 'a') as f:
      f.write('World')
  
  # 读写
  with open('file.txt', 'r+') as f:
      content = f.read()
  
  # 二进制读取（图片、音频等）
  with open('image.png', 'rb') as f:
      data = f.read()
  
  # 二进制写入
  with open('image.png', 'wb') as f:
      f.write(data)
  ```
  
  ### `.strip()`
  
  去除字符串**首尾**的空白字符（空格、换行符、制表符等）
  
  ### `.split("\n")`
  
  按**换行符**把字符串切割成列表：：
  
  
  
  
  
  
  
  _exit_()方法接受三个参数
  
  返回True代表异常值已被处理，不会继续传播，反之
  
  - exc_type:异常类型
  - exc_val：异常值
  - exc_tb:异常追踪信息

### 实际应用场景

1.文件操作

```python
with open('input.txt','r')as infile,open('output.txt','m')as outfile:
    content=infile.read()
    outfile.write(content.upper())
```

2.数据库连接

```python
import sqlite3

with sqlite3.connect('database.db')as conn:
    cursor=conn.cursor
    cursor.execute('SELECT*FROM users')
    results=cursor.fetchall()
```

3.线程锁

```python
import threading

lock=threading.lock()

with lock:
    #临界区代码
    print("这段代码是安全的")

```



## python推导式

- 列表（list）推导式

  ```python
  表达式 for 变量 in 列表
  
  表达式 for 变量 in 列表 if条件
  ```

  

- 字典（dictonary）推导式

- 集合（set）推导式

- 元组（tuple）推导式

## 匿名函数python lambda

他们没有函数名,只能通过赋值给变量或作为参数传递给其他函数来使用

```python
lambda arguments:expression
```

- `lambda`是 Python 的关键字，用于定义 lambda 函数。
- `arguments` 是参数列表，可以包含零个或多个参数，但必须在冒号(`:`)前指定。
- `expression` 是一个表达式，用于计算并返   回函数的结果。

```python
x = lambda a : a + 10
print(x(5))
```

## python装饰器

把函数作为参数放到装饰器内

## 



**进阶**

给装饰器传递参数

```python
import time
def logger(msg):
    def time_master(func):
        def call_func():
            start=time.time()
            func()
            stop=time.time()
            print(f"[{msg}]一共耗费了{(stop-start):.2f}")
         return call_func
    return time_master

@logger(msg="A")
def funA():
    time.sleep(1)
    print("正在调用funA")
@logger(msg="B")
def funB():
    time.sleep(1)
    print("正在调用funB")
```



## 数据结构

#### 将列表当作栈使用

栈操作

- 压入push
- 弹出pop
- 查看栈顶元素
- 检查是否为空
- 获取栈的大小

创建空栈

```python
stack=[]
```

压入操作

```python
stack.append(1)
stack.append(2)
print(stack)
#输出[1,2]
```

弹出pop操作

移除并返回栈顶元素

```python
top_element=stack.pop()
print(top_element)
print(stack)
```

查看栈顶元素（peek/top）

```python
top_element=stack[-1]  #直接访问列表的最后一个元素
print(top_element)
```

检查是否为空IsEmpty

```python
is_empty=len(stack)==0
print(is_empty)  
#输出 False
```

获取栈的大小（size）

```python
size=len(stack)
print(size)
#输出2
```

#### 将列表当作队列使用（不好）

#### 使用collection.deque实现队列

```python
from collection import deque
queue=deque()#创建空队列
#向队尾添加元素

```

#### del语句

根据从一个列表中根据索引删除一个元素

```python
a=[1,2,3,4,5,6]
del a[0]
[2,3,4,5,6]
```

#### 元组和序列

#### 集合

是一个无序不重复元素的集。

**注意：如果要创建一个空集合，你必须用 set() 而不是 {} ；后者创建一个空的字典**

#### 字典

序列是以连续的整数为索引，与此不同的是，字典以关键字为索引，关键字可以是任意不可变类型，通常用字符串或数值。

无序的键=>值对的集合（同一个字典之内，关键字必须是互不相同）

**遍历技巧**

在字典中遍历时，关键字和对应的值可以使用items（）方法同时解读出来：

```python
>>> knights = {'gallahad': 'the pure', 'robin': 'the brave'}
>>> for k, v in knights.items():
...     print(k, v)
...
gallahad the pure
robin the brave
```

在序列中遍历时，索引位置和对应值可以使用 enumerate() 函数同时得到：

```python
>>> for i, v in enumerate(['tic', 'tac', 'toe']):
...     print(i, v)
...
0 tic
1 tac
2 toe
```

反向遍历

```python
>>> for i in reversed(range(1, 10, 2)):
...     print(i)
...
9
7
5
3
1
```

顺序遍历

```python
>>> basket = ['apple', 'orange', 'apple', 'pear', 'orange', 'banana']
>>> for f in sorted(set(basket)):
...     print(f)
...
apple
banana
orange
pear
```

## python模块

### 模块的作用

- **代码复用**：将常用的功能封装到模块中，可以在多个程序中重复使用。
- **命名空间管理**：模块可以避免命名冲突，不同模块中的同名函数或变量不会互相干扰。
- **代码组织**：将代码按功能划分到不同的模块中，使程序结构更清晰。

b标准模块

| 名            | 功能描述                                    |
| :------------ | :------------------------------------------ |
| `math`        | 数学运算（如平方根、三角函数等）            |
| `os`          | 操作系统相关功能（如文件、目录操作）        |
| `sys`         | 系统相关的参数和函数                        |
| `random`      | 生成随机数                                  |
| `datetime`    | 处理日期和时间                              |
| `json`        | 处理 JSON 数据                              |
| `re`          | 正则表达式操作                              |
| `collections` | 提供额外的数据结构（如 defaultdict、deque） |
| `itertools`   | 提供迭代器工具                              |
| `functools`   | 高阶函数工具（如 reduce、lru_cache）        |

## 永久储存

打开文件

`open()`:file 和mode两个参数

`file`指定一个将要打开的文件路径（绝对路径或者相对路径）

`mode`可选参数，指定文件的打开模式

```python
#指定 utf-8 编码
with open('file','r',encoding="utf-8")as file:
```



| 字符串 | 含义                                       |
| ------ | ------------------------------------------ |
| 'r'    | 读取(默认)                                 |
| 'w'    | 写入（如果文件已存在则先截断清空文件）     |
| 'x'    | 排他性创建文件（如果文件已存在则打开失败） |
| 'a'    | 追加（如果文件已存在则在末尾追加内容）     |
| 'b'    | 二进制模式                                 |
| 't'    | 文本模式（默认）                           |
| '+'    | 更新文件（读取和写入）                     |

​       将字符串写入文件对象中

1. f.write(text,/)

2. f.writelines(lines,/)

   关闭文件对象

3. f.close()

   从文件对象中读取指定数量的字符（遇到EOF停止）当未指定该参数，或者该参数为负值，读取剩余所有字符

4. f.read(size=-1,/)

   返回当前文件指针在文件对象中的位置

5. f.tell()

   修改文件指针的位置，从`whence`参数指定的位置（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset字节，返回值是新的索引位置

6. f.seek()

#### 路径处理







## 异常

### 处理异常

try-except语句

```python
try:
    检测范围
  
except [expression[as identifier]]:
    异常处理代码
```



try-except-else语句进行搭配

```python
try:
    1/0
except:
    print("逮到了")
else:
    print("没逮到")
```

try-except-finally

```python
try:
    1/0
except:
    print("逮到了")
else:
    print("没逮到")
finally:
    print("带没逮到都会吱一声")
    
 

#用于处理结尾工作的
try:
    f=open("文件名","w")
    f.write("i love c")
except:
    print("出错啦")
finally:
    f.close()
```

**异常的嵌套**





raise语句

assert语句





利用异常实现goto









## 类和对象



## class

![image-20260314162144041](https://raw.githubusercontent.com/sherlocky7y/blog-images/main/imgs/image-20260314162144041.png)

`self` 是什么？

`self` 代表**当前这个实例对象本身**。每个方法的第一个参数都要写 `self`，但调用时不用传——Python 自动帮你传入。

### 封装

通俗理解就是打包到一起

### 继承

通过继承创建的类称为`子类`，而被继承的类我们称之为`父类`

判断体个对象是否属于某个类使用`isinstance()函数`

`多重继承`

一个`子类`可以继承多个父类

正常访问顺序从左到右，除非前面的类中没有对应的对象才会到下一个类里面找

### 组和

```python
class Turtle:
    def say(self):
        print("1")
class Cat:
    def say(self):
        print("2")
class Dog:
    def say(self):
        print("3")
class Garden:
    t=Turtle()
    c=Cat()
    d=Dog()
    def say(self):
        self.t.say()
        self.c.say()
        self.d.say()
       
g=Garden()
print(g.say())

'''
1
2
3
'''
```

### 绑定

用`self`

## 正则表达式

匹配`字符串`的强有力的武器,计思想是用一种描述性的语言来给字符串定义一个规则，凡是符合规则的字符串，我们就认为它“匹配”了，否则，该字符串就是不合法的.

> 因为匹配的是字符串所以对于数字来说范围就是0-9

```python
#譬如要找一个范围在0-255的数字时
import re
re.search(r'[01]\d\d|2[0-4]\d|25[0-5]','188')
```

正则表达式中，如果直接给出字符，就是精确匹配。

`\d`可以匹配一个数字，`\w`可以匹配一个字母或数字

- `'00\d'`可以匹配`'007'`，但无法匹配`'00A'`；
- `'\d\d\d'`可以匹配`'010'`；
- `'\w\w\d'`可以匹配`'py3'`；

`.`可以匹配任意字符，所以：

- `'py.'`可以匹配`'pyc'`、`'pyo'`、`'py!'`等等。

`'\'`转义字符

如果想要匹配`'.'`这个符号就需要使用转义字符

**eg**

来看一个复杂的例子：`\d{3}\s+\d{3,8}`。

我们来从左到右解读一下：

1. `\d{3}`表示匹配3个数字，例如`'010'`；
2. `\s`可以匹配一个空格（也包括Tab等空白符），所以`\s+`表示至少有一个空格，例如匹配`' '`，`' '`等；
3. `\d{3,8}`表示3-8个数字，例如`'1234567'`。

进阶

可以用`[ ]`表示范围

比如:

- [0-9a-zA-Z\\_]    可以匹配一个数字,字母或者下划线;
- [0-9a-zA-Z\\_]+   可以匹配至少由一个数字,字母或者下划线组成的字符串;
- `[a-zA-Z\_][0-9a-zA-Z\_]*`可以匹配由字母或下划线开头，后接任意个由一个数字、字母或者下划线组成的字符串，也就是Python合法的变量；
- `[a-zA-Z\_][0-9a-zA-Z\_]{0, 19}`更精确地限制了变量的长度是1-20个字符（前面1个字符+后面最多19个字符）。

### re模块

Python提供`re`模块，包含所有正则表达式的功能。由于Python的字符串本身也用`\`转义，所以要特别注意：

因此我们强烈建议使用Python的`r`前缀，就不用考虑转义的问题了

```python
s = r'ABC\-001' # Python的字符串
# 对应的正则表达式字符串不变：'ABC\-001'
```

判断正则表达式是否匹配

match():如果匹配成功，返回一个Match对象，否则返回None

```python
test='用户输入的字符串'
if re.match(r'正则表达式'，test):
    print('OK')
else:
    print('failed')
```

## 库

`s = Solver()` 这行代码通常出现在使用 **Z3 定理证明器**（Z3 Theorem Prover）的 Python 脚本中。

Z3 是由微软研究院开发的一个高性能 SMT（Satisfiability Modulo Theories，可满足性模理论）求解器。简单来说，这行代码的作用是**创建一个求解器实例**，你可以把它想象成一个“超级逻辑计算器”或“万能解题助手”，准备接收你给出的条件（约束）并帮你找出答案。

以下是详细的解释：

### 1. 代码含义拆解

- **`Solver`**: 这是 Z3 库中的一个类。它代表了求解引擎的核心，负责管理约束条件、执行搜索算法以及判断是否存在满足所有条件的解。
- **`()`**: 调用构造函数，初始化这个求解器对象。
- **`s =`**: 将创建好的求解器对象赋值给变量 `s`，以便后续通过 `s` 来调用求解器的功能（如添加约束、检查可满足性）。

### 2. 这个对象能做什么？

一旦你执行了 `s = Solver()`，你就拥有了一个可以处理复杂逻辑和数学问题的工具。通常的使用流程如下：

1. **定义变量**：创建整数、布尔值、位向量（BitVec）等变量。
2. **添加约束 (`s.add(...)`)**：告诉求解器题目是什么。例如 `s.add(x > 0)` 或 `s.add(x + y == 10)`。
3. **检查求解 (`s.check()`)**：让求解器开始工作。它会返回 `sat`（有解）、`unsat`（无解）或 `unknown`（未知）。
4. **获取模型 (`s.model()`)**：如果有解，这一步可以拿出具体的数值解。
