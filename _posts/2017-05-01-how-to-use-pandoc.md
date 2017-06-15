---
layout: post
title: pandoc使用简介
date: 2017-05-01
tag: 工具
---


## 目录

* TOC 
{:toc}


## 一、安装pandoc

### 1. win系统

- 在pandoc官网下载msi安装包。[官网安装指南](http://pandoc.org/installing.html)
- 对于Pdf输出，则必须要用到latex。故推荐安装MikTex(这里不再赘述)。

下载msi后，直接双击安装即可。一般默认安装在C:\Program Files (x86)\Pandoc。

### 2. linux系统（只在Ubuntu下实践过）

linux系统下一般都是在线使用命令行安装。不过在线安装的版本都比较老。所以推荐使用deb包安装。

- 下载deb包，[链接](https://github.com/jgm/pandoc/releases/tag/1.19.2.1)
- 假设上述安装包重命名为pandoc.deb，命令行安装：

```
sudo dpkg -i pandoc.deb
```

- 对于pdf输出需要的，安装Tex Live。这个比较麻烦，主要是时间叫长。
在线：
```shell
sudo apt-get install texlive
```

离线：下载texlive镜像（有2G多），然后安装，具体参考（http://www.cnblogs.com/wenbosheng/archive/2016/08/03/5725834.html）

## 二、设置latex模板

### 1. win系统下

新建一个latex模板：template.latex

内容为：

```latex
\documentclass[$if(fontsize)$$fontsize$,$endif$$if(lang)$$babel-lang$,$endif$$if(papersize)$$papersize$paper,$endif$$for(classoption)$$classoption$$sep$,$endfor$]{$documentclass$}
$if(beamerarticle)$
\usepackage{beamerarticle} % needs to be loaded first
$endif$
$if(fontfamily)$
\usepackage[$for(fontfamilyoptions)$$fontfamilyoptions$$sep$,$endfor$]{$fontfamily$}
$else$
\usepackage{lmodern}
$endif$
$if(linestretch)$
\usepackage{setspace}
\setstretch{$linestretch$}
$endif$
\usepackage{amssymb,amsmath}
\usepackage{ifxetex,ifluatex}
\usepackage{fixltx2e} % provides \textsubscript
\ifnum 0\ifxetex 1\fi\ifluatex 1\fi=0 % if pdftex
  \usepackage[$if(fontenc)$$fontenc$$else$T1$endif$]{fontenc}
  \usepackage[utf8]{inputenc}
$if(euro)$
  \usepackage{eurosym}
$endif$
\else % if luatex or xelatex
  \ifxetex
    \usepackage{mathspec}
  \else
    \usepackage{fontspec}
  \fi
  \defaultfontfeatures{Ligatures=TeX,Scale=MatchLowercase}
$for(fontfamilies)$
  \newfontfamily{$fontfamilies.name$}[$fontfamilies.options$]{$fontfamilies.font$}
$endfor$
$if(euro)$
  \newcommand{\euro}{€}
$endif$
$if(mainfont)$
    \setmainfont[$for(mainfontoptions)$$mainfontoptions$$sep$,$endfor$]{$mainfont$}
$endif$
$if(sansfont)$
    \setsansfont[$for(sansfontoptions)$$sansfontoptions$$sep$,$endfor$]{$sansfont$}
$endif$
$if(monofont)$
    \setmonofont[Mapping=tex-ansi$if(monofontoptions)$,$for(monofontoptions)$$monofontoptions$$sep$,$endfor$$endif$]{$monofont$}
$endif$
$if(mathfont)$
    \setmathfont(Digits,Latin,Greek)[$for(mathfontoptions)$$mathfontoptions$$sep$,$endfor$]{$mathfont$}
$endif$
\XeTeXlinebreaklocale "zh"
$if(CJKmainfont)$
    \usepackage{xeCJK}
    \setCJKmainfont[$for(CJKoptions)$$CJKoptions$$sep$,$endfor$]{$CJKmainfont$}
$endif$
\fi
% use upquote if available, for straight quotes in verbatim environments
\IfFileExists{upquote.sty}{\usepackage{upquote}}{}
% use microtype if available
\IfFileExists{microtype.sty}{%
\usepackage[$for(microtypeoptions)$$microtypeoptions$$sep$,$endfor$]{microtype}
\UseMicrotypeSet[protrusion]{basicmath} % disable protrusion for tt fonts
}{}
\PassOptionsToPackage{hyphens}{url} % url is loaded by hyperref
$if(verbatim-in-note)$
\usepackage{fancyvrb}
$endif$
\usepackage[unicode=true]{hyperref}
$if(colorlinks)$
\PassOptionsToPackage{usenames,dvipsnames}{color} % color is loaded by hyperref
$endif$
\hypersetup{
$if(title-meta)$
            pdftitle={$title-meta$},
$endif$
$if(author-meta)$
            pdfauthor={$author-meta$},
$endif$
$if(keywords)$
            pdfkeywords={$for(keywords)$$keywords$$sep$, $endfor$},
$endif$
$if(colorlinks)$
            colorlinks=true,
            linkcolor=$if(linkcolor)$$linkcolor$$else$Maroon$endif$,
            citecolor=$if(citecolor)$$citecolor$$else$Blue$endif$,
            urlcolor=$if(urlcolor)$$urlcolor$$else$Blue$endif$,
$else$
            pdfborder={0 0 0},
$endif$
            breaklinks=true}
\urlstyle{same}  % don't use monospace font for urls
$if(verbatim-in-note)$
\VerbatimFootnotes % allows verbatim text in footnotes
$endif$
$if(geometry)$
\usepackage[$for(geometry)$$geometry$$sep$,$endfor$]{geometry}
$endif$
$if(lang)$
\ifnum 0\ifxetex 1\fi\ifluatex 1\fi=0 % if pdftex
  \usepackage[shorthands=off,$for(babel-otherlangs)$$babel-otherlangs$,$endfor$main=$babel-lang$]{babel}
$if(babel-newcommands)$
  $babel-newcommands$
$endif$
\else
  \usepackage{polyglossia}
  \setmainlanguage[$polyglossia-lang.options$]{$polyglossia-lang.name$}
$for(polyglossia-otherlangs)$
  \setotherlanguage[$polyglossia-otherlangs.options$]{$polyglossia-otherlangs.name$}
$endfor$
\fi
$endif$
$if(natbib)$
\usepackage{natbib}
\bibliographystyle{$if(biblio-style)$$biblio-style$$else$plainnat$endif$}
$endif$
$if(biblatex)$
\usepackage[$if(biblio-style)$style=$biblio-style$,$endif$$for(biblatexoptions)$$biblatexoptions$$sep$,$endfor$]{biblatex}
$for(bibliography)$
\addbibresource{$bibliography$}
$endfor$
$endif$
$if(listings)$
\usepackage{listings}
$endif$
$if(lhs)$
\lstnewenvironment{code}{\lstset{language=Haskell,basicstyle=\small\ttfamily}}{}
$endif$
$if(highlighting-macros)$
$highlighting-macros$
$endif$
$if(tables)$
\usepackage{longtable,booktabs}
% Fix footnotes in tables (requires footnote package)
\IfFileExists{footnote.sty}{\usepackage{footnote}\makesavenoteenv{long table}}{}
$endif$
$if(graphics)$
\usepackage{graphicx,grffile}
\makeatletter
\def\maxwidth{\ifdim\Gin@nat@width>\linewidth\linewidth\else\Gin@nat@width\fi}
\def\maxheight{\ifdim\Gin@nat@height>\textheight\textheight\else\Gin@nat@height\fi}
\makeatother
% Scale images if necessary, so that they will not overflow the page
% margins by default, and it is still possible to overwrite the defaults
% using explicit options in \includegraphics[width, height, ...]{}
\setkeys{Gin}{width=\maxwidth,height=\maxheight,keepaspectratio}
$endif$
$if(links-as-notes)$
% Make links footnotes instead of hotlinks:
\renewcommand{\href}[2]{#2\footnote{\url{#1}}}
$endif$
$if(strikeout)$
\usepackage[normalem]{ulem}
% avoid problems with \sout in headers with hyperref:
\pdfstringdefDisableCommands{\renewcommand{\sout}{}}
$endif$
$if(indent)$
$else$
\IfFileExists{parskip.sty}{%
\usepackage{parskip}
}{% else
\setlength{\parindent}{0pt}
\setlength{\parskip}{6pt plus 2pt minus 1pt}
}
$endif$
\setlength{\emergencystretch}{3em}  % prevent overfull lines
\providecommand{\tightlist}{%
  \setlength{\itemsep}{0pt}\setlength{\parskip}{0pt}}
$if(numbersections)$
\setcounter{secnumdepth}{$if(secnumdepth)$$secnumdepth$$else$5$endif$}
$else$
\setcounter{secnumdepth}{0}
$endif$
$if(subparagraph)$
$else$
% Redefines (sub)paragraphs to behave more like sections
\ifx\paragraph\undefined\else
\let\oldparagraph\paragraph
\renewcommand{\paragraph}[1]{\oldparagraph{#1}\mbox{}}
\fi
\ifx\subparagraph\undefined\else
\let\oldsubparagraph\subparagraph
\renewcommand{\subparagraph}[1]{\oldsubparagraph{#1}\mbox{}}
\fi
$endif$
$if(dir)$
\ifxetex
  % load bidi as late as possible as it modifies e.g. graphicx
  $if(latex-dir-rtl)$
  \usepackage[RTLdocument]{bidi}
  $else$
  \usepackage{bidi}
  $endif$
\fi
\ifnum 0\ifxetex 1\fi\ifluatex 1\fi=0 % if pdftex
  \TeXXeTstate=1
  \newcommand{\RL}[1]{\beginR #1\endR}
  \newcommand{\LR}[1]{\beginL #1\endL}
  \newenvironment{RTL}{\beginR}{\endR}
  \newenvironment{LTR}{\beginL}{\endL}
\fi
$endif$

% set default figure placement to htbp
\makeatletter
\def\fps@figure{htbp}
\makeatother

$for(header-includes)$
$header-includes$
$endfor$

$if(title)$
\title{$title$$if(thanks)$\thanks{$thanks$}$endif$}
$endif$
$if(subtitle)$
\providecommand{\subtitle}[1]{}
\subtitle{$subtitle$}
$endif$
$if(author)$
\author{$for(author)$$author$$sep$ \and $endfor$}
$endif$
$if(institute)$
\providecommand{\institute}[1]{}
\institute{$for(institute)$$institute$$sep$ \and $endfor$}
$endif$
\date{$date$}

\begin{document}
$if(title)$
\maketitle
$endif$
$if(abstract)$
\begin{abstract}
$abstract$
\end{abstract}
$endif$

$for(include-before)$
$include-before$

$endfor$
$if(toc)$
{
$if(colorlinks)$
\hypersetup{linkcolor=$if(toccolor)$$toccolor$$else$black$endif$}
$endif$
\setcounter{tocdepth}{$toc-depth$}
\tableofcontents
}
$endif$
$if(lot)$
\listoftables
$endif$
$if(lof)$
\listoffigures
$endif$
$body$

$if(natbib)$
$if(bibliography)$
$if(biblio-title)$
$if(book-class)$
\renewcommand\bibname{$biblio-title$}
$else$
\renewcommand\refname{$biblio-title$}
$endif$
$endif$
\bibliography{$for(bibliography)$$bibliography$$sep$,$endfor$}

$endif$
$endif$
$if(biblatex)$
\printbibliography$if(biblio-title)$[title=$biblio-title$]$endif$

$endif$
$for(include-after)$
$include-after$

$endfor$
\end{document}
```

保存，放到一个常用目录，比如：用户目录，```ddd```
### 2. linux系统下 

参考：http://www.bagualu.net/wordpress/archives/5396


## 三、编译转换

### 1. win系统下

- md转换为pdf，新建一个bat脚本文件，toPDF.bat:

```bat
pandoc -f markdown -t latex -s 
-M mainfont:simsun.ttc -M sansfont:simsun.ttc -M monofont:simsun.ttc 
--latex-engine=xelatex --toc -M geometry:"top=1in, inner=1in,outer=1in,bottom=1in, headheight=3ex, headsep=2ex" 
--template=C:/Users/wenba/template.tex %1 -o %2
```

可以将该脚本文件放在一个加入系统环境变量的路径，比如pandoc的安装路径下```C:\Program Files (x86)\Pandoc```。

上述的```simsun.ttc```是win系统下的宋体字体，也可以换成其他的，win下字体在```C:\Windows\Fonts```路径下，不过你打开后看到的是它的宋体之类的名字，
而不是英文的名字，可以通过选中某个字体右键查看属性，可以看到其文件名。可以用其他字体替换```simsum.ttc```。记得要带后缀，否则找不到。

然后测试，新建一个markdown文件source.md：

```markdown
# 标题：这是一个测试文件

## 一、测试一

可以在这里输入你的内容

## 二、测试二

继续输入：

- 关注我
- 关注我
- 关注我

## 三、测试三

重要的事情说三遍：

1. 关注我
2. 关注我
3. 关注我
```

在cmd下运行：

```cmd
toPDF source.md target.pdf
```

其中source.md是你要转换的markdown文件名，target.pdf是目标文件名。效果如下图：

<center><img src="/images/posts/mdtest" width = "70%"/></center>


- markdown转pdf slides

新建脚本：

```bat
pandoc -t beamer -M mainfont:simsun.ttc -M sansfont:simsun.ttc -M monofont:simsun.ttc
 -i --latex-engine=xelatex 
 -M geometry:"top=1in, inner=1in,outer=1in,bottom=1in, headheight=3ex, headsep=2ex" %1 -o %2
```

这里没有指定一个模板文件，会使得输出的行如果过长不会自动换行。

但是如果按照上面那个指定模板又报一些关于latex包的错，尚未解决。

所以只能编辑Md文件的时候不要写太长的行。

### 2. linux系统下

类似的。可参考[http://www.bagualu.net/wordpress/archives/5396](http://www.bagualu.net/wordpress/archives/5396)