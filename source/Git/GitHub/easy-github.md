
## 假设 ##

假设在 H:\ 建立一个名为 `first-rep` 的仓库文件夹


## 在目标目录下建立仓库文件夹 ##

`cd h:\`

![](/../../Resource/GitHub/easy-gh-mkdir1.png)

`mkdir first-rep`

![](/../../Resource/GitHub/easy-gh-mkdir2.png)

`cd first-rep`

![](/../../Resource/GitHub/easy-gh-mkdir3.png)

## 初始化 Initialization ##

**`git init`**

![](/../../Resource/GitHub/easy-gh-init.png)

## 获取当前状态 Status ##

`git status`

![](/../../Resource/GitHub/easy-gh-status1.png)

**[GitHub 官方提示](https://try.github.io/levels/1/challenges/3)**

> 经常运行 `git status` 有利于仓库的健康
> 有时候事情会发生一些改变，而你没有注意到（这条命令可以帮你发现问题）

当添加了新文件时，如在 `first-rep` 文件夹下添加了文件 `file-1.txt`  
此时键入

`git status`

![](/../../Resource/GitHub/easy-gh-status1.png)

注意到。。。

## reset ##

`git reset`

![](/../../Resource/GitHub/easy-gh-reset.png)

## git add ##

键入 `ls`。。。。确认需要添加。。。

`git add file-1.txt`  
`git status`

![](/../../Resource/GitHub/easy-gh-add1.png)
  

++++++++++++++
`git commit -m '[Message Content]'`

![](/../../Resource/GitHub/easy-gh-commit1.png)


> The '-a' option
If you happen to delete a file without using 'git rm' you'll find that you still have to 'git rm' the deleted files from the working tree. You can save this step by using the '-a' option on 'git commit', which auto removes deleted files with the commit.

`git commit -am "Delete stuff"`  

++++++++++++++

`git log`

![](/../../Resource/GitHub/easy-gh-log1.png)
  

++++++++++++++

`git log --summary`

![](/../../Resource/GitHub/easy-gh-log2.png)

添加在线仓库地址

`git remote add origin [你的地址]`

从。。。点。。。复制，粘贴。。。


`git push -u origin master`

> The name of our remote is origin and the default local branch name is master. The -u tells Git to remember the parameters, so that next time we can simply run git push and Git will know what to do. Go ahead and push it!


以后只要

`git push`

别人修改了。。或者在线修改了。。。

`git pull origin master`  
++++++++++++++

`git checkout -- <target-name>`  
++++++++++++++

`git branch <branch-name>`  

++++++++++++++

You can switch branches using the git checkout <branch> command. Try it now to switch to the <branch-name> branch:

`git checkout <branch-name>`

`git checkout -b new_branch`  
=`git branch new_branch` + `git checkout new_branch`

to checkout and create a branch at the same time.   

+++++++++++++++++++++++

`git rm <target-name, e.g. '*.txt'>`


Removing one file is great and all, but what if you want to remove an entire folder? You can use the recursive option on git rm:

`git rm -r folder_of_cats`  

+++++++++++++++++++++++

`git merge <branch-name>`  


> Merge Conflicts
> Merge Conflicts can occur when changes are made to a file at the same time. A lot of people get really scared when a conflict happens, but fear not! They aren't that scary, you just need to decide which code to keep.
> Merge conflicts are beyond the scope of this course, but if you're interested in reading more, take a look the section of the [Pro Git book](http://git-scm.com/book) on [how conflicts are presented](http://git-scm.com/docs/git-merge#_how_conflicts_are_presented).

+++++++++++++++++++++++++

You can use git branch -d <branch name> to delete a branch. Go ahead and delete the clean_up branch now:

`git branch -d <branch-name>` 

> Force delete
> What if you have been working on a feature branch and you decide you really don't want this feature anymore? You might decide to delete the branch since you're scrapping the idea. You'll notice that git branch -d bad_feature doesn't work. This is because -d won't let you delete something that hasn't been merged.

> You can either add the --force (-f) option or use -D which combines -d -f together into one command. 

++++++++++++++++++++++

> Learning more about Git
> 
> 
> We only scratched the surface of Git in this course. There is so much more you can do with it. Check out the [Git documentation](http://git-scm.com/docs) for a full list of functions.
> 
> The [Pro Git book](http://git-scm.com/book), by Scott Chacon, is an excellent resource to teach you the inner workings of Git.
> 
> [help.github](https://help.github.com/) and GitHub Training are also great for anything related to Git in general and using Git with GitHub.

