# Markdown 列表FAQ(FAQ about Markdown List) #

## Q1 重新计数 与 缩进 ##

### 表现 ###

1. 水果

苹果  
李子

2. 蔬菜

生菜  
西红柿

3. 肉类

鸡肉  
鱼肉

### 概述 ###

这里的问题是：

1. **每个列表都重新计数了（从 1 开始）**
2. 每个列表下面的具体内容看起来并没有归该表头所有（没有缩进）


### 分析 ###

造成问题的原始代码如下：

> `1. 水果`  
> 
> `苹果`  
> `李子`
> 
> `2. 蔬菜`  
> 
> `生菜`   
> `西红柿`
> 
> `3. 肉类`  
> 
> `鸡肉`  
> `鱼肉`


注意到：每个列表内容**前后均有一个空行**。  

### 尝试1 ###

让我们删去表头与其**下**内容之间的空行试试，即当代码是这样的时候：
> `1. 水果`  
> `苹果`  
> `李子`
> 
> `2. 蔬菜`  
> `生菜`  
> `西红柿`
> 
> `3. 肉类`  
> `鸡肉`  
> `鱼肉`

显示效果是： 

1. 水果  
苹果  
李子

2. 蔬菜  
生菜  
西红柿

3. 肉类  
鸡肉  
鱼肉

两个问题都得到了解决！  

### 尝试2 ###

要是删去表头与其**上**内容之间的空行，即当代码是这样的时候：
> `1. 水果`  
> 
> `苹果`  
> `李子`  
> `2. 蔬菜`  
> 
> `生菜`   
> `西红柿`  
> `3. 肉类`  
> 
> `鸡肉`  
> `鱼肉`

显示效果是：  
1. 水果

苹果  
李子  
2. 蔬菜
 
生菜  
西红柿  
3. 肉类
 
鸡肉  
鱼肉

好吧，看起来只解决了第 1 个问题，而第2个问题仍然存在。

### 尝试3 ###

要是将这两个空行都删除，即当代码是这样的时候：
> `1. 水果`  
> `苹果`  
> `李子`  
> `2. 蔬菜`  
> `生菜`   
> `西红柿`  
> `3. 肉类`  
> `鸡肉`  
> `鱼肉`

显示效果是：  
1. 水果  
苹果  
李子  
2. 蔬菜  
生菜  
西红柿  
3. 肉类  
鸡肉  
鱼肉

与尝试2的效果一样啊……

### A1 解决 ###

综上所述：

1. 为了避免列表出现上述**重新计数**问题，写列表时请**直接将项目内容直接紧跟在其表头后**，而不要在表头与其统辖的项目内容之间加入空行。
2. 为了避免出现上述的列表下缩进问题，请在第 n 个列表项目内容尾部、第 n+1 个列表项目序号之间加入一个空行。

## Q2 列表与正文粘在一起 ##

### 表现 ###

比如说我本想在这段话后跟上一个列表，却出现这种状况：
1. 列表1
2. 列表2
3. 列表3

### 概述 ###

这里的问题是：

1. 列表与正文粘在一起了，没有与正文独立开来


### 分析 ###

造成问题的原始代码如下：

`比如说我本想在这段话后跟上一个列表，却出现这种状况：`  
`1. 列表1`  
`2. 列表2`  
`3. 列表3`

注意到原始代码中列表与正文之间**只有一个换行符**

### 尝试1 ###

考虑到[《如何在 markdown 语法下键入换行符》](/source/Markdown/FAQ/how-to-newline-in-markdown.md)一文中提到了：


> 写作者必须键入**2个连续的**`空格`之后再按`Enter`，才能完成`强制换行`这个动作
 
那么在正文与列表之间加入两个连续的空格是看看，即当代码是这样的时候（1个[Space]表示此处有1个空格）：

`比如说我本想在这段话后跟上一个列表，却出现这种状况：[Space][Space]`  
`1. 列表1`  
`2. 列表2`  
`3. 列表3`  

显示效果是：  

比如说我本想在这段话后跟上一个列表，却出现这种状况：  
1. 列表1
2. 列表2
3. 列表3

看来问题没有得到实质性的解决：markdown 没有把代码识别为列表，而是认为这串代码是正文。

### 尝试2 ###

显然不能考虑在每个列表的表头后插入两个空格，因为这样仅仅是将代码视为正文来处理，没有解决实质性问题。  
那么我们不妨在列表最前面与正文之间再插入一个空行，即当代码是这样的时候：

`比如说我本想在这段话后跟上一个列表，却出现这种状况：`  

`1. 列表1`  
`2. 列表2`  
`3. 列表3`  

显示效果是：  

比如说我本想在这段话后跟上一个列表，却出现这种状况：  

1. 列表1
2. 列表2
3. 列表3

问题好像得到解决了？再向表头下面添加项目试试看：

比如说我本想在这段话后跟上一个列表，却出现这种状况：  

1. 列表1
 1. 项目1.1
 2. 项目1.2
2. 列表2
 1. 项目2.1
 2. 项目2.2
3. 列表3
 1. 项目3.1
 2. 项目3.2

非常好，问题得到了圆满解决。

### A2 解决 ###

综上所述：
为了让 markdown 能识别出列表，应在正文与列表之间插入一个空行，亦即两个换行符（键入2个`Enter`）。

##Q3 引用之后的重新计数 ##

### 表现 ###

比如说我本想在这段话后跟上一个列表，在第 2 点后引用一段文字，但原计划的第 3 点项目序号却重新计数（从 1 开始）了：

1. 列表1
2. 列表2

> 这里是引用的内容

3. 列表3

### 概述 ###

这里的问题是：

1. 引用之后的项目序号重新计数


### 分析 ###

造成问题的原始代码如下：

`1. 列表1`  
`2. 列表2`  

`> 这里是引用的内容`  

`3. 列表3`

注意到引用前没有缩进的空格。

### 尝试1 ###

考虑到[。。。]()中提到的

> 此处引用[基本语法（未完成）]()，列表要加缩进空格

尝试在

`> 这里是引用的内容` 

前加上连续的 4 个空格（以下用`[[Space] * 4]`表示），即当代码是这样的时候：

`1. 列表1`  
`2. 列表2`  

`[[Space] * 4]> 这里是引用的内容`  

`3. 列表3`

显示效果是：  

1. 列表1
2. 列表2

    > 这里是引用的内容

3. 列表3

问题解决。

###A3 解决 ###

综上所述：
在项目列表中间引用文字时（即引用内容前后的项目序号是连续的），为了避免项目序号在引用之后重新计数，要像在项目列表下的引用前加入连续的 4 个空格（或更多。。。此处应补更多空格的例，以及最多进行二次引用，即引用中最多包含 1 次引用）。
