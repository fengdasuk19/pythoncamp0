## 如何调用模块 simpleGUI ##

使用以下代码

`import simplegui`

## 窗体创建 ##

以下代码创建一个标题为 [headline] 的窗体 [frame_name]，其大小为 [a] * [b]

`[frame_name] = simplegui.create_frame('[headline]', [a], [b])`

用以下代码初始化窗体

`[frame_name].start()`

若没有初始化窗体，则任何有关窗体的更改（如添加按钮、文本框、画布……）都不会起作用。你将仍然得到一个窗体，但这个窗体没什么用……除了让你看着发呆以外

## 计时器 ##

以下代码创建一个名为 [timer_name] 的计时器，该计时器规定每 [x] ms 触发一次事件：执行函数 [fun]

`[timer_name] = simplegui.create_timer([x], [fun])`

以下代码触发计时器 [timer_name] 开始计时

`[timer_name].start()`

## 按钮 ##

在建立了窗体 [frame_name] 的基础上，使用以下代码，创建其上提示文字为 [按钮名> 的按钮，（宽度为 [按钮宽度]，）按下该按钮后将触发触发一次事件：执行函数 [fun]

`[frame_name].add_button([按钮名], [fun])`

或

`[frame_name].add_button([按钮名], [fun], [按钮宽度])`

## 建立文本框并获取输入 ##

在建立了窗体 [frame_name] 的基础上，使用以下代码，创建其上提示文字为 [按钮名] 的按钮，宽度为 [按钮宽度]，按下输入完毕、按下 `Enter` 后将触发触发一次事件：执行函数 [fun]

`[frame_name].add_input([提示信息], [fun], [文本框宽度])`

## 画布 Canvas ##

### 尺寸 ###

设尺寸为 a * b

那么，左上角是 [0, 0] 点，右下角是 [a-1, b-1]，因为 [0, 0] 本身也占 1 个像素点， 而横坐标所谓的 a 是指有 a 个像素点

### 触发 ###

设触发函数名为 [draw]

`def draw(canvas) :`  
&nbsp;&nbsp;&nbsp;&nbsp;`...`

`[frame_name].set_draw_handler(draw)`

### 覆盖 ###

根据触发函数 draw 中绘制图形的顺序，后面绘制的图案将覆盖先前绘制的图案

### 写字 ###

`canvas.draw_text(文本, 文本左下角点坐标, 文本字体大小, 文本颜色[, 字体])`

支持字体 "serif"（默认），"sans-serif"，以及"monospace"

需要在画布上直接显示信息时，在`文本`处使用包含文本的字符串  
需要在在画布上显示动态信息时，在`文本`处使用包含文本的**全局**变量（为什么要全局？因为信息是**动态**的，意味着传递该信息的变量很可能是要和canvas触发函数外的交互，因此该变量通常不是局部的）

### 画线 ###

`canvas.draw_line(点 1 坐标, 点 2 坐标, 线宽, 线色)`

### 折线 ###

`canvas.draw_polyline(顶点坐标列表, 线宽, 边框色)`

### 多边形 ###

`canvas.draw_polygon(顶点坐标列表, 线宽, 边框色[, 填充色])`

### 画圆 ###

`canvas.draw_circle(圆心坐标, 半径, 线宽, 边框色[, 填充色])`