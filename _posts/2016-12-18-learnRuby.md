---
layout: post
title: ruby入门(未完待续)
date: 2016-12-18
tag: 语言
---


### ruby简介

ruby是一种纯粹的面向对象编程语言。它由日本的松本行弘（まつもとゆきひろ/Yukihiro Matsumoto）创建于1993年。
您可以在 www.ruby-lang.org 的 ruby 邮件列表上找到松本行弘（まつもとゆきひろ/Yukihiro Matsumoto）的名字。在 ruby 社区，松本也被称为马茨（Matz）。

以上摘自：<a href="http://www.runoob.com/ruby/ruby-intro.html">菜鸟教程</a>

看知乎上的解释：相比于JAVA这类语言，ruby的开发更高效，快捷，简洁。创业公司常用此语言，而相应的ruby程序员也比较稀缺。三年ruby开发经验就算是不错的了。

### ruby基本语法

每一个编程的语言的学习都是从一个```Hello, World!```开始的。例如：

```ruby
puts "Hello, World!"
```

就会输出

```
Hello, World!
```
下面我们来学习ruby的一些基本语法。

#### ruby打印到控制台：输出

```ruby
puts <your output>
```

或者

```ruby
print <your output>
```

puts输出会带回车换行符，而print则不带。


#### ruby中的Here Document

```ruby
#ruby中的Here Document
print <<EOF
	这是第一种方式创建here document。
	多行字符串
EOF

print <<"EOF";
	这是第二种方式创建here document。
	多行字符串。
EOF

print <<'EOC'
	echo hi there
	echo lo there
EOC

print <<"A", <<"B", <<"C"
	I said foo.
A
	I said bar.
B
	I said C.
C
```

输出：

```
	这是第一种方式创建here document。
	多行字符串
	这是第二种方式创建here document。
	多行字符串。
	echo hi there
	echo lo there
	I said foo.
	I said bar.
	I said C.
```

#### ruby BEGIN语句

BEGIN语句包含的code会在程序运行之前被调用。

例如：

```ruby
puts "Hello, World!"

BEGIN {
	puts "声明code会在程序运行之前被调用"
}
```

上述程序运行之后会输出

```
声明code会在程序运行之前被调用
Hello, World!
```

#### ruby END语句

END语句包含的code会在程序运行之后被调用。

例如：

```ruby
END {
	puts "声明code会在程序运行之后被调用"
}
puts "Hello, World!"
```

上述程序运行之后会输出

```
Hello, World!
声明code会在程序运行之后被调用
```

#### ruby注释

- 单行注释：使用```#```（与python一样的）

例如：

```ruby
#这是注释
```

- 多行注释（块注释）嵌入式文档注释

使用```=begin```与```=end```包围，例如：

```ruby
=begin
这是块注释
这是块注释
这还是块注释
=end
```

#### ruby数据类型

ruby支持的数据类型包括基本的
Number, String, Ranges, Symbols, 以及true, false和nil这几个特殊值
同时还有两种重要的数据结构——Array和Hash。ruby在使用变量的时候不需声明类型等。

- Number(数值型)又分为整型(Interger)与浮点型(Float)。
	- 而整型根据其范围又有Fixnum与Bignum之分。还有进制之分，八进制以0开头，十六进制以0x开头，二进制以0b开头。同时数字中可以用下划线来分位，程序会忽略数字中的下划线。
	- 浮点型也有很多种表示方法，如科学计数法(1.0e6)，指数表示(4E20, 4e+20)

具体例子如下：

```ruby
123 	# Fixnum 十进制
1_234	# Fixnum 带有下划线的十进制
-500	# 负的Fixnum
0377	# 八进制
0xff	# 十六进制 
0b1011	# 二进制
"a".ord	# "a"的字符编码
?\n 	# 换行符（0x0a）的编码
12345678901234567890	# 大数

a=0
b=1_000_000
c=0xa
puts a, b, c


#浮点数，带有小数的数字，是类Float的对象，且可以是下列中任意一个

fa=123.4
fb=1.0e4
fc=4e+20
fd=4E20

puts fa, fb, fc, fd
```

- 字符串类型String，可以用双引号或者单引号。在字符串中另外可以用#{expr}替换任何字符串表达式的值。例如：

```ruby
puts "计算表达式的值：#{24*3+2}"
```

输出：

```
计算表达式的值：74
```

#### 数组Array

ruby的数组中可以是任意类型的，每个元素的类型不一定是一样的。

- 数组通过[]索引访问
- 通过赋值操作插入，删除，替换元素
- 通过+,-号进行合并和删除元素，且集合作为新集合出现
- 通过<<号向原数据追加元素
- 通过*号重复数组元素
- 通过\|和&符号做并集和交集操作(注意顺序)

例如：

```ruby
#给出一个数组
ary = ["fred", 10, 3.14,"This is a sstring", "last element",]

#循环遍历数组中的元素，并输出
ary.each do |i|
	puts i
end

#取数组中的元素
puts ary[3]

#修改数组元素
ary[2] = 3.141592654 #修改原来的值
ary[5] = "new entry" #新增一个元素
ary<<true #追加新元素
new_ary = ary + [12,13,'Hello'] #并,加元素
new_ary2 = ary - ['new entry'] #减元素

#对数组的加倍操作
double = ary*2
puts double
```

#### 哈希类型Hash

在其他语言里也学习过很多次哈希表了，是一个键值对的集合。例如：

```ruby
hsh = colors = {"red" => 0xf00, "green" => 0x0f0, "blue" => 0x00f}
hsh.each do |key, value|
	print key, " is ", value, "\n"
end
```

输出为：

```
red is 3840
green is 240
blue is 15
```

#### 范围类型Range

用```s..e```来表示一个范围类型，其中```s```为起始值，```e```为结束值，得到的范围是包含```s```和```e```的。例如：

```ruby
range = 10..15
range.each do |i|
	print i,','
end
```

输出为：

```
10,11,12,13,14,15,
```

#### ruby类和对象

ruby是一种完美的面向对象编程语言。面向对象编程语言的特性包括：

- 数据封装
- 数据抽象
- 多态性
- 继承

这些ruby都具有。后面将会进行讨论。

下面来实际看下ruby的类怎么进行声明。

例子：比如我们先来创建一个顾客Customer类。一般构建类无非就是它的属性与方法。在ruby中类的属性（变量）有四种类型：

- 局部变量：只在方法中定义和使用的变量，以小写字母或下划线开始
- 实例变量：可以跨任何特定的实例或对象中的方法使用，以@开始的。
- 类变量：可以跨不同的对象使用。类变量属于类，且只是类的一个属性。以@@开始的。
- 全局变量：类变量不能跨类使用。而全局变量则可以。以$开始的。

创建类以如下方式：

```ruby
$全局变量
class 类名
	@@类变量
	@实例变量
	#类中的方法
	def 函数名
		函数体
		@实例变量
		局部变量

	end
end
```

例如Customer类：

```ruby
class Customer
	@@no_of_customer = 0

	#自定义方法来创建ruby对象（初始化方法）
	def initialize(id, name, addr)
		@cust_id = id
		@cust_name = name
		@cust_addr = addr
	end

	#定义其他成员函数:方法名总是以小写字母开头，以def开头，以end结束
	def sayHello
		puts "Hello, I\'m #@cust_name"
	end

	def display_details()
		puts "Customer id #@cust_id"
		puts "Customer name #@cust_name"
		puts "Customer addr #@cust_addr"
	end

	#使用类变量
	def total_no_of_customer
		@@no_of_customer += 1
	end
end

#使用new来创建类的对象
cust1 = Customer.new("1", "John", "USA")
cust2 = Customer.new("2", "Yukihiro", "Japan")

#调用成员函数
cust1.display_details
cust1.sayHello
cust1.total_no_of_customer
puts 67*"_"
cust2.display_details
cust2.sayHello
cust2.total_no_of_customer
```

#### ruby变量

变量是持有可被任何程序使用的任何数据的存储位置

ruby支持五中类型的变量：

- 一般小写字母、下划线开头：变量（Variable）
- $开头：全局变量（Global variable）
- @开头：实例变量（Instance variable）
- @@开头：类变量（Class variable）类变量被共享在整个继承链中
- 大写字母开头：常数（Constant）

在ruby中，通过在变量或常量前放置#字符(字符串中)，来访问任何变量或常亮的值

```ruby
name = "lilian"
puts name
```

实例变量可以参考上一小节中的customer类中的```@cust_id, @cust_name, @cust_addr```
类变量则参考```@@no_of_customer```

对于常量而言，以大写字母开头。定义在类或模块内的常量可以从类或模块的内部访问，定义在类或模块外的常量可以被全局访问。常量不能定义在方法内。引用一个未初始化的常量会产生错误。对已经初始化的常量赋值会产生警告。

```ruby
class Example
	VAR1 = 100
	VAR2 = 200
	def show
		puts "The first contant is #{VAR1}"
		puts "The second contant is #{VAR2}"
	end
end

object = Example.new()
object.show
```

注意：当函数无参时，调用时可以省略括号。

除了上述的一些变量与常量外，ruby中还有一些特殊的变量（伪变量）：它们是特殊的变量，有着局部变量的外观，但行为却像常量。您不能给这些变量赋任何值。

- ```self```:当前方法的接收器对象
- ```true```:代表true的值
- ```false```:代表false的值
- ```nil```:代表undefined的值，类似java中的null,python中的None
- ```__FILE__```:当前源文件的名称
- ```__LINE__```:当前行在源文件中的编号

#### ruby运算符

- 常规的算术运算符：```+,-,*,/,%,**(乘方)```
- 常规的比较运算符：```==, !=, >, <, >=, <=, <=>(联合比较运算符), ===, .eql?(内容相同), equal?```
- 赋值运算符：```=, +=, -=, *=, /=, %=, **=```,ruby支持并行赋值，如：

```ruby
a, b, c = 10, 20, 30
```

- 位运算符：```&(and), |(or), ^(异或), ~(非), <<, >>```
- 逻辑运算符：```and, or, &&, ||, !, not```
- 三元运算符：```?;```(类似其他语言中的)
- 范围运算符：```..```(创建一个从开始点到结束点的范围，包含结束点), ```...```(创建一个从开始点到结束点但不包含结束点的范围)
- defined?运算符： defined? 是一个特殊的运算符，以方法调用的形式来判断传递的表达式是否已定义。它返回表达式的描述字符串，如果表达式未定义则返回 nil。

用法如下：

```ruby
#用法1 :defined? variable # 如果 variable 已经初始化，则为 True
foo = 42
defined? foo    # => "local-variable"
defined? $_     # => "global-variable"
defined? bar    # => nil（未定义）

#用法2：defined? method_call # 如果方法已经定义，则为 True
defined? puts        # => "method"
defined? puts(bar)   # => nil（在这里 bar 未定义）
defined? unpack      # => nil（在这里未定义）

#用法3：# 如果存在可被 super 用户调用的方法，则为 True
#defined? super
defined? super     # => "super"（如果可被调用）
defined? super     # => nil（如果不可被调用）

#用法4：defined? yield   # 如果已传递代码块，则为 True
defined? yield    # => "yield"（如果已传递块）
defined? yield    # => nil（如果未传递块）
```

- 点运算符“.”和双冒号运算符“::”

您可以通过在方法名称前加上模块名称和一条下划线来调用模块方法。您可以使用模块名称和两个冒号来引用一个常量。
:: 是一元运算符，允许在类或模块内定义常量、实例方法和类方法，可以从类或模块外的任何地方进行访问。
请记住：在 ruby 中，类和方法也可以被当作常量。
您只需要在表达式的常量名前加上 :: 前缀，即可返回适当的类或模块对象。
如果未使用前缀表达式，则默认使用主 Object 类。


#### ruby判断

- ```if...else```语句

```ruby
if conditional [then]
	code...
[elsif conditional [then]
	code...]...
[else
	code...]
end
```

例如：判断一个数的正负：

```
a = 32

if a > 0
	puts "正数"
elsif a < 0
	puts "负数"
else
	puts "0"
end
```

以上输出：

```
正数
```

- if修饰符```code if condition```:表示当if右边的条件成立时才执行if左边的式子。例如：

```ruby
$debug = 1
print "debug\n" if $debug
```

- unless语句:语法如下

```ruby
unless condition [then]
	code
[else
	code]
end
```

与if相反，当condition为假时执行code。否则执行else的部分。

```ruby
#!/usr/bin/ruby
# -*- coding: UTF-8 -*-
 
x=1
unless x>2
   puts "x 小于 2"
 else
  puts "x 大于 2"
end
```

输出：

```
x 小于 2
```

- unless修饰符

同理。。。```code unless condition```

```ruby
$debug = false
print "Don\'t debug\n" unless $debug
```

输出：

```
Dont't debug
```
- case语句:语法如下

```ruby
case expression
[when expression [, expression ...] [then]
   code ]...
[else
   code ]
end
```

例如：

```ruby
day = 3
case day
when 1
	puts "Monday"
when 2
	puts "Tuesday"
when 3
	puts "Wednesday"
when 4
	puts "Thursday"
when 5
	puts "Friday"
when 6
	puts "Saturday"
else 7
	puts "Sunday"
end
```

输出：

```
Wednesday
```

当case的"表达式"部分被省略时，将计算第一个when条件部分为真的表达式。

```ruby
foo = false
bar = true
quu = false
 
case
when foo then puts 'foo is true'
when bar then puts 'bar is true'
when quu then puts 'quu is true'
end
# 显示 "bar is true"
```

#### ruby循环

- while语句

```ruby
while condition [do]
	code
end
```

或者

```ruby
while condition [:]
	code
end
```

do和:可以不写，但要是一行内的话必须写。

```ruby
i = 10
sum = 0
while i > 0
	sum += i
	i -= 1
end
puts "1 - 10的和为：#{sum}"
```

- while修饰符:```code while condition```

或者：

```ruby
begin
	code
end while condition
```
如果 while 修饰符跟在一个没有 rescue 或 ensure 子句的 begin 语句后面，code 会在 conditional 判断之前执行一次。相当于java的do...while语句。

- until语句

```ruby
until conditional [do]
	code
end
```

conditional为假时，执行code。

- until修饰符```code until conditional```或

```ruby
begin
	code
end until conditional
```

类似。

- for语句

```ruby
for variable [, variable ...] in expression [do]
	code
end
```

等价于：

```ruby
(expression).each do |variable..| code end
```

- break语句：终止最内部的循环。如果在块内调用，则终止相关块的方法（方法返回nil）。
- next语句：跳到循环的下一个迭代（类似java的continue）。如果在块内调用，则终止块的执行（yield表达式返回nil）。
- redo语句：重新开始最内部循环的该次迭代，不检查循环条件。
- retry语句：如果 retry 出现在 begin 表达式的 rescue 子句中，则从 begin 主体的开头重新开始。

```ruby
begin
   do_something   # 抛出的异常
rescue
   # 处理错误
   retry          # 重新从 begin 开始
end
```

#### ruby方法
