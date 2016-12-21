---
layout: post
title: java的jdbc连接与sql操作
date: 2015-07-03
tag: 语言
---


## 目录

* TOC 
{:toc}



转自<a href="http://blog.csdn.net/lilianforever/article/details/46740225">我的CSDN博客</a>。

## 一、前言

本文主要介绍怎样连接数据库。即```JDBC```的操作。以```MySQL```为例子。
前提是首先要将驱动jar包放入对应路径中。

## 二、过程说明


### 1.加载jdbc驱动程序

```java
Class.forName("com.mysql.jdbc.Driver");
```

这里的驱动根据不同类型的数据库来改变。
比如```mysql```数据库，就是```com.mysql.jdbc.Driver```,
```Oracle```数据库，```oracle.jdbc.driver.OracleDriver```,
```ms_sql server```数据库，```com.microsoft.jdbc.sqlserver.SQLServerDriver```
等等。

### 2.建立连接

```java
Connection connect = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test","root","123456");
```

其中三个参数分别是：加载数据库的地址```url```，加载数据库的用户名```user```,加载数据库的用户相应的登陆密码```password```;

### 3.创建Statement对象

```java
Statement stmt = connect.createStatement();
```

大部分数据库驱动程序允许在同一个连接中打开多个并行的```Statement```对象，创建好```Statement```对象之后，就可以使用它来进行数据库的操作了。```Statement```类中的常用方法，可以去帮助文档中查找。


### 4.执行sql语句及结果集的处理


```java
ResultSet rs = stmt.executeQuery("select * from stu_table");
			
while(rs.next()){
	System.out.println(rs.getString("name"));
}
```

### 5.一些其他如```insert```插入操作

```java
int num = 100;
PreparedStatement pst = connect.prepareStatement("insert into stu_table values(?,?,?,?)");
int i;
for( i = 0; i < num ; i++){
	pst.setString(1,i+"3");
	
	pst.setString(2,"Lilly" + (i+1));
	pst.setString(3, "female");
	pst.setString(4, "001");
	pst.execute();
}
System.out.println("success inserting notes!");
```



### 6.关闭连接

```java
rs.close();
stmt.close();
connect.close();
```

在关闭连接前先将相应的```ResultSet```对象及```statement```对象也关闭。

## 三、程序完整实现


```java
package test;

import java.sql.*;

public class testJDBC {

	public static void main(String[] args) {
		try{
			//first:load jdbc driver
			Class.forName("com.mysql.jdbc.Driver");
			
			System.out.println("Success loading Mysql Driver!");
		}
		catch(Exception e){
			System.out.println("Error loading mysql driver!");
			e.printStackTrace();
		}
		try{
			//second:connect sql server
			Connection connect = DriverManager.getConnection("jdbc:mysql://127.0.0.1:3306/test","root","123456");
			System.out.println("success connecting mysql server!");
			

			//third:selct from the table of database using a sql query
			Statement stmt = connect.createStatement();
			ResultSet rs = stmt.executeQuery("select * from stu_table");
			
			while(rs.next()){
				System.out.println(rs.getString("name"));
			}
			
			//four:do some other operation such as insert notes
			int num = 100;
			PreparedStatement pst = connect.prepareStatement("insert into stu_table values(?,?,?,?)");
			int i;
//			for( i = 0; i < num ; i++){
//				pst.setString(1,i+"3");
//				
//				pst.setString(2,"Lilly" + (i+1));
//				pst.setString(3, "female");
//				pst.setString(4, "001");
//				pst.execute();
//			}
			System.out.println("success inserting notes!");
			rs.close();
			stmt.close();
			connect.close();
		}
		catch(SQLException e){
			System.out.println("Error connecting mysql server!");
			e.printStackTrace();
		}

	}

}

```