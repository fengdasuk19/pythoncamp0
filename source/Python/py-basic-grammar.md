## 变量 ##

### 命名规则 ###

与传统编程语言并无明显差异：大多以字母开头，不能以数字开头。

通常使用大写字母定义**常量**

### 局部变量与全局变量 ###

何时定义局部变量/全局变量？

1. 若希望所定义的变量对其他函数（包括主函数）隐藏信息，则定义为局部变量

2. 若希望所定义的变量对其他函数可用，即要在不同函数中对同一变量进行操作，通过该变量进行通讯，则定义为全局变量

关于修改局部变量/全局变量，要注意：

若定义了全局变量

`[v_0] = [data_0]`

则无法在函数 [fun] 内部通过以下代码修改全局变量 [v_0] 的值为 [data_1]

`[v_0] = [data_1]`

取而代之，该行代码将在函数内部创建一个作用于仅限于 [fun] 内部的局部变量 [v_0]，并赋值为 [data_1]；当返回主函数体时，名为 [v_0] 的局部变量消失，即此时若在主函数体中运行下述代码

`print [v_0]`

会得到如下输出

> [data_0]

所以首先应该明确一点：**在函数内部定义局部变量，起名不要与全局变量重复**

如果希望在函数 [fun] 内部修改全局变量 [v_0]，则在函数体内部，使用该变量前，**声明**该变量为全局的

`global [v_0]`

此后在 便可在 [fun] 中对全局变量 [v_0] 进行修改

**请正确声明全局变量名称，否则声明错误而不使用到被错误声明的变量，将导致意外错误**，如下：

原计划在函数内部修改全局变量`count_win`，但由于声明错误

`global counter_x, counter_y, counte_win`

导致以下代码虽然没有语法错误，但产生了语义错误，即创建了局部变量`count_win`，而没有修改到全局的`count_win`

`count_win = str(counter_x)+'/'+str(counter_y)`

## 数据类型 ##

### 常用数据类型 ###

int, float, string

---------------------------

### 强制类型转换 ###

### 调用格式 ###

强制转换 a 为类型 type

`[类型名type](a)`

也许你会有疑问：强制转换整型为浮点型，会发生什么呢？请看例子

### 例子 ###

你有以下代码

`print int(4.9)`  
`print float(5)`

运行该句，将打印出以下结果：

> 4  
5.0

---------------------------

### 查看数据类型 ###

### 调用格式 ###

查看数据 a 的类型 type

`type(a)`

### 例子 ###

你有以下代码

`print type(4.9)`  
`print type(5)`

运行该句，将打印出以下结果：

> [type 'float']  
[type 'int']

## 计算某数的幂 ##

可直接通过运算符 `**`实现

### 调用格式 ###

计算 a 的 b 次幂

`a ** b` 

### 例子 ###

你有以下代码

`print 2, '^', 7, '=', 2**7`

运行该句，将打印出以下结果：

> 2 ^ 7 = 128

## 一般除法，整除，求余（求模） ##

一般除法：可直接通过运算符 `/`实现
整除（得商）：可直接通过运算符 `//`实现
求余（求模）：可直接通过运算符 `%`实现

### 调用格式 ###

一般除法：计算 a 除以 b `a / b`
整除（得商）：计算 a 整除 b （a 除以 b 所得商） `a // b`
求余（求模）：计算 a 对 b 求模结果（a 除以 b 所得余数）`a % b`

### 例子 ###

你有以下代码

`a = 49.0`  
`b = 10`  
`c = a // b`  
`d = a / b`  
`e = a % b`  
`print c, d, e`  

运行该句，将打印出以下结果

> 4.0 4.9 9.0

## 函数 ##

### 定义格式 ###

`def [函数名]（形参列表，注意括弧是**半角**状态；不需要接受参数时，直接输入一对括弧即可):[注意此处的**冒号**！]`  
`[缩进 * n_0，注意，严格缩进，同样的缩进格数表示同一级内容，n_i表示缩进空格数]`  
`[缩进 * n_1]`  
`[缩进 * n_2]`  
`[...]`  
`[缩进 * n_0，注意，与函数体内部最外层缩进空格数一样多]return [函数返回值]（注意，若无提供 return 语句，python 将返回值 None）`

### 调用格式 ###

`[函数名](实参列表；如果函数不需要参数，直接输入一对括弧即可)`

### 例子 ###


注：请用中文所提示的内容替代以上『[]』及其框住的内容。下同，不再赘述。

你有以下代码

`def cal_add(a, b):`  
&nbsp;&nbsp;&nbsp;&nbsp;`c = a + b`  
&nbsp;&nbsp;&nbsp;&nbsp;`print a, '+', b, '=', c`  
&nbsp;&nbsp;&nbsp;&nbsp;`print 'Now print', a, 'to', b - 1, ':'`  
&nbsp;&nbsp;&nbsp;&nbsp;`for i in range(a, b):`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`print i`  
&nbsp;&nbsp;&nbsp;&nbsp;`return c`

`def test_hello():`  
&nbsp;&nbsp;&nbsp;&nbsp;`print 'Hello, world!'`    

被这样调用时

`x = cal_add(1, 10)`  
`y = test_hello()`  
`print y`

将打印出以下结果（注意缩进！）

> 1 + 10 = 11  
Now print 1 to 9 :  
1  
2  
3  
4  
5  
6  
7  
8  
9  
Hello, world!  
None

#### 预先构建框架写函数头时 ####

请在函数头下至少写一句 `print`，不要仅仅在函数头下写一句注释，否则会在解释最近的下一个函数头时出现语法错误

> IndentationError: expected an indented block

例如，如下代码将在解释到`def t_entrain_ratio(is_air, t):`时出现以上错误

`def input_data():`  
&nbsp;&nbsp;&nbsp;&nbsp;` # input data for here`

`# mass conversion`


`# temperature conversion`


`# equivalent loading from air`
`def t_entrain_ratio(is_air, t):`  

只要在` # input data for here`所在行加入一句 `print`，问题即可得到解决

## 库和库函数调用（模块调用） ##

### 格式 ###

1. 若希望从库 lib 中调用库函数 lib_fun，键入以下代码载入它

    `from [lib] import [lib_fun]`

    此后直接引用函数 [lib_fan] 即可

2. 若觉得键入一个一个库函数太麻烦，键入以下代码载入库

    `import [lib]`

    此后引用函数 [lib_fun] 时，应按照以下格式

    `[lib].[lib_fun]`

### 例子 ###

1. 例如，希望从库 math 中调用自然对数的底数 e，可键入以下代码
    `from math import e`  
   此后需要打印 e 时，只要键入以下代码  
    `print e`  
   将得到如下显示  
    > 2.71828182846

2. 例如，希望调用库 math 中的大量函数，包括调用自然对数的底数 e，可键入以下代码
    `import math`
   此后需要打印 e 时，只要键入以下代码  
    `print math.e`  
   将得到如下显示  
    > 2.71828182846




# 参考资料 #

1. [Py - 2.7.10rc 0 - Documentation - The Standard Library - Built-in Types](https://docs.python.org/2/library/stdtypes.html)
2. [python中如何判断一个变量的数据类型？](http://bbs.csdn.net/topics/90061442)