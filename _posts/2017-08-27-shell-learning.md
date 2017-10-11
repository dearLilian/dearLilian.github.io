---
layout: post
title: shell学习笔记
date: 2017-08-27
tag: 语言
---

## 目录

* TOC
{:toc}


## shell

### 输出

```
echo "Hello, world"
```

### 变量

- 定义变量

```shell
a=10
b=20
```

> 注意：变量名和等号间不能有空格

- 使用变量

> 用美元符号前缀在变量名```$variable_name```或者```${variable_name}```，来访问变量。


如下所示：

```shell
echo $a
c=`expr $a + $b`
echo $c
echo "$a + $b = "${c}
```

- 重新定义变量

```shell
a=10
echo $a
a=20
echo $b
```

- 只读变量

```shell
a=10
readonly $a
a=20
```

这里，```a=20```会报错

- 删除变量

```shell
a=10
echo $a
unset $a
```

> 变量被删除后不能再使用，只读变量不能被删除

- 变量类型
    - 局部变量
    - 环境变量
    - shell变量

### 字符串变量

> 可以用单引号、双引号、或者不用引号来定义变量。


如下所示：

```shell
s='123'
ss="haha"
sss=liwenbao
```

- 拼接字符串

```shell
name='liwenbao'
greeting1="Hello, "$name" !"
greeting2="Hello, ${name} !"
```

- 字符串长度

使用“#”

```shell
name='Li wenbao'
echo ${#name}
```

- 提取子字符串

使用“:”

```shell
name='Li wenbao'
echo ${name:3:8}
```

### shell数组

> - 用括号表示，元素之间用空格分隔开。
> - 使用方括号访问数组元素，下标从0开始。
> - 使用*或@来访问数组所有元素。
> - 使用#来访问数组的长度。

```shell
array= (1 2 3 4 5 6 7 8 9 10)
echo "第一个元素为："${array[0]}

echo "数组的元素为："${array[*]}
echo "数组的元素为："${array[@]}

echo "数组的长度为："${#array[*]}
```


### 流程控制


#### if条件句

```shell
# simple if statement
if condition
then {
    statement
}
fi


# if else statement
if condition
then {
    statement1
}
else {
    statement2
}
fi


# if elif statement
if condition
then {
    statement1
}
elif condition2
then {
    statement2
}
else {
    statement3
}
fi

```


#### for 循环

```shell
array=(1 2 3 4 5 6 7)

for num in ${array[*]}
do {
    echo $num
}
done
```


#### while 循环

```shell
while condition
do 
    statement
done
```

while循环可用于读取键盘信息，例如：

```shell
echo -n '输入你的名字：'
while read NAME
do
    echo "你好，$NAME"
```


