# 多元组 Tuple  #

需要保护数据时，将数据放入多元组 Tuple

## 创建多元组 ##

类似列表语法，区别在于

- 使用圆括弧()而非方括弧[]进行赋值
- 不可对多元组元素进行赋值操作

以下代码创建一个包含 element(0) 到 element(n) 共 n 个元素的多元组，多元组名 tuple_name

`tuple_name = ('element(0)', 'element(1)', 'element(2)', ..., 'element(n)')`

## 常见例子 ##

例如字符串类型 string 即为典型的 tuple

如下代码将造成典型的 TypeError

`string = 'ABCD'`  
`string[0] = 'W'`  

## 其余语法 ##

- 与 List 一样（。。。？）

- 需要引用 tuple 但为了避免某些试图修改其值的动作导致错误（tuple 不可被修改），可使用 `list(tuple)` 创建一个 List，内容复制自 tuple，区别在于新 list 可被用户修改