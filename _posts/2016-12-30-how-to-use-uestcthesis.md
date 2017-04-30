---
layout: post
title: UESTCthesis模板使用（持续更新）
date: 2016-12-30
tag: Latex
---

* TOC 
{:toc}


## 写在前面的话

本文记录了使用UESTCthesis写论文过程中的一些问题及解决之法。


## UESTCthesis模板简介使用入门

UESTCthesis latex模板是时富军同学为了方便UESTCer们写毕业论文（学士硕士or博士）而编写的latex模板。将该学校要求的论文的基本格式都基本覆盖。

该模板的主要目录结构如下：


- chapters/
	- chapter1.tex(第一章的内容，名字可以自定义)
	- chapter2.tex
	- ...
- contents/
	- acknowledgements.tex : 致谢部分
	- appendix.tex : 附录部分
	- Cabstract.tex : 中文摘要部分
	- cv.tex : 个人简历部分
	- Eabstract.tex : 英文摘要部分
	- original.tex: 英文原文
	- publications.bib : 出版论文
	- reference.bib : 参考文献
	- titlepage.tex : 标题部分
	- translation.tex : 原文翻译
- dependencies/ : 所依赖的宏包
- pics/ : 文中要引用的图片
- clean.bat : 清除日志文件及输出的win脚本
- compile.bat : 完整的编译的win脚本
- main.tex : 论文的主文件
- uestcthesis.cls:正文等格式定义文件
- uestcthesis.bst:参考文件格式定义文件



## 问题集锦

### 如何添加新的宏包？

对于一般的latex编辑，我们通常是在文件的documentclass声明与begin{document}声明之间使用usepackage命令引用所需要的宏包。
然而在该模板中，使用宏包的命令是在uestcthesis.cls文件中声明的。使用如下方式：

```latex
\RequirePackage[选项]{宏包名}
```

如果需要重新定义宏包中的环境或选项，则在对应的宏包声明下面使用命令```renewcommand```。

更新：后来发现不是必须要这样。像一般的直接放在主文件的导言区就可以了。

### 如何设置参考文献引用为上标格式？

打开```uestcthesis.cls```文件，查找natbib，即该宏包被引用的那一行命令，然后在选项上（[]里）添加super,square。表示使用方括号与上标显示。

更多设置可参考：<a href="http://blog.sina.com.cn/s/blog_5e16f1770100lqh2.html">LaTeX技巧355：natbib宏包使用说明中文版</a>


### 如何使用algorithm2e包编写算法伪代码？

参考<a href="http://blog.sina.com.cn/s/blog_5e16f1770100lp7u.html">http://blog.sina.com.cn/s/blog_5e16f1770100lp7u.html</a>

### 脚注问题

模板的脚注上面的横线前面增加了空，但实际上不应该空。

修改方法：打开cls文件，搜索```\renewcommand{\footnoterule}{\vfill\noindent```，删除下一行中的```\hspace{7.4mm}```即可。



