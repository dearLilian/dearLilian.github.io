---
layout: post
title: c++:A new beginning——Hello World
date: 2017-02-27
tag: 语言
---


* TOC 
{:toc}


### C++的Hello World

- 工作平台：Windows
- 编辑器：记事本或者sublime或其他编辑器。

新建一个文件，填入下列内容：

```cpp
#include<iostream>			//引入库：预处理命令
using namespace std;		//编译指令
int main()					//主函数入口：函数头，int表示返回类型
{							//函数体开始标志
	cout << "Hello world!";	//输出字符串
	return 0;				//结束函数main()
}							//函数体结束标志
```

将该文件保存到工作目录下，命名为HelloWorld.cpp。

打开命令提示符，输入下列命令：

```shell
g++ HelloWorld.cpp
```

这是一个编译过程，会产生HelloWorld.exe这样一个可执行程序。

然后可以双击执行该程序。或者直接在命令行提示符输入：

```
HelloWorld.exe
```
则会在命令行下输出
```
Hello world!
```

当然，对于一个程序，比较完成的流程是：编译->链接->执行。

C++程序中必须包含一个名为main()的函数。否则，程序将不完整。

#### 参考文献

[1] C++ Primer Plus(第6版) 中文版