---
layout: post
title: 数据结构之排序算法(java)
date: 2016-07-15 
tag: 数据结构
---



* TOC 
{:toc}



# 一、排序算法

## 1. 插入排序

### 1.1 ＊直接插入排序＊

#### 1.1.1 思想

- 每次取剩下的一个元素插入到已经有序的序列中．

#### 1.1.2 代码


{% highlight java %}
public static void InsertSort(int[] arr){
	if(arr == null || arr.length == 0){
		System.err.println("ERROR INPUT");
		return;
	}
	
	int n = arr.length;
	
	for(int i = 1; i < n; i++){
		
		int temp = arr[i];
		int j = i - 1;
		while(j >= 0 && temp < arr[j]){
			arr[j+1] = arr[j];
			j--;
		}
		
		arr[j+1] = temp;
	}
}
{% endhighlight %}


#### 1.1.3 算法分析
- 最好情况下：每次循环，内层都不需要比较，只有外层循环的常量级操作，时间复杂度为$O(n)$
- 最坏情况下：内层循环每次都要比较i次，故总的执行次数是：1+2+3+...+n=n*(n-1)/2，故时间复杂度为$O(n^2)$
- 最后平均时间复杂度为：$O(n^2)$
- 空间复杂度：$O(1)$


### 1.2 ＊折半插入排序＊

#### 1.2.1 思想

- 基本思想与直接插入是一样的，区别在于寻找插入位置的方法不同，折半插入排序是采用折半查找来寻找插入位置的．

#### 1.2.2 代码

```java
public static void halfInsertSort(int[] arr){
	if(arr == null || arr.length == 0){
		System.err.println("ERROR INPUT");
		return;
	}
	
	for(int i = 1; i < arr.length; i++){
		
		int temp = arr[i];
		
		int low = 0;
		int high = i - 1;
		int idx = -1;
		while(low <= high){
			int m = (low+high)/2;
			
			if(arr[m] < temp){
				low = m+1;
			}else if(arr[m] > temp){
				high = m-1;
			}else{
				idx = m+1;
				break;
			}
		}
		if(low > high){
			idx = high + 1;
		}
		
		for(int j = i-1; j >= idx; j--){
			arr[j+1] = arr[j];
		}
		
		arr[idx] = temp;
	}
	
}
```

#### 1.2.3 算法分析

- 外层循环为n－１次，内层循环是折半查找，
- 最好情况是：复杂度为$O(\log n)$.故总的时间复杂度为$O(n\log n)$；最坏情况是$O(n^2)$;平均情况为$O(n^2)$．
- 空间复杂度为：$O(1)$


### 1.3 希尔排序（shellsort)

希尔排序，又称缩小增量排序，其本质还是插入排序，只不过将待排序的序列按某种规则分为几个子序列，分别对这几个子序列进行直接插入排序．这个规则就是增量

#### 1.3.1 思想

- 比如对序列：49, 38, 65, 97, 76, 13, 27, 49
- 先选择３为增量，则得到序列１：49, 97, 27;序列２：38,76, 49;序列３：65, 13
- 分别对这三个使用直接插入排序，序列１：27,49,97;序列２：38,49,76;序列３：13,65
- 将三个序列合并起来：27,38,13,49,49,65,97,76
- 这就是一趟希尔排序了．接下来，再也２（或１）为增量进行一趟希而排序

#### 1.3.2 代码


#### 1.3.3 算法分析

- 平均时间复杂度：$O(n\log n)$
- 空间复杂度：$O(1)$


## 2. 交换排序

### 2.1 冒泡排序

#### 2.1.1 思想

- 每次通过一系列的交换动作，将最大（或最小)的数字冒出来.终止条件是一趟排序过程中没有发生元素交换


#### 2.1.2 代码

```java
public static void BubbleSort(int[] arr){
	if(arr == null || arr.length == 0){
		System.err.println("Error input");
		return;
	}
	
	for(int i = arr.length-1; i >= 1; i--){
		
		boolean flag = false;
		for(int j = 0; j < i; j++){
			if(arr[j] > arr[j+1]){
				int temp = arr[j];
				arr[j] = arr[j+1];
				arr[j+1] = temp;
				
				flag = true;
			}
		}
		
		if(flag == false){
			return;
		}
	}
}
```

#### 2.1.3 算法分析

- 时间复杂度：最好$O(n)$最坏$O(n^2)$平均$O(n^2)$
- 空间复杂度：$O(1)$

### 2.2 快速排序

#### 2.2.1 思想

- 快速排序也是＂交换＂类的排序，它的基本思想是找出一个枢纽，使得在它左边的比它小，右边的比它大．

#### 2.2.2 代码

```java
public static void QuickSort(int[] arr, int l, int r){
	if(arr == null || arr.length == 0 || l < 0 || r >= arr.length){
		System.err.println("ERROR INPUT");
		return;
	}
	
	int i = l;
	int j = r;
	if(l < r){
		int temp = arr[l];
		while(i != j){
			while(j > i && arr[j] > arr[i]){
				j--;
			}
			
			if(i < j){
				arr[i] = arr[j];
				i++;
			}
			
			
			while(j > i && arr[i] < arr[j]){
				i++;
			}
			if(i < j){
				
				arr[j] = arr[i];
				j--;
			}
			
		}
		
		arr[i] = temp;
		QuickSort(arr, l, i-1);
		QuickSort(arr, i+1, r);
	}
}
```


另外一个写法：

```java
public int Partition(char[] arr, int start, int end){
    if(arr == null || arr.length == 0 || start < 0 || end < 0){
        return -1;
    }

    int index = start + (int)(Math.random() * ((end - start) + 1));//随机选择一个作为标杆的数字


    //将标杆放在数组最后一位
//        System.out.println(arr.toString());
//        System.out.println(arr[index]);
//        System.out.println(arr[end]);
    char tmp = arr[index]; arr[index] = arr[end]; arr[end] = tmp;

    int small = start - 1;//small用来存储从右到左第一个小于标杆的数字的下标
    for(index = start; index < end; index++){
        if(arr[index] < arr[end]){//如果小于标杆
            small++;//更新第一个小的
            if(small != index){//如果当前遍历的不是第一个小的
                tmp = arr[index];arr[index] = arr[small];arr[small] = tmp;//将当前遍历的数字放在第一个小的位置上

            }
        }
    }

    //由于small指示的是从右到左第一个小于标杆的，而此时标杆还放在数组最后，因此，应该将标杆放在small后面一位。
    small++;
    tmp = arr[small];arr[small] = arr[end]; arr[end] = tmp;

    return small;//返回位置为所选择的标杆最后的位置


}

public void QuickSort(char[] arr, int start, int end){

    if(start == end){
        return;
    }
    int index = Partition(arr, start, end);

    if(index > start){
        QuickSort(arr, start, index - 1);
    }
    if(index < end){
        QuickSort(arr, index + 1, end);
    }
}
```

#### 2.2.3 算法分析

- 时间复杂度：最好$O(n\log_2 n)$，平均$O(n\log_2 n)$，最坏：$O(n^2)$
- 空间复杂度$O(\log_2 n)$
- 快速排序是所有排序算法中最好的．


## 3. 选择排序

### 3.1 简单选择排序

#### 3.1.1 思路：

- 简单选择排序采用最简单的选择方式，从头至尾顺序扫描序列，找出最小的一个记录，和第一个记录交换，接着从剩下的记录中继续这种选择和交换，最终使序列有序．

#### 3.1.2 代码：

```java
public static void SimpleSelectSort(int[] arr){
	
	if(arr == null || arr.length == 0){
		System.err.println("ERROR INPUT");
		return;
	}
	
	
	for(int i = 0; i < arr.length; i++){
		int temp = arr[i];
		
		int min = arr[i];
		int idx = i;
		for(int j = i; j < arr.length; j++){
			if(arr[j] < min){
				min = arr[j];
				idx = j;
			}
		}
		
		arr[idx] = temp;
		arr[i] = min;
		
	}
}
```

#### 3.1.3 算法分析：

- 时间复杂度：$O(n^2)$
- 空间复杂度：$O(1)$

### 3.2 堆排序


#### 3.2.1 思路

将序列调整成一个堆．

#### 3.2.2 代码

```java
/**
* 本函数完成对在数组Ｒ[low]到Ｒ[high]范围内对在位置low上的结点进行调整
* @param arr
* @param low
* @param high
*/
public static void shift(int[] arr, int low, int high){
	if(arr == null || arr.length == 0){
		return;
		
	}
	
	int i = low;
	int j = 2 * i;//arr[j]是arr[i]的左孩子结点
	int temp = arr[i];
	while(j <= high){
		if(j < high && arr[j] < arr[j+1]){//若右孩子较大，则把j指向右孩子
			j++;						//j变为2*i+1
		}
		
		if(temp < arr[j]){//将Ｒ[j]调整到双亲位置上
			arr[i] = arr[j];
			i = j;
			j = 2 * i;
		}else{
			break;//调整结束
		}
	}
	
	arr[i] = temp;//被调整结点的值放入最终位置
}

/**
 * 堆排序函数
 * @param arr
 */

public static void heapSort(int[] arr){
	if(arr == null || arr.length == 0){//输入参数的非法性检查
		System.err.println("ERROR INPUT");
		return;
	}
	
	int i;
	int temp;
	int n = arr.length;
	
	for(i = n / 2; i >= 0; i--){//建立初始堆
		shift(arr, i, n-1);
	}
	
	for(i = n-1; i >= 1; i--){//进行n-1次循环完成堆排序
		temp = arr[0];
		arr[0] = arr[i];
		arr[i] = temp;
		shift(arr, 0, i-1);//在减少了１个元素的无序序列中进行调整
	}
}
```

#### 3.2.3 算法分析：

- 时间复杂度：$O(n\log _2 n)$
- 空间复杂度：$O(1)$


## 4. 归并排序

### 4.1 二路归并排序

#### 4.1.1 思路

- 初始状态是每个元素是一个子序列，然后两两合并，形成了几个两个元素的子序列，．．．．，依次合并下去，直到合并为一个有序序列．

#### 4.1.2 代码


#### 4.1.3 算法分析

- 时间复杂度：$O(n\log _2 n)$
- 空间复杂度：$O(n)$

## 5. 基数排序

#### 5.1.1 算法分析

- 时间复杂度：$O(d(n+r_d))$
- 空间复杂度：$O(r_d)$


# 二、排序算法的对比

## 1. 时间复杂度

- ＂快些以$O(n\log _2 n)$的速度归队＂
- 即快，希，归，堆都是$O(n\log _2 n)$，其他都是$O(n^2)$，基数排序例外，是$O(d(n+r_d))$

## 2. 空间复杂度：

- 快排$O(\log _2n)$
- 归并$O(n)$
- 基数$O(r_d)$
- 其他$O(1)$

## 3. 稳定性

- ＂心情不稳定，快些找一堆朋友聊天吧＂
- 即不稳定的有：快，希，堆


## 4. 其他性质

 1. 直接插入排序，初始基本有序情况下，是$O(n)$
 2. 冒泡排序，初始基本有序情况下，是$O(n)$
 3. 快排在初始状态越差的情况下算法效果越好．
 4. 堆排序适合记录数量比较大的时候，从n个记录中选择k个记录．
 5. 经过一趟排序，元素可以在它最终的位置的有：交换类的（冒泡，快排），选择类的（简单选择，堆）
 6. 比较次数与初始序列无关的是：简单选择与折半插入
 7. 排序趟数与原始序列有关的是：交换类的（冒泡和快排）