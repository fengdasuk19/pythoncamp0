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

    8. 考虑到画笔大小必须是正数，因此试图通过以下表达式判断大小非负。然而此段代码于本地运行成功，于在线平台 CodeSkulptor 运行失败，于 test_positive 处提示错误 TypeError: Expecting a function in instanceof check, but got [object Object]。。。。。。。。。。。。[20150425 增补]学会了用 `raise` 强制返回异常值给系统过后，就不需要使用第 1 段代码了，而改用第 2 段代码

                        [第一段]
                        size_abs = math.fabs(brush_size)
                        test_positive = 1 / (1 + brush_size / size_abs)

                        [第二段]

                        if (brush_size <= 0):
                            raise ValueError



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

3. 接下来尝试为画笔添加颜色

    1. 尝试设置了 3 个文本框，用于分别输入在 R/G/B 3个维度的分量数值，触发事件均为：尝试将输入转换为 int 类型数值，并传递给相应的全局变量分量（用于储存画笔色的 R/G/B 分量数值）；一旦失败（非整形，或），返回异常并返回提示信息。代码如下：

            def set_R(inp):

                global color_R, color_hint
    
                try:
                    color_R = int(inp)
                    if ((color_R < 0) or (color_R > 255)):
                        return ValueError
                    color_hint = ''
                    color_label.set_text(color_hint)
                except:
                    color_hint = 'Input an integer, range:[0, 255]'
                    color_label.set_text(color_hint)
    
    2. 以上代码对非数值输入反应达到预期（标签提示 Input an integer, range:[0, 255] ），而对超过范围的输入并未产生预期效果。仔细检查代码，考虑到 return 语句是将返回值作为右值返回给调用函数的左值，因此 ValueError 并不能产生并返回给系统，从而实现跳转到 except 语句的目的。于是考虑了一种替代实现，代码如下：

            def set_R(inp):

                global color_R, color_hint
    
                try:
                    color_R = int(inp)
                    color_hint = ''
                    color_label.set_text(color_hint)
                    if (not color_R in range(0, 256)):
                        color_hint = 'Input an integer, range:[0, 255]'
                        color_label.set_text(color_hint)
                except:
                    color_hint = 'Input an integer, range:[0, 255]'
                    color_label.set_text(color_hint)

    3. 然而以上写法显然使用了重复的代码。能不能自己设定异常情况，当情况出现时，自动把异常值返回给系统呢？参考了[资料 6](http://greenlcat.diandian.com/post/2012-10-23/40041946525) 后，答案是有，设定条件后使用 `raise Some_type_of_Error` 即可。因此修改代码如下：

            def set_R(inp):

                global color_R, color_hint
    
                try:
                    color_R = int(inp)
                    if (not color_R in range(0, 256)):
                        raise ValueError
                    color_hint = ''
                    color_label.set_text(color_hint)
                except:
                    color_hint = 'Input an integer, range:[0, 255]'
                    color_label.set_text(color_hint)

    4.  此后简单地将几个颜色数值转化为字符串即可。这里有个点：为了方便起见，程序可以修改为：即便在输入数值后没有键入 Enter，在点击 Mix them! 后，程序也能主动获取文本框中的输入。因此，为文本框设置变量名，使用 `get_text()` 方法即可——但这显然还要增加各种判断，可能需要修改几个接口，因此暂时按下不做，待完成程序后再补充。。。。。。。。。。。即目前，按钮 Mix them! 的代码如下：

            def set_color():

                global color_R, color_G, color_B, color_mix

                color_mix = 'rgb(' + str(color_R) + ', ' + str(color_G) + ', ' + str(color_B) + ')' 
                color_label.set_text('Color: ' + color_mix)

4. 之后尝试增加回放功能。

    1. 一开始我考虑了每 interval 秒停滞一次，然而考虑过后发现这似乎没有可行性，考虑到对于画笔痕迹留在画布上的实现，是通过在列表 `history_list` 中循环绘制而完成的，于是改变思路为：创建另一个表 `save_list`，程序可保存之前画过的图，可清空历史列表 `history_list`；当点击回放后，每 interval 秒从 `save_list` 中取出 1 个对象添加到 `history_list`中；反复添加，直到添加数量到达保存列表 `save_list` 中元素个数的上限为止；且当回放时，点击回放没有反应；而当回放结束后，不仅画布上的图和保存的图一致，历史列表也要回到保存时的状态。
    
    2. 考虑到该过程需要通过计时器 timer 来实现，而启动和停止计时器需要在计时器触发函数外部才能对计时器起作用；又考虑到计时器起作用的范围正是在画布 canvas 处表现出来，因此决定采用一个标志变量 `in_play` 来进行通信，判断是否在回放过程中；同时，由于只有在回放时才需要计时器，因此，计时器在单击按钮后被触发，而只有在触发之后，程序中才含有计时器对象，因此还需要一个标志变量 `timer_created` 来表明计时器对象是否已经被创建（只有在已经存在计时器的情况下，才能停止计时器）。

    3. 如果没有保存任何图像，显然没法进行回放，因此要判断保存信息的列表 `save_list` 是否为空

    4. 有可能我只需要恢复保存的图像即可，不需要绘制过程的信息，因此增加了一个「一键恢复原图」的按钮
    
    5. 考虑到保存过后要作新的图，因此增加了清空画布的按钮，一开始本考虑了覆盖画布或者设置画布背景色的方法，发现无效（设置黑色），于是考虑到画图的实质是 canvas 中对历史列表 `history_draw` 中对象的循环绘制，因此决定直接全局声明该列表，并赋值为空列表即实现了该功能

    6. 至于改变绘制回放速度，由于我对回放的理解就是每 interval 秒往列表中添加 1 个对象，因此方法就是使添加对象的速度变慢。怎么做到这点？由于 interval 是通过全局变量（可由用户输入）控制的，因此将此全局变量赋值给计时器触发间隔时间即可

5. 最后是增加文件输入与输出功能

    1. 首先考虑了一下，要先写读文件的过程还是写文件的过程呢？最后决定先编制写文件的过程：因为读取的文件一定是按一定接口要求生成的，满足某种固定格式，这个格式从哪里来？肯定是从输出该文件的程序来。所以先编制写文件的程序
    
    2. 考虑了一下，查看了一些资料，如[Python 文件I/O](http://www.w3cschool.cc/python/python-files-io.html)以及《笨办法学 Python》的[Exercise 15: Reading Files](http://learnpythonthehardway.org/book/ex15.html)、[Exercise 16: Reading and Writing Files](http://learnpythonthehardway.org/book/ex16.html)、[Exercise 17: More Files](http://learnpythonthehardway.org/book/ex17.html)，然后设计了一份输出格式。关于格式，有几点需要说明

        1. 一开始本打算直接用 tuple 保存坐标，后来一想，这种格式不便读取时的处理（还要写代码判断非数字字符），于是决定改成用 2 行数值保存
        
        2. 而一开始直接向文件中写入数据的时候，发现直接写入数值失败，提示 TypeError: expected a character buffer oject。仔细察看[资料](http://www.w3cschool.cc/python/python-files-io.html)发现这里提到了一句话，于是我用 str() 方法将数值转化为字符串，从而成功将数值写入文件
            
            > Write()方法可将任何字符串写入一个打开的文件。

        4. 如果输出文件成功，最好给用户提示下，否则用户必须开文件夹察看才知道是否成功生成文件了
        
    3. 随后进入读取文件过程的编写
    
        1. 使用 try-except 语句来完成一个功能：如果读取的文件不存在返回错误时，给出提示信息
        
        2. 原计划使用 try-except 来完成判断文件尾 EOFError 的功能，后来想到，似乎无法完成循环，于是考虑了其他办法：曾考虑了 while 循环（受 C 语言中存在文件尾标志 EOF 的影响，本打算设置判断条件为：如果不到文件尾，继续循环读取文件），但最终测试失败（Python 中不存在定义为 EOF 的量，发生 NameError: name 'EOF' is not defined）
        
        3. 于是最终打算采用次数已知的 while 循环（其实可以被 for 循环替代，一个意思），循环次数为保存列表中的元素个数，当读取完所有元素后，停止读取。每次读取 1 行，使用 `file_object.readline()` 方法
        
        4. （！大坑一个）然而，在测试过程中，发现尽管读取了数据，却不能成功绘制回放，这是为什么？抓耳挠腮观察了半天，经过在读取后添加 for-print 语句把每个对象中的每个属性都打印一遍后，发现了问题：似乎是由于字符串本身存储的原因。。。。。（这里或许可以增加探究？）。。。。。加上我的输出格式是每输出一个属性就加 1 个换行符，在读取到字符串时，读入了超过 1 个换行符，于是当我打印的时候（我使用 for-print 察看对象属性时，是每个属性用 1 个 print 输出（除了坐标，分为 2 项输出），这就使每个属性应该只占 1 行），原类型（即作为对象属性时的数据类型）是字符串类型的 2 种属性，每次在打印了自身之后，还多打了 1~2 个换行符（？！）。一开始我不以为意，以为和这个无关。后来实在找不到出口，想来想去，想到：**读取数据后，把读取到的数据传递给新对象的属性；绘制图形时，canvas 是读取新对象的属性来进行绘制的；既然赋予新对象的属性值在 for-print 中显示异常，会不会就是因为这个异常读取，导致赋予新对象的属性值本身异常，从而在实际绘制循环中无法认出这个属性值，因此绘制失败？**想到这里，由于直接作为字符串对象存入对象属性中的值只有「形状」与「颜色」共 2 个值，而这 2 个值的截断处理也很容易，因此马上简单截取了这 2 个值的有效部分。至此，读取成功，大坑解决。 内牛满面！
        
        5. 读取成功后，仍然给与用户提示；若读取不存在的文件，也给出提示

6. 至此，基本的点彩画板完成了，达到以下要求

    - 有画笔
    - 有颜色
    - 可点绘
    - 可回放
    - 回放速度可调节
    - 回放可输出为文件

7. 当然，目测有几个小瑕疵有待完善

    1. 在 R/G/B 输入框输入后，能否在直接点击 Mix them! 时就直接获取文本，直接混合颜色，而不必每次输入都敲击 Enter？ 答案当然是可以的，使用 `input_box.get_text()` 方法，但需要修改代码判断输入是否符合要求
    
    2. 考虑到面向对象有臃肿的风评，每次绘制都制作新的对象，是否会增加内存开销？换成通过全局列表来存储和通信，是否会速度更快？我猜想，用数组来重写这个程序中各种属性的保存是可以做到的

    3. 没有限制只能记录 1024 次（……详见课程 1.1py 期待）

## 参考资料 ##

1. [CS 文档 - Colors](http://www.codeskulptor.org/docs.html#Colors)
2. [Colors in CSS format](http://www.w3schools.com/cssref/css_colors_legal.asp)
3. [Python Doc - 2.7.10rc0 - 5.Built-in Types - 5.6.1. String Methods](https://docs.python.org/2/library/stdtypes.html#str.isalpha)
4. [python获得字符的ASCII码，将ASCII数字转换为字符](http://outofmemory.cn/code-snippet/530/python-get-charaeter-ASCII-code-jiang-ASCII-number-switch-charaeter)
5. [简明 Python 教程 - 第13章 异常](http://sebug.net/paper/python/ch13s02.html)
6. [Python学习笔记（十）之错误和异常](http://greenlcat.diandian.com/post/2012-10-23/40041946525)
7. [paint-board-20150425-1050am.py](https://github.com/fengdasuk19/omooc.py/blob/master/src/paint-board-20150425-1050am.py)
8. [Python 文件I/O](http://www.w3cschool.cc/python/python-files-io.html)
9. [Exercise 15: Reading Files](http://learnpythonthehardway.org/book/ex15.html)
10. [Exercise 16: Reading and Writing Files](http://learnpythonthehardway.org/book/ex16.html)
11. [Exercise 17: More Files](http://learnpythonthehardway.org/book/ex17.html)