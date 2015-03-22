## 添加评论插件 Disqus ##

### 前期准备 ###

 - 本地已安装 NPM

### 1 ###

打开 Node.js 命令行 `Node.js command prompt`，输入以下命令

> `npm install gitbook-plugin-disqus`

### 2 ###

建立 `book.json`，输入以下内容

{  
&nbsp;&nbsp;&nbsp;&nbsp;"plugins": [  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"disqus"  
&nbsp;&nbsp;&nbsp;&nbsp;],  
&nbsp;&nbsp;&nbsp;&nbsp;"pluginsConfig": {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"shortName": "<你刚才注册的shortName>"  
&nbsp;&nbsp;&nbsp;&nbsp;}  
} 

### 3 ###

重新编译书籍，推送，完成


## 参考资料 ##

1. [使用Gitbook制作电子书](http://www.ituring.com.cn/article/127645)
2. [disqus_setup](https://github.com/OpenMindClub/OMOOC.py/wiki/disqus_setup)