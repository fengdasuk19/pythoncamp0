# 点彩画板制作教程 #

1. 尝试 RGB

    1. 阅读CS 文档 Canvas -> draw text -> [Colors](http://www.codeskulptor.org/docs.html#Colors)  -> custome -> [Colors in CSS format](http://www.w3schools.com/cssref/css_colors_legal.asp)...

    2. 直接定义 `fc = rgb(255, 255, 0)` 代入 `draw_text` 的 `font_color` 处失败

    3. 改用 `rgb(255, 255, 0)` 代入 `draw_text` 的 `font_color` 处失败

    4. 改用 `(255, 255, 0)` 代入 `draw_text` 的 `font_color` 处提示必须是 string

    5. **改用 `fc = 'rgb(255, 255, 0)'` 代入 `draw_text` 的 `font_color` 处，成功**

2. 选择画笔（不含颜色）并绘制图像

    1. 考虑通过文字输入框输入字母来进行选择，因此首先需要解决对输入进行判断的问题。目标希望输入选择后在画布上打印选择，之后通过画笔对象来替代打印函数

    2. CodeSkulptor 连接的 python 版本不支持 `string.isalpha()` 方法（该方法用于判断字符串是否全为字符；类似有用的还有判断数字等，参见 python 官方[这篇文档](https://docs.python.org/2/library/stdtypes.html#str.isalpha)）

    3. 因为对 C 的方法（数据都是数值）较为熟悉，本想采用 `if input in range('a', 'z')` 来判断输入 input 是否在 'a' 到 'z' 中，发现提示出错 TypeError: start must be a integer，在本地python环境尝试 `print range('a', 'z')`，也是报错 TypeError: range() integer end argument expected, got str.

    4. 考虑到从更深一层看 C 的方法，当其能通过诸如 `'a'<'z'` 这样的表达式进行比较的时候，是通过 ASCII 码的比较进行运算的。因此以「python 取字符ascii」为关键词 Google，从[第一篇](http://outofmemory.cn/code-snippet/530/python-get-charaeter-ASCII-code-jiang-ASCII-number-switch-charaeter)中学会了 ord()方法， 因此通过以下代码完成判断

            if (ord(inp) in range(ord('a'), ord('z'))) or (ord(inp) in range(ord('A'), ord('Z'))):

    5. 尽管已经能成功地判断单字输入，然而紧跟着的测试出现了一个问题：当输入超过 1 个字符时会报错。本打算通过循环弹出后面的字符，但后来马上想到，只要保留字符串第 1 个字符时就可以了。因此修改判断条件为下

                if (ord(inp[0]) in range(ord('a'), ord('z'))) or (ord(inp[0]) in range(ord('A'), ord('Z'))):

    6. 这次输入长字符串时不会报错了。然而问题是，输入 `tr` 时，却没有按照预料的，在画布上打印 triangle，而是打印 Input t/r/c，即输入为字母但不是 t/r/c。检查代码发现之前为了使输入 `t` 与 `T` 效果一致，在总判断条件与接下来用于判断输入属于t/r/c还是非字母字符的语句之间使用了代码 `inp = inp.lower()`，但更改了总判断条件后没有修改这句。因此将该句修改为如下，成功通过测试

                inp = inp[0].lower()

    7. 考虑了一下，希望画笔的大小可调节，故设置了一输入框，由用户输入画笔印迹的大小 r （r 表示由落笔处即单击点到多边形的角上的距离，或圆半径），传递给程序。坐标计算公式如下图所示。而如果仅能实现整数控制画笔大小，又不符合我的愿望，因此打算用 float(inp) 来把输入内容 inp 转换为浮点数；问题是输入可能不一定是可转换类型（如输入字母等），当这样尝试转换时会造成 ValueError，而if-else语句无法处理异常值返回。想到猜数游戏中几个同学的代码中曾出现过 try-except 语句，于是就找到了糖糖糖同学的代码观摩了下，并找到了教程简单学习了下，然后用如下代码完成数值转换，转换成功，则将转换结果再转换回字符串，传递给即将打印在画板上的字符串变量，否则提示出错

                try:
                    p = float(inp)
                    outcome1 = str(p)
                except ValueError:
                    outcome1 = 'Pleas input a number.'

    8. 考虑到画笔大小必须是正数，因此试图通过以下表达式判断大小非负。然而此段代码于本地运行成功，于在线平台 CodeSkulptor 运行失败，于 test_positive 处提示错误 TypeError: Expecting a function in instanceof check, but got [object Object]。。。。。。。。。。。。

                        size_abs = math.fabs(brush_size)
                        test_positive = 1 / (1 + brush_size / size_abs)


    9. 此后可以开始制作画笔对象。创建了一个 Brushes 类。考虑到画印迹需要获取鼠标位置，因此通过 2 个全局变量 `center_x` 与 `center_y` 得到当的横、纵坐标。
        
    10. 由于需要传递 canvas 给画笔，从而使画笔能在画布上画，因此直接在 canvas 的触发函数 draw 中直接调用 Brushes 的方法。由于窗体加载成功，画布便被触发，从而一旦确认了画笔类型，画笔将直接在给定的坐标处留下印迹。基于此，有 2 个问题需要被解决：
        
        1. 必须将极小的负值作为初始值赋予 center_x 与 center_y。否则若初值是 (0, 0)，当确定了画笔大小后，画笔将自动在画布左上角绘制出第 1 个印迹，这通常是用户不希望得到的结果
            
        2. 当画笔为圆时，必须处理半径值为异常的情况。否则当输入 c 选择画笔时，或者改变半径为非正值时，将报错（例如，未输入画笔大小而先输入画笔种类 c 时，将返回 AssertionError）
 
    11. 因为发现当半径非正数时所显示的提示信息比较长，当前显示不完整（有一部分会溢出与下面的标签重叠），一开始试图通过增加标签（Label）长度的方法扩展，无效；后来想到了之前无意间玩窗体时「增加控制台长度」这个功能，尝试增加控制台长度，成功实现完整显示提示信息
        
    12. 之前步骤仅仅能实现在单击的地方绘制出图形，但当单击另一个地方时，图形又消失了。于是希望使用一个全局的列表来存储画笔痕迹的位置信息，每次点击历史是一个对象，属性为（坐标， 形状， 大小，颜色），此时的设计暂时不考虑颜色

        1. 首先，每次点击时应进行判断：如果画笔形状在画笔列表中，且画笔大小为正数，则将点击历史存入历史列表中
            
        2. 接下来，要在 draw 函数中绘制出历史，即在列表中循环绘制。这里有一个问题：必须区分历史存储信息和当前状态。也就是说，基本逻辑是这样的，同时做 2 件事：(1)设定了画笔样式 -> 点击 -> 判断画笔是否正常（形状在列表中，大小为正数） -> 判断通过，则把当前状态存入历史 (2)draw 函数在历史状态列表中不断循环，绘制出点过的痕迹
            
        3. 基于 2，不再使用全局变量来进行单击位置坐标的传递，而使用列表中的每个对象记录每次点击的位置信息，而在 draw 函数中通过读取每个对象的位置信息来完成绘制


    13. 至此，一个可以选择形状与大小的画板就做好了，之后我们将进行进一步的修饰。这阶段的代码[如下](https://github.com/fengdasuk19/omooc.py/blob/master/src/paint-board-20150425-1050am.py)

3. 


## 参考资料 ##

1. [CS 文档 - Colors](http://www.codeskulptor.org/docs.html#Colors)
2. [Colors in CSS format](http://www.w3schools.com/cssref/css_colors_legal.asp)
3. [Python Doc - 2.7.10rc0 - 5.Built-in Types - 5.6.1. String Methods](https://docs.python.org/2/library/stdtypes.html#str.isalpha)
4. [python获得字符的ASCII码，将ASCII数字转换为字符](http://outofmemory.cn/code-snippet/530/python-get-charaeter-ASCII-code-jiang-ASCII-number-switch-charaeter)
5. [简明 Python 教程 - 第13章 异常](http://sebug.net/paper/python/ch13s02.html)
6. [Python学习笔记（十）之错误和异常](http://greenlcat.diandian.com/post/2012-10-23/40041946525)
7. [paint-board-20150425-1050am.py](https://github.com/fengdasuk19/omooc.py/blob/master/src/paint-board-20150425-1050am.py)