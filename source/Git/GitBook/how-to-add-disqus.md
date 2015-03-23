## 添加评论插件 Disqus ##

### 前期准备 ###

 - 本地已安装 NPM
 - 在 [https://disqus.com/](https://disqus.com/) 注册了账户，并在登陆后从右上角齿轮处的下拉列表进入 [Add Disqus To Site](https://disqus.com/admin/create/) ，特别注意 `Choose your unique Disqus URL` 这一项（也就是 `shortname`），下文要用到
 - 在注册后跳转到的页面中进入 Settings，在 Trusted Domains 这里填入

    gitbooks.io（请注意是gitbook【s】.io）
    gitbook.com

### 1 ###

打开 Node.js 命令行 `Node.js command prompt`，输入以下命令

> `npm install gitbook-plugin-disqus`

### 2 ###

建立 `book.json`，输入以下内容

{
&nbsp;&nbsp;"plugins": ["disqus"],  
&nbsp;&nbsp;"pluginsConfig": {  
&nbsp;&nbsp;&nbsp;&nbsp;"disqus": {  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"shortName": "你注册的 `shortname` 代替这里"  
&nbsp;&nbsp;&nbsp;&nbsp;}  
&nbsp;&nbsp;}  
}

### 3 ###

重新编译书籍，推送，完成

### 4 ###

注意


## 参考资料 ##

1. [使用Gitbook制作电子书](http://www.ituring.com.cn/article/127645)
2. [disqus_setup](https://github.com/OpenMindClub/OMOOC.py/wiki/disqus_setup)