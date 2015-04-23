# 面向对象（Object-Oriented）设计 #

面向对象的一个主要目标是：增加代码的可复用性，减少代码量

类（class）是一种可由用户自行定义的数据类型，用于封装一些数据，对这些数据有某些特定的函数作为其操作方法（由于这些函数作用域仅为定义这些函数的类，因而通常不称之为函数，而成为该类的方法）。

定义了类之后，通过实例化来构建一个对象。

## 定义类的语法 ##

`class ClassName: # 类名通常以大写字母开头`  
&nbsp;&nbsp;&nbsp;&nbsp;`def __init__(self, arg_0, arg_1, ..., )`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 该方法将创建对象的一些域（属性），并用实参初始化这些域（属性）`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 通过 对象名.域（属性） 的方式引用属于某对象的域（属性）`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`self.arg_0 = val_0`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`self.arg_1 = val_1`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`...`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 该方法不返回任何值`

&nbsp;&nbsp;&nbsp;&nbsp;`def __str__(self)`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 该方法将将指明，当用户要求打印该对象时，返回的值 s_value`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# ...`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`return s_value`  

&nbsp;&nbsp;&nbsp;&nbsp;`def other_method_0(arg_0, arg_1, ...)`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 像定义普通函数一样定义该类的方法`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 用户并不需要知道该方法是怎么实现的`
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 只要知道接口需要什么，会输出什么即可`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`# 定义者也不用担心用户使用未提供的方法：用户只能使用定义者提供的方法`  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`...`  

## 使/用类与对象的语法 ##

例如，已经定义了一个类 `Examples_class`，定义了方法...

test0 = Examples_class('Math', 7)
print test0
...........


## 发现错误时... ##

1. 语法错误

    1. 属性错误（Attribute Error）

        检查应用该方法的对象类型  
        若不确定类型，使用 `print type(object_name)` 来打印出对象类型名

2. 语义错误

    1. 别名
    
        在使用面向对象设计时，注意 `object_1 = object_0` 的意思是把对象 `object_0` 的地址赋予 `object_1`，即使 `object_1` 指向 `object_0` 指向的内存区域，而不是创建一个 `object_0` 的副本并命名为 `object_1`。

        如何创建一个对象的副本呢？使用如下代码

            import copy
            object_1 = copy.copy(object_0)

        关于创建对象的副本。。深复制。。浅复制。。。待续。。

        当通过对象对外部数据进行操作时，有类似的问题：例如通过对象作为接口操作列表 lists 时，如果希望每次都创建一个原始列表 lists 的副本并修改之、存储之，则应在引用 lists 时使用 list()函数，即

            list(lists)

        。。。（待续）




## 参考资料 ##

1. [探索 Python 的变量、类型和引用](http://upsuper.github.io/blog/python-variable-type-and-reference.html)
2. [Python 拷贝对象（深拷贝deepcopy与浅拷贝copy）](http://www.jb51.net/article/15714.htm)
3. [8.17. copy — Shallow and deep copy operations](https://docs.python.org/2/library/copy.html)
4. [Python学习笔记（3）](http://www.jianshu.com/p/14bc454170a0)
5. [Python引用与复制之浅复制](http://www.oschina.net/question/872916_84343)
6. [python的赋值、浅拷贝和深拷贝 ](http://blog.chinaunix.net/uid-26137687-id-3043428.html)
7. [python的赋值、浅拷贝和深拷贝](http://www.cnblogs.com/wait123/archive/2011/10/10/2206580.html)