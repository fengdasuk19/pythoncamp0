# 如何在 markdown 语法下键入换行符(How to Newline in Markdown? )

## 标准 Markdown (Standard Markdown, SM) 版 ##

对于用惯 `Microsoft Word` 的人来说需要注意一点：写作者必须键入**2个连续的**`空格`之后再键入 1 个换行符（`Enter` * 1），才能完成`强制换行`这个动作（参考[[1]](https://github.com/typecho/typecho/issues/51)与[[2]](http://wowubuntu.com/markdown/#p)）。

也就是说，为了在 SM 中得到如下显示：  
Or you won't succed,   
only to get a long line like this sentence.

应键入以下代码：（1 个 [Space] 代表 1 个空格字符）  
`Or you won't succed, [Space][Space]`  
`only to get a long line like this sentence.`

否则，当你键入以下代码时：  
`Or you won't succed, `  
`only to get a long line like this sentence.`

你将得到如下显示：  
Or you won't succed, only to get a long line like this sentence.

类似地，通过 2 个连续的换行符（`Enter` * 2）可达到强制换段的目的。

Users who are used to typing in `Microsoft Word` need to notice this: to create a newline, you need to type **TWO CONSECUTIVE** `Space` before you type `Enter`, or to type a `Enter` followed by another new one.  

Namely, to get stuff like the following:  
Or you won't succed,   
only to get a long line like this sentence.

you need to type code like this:( each [Space] means one space character)  
`Or you won't succed, [Space][Space]`  
`only to get a long line like this sentence.`

Or when you type code like this:  
`Or you won't succed, `  
`only to get a long line like this sentence.`

you'll get the following:  
Or you won't succed, only to get a long line like this sentence.

Similarly, you can type two **TWO CONSECUTIVE** `Enter` to get a new paragraph.

## [GitHub Flavored Markdown(GFM)](https://help.github.com/articles/github-flavored-markdown/) 版 ##

经 [yzha3917](https://github.com/yzha3917) 的[提醒](https://github.com/OpenMindClub/OMOOC.py/issues/10#issuecomment-81923507)，我在 [《Writing on GitHub》](https://help.github.com/articles/writing-on-github/) 中发现了这个：

> Issues, comments, and pull request descriptions are written using GitHub Flavored Markdown along with some additional features to make writing content on GitHub easy.

也就是说在 **Issues**、**Comments**、**pull request descriptions** 这 3 部分采用了 GitHub 方言（GFM）处理，在这些地方写作而需要换行时，仅需像在 `Mircrosoft Word` 等传统 MS 文本处理软件中一样，键入 1 个换行符（`Enter` * 1）即可。

例如，还是上面那个例子，当在 GitHub 的上述 3 个地方书写时，仅需按照上面本在 SM 中失效的代码，即  
`Or you won't succed, `  
`only to get a long line like this sentence. `

即可得到下面的效果：  
Or you won't succed,   
only to get a long line like this sentence. 

## 参考资料  
1. [添加 markdown 回车换行语法 #51](https://github.com/typecho/typecho/issues/51)
2. [Markdown 语法说明 (简体中文版) ：段落和换行](http://wowubuntu.com/markdown/#p)
3. [Writing on GitHub](https://help.github.com/articles/writing-on-github/)
4. [Writing on GitHub - Newlines](https://help.github.com/articles/writing-on-github/#newlines)
