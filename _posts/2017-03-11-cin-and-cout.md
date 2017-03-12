---
layout: post
title: C++ cin 与cout输入与输出浅析
date: 2017-03-11
tag: 语言
---

* TOC 
{:toc}


### cin

```cpp
int a;
cin >> a;
```

输入一个整数赋值给变量```a```，可以看到信息是从```cin```流向变量```a```，右移符号```>>```也表示了这种信息流的方向。

在iostream中cin是一个表示这种流的对象。

### cout

cout也是类似的。它是一个ostream类对象。


### 编译指令

```using namespace std;```

- 将它放在函数定义前，让所有的函数都能够访问它

- 将它放在特定的函数中，使得只有该函数能够访问它



