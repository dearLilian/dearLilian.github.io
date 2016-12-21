---
layout: post
title: java的文件操作
date: 2015-07-04
tag: 语言
---



## 目录

* TOC 
{:toc}


本文转自<a href="http://blog.csdn.net/lilianforever/article/details/46724827">我的CSDN博客</a>。

## 一、前言

学习java没多久，关键是没怎么系统学过。都是看别人的代码来学习的。今天就把一直以来让我头痛的java  IO 的一些基本操作来记录下来，加深记忆。

## 二、java导入文件到内存中

首先放一个完整的加载函数（这里我的返回值是定义的一个稀疏矩阵类）

```java
public SMatrix Load(String file, String delimeter){
		
		
	Map<ArrayList<Integer>,Integer> triples = new HashMap<ArrayList<Integer>,Integer>();
	
	try{
		File f = new File(file);
		FileReader fr = new FileReader(f);
		BufferedReader br = new BufferedReader(fr);
		
		String line;
		
		while((line = br.readLine()) != null){
			String[] str = line.trim().split(delimeter);
			
			ArrayList<Integer> s = new ArrayList<Integer>();
			for(int i = 0;i < str.length - 1; i++){
				s.add(Integer.parseInt(str[i]));
			}
			
			triples.put(s, Integer.parseInt(str[str.length - 1]));
			
		}
		
		
		br.close();
		fr.close();
		
	}catch(IOException e){
		e.printStackTrace();
	}
	SMatrix sm = new SMatrix(triples);
	return sm;
}
```

解析：所以基本的步骤是：

```java
try{
			
	File f = new File(file);//Step1:利用文件的路径file，创建文件类
	FileReader fr = new FileReader(f);//Step2:创建文件读入类
	BufferedReader br = new BufferedReader(fr);//Step3:创建读入的缓存类
	
	String line;
	
	while((line = br.readLine()) != null){//循环读入文件的每一行
		String[] str = line.trim().split(delimeter);//将每一行按字符串delimeter分割成一个字符串数组
		
		XXXXXXXXX;//TODO:接下来就将得到的字符串数组按照你构造的对象来赋值等等。这里面要注意字符串到整型或Double的转化等。
		
	}
	
	
	br.close();//关闭缓存读入
	fr.close();//关闭文件读入
	
}catch(IOException e){
	e.printStackTrace();
}
```


## 三、java将数据从内存输出到硬盘文件中

定义输出文件路径：例如，```String of = "D:/data/blablabal.txt";```

```java
String outFile = "data/eigenVector.txt";
try{
	File f = new File(outFile);//构造输出文件类
	FileOutputStream fout = new FileOutputStream(f);//构造一个输出文件流
	fout.write("@RELATION\teigenVector\n".getBytes());//主要函数就是  write(args)，里面的参数要求是byte[]型的
	for(int i = n-k;i<n;i++){
		fout.write(("@ATTRIBUTE\t"+i + "\tREAL\n").getBytes());
	}
	fout.write("@DATA\n".getBytes());
	if(k <= n){
		for(int i = 0;i < m;i++){
			for(int j = n-k;j<n;j++){
				Double temp = new Double(eigVector.getArray()[i][j]);
				String tem = temp.toString();
				fout.write((tem + "\t").getBytes());
				
			}
			fout.write(("\n").getBytes());
		}
	}
}
catch(IOException e){
	e.printStackTrace();
}
```

比如你想写一段文字：“I am a student,and I come from China”

```java
fout.write(("I am a student,and I come from China").getBytes());
```

相应的输出一个table键为：

```java
fout.write(("\t").getBytes());
```

输出换行：

```java
fout.write(("\n").getBytes());
```

等等。

