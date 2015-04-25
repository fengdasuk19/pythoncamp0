### 判断字符串数据类型。。。 ###

### 调用格式 ###

假定待判断字符串为 [str]

方法名|格式|作用描述
-------------------|-----------|---------
[str].isdigit()|。。。|判断 [str] 中是否全为数字，是则返回 True，否则返回 False


### 例子 ###

你有以下代码

`s0 = '123'`  
`print s0.isdigit()`  
`s1 = '123.456'`  
`print s1.isdigit()`  
`s2 = '123.abc'`  
`print s2.isdigit()`  
`s3 = 'abc'`  
`print s3.isdigit()`  

运行该句，将打印出以下结果：

> True  
False  
False  
False

---------------------------

## 字符串专题 ##

### 强制将数据 data 转换成字符串 ###

使用以下代码

`str(data)`

### 连接字符串 ###

### 调用格式 ###

为了将字符串string_0、string_1、string_2按顺序连接在一起，使用以下代码

`string_0 + string_1 + string_2`

### 例子 ###

你有以下代码

`split = 10`  
`hr = 6`  
`min = 5`  
`hr_ones = hr % sp-1lit`  
`hr_tens = hr // split`  
`min_ones = min % split`    
`min_tens = min // split`    
`print str(hr_tens) + str(hr_ones) + ':' + str(min_tens) + str(min_ones)` 

运行该句，将打印出以下结果

> 06:05

## 大小写转换（。。。未完成） ##

请参考[这里](http://wangwei007.blog.51cto.com/68019/1134323)

---------------------------

## 字符串数组 ##

设有字符串名为 s，则

字符串首字符为 s[0]，以此类推

字符串尾部字符为 s[-1]，以此类推

字符串长度通过函数len()进行计算： len(s)

s[a:b] 表示取字符串第 a 位到第 b - 1 位的内容

s[a:] 表示从第 a 位开始取字符串内容直到到字符串结束

s[:b] 表示从第 0 位开始取字符串内容直到第 b - 1 位

---------------------------

# 参考资料 #

1. [python 中字符串大小写转换](http://wangwei007.blog.51cto.com/68019/1134323)
2. [python写一个要求用户输入数字，如果不是数字就一直循环要求输入，直到输入数字为止的代码](http://zhidao.baidu.com/question/499536267.html)