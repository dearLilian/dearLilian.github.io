---
layout: post
title: 数据结构之链表大解析(java)
date: 2016-08-09
tag: 数据结构
---


## 目录

* TOC 
{:toc}



本文内容主要总结链表的的相关知识与常见题目。转自<a href="http://blog.csdn.net/lilianforever/article/details/52163370">我的CSDN博客</a>。


## 一、链表的定义

链表是线性表的链式存储的实现（物理顺序可以是任意的，不一定要与逻辑顺序一致）。

线性表是指存储相同类型的一组数据，除了第一个和最后一个元素外，每一个元素都有它的一个直接前驱和直接后继，第一个元素有一个直接后继，最后一个元素有一个直接前驱。链表基本元素是结点，它里面包含数据域与指针域，结点之间用指针连接起来，形成一个简单的链。它有以下几种类型：

## 二、链表的分类

### 1.单链表

定义：单链表是指每一个结点只包含一个指针域的链表，这个指针指向当前节点的逻辑上的下一个节点，即该指针存储着下一个节点的地址。

```java
public class LNode {

	public int value;
	
	public LNode next;
}
```

### 2.循环单链表

循环单链表与单链表的区别就在于它的最后一个节点的指针项指向该链表的头结点。（而非循环的单链表则的最后一个节点指针为null）

### 3.双向链表

与单链表不同，双向链表是指在链表的节点中设置两个指针域，一个指向当前节点的直接前驱，另一个指向它的直接后继。

```java
public class DLNode {

	public int data;
	public DLNode prior;
	public DLNode next;
}
```

### 4.循环双链表

循环双链表也是一个环形的链表。将头结点的前驱设置为尾节点，而尾节点的后继设置为头结点。

## 三、链表的基本操作


### 1.链表的插入
#### (1)单链表

在节点p后面插入一个元素e

```java
//创建数据项为x的新结点
LNode q = new LNode();
q.value = x;
q.next = null;

//插入开始
q.next = p.next;//设置q的后继为p当前的后继
p.next = q;//更新p的后继为q
```

#### (2)双链表

在节点p后面插入一个元素x

```java
//创建数据项为x的新结点
LNode q = new LNode();
q.value = x;
q.prior = null;
q.next = null;

//插入开始
q.prior = p;//设置q的前驱为p
q.next = p.next;//设置q的后继为p当前的后继
p.next.prior = q;//更新p的后继节点的前驱为q（之前是p）
p.next = q;//更新p的后继为q
```

### 2.链表的删除

#### (1)单链表

删除节点p后面的节点

```java
int x = p.next.value;//保存要删除的节点内容
p.next = p.next.next;//直接更新p的后继为它当前后继的后继
```

#### (2)双链表

删除节点p后面的节点

```java
int x = p.next.value;//保存要删除的节点内容
p.next.next.prior = p;//更新要删除的节点的后继节点的前驱为p
p.next = p.next.next;//更新p的后继为要删除的节点的后继
```

## 四、单链表的常见操作（由基本操作衍生）

### 0. 打印链表

就是简单把链表的元素逐个打印到屏幕上（方便后面测试）

```java
public static void printLinkedList(LNode head){//头结点不存数据
		
		if(head == null){
			System.err.println("Wrong input;");
			return;
		}
		
		LNode p = head.next;
		System.out.print("[");
		while(p != null){
			if(p.next == null){
				System.out.println(p.value + "]");
				break;
			}else{
				System.out.print(p.value+",");
			}
			
			p = p.next;
		}
		
	}
```

### 1. 头插法建立链表

即每次都插入到头结点的后面

```java
public static LNode createLinkedListHead(){
		Scanner sc = new Scanner(System.in);
		
		LNode head = new LNode();
		LNode p = head;
		while(sc.hasNextInt()){
			int data = sc.nextInt();
			LNode q = new LNode();
			q.value = data;
			q.next = p.next;
			p.next = q;
		}
		
		return head;
	}
```

测试：

```
public static void main(String[] args){ 
		
		LNode l = createLinkedListHead();
		
		printLinkedList(l);
	}
```

运行，依次在控制台输入：

>1 2 3 4 5 6 ;

输出链表元素到屏幕：

>[6,5,4,3,2,1]


### 2. 尾插法建立链表

```java
public static LNode createLinkedListTail(){
		Scanner sc = new Scanner(System.in);
		
		LNode head = new LNode();
		LNode p = head;
		while(sc.hasNextInt()){
			int data = sc.nextInt();
			LNode q = new LNode();
			q.value = data;
			q.next = null;
			p.next = q;
			p = p.next;
		}
		
		return head;
	}
```

测试：

```java
public static void main(String[] args){ 
		
		LNode l = createLinkedListTail();
		
		printLinkedList(l);
	}
```

运行，依次在控制台输入：

>1 2 3 4 5 6 ;

输出链表元素到屏幕：

>[1,2,3,4,5,6]


### 3.  向链表某位置插入元素

在链表l的第index个位置插入元素x，即若插入成功，链表的第index位置就是元素x。

```java
	public static void insertElement(LNode head, int index, int data){
		if(head == null || index <= 0){
			System.err.println("Wrong input");
			return;
		}
		
		int pos = 0;
		
		LNode p = head;//p用来寻找要插入位置的前驱结点
		
		while(pos < index-1){
			p = p.next;
			pos++;
			
			if(p == null){
				System.err.println("Insertion failed, index is too large, it should be less than " + (pos+1));
				return;
				
			}
		}
		
		LNode q = new LNode();
		q.value = data;
		q.next = null;
		q.next = p.next;
		p.next = q;	
	}
```

测试：

```java
	public static void main(String[] args){ 
		
		LNode l = createLinkedListTail();
		
		System.out.print("插入前：");
		printLinkedList(l);
		
		insertElement(l, 3, 8);
		
		System.out.print("插入后：");
		printLinkedList(l);
	}
```

输入：(注意分号前面有空格)

>1 2 3 4 5 6 ;

输出：

> 插入前：[1,2,3,4,5,6]
插入后：[1,2,8,3,4,5,6]



### 4. 从链表某位置删除元素


```java
/**
	 * 删除链表head中的第index个节点
	 * @param head
	 * @param index
	 */
	public static void deleteElement(LNode head, int index){
		if(head == null || index <= 0){
			System.err.println("Wrong input.");
			return;
		}
		
		LNode p = head;//p用来寻找要删除节点的前驱
		int pos = 0;
		
		while(pos < index-1){
			System.out.println(pos);

			p = p.next;
			pos++;
			
			if(p.next == null){
				System.err.println("Deletion failed, index is too large, it should be less than " + (pos+1));
				return;
				
			}
			

		}
		
		
		int x = p.next.value;
		System.out.println("删除的节点的值为：" + x);
		p.next = p.next.next;
	}
```

测试：

```java
	public static void main(String[] args){ 
		
		LNode l = createLinkedListTail();
		
		System.out.print("删除前：");
		printLinkedList(l);
		
		deleteElement(l, 2);
		
		System.out.print("删除后：");
		printLinkedList(l);
	}
```

输入：

>1 2 3 4 5 6 ;

输出：

> 删除前：[1,2,3,4,5,6]
删除的节点的值为：2
删除后：[1,3,4,5,6]


### 5. 链表中按值查找元素

```java
/**
	 * 查找链表head中元素x第一次出现的位置，即第一个x是head的第几个元素
	 * @param head
	 * @param x
	 */
	public static void searchElement(LNode head, int x){
		if(head == null){
			System.err.println("Wrong input");
			return;
		}
		
		LNode p = head.next;
		int pos = 1;
		while(p != null){
			if(p.value == x){
				System.out.println("The first place which " + x + " shows in is " + pos);
				return;
			}else{
				p = p.next;
				pos++;
			}
		}
		
		if(p == null){
			System.out.println("There is no " + x + "in the list.");
		}
	}
```

测试：

```java
	public static void main(String[] args){ 
		
		LNode l = createLinkedListTail();
		
		System.out.print("操作前：");
		printLinkedList(l);
		
		searchElement(l, 5);
	}
```

输入：

>1 2 3 4 5 ;

输出：

>操作前：[1,2,3,4,5]
The first place which 5 shows in is 5


除此之外还有按位置查找，这个就相当于取元素，比较简单。（在删除操作里基本上已经实现过了）。

相应可以延伸到按值删除操作。先利用按值查找找到元素，再利用其前驱结点删除该元素即可。


### 6. 删除链表中所有值为key的节点

直接边扫描边删除即可。
时间复杂度： $O(n)$

### 7. 删除链表中有重复的元素，对于重复多次的元素，保留一次

思路：直接用后面的元素覆盖重复的元素。



### 8.删除链表中有重复的元素，不保留

即只留下那些出现一次的节点

1. 链表元素未排序时


- 最简单的思路：对于每一个结点p，遍历其后的节点，遇到与其值相同的统计并删除，若统计数大于0，则同时删除当前节点p。

时间复杂度： $O(n^2)$

```java
	/**
	 * 删除链表中重复的节点，不保留任何重复节点
	 * @param head
	 */
	public static void deleteRepeated2_1(LNode head){
		if(head == null){
			System.err.println("Wrong input.");
			return;
		}
		LNode prior = head;
		LNode p = head.next;
		
		
		while(p != null){
			
			int times = 0;
			LNode qprior = p;
			LNode q = p.next;
			
			
			//删除所有与p值相同的节点
			while(q != null){
				if(q.value == p.value){
					times++;
					qprior.next = q.next;
					
				}else{
					qprior = qprior.next;
				}
				
				q = q.next;
			}
			
			//若不存在与p值相同的节点
			if(times == 0){
				prior = prior.next;
			}else{
				prior.next = p.next;	
			}
			p = p.next;
		}
	}
```

测试：

```java
	public static void main(String[] args){ 
		
		LNode l = createLinkedListTail();
		
		System.out.print("操作前：");
		printLinkedList(l);
		
		deleteRepeated2_1(l);
		
		System.out.print("操作后：");
		printLinkedList(l);
		
	}
```

输入样例：

>2 1 2 3 1 4 5 2 3 6 ;

样例输出：

>操作前：[2,1,2,3,1,4,5,2,3,6]
操作后：[4,5,6]


-  先遍历一遍链表，利用哈希表统计每个元素出现的次数，然后再遍历一遍，删除那些出现次数超过1的节点。时间复杂度：$O(n)$ , 空间复杂度： $O(n)$

```java
	/**
	 * 删除链表中重复的节点，不保留任何重复节点
	 * 时间复杂度： O(n), 空间复杂度 ： O(n)
	 * @param head
	 */
	public static void deleteRepeated2_2(LNode head){
		if(head == null){
			System.err.println("Wrong input.");
			return;
		}
		
		LNode p = head.next;
		Map<Integer, Integer> ht = new HashMap<Integer, Integer>();
		while(p != null){
			int value = p.value;
			if(ht.containsKey(value)){
				ht.put(value, ht.get(value)+1);
			}else{
				ht.put(value, 1);
			}
			p = p.next;
		}	
		LNode prior = head;
		p = head.next;		
		while(p != null){
			if(ht.get(p.value) > 1){
				prior.next = p.next;
			}else{
				prior = prior.next;
			}
			
			p = p.next;
		}	
	}
```

测试与第一种类似。

2.链表元素已排序时

这个在本博客已经写过：[链表：删除链表中重复的结点（java实现）](http://blog.csdn.net/lilianforever/article/details/51837791%20%E5%88%A0%E9%99%A4%E6%9C%89%E5%BA%8F%E9%93%BE%E8%A1%A8%E4%B8%AD%E9%87%8D%E5%A4%8D%E7%9A%84%E8%8A%82%E7%82%B9)



## 五、链表常见显式面试题

### 1.从尾到头打印链表

方法一：遍历一遍，依次将节点值存入栈中，然后出栈，打印。时间复杂度：$O(n)$,空间复杂度：$O(n)$

方法二：想到利用栈，就可以利用递归（它的本质就是栈结构）。每次访问到一个节点时，先打印结点后面的的结点，再打印该结点自身，这样链表的打印结果就反过来了。但是如果链表本身很长的话，递归的层次会很深，可能会导致函数调用栈溢出。

故推荐使用第一种方法。

实现参考：[剑指Offer：面试题5——从尾到头打印链表（java实现）](http://blog.csdn.net/lilianforever/article/details/51830414)

### 2.链表反转

方法一：遍历一遍，依次将节点存入栈中，然后出栈，并建立指针连接。时间复杂度：$O(n)$,空间复杂度：$O(n)$。

方法二：依次遍历节点，并改变指针情况。每次扫描到一个节点时，先保存该结点的后继，然后重新设置该结点的后继为它的前驱结点。仅需要时间复杂度$O(n)$，空间复杂度则为$O(1)$.

实现参考：[剑指Offer:面试题16——反转链表(java实现)](http://blog.csdn.net/lilianforever/article/details/51839810)

### 3.链表倒数第K个

方法一：暴力法，直接先遍历一遍得到链表的长度L， 然后它的倒数第K个就是正数第L+1-K个。遍历即得。
这样要遍历两次链表。

方法二：（只需要遍历一次链表）用两个指针p1, p2,先让p1走K步，然后p1,p2同时每次走一步直到p1.next为空时，表明p1到达尾巴，此时p2即指向倒数第K个。

实现参考：[剑指Offer:面试题15——链表中倒数第k个结点(java实现)](http://blog.csdn.net/lilianforever/article/details/51839755)

### 4.链表是否有环以及环的入口节点


方法一：依次遍历结点，将它的next都存在一个哈希表中，每次检查next是否出现在哈希表中直到到达尾端，如果存在则说明有环。

方法二：设置两个指针p1, p2，p1每次走一步，p2每次走两步。如果到后面p2能追上p1(即p2 == p1)，则说明有环。否则没有。如果有环的话，那么当前p1和p2相遇的节点一定是在环中，故我们随便选一个指针p1（p1或者p2）继续往下走直到再次遇到p2，那么就算出了环的长度N。然后 p1, p2重新指向头结点 ，p1先走N步，然后两个指针同步向前，直到两个相遇，此时的节点就是换的入口。

### 5.在$O(1)$时间内删除链表结点

方法：假如要删除的节点是p，它的后继是q，那么我们直接用q的数据域覆盖p的数据域，然后删除q。

实现参考：[剑指Offer:面试题13——在O(1)时间删除链表结点](http://blog.csdn.net/lilianforever/article/details/51837463)

### 6.合并两个排序的链表

方法：两个指针p1指向链表1，p2指向链表2，p3指向新链表的尾节点，每次比较p1与p2节点的值，小的则用p2指向它，然后对应p向后移动一位。知道p1或p2为空。

实现参考：[剑指Offer:面试题17——合并两个排序的链表](http://blog.csdn.net/lilianforever/article/details/51840497)

### 7.复杂链表的复制

具体问题及解法参见：[剑指Offer:面试题26——复制复杂的链表(java实现)](http://blog.csdn.net/lilianforever/article/details/51853155)

### 8.从无头单链表中删除节点

参见：

### 9.两个链表是否有公共节点以及第一个公共节点



## 六、 链表常见隐式面试题（即运用链表解决的题型）


### 1.约瑟夫环问题

### 2.多项式运算问题

### 3.操作系统原理中的内存管理器实现

明天继续写。。。今天写不动了。。。