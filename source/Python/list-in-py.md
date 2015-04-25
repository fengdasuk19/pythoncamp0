# 列表 List  #

## 创建列表 ##

以下代码创建一个名为 list_name 的列表，列表中包含 element(0) 到 element(n) 共 n 个元素

`list_name = [element(0), element(1), element(2), ..., element(n)]`

可以用 Python 支持的任何数据类型替代 'element(i)'（i = 0, 1, 2, ..., n）

用 list_name[i] 取出 list_name 中的第 i 个元素

**字符串也是一种列表。事实上，对字符串的常见操作本质上是对列表元素进行操作，也就是说那些操作，例如len()等，是可以用于一般列表中的**


## 指向列表 与 复制列表 ##

当你有一个列表

`a = [1, 2, 3]`

时，使用代码

`b = a`

将产生一个名为 b 的指针指向 a 所指向的列表（a 与 b 指向同一个对象）

当使用代码

`b = list(a)`

时，将产生一张新的列表，内容复制于 a 所指向的列表（a 与 b 指向不同对象）


## 列表与全局变量 ##

假设有一个定义为列表的全局变量 a，则在函数中不需要通过关键字 global 进行声明，就能直接对全局变量 a 进行**列表操作**

注意，只能通过 [] 在未经全局声明时对 a 直接操作，如这样的代码

`a[0] = 'hello'`

而如果直接这样操作

`a = 'hello'`

则是直接创建一个名为 a 的局部变量，指向内存中新放入 'hello' 这个字符串的位置

没有任何关键字能让 a 成为局部变量，如果非要使用局部变量a[i]，只能换个名字


## 常见操作符 ##



1. `list.append(element(i)) # 将元素 element(i) 添加到列表 List 中`

2. 删除列表中的元素
    1. `list.pop() # 弹出（去掉）列表 list 中最后一个元素，并返回该元素的值`
        - `list.pop(i) # 弹出（去掉）列表 list 中索引为 i 的元素`
        - 注意：在遍历列表时，不能删除列表中的元素；故如果要在遍历列表 list 时删除列表元素，则应另外建立一张新表
    2. `list.remove(element(i)) # 删除列表中值为 element(i) 的**第 1 个**元素；若不存在这样的元素，返回错误值`


3. `list.index(element(i)) # 若元素 element(i) 在列表 list 中，返回其在列表中的索引`

4. `element(i) in list # 若元素 element(i) 在列表 list中，返回 True，否则返回False`

    - 常见于 for 循环中的特殊列表为 range(start, stop, step)

5. `list.extend(another_list) # 扩展 list，将另一张列表 another_list 中的内容添加到 list 尾部`

6. `[element for i in list] or [element for i in list ]` blabla...参考[列表推导式](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions)


# 参考资料 #

1. [The CodeSkulptor documentation](http://www.codeskulptor.org/docs.html)

2.[list-comprehensions](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions)