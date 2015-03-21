# 未完成 #

1. clone 到本地

2. 得到书的 Git URL  
GitBook 》 MY BOOKS 》 [你的书名] 》 Settings 》 Publication 》 Git URL  
得到自己书的 Git 超链接：`https://git.gitbook.com/{{UserName}}/{{Book}}.git`

3. 第一次推送更新  
在 Git Shell 中 cd 到本地库下，输入
    > git push `Git URL of your book` master
 
4. 以后的推送
在 Git Shell 下输入
    > `git push`

5. 创建目录结构
 1. 编写 SUMMARY.md  
 例如下面这样写。。。
 2. 编译过程  
 若是第 1 次创建目录，输入`gitbook init`  
 否则，输入以下代码`gitbook build ./`
 3. 更新双推。。。

## 参考资料 ##

1. [Update your book using GIT](http://help.gitbook.com/build/push.html)
2. [gitbook double push](https://github.com/OpenMindClub/OMOOC.py/wiki/gitbook_double_push)
3. [git push confilct](https://github.com/OpenMindClub/OMOOC.py/wiki/git_push_confilct)
4. [用 Github、Markdown 和 GitBook 写开源书](http://www.waylau.com/using-github-markdown-gitbook-write-open-source-books/)
5. [使用 GitBook 写开源书](http://www.waylau.com/about-gitbook/)