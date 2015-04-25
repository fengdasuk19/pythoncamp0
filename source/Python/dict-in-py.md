# 字典 Dictionary #

## 创建字典 ##

首先注意，如下代码中与创建**列表**的一个**明显差别**是：使用**花括弧{}**进行定义

以下代码创建一个名为 dicts 的字典，其索引为 key(i)(i = 0, 1, 2, 3, ..., n)，对应的键值（即索引所映射/指向的值）为 value(i)(i = 0, 1, 2, 3, ..., n)

`dicts = {key(0):value(0), key(1):value(1), key(2):value(2), ..., key(n):value(n)}`

其中，对索引值（键名）的要求是：数据类型必须是不可变的(immutable type)，因此，列表、字典均不可作为索引值（键名）

此外没有更多要求。从而，与列表是有序的这一事实不同，字典是无序的

## 遍历字典 ##

以下两种代码都可以实现对字典 dicts 的遍历

1. `for key in dicts:`  
   &nbsp;&nbsp;&nbsp;&nbsp;`print dicts[key]`

2. `for key, value in dict.items():`  
  &nbsp;&nbsp;&nbsp;&nbsp;`print value` 

## 向字典中添加 ##