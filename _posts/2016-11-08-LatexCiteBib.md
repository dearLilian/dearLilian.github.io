---
layout: post
title: Latex引用Bib文件步骤
date: 2016-11-08 
tag: Latex
---


## 目录

* TOC 
{:toc}



### 引用```cite```包

- 首先我们要在tex文件前面添加使用```cite```包

```latex
\documentclass{article}
\usepackage{cite}
\begin{document}
```

### 文中引用对应论文

这个过程有两个步骤。

- 首先建立一个新的后缀为bib的文件，例如文件名为：```cited.bib```。其次google  scholar你要引用的paper，获取其bibtex，并copy到你的bib文件中。
- 另一方面，在你要引用该paper的位置，使用命令```\cite{<被引用paper的缩写名>}```

eg:我要引用 ```WAIM'08``` 的```Recommendation over a Heterogeneous Social Network```这篇paper
。我在google scholar上搜索到它的bibtex（具体步骤是搜索，点击引用，点击bibtex）是

```
@inproceedings{zhang2008recommendation,
  title={Recommendation over a heterogeneous social network},
  author={Zhang, Jing and Tang, Jie and Liang, Bangyong and Yang, Zi and Wang, Sijie and Zuo, Jingjing and Li, Juanzi},
  booktitle={Web-Age Information Management, 2008. WAIM'08. The Ninth International Conference on},
  pages={309--316},
  year={2008},
  organization={IEEE}
}
```

那么当前```cited.bib```文件中就包含上述内容。

然后我们在tex文件要引用该论文的位置添加```\cite{zhang2008recommendation}```


### ```tex```文末

在添加```cite```包引用后，还要注意，我们要在```tex```文件最后面添加引用对应bib文件的操作。具体添加如下代码(注意要在```\end{document}```前)：

```latex
...
\bibliographystyle{abbrv}
\bibliography{<bib文件名>}%%我们的例子应该是\bibliography{cited}
\end{document}
```

### 编译过程（引用知乎的回答）

- 用```pdfLaTeX```编译你的```.tex```文件 , 这是生成一个```.aux```的文件, 这告诉```BibTeX```将使用那些应用.
- 用```BibTeX```编译```.bib```文件.
- 再次用```pdfLaTeX```编译你的```.tex```文件, 这个时候在文档中已经包含了参考文献, 但此时引用的编号可能不正确.最后用 再再次```pdfLaTeX```编译你的```.tex```文件, 如果一切顺利的话, 这是所有东西都已正常了.


- 作者：swear
- 链接：<a href="https://www.zhihu.com/question/30344123/answer/53377390">https://www.zhihu.com/question/30344123/answer/53377390</a>
- 来源：知乎 著作权归作者所有，转载请联系作者获得授权。


### 结束

每次都要查资料,索性记录在这里.汗颜。