---
layout: post
title: python之matplotlib学习
date: 2015-09-29
tag: 语言
---


## 目录

* TOC 
{:toc}



本文转自<a href="http://blog.csdn.net/lilianforever/article/details/52163370">我的CSDN博客</a>。

前言：matplotlib是一个python的第三方库，里面的pyplot可以用来作图。下面来学习一下如何使用它的资源。


<h2>一、使用前</h2>

首先在python中使用任何第三方库时，都必须先将其引入。即：

```python
import matplotlib.pyplot as plt
```
或者：

```python
from matplotlib.pyplot import *
```

<h2>二、用法</h2>

<h3>1.建立空白图</h3>

```python
fig = plt.figure()
```

得到如下图的效果：
图片上方-----（这里由于图是空白的所以看不见内容）--------------------------------

![figure1](http://img.blog.csdn.net/20150928161109227)
图片下方--------（这里由于图是空白的所以看不见内容）----------------------------------

也可以指定所建立图的大小

```python
fig = plt.figure(figsize=(4,2))
```

效果如下：
图片上方-----（这里由于图是空白的所以看不见内容）--------------------------------

![figure2](http://img.blog.csdn.net/20150928161318733)
图片下方--------（这里由于图是空白的所以看不见内容）----------------------------------
当然我们也可以建立一个包含多个子图的图，使用语句：

```python
plt.figure(figsize=(12,6))
plt.subplot(231)
plt.subplot(232)
plt.subplot(233)
plt.subplot(234)
plt.subplot(235)
plt.subplot(236)
plt.show()
```
效果如下：


![figure3](http://img.blog.csdn.net/20150928162013567)

其中`subplot()`函数中的三个数字，第一个表示Y轴方向的子图个数，第二个表示X轴方向的子图个数，第三个则表示当前要画图的焦点。


当然上述写法并不是唯一的，比如我们也可以这样写：

```python
fig = plt.figure(figsize=(6, 6))
ax1 = fig.add_subplot(221)
ax2 = fig.add_subplot(222)
ax3 = fig.add_subplot(223)
ax4 = fig.add_subplot(224)
plt.show()
```
效果如下：

![figure4](http://img.blog.csdn.net/20150928162601804)

可以看到图中的x,y轴坐标都是从0到1，当然有时候我们需要其他的坐标起始值。
此时可以使用语句指定：

```python
ax1.axis([-1, 1, -1, 1])
```
或者：

```python
plt.axis([-1, 1, -1, 1])
```

效果如下：

![figure5](http://img.blog.csdn.net/20150928164659989)

注意第一个子图。

<h3>2.向空白图中添加内容，想你所想，画你所想</h3>

首先给出一组数据：
```
x = [1, 2, 3, 4, 5]
y = [2.3, 3.4, 1.2, 6.6, 7.0]
```
<h4>A.画散点图*</h4>

```python
plt.scatter(x, y, color='r', marker='+')
plt.show()
```
效果如下：

![scatter](http://img.blog.csdn.net/20150928165938313)

这里的参数意义：

 1.  x为横坐标向量，y为纵坐标向量，x,y的长度必须一致。
 2. 控制颜色：color为散点的颜色标志，常用color的表示如下：

	```
	b---blue   c---cyan  g---green    k----black
	m---magenta r---red  w---white    y----yellow
	```
	
	有四种表示颜色的方式:
	
	 - 用全名
	 - 16进制，如：#FF00FF
	 - 灰度强度，如：‘0.7’
 3. 控制标记风格：marker为散点的标记，标记风格有多种：

	```
	.  Point marker
	,  Pixel marker
	o  Circle marker
	v  Triangle down marker 
	^  Triangle up marker 
	<  Triangle left marker 
	>  Triangle right marker 
	1  Tripod down marker
	2  Tripod up marker
	3  Tripod left marker
	4  Tripod right marker
	s  Square marker
	p  Pentagon marker
	*  Star marker
	h  Hexagon marker
	H  Rotated hexagon D Diamond marker
	d  Thin diamond marker
	| Vertical line (vlinesymbol) marker
	_  Horizontal line (hline symbol) marker
	+  Plus marker
	x  Cross (x) marker
	```

<h4>B.函数图（折线图）</h4>

数据还是上面的。

```python
fig = plt.figure(figsize=(12, 6))
plt.subplot(121)
plt.plot(x, y, color='r', linestyle='-')
plt.subplot(122)
plt.plot(x, y, color='r', linestyle='--')
plt.show()
```

效果如下：
![plot](http://img.blog.csdn.net/20150928172212469)

这里有一个新的参数linestyle，控制的是线型的格式：符号和线型之间的对应关系

```
-      实线
--     短线
-.     短点相间线
：     虚点线
```

另外除了给出数据画图之外，我们也可以利用函数表达式进行画图，例如：`y=sin(x)`

```python
from math import *
from numpy import *
x = arange(-math.pi, math.pi, 0.01)
y = [sin(xx) for xx in x]
plt.figure()
plt.plot(x, y, color='r', linestyle='-.')
plt.show()
```

效果如下：

![sin(x)](http://img.blog.csdn.net/20150929093631843)


<h4>C.扇形图</h4>

示例：

```python
import matplotlib.pyplot as plt
y = [2.3, 3.4, 1.2, 6.6, 7.0]
plt.figure()
plt.pie(y)
plt.title('PIE')
plt.show()
```

效果如下：

![pie](http://img.blog.csdn.net/20150929093937867)

<h4>D.柱状图bar</h4>

示例：

```python
import matplotlib.pyplot as plt
x = [1, 2, 3, 4, 5]
y = [2.3, 3.4, 1.2, 6.6, 7.0]

plt.figure()
plt.bar(x, y)
plt.title("bar")
plt.show()
```

效果如下：

![bar](http://img.blog.csdn.net/20150929094224604)


<h4>E.二维图形（等高线，本地图片等）</h4>

```python
import matplotlib.pyplot as plt
import numpy as np
import matplotlib.image as mpimg
# 2D data

delta = 0.025
x = y = np.arange(-3.0, 3.0, delta)
X, Y = np.meshgrid(x, y)
Z = Y**2 + X**2
plt.figure(figsize=(12, 6))
plt.subplot(121)
plt.contour(X, Y, Z)
plt.colorbar()
plt.title("contour")

# read image

img=mpimg.imread('marvin.jpg')

plt.subplot(122)
plt.imshow(img)
plt.title("imshow")
plt.show()
#plt.savefig("matplot_sample.jpg")
```

效果图：

![2D](http://img.blog.csdn.net/20150929095204662)


<h4>F.对所画图进行补充</h4>

```python
__author__ = 'wenbaoli'


import matplotlib.pyplot as plt
from math import *
from numpy import *
x = arange(-math.pi, math.pi, 0.01)
y = [sin(xx) for xx in x]
plt.figure()
plt.plot(x, y, color='r', linestyle='-')
plt.xlabel(u'X')#fill the meaning of X axis
plt.ylabel(u'Sin(X)')#fill the meaning of Y axis
plt.title(u'sin(x)')#add the title of the figure

plt.show()
```

效果图：
![others](http://img.blog.csdn.net/20150929100519886)



<h2>三、结束语</h2>

尽管上述例子给出了基本的画图方法，但是其中的函数还有很多其他的用法（参数可能不只如此），因此本文只能算做一个基本入门。还需要参考API进行详尽的知识学习。


<h2>四、参考</h2>

上述内容部分引用自：

> http://www.cnblogs.com/vamei/archive/2013/01/30/2879700.html






