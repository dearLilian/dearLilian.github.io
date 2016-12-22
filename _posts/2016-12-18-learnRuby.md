---
layout: post
title: ruby入门(未完待续)
date: 2016-12-18
tag: 语言
---

## 目录

* TOC 
{:toc}




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

### ruby打印到控制台：输出

```ruby
puts <your output>
```

或者

```ruby
print <your output>
```

puts输出会带回车换行符，而print则不带。


### ruby中的Here Document

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

### ruby BEGIN语句

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

### ruby END语句

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

### ruby注释

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

### ruby数据类型

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

### 数组Array

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

### 哈希类型Hash

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

### 范围类型Range

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

### ruby类和对象

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

### ruby变量

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

### ruby运算符

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


### ruby判断

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

### ruby循环

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

### ruby方法

ruby方法即函数。与python中的函数语法类似。

```ruby
def method_name [([arg[=default]]...[,*arg [, &expr]])]
	expr
end
```

首先是如何定义函数：def开头，end结尾。
其次是函数的参数：可以无参数（括号也可以省去）,也可以是多个参数，也可以是不定长参数。

例如：

```ruby
#无参函数
def sayHello
	puts "Hello."
end

#调用无参函数
sayHello

#有参函数
def sum (a, b)
	a + b  #函数的返回值是函数中最后一个表达式的值
end

#调用
c = sum 10, 20  #调用函数时，直接在函数名后面写参数

#不定长参数
def test (*args)
	puts "参数长度为：#{args.length}"
	args.each do |i|
		puts i
	end
end

#调用
test "a",3, true
```

函数的返回：

- 返回一个值：可以直接用最后一个表达式的值为函数的返回值
- 返回多个值：用return语句来返回（类似python中的return）。如果给出超过两个的表达式，包含这些值的数组将是返回值。如果未给出表达式，nil 将是返回值。


### 类方法

当方法定义在类的外部，方法默认标记为```private```,另一方面，如果方法定义在类中，则默认标记为```public```。

当想要访问类的方法时，首先需要实例化类。然后，使用对象，就可以访问类的任何成员。

另外一种（类似java中的静态方法），即不用实例化类即可访问方法的方式。在ruby中是这样声明的：

```ruby
class Account
	def reading_charge
		code 
	end

	def Account.return_date
		code 
	end
end
```
即在类名后跟一个点号，然后再加方法名来声明。这样我们可以直接用类名来访问类方法：

```ruby 
Account.return_date
```

### ruby <i>alias</i>语句

这个语句用于为方法或全局变量起别名。别名不能在方法主体内定义。即使方法被重写，方法的别名也保持方法的当前定义。

为编号的全局变量起别名是被禁止的。

```ruby
alias new_method_name original_method_name
alias new_global_variable original_global_variable
```

### ruby <i>undef</i>语句

这个语句用于取消方法定义。<i>undef</i>不能出现在方法主体内。

通过使用<i>undef</i>和<i>alias</i>，类的接口可以从父类独立修改。

```ruby
undef 方法名
```

### ruby块

类似与方法，ruby有一个块的概念。

- 块由大量的代码组成
- 您需要给块取个名称
- 块中的代码总是包含在大括号{}内
- 块总是从与其具有相同名称的函数调用。这意味着如果您的块名称为```test```,那么您要使用函数```test```来调用这个块。
- 您可以使用```yield```语句来调用块。

```ruby
block_name {
	statement1
	statement2
	..........
}
```

下面是相应的声明实例与调用

```ruby
#!/usr/bin/env ruby

def test
	puts "在 test 方法内"
	yield
	puts "你又回到了test方法内"
	yield
end

test {
	puts "你在test块内"
}
```

输出：

```ruby
在 test 方法内
你在test块内
你又回到了test方法内
你在test块内
```

```yield```还可以传递带有参数的语句。

```ruby
def test2
	yield 5
	puts "in the function test"
	yield 10
end

test2 {
	|i| puts "in the block #{i}"
}
```

输出：

```ruby
in the block 5
in the function test
in the block 10
```

当然也可以传递多个参数，例如：

```ruby
def test2
	yield 5, 25
	puts "in the function test"
	yield 10,100
end

test2 {
	|a, b| puts "in the block #{a+b}"
}
```

上述显然说明了方法与块之间的关系。

另外：如果方法最后一个参数前带有```&```，那么我们可以向该方法传递一个块，且这个块可被赋给最后一个参数。如果```*```和```&```同时出现在参数列表中，```&```应放在后面。

```ruby
def test(&block)
	block.call
end
test { puts "Hello, World!"}
```

最后就是我们之前介绍过的BEGIN和END块。一个程序中可以有多个BEGIN块以及END块。其中BEGIN块按照出现的顺序执行，END块按照他们出现的相反顺序执行。

### ruby模块(Module)

模块是一种把方法、类和常量组合在一起的方式。模块提供两大好处。

- 模块提供了一个命名空间和避免名字冲突
- 模块实现了mixin装置

模块类似于类，但有以下不同：

- 模块不能实例化
- 模块没有子类
- 模块只能被另一个模块定义

语法：

```ruby
module Identifier
	statement1
	statement2
	..........
end
```

使用模块名.方法名来调用模块方法，模块名::常量引用模块中的常量。

不同的模块中可以定义相同名称的函数（功能不同）


### ruby require语句

类似c与c++中的include语句以及java中的import语句。如果一个第三方的程序想要使用任何已定义的模块，则可以简单地使用require来加载模块文件：

```ruby
require filename
```

在文件开头使用```$LOAD_PATH << '.' ```让ruby知道必须在当前目录中搜索被引用的文件。


#### include语句

在类中嵌入模块时，需要在类中使用include语句

```ruby
include modulename
```

例如：

```ruby
#!/usr/bin/env ruby


module Week
	FIRST_DAY = "Sunday"
	def Week.weeks_in_month
		puts "You have four weeks in a month"
	end

	def Week.weeks_in_year
		puts "You have 52 weeks in a year"
	end
end
```

将该文件存储命名为support.rb。

然后在下面文件中引用。

```ruby
#!/usr/bin/env ruby
$LOAD_PATH << '.' 

require "support"

class Decade
include Week
	no_of_yrs = 10
	def no_of_months
		puts Week::FIRST_DAY
		number = 10*12
		puts number
	end
end

d1 = Decade.new
puts Week::FIRST_DAY
Week.weeks_in_month
Week.weeks_in_year
d1.no_of_months
```


### ruby中的Mixins

ruby不支持多重集成，但是ruby的模块有一个神奇的功能。它几乎消除了多重继承的需要，提供了一种名为Mixin的装置。

ruby的类通过include多个module可以间接的实现了多重继承，模块中的方法到可以被类调用。

实例：

```ruby
module A
   def a1
   end
   def a2
   end
end
module B
   def b1
   end
   def b2
   end
end
 
class Sample
include A
include B
   def s1
   end
end
 
samp=Sample.new
samp.a1
samp.a2
samp.b1
samp.b2
samp.s1
```

- 模块 A 由方法 a1 和 a2 组成。
- 模块 B 由方法 b1 和 b2 组成。
- 类 Sample 包含了模块 A 和 B。
- 类 Sample 可以访问所有四个方法，即 a1、a2、b1 和 b2。

因此，可以看到类 Sample 继承了两个模块，您可以说类 Sample 使用了多重继承或 mixin 。

### ruby字符串(String)

ruby字符串分为单引号字符串和双引号字符串，区别在于后者支持更多的转义字符。

关于字符串的一般内容如：转义字符，字符编码等类似于其他语言。

ruby的string特性有：在双引号字符串中可以使用#{表达式}来计算表达式的值。

除此之外就是String的内建方法。

- 实例化String对象：

```ruby
myStr = String.new("THIS IS TEST")
foo = myStr.downcase

puts "#{foo}"	#=>this is test
```
- str % arg
- str * integer:重复integer次，返回新字符串
- str + other_str:连接字符串
- str << obj:连接对象到字符串
- str <=>other_str:
- ...


### ruby数组(Array)

#### 初始化方式：

- ```Array.new(length)```
- ```Array.new(length, 初始值)```
- ```Array.[](...)```
- ```Array[...]```
- ```[...]```

#### 常用方法：

- & other_array
- * int
- * str:返回一个字符串
- + other_array
- [index]
- at(index)
- delete_at(index)
- insert(index, obj)
- length
- index(obj)
- size
- pop
- push(obj)
- reverse
- sort
- transpose (转置)数组的数组时使用
- ...

### ruby 哈希(Hash)

哈希的元素没有特定的顺序。

#### 创建哈希

- Hash.new
- Hash.new 默认值