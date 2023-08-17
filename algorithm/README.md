# Learn_Algorithm

## 前言



&emsp;&emsp;讲述算法之前，首先需要计算机中有哪些数据结构，数据结构是算法的根基，算法是处理数据问题的解决方法。

## 数据结构
数据结构（Data structure）是计算机中存储、组织数据的方式。数据结构是一种具有一定逻辑关系，在计算机中应用某种存储结构，并且封装了相对应操作的数据元素集合，它包含三方面的内容，逻辑关系、存储关系及操作。

## 堆栈
堆栈是一种特殊的线性表，它只能在一个表的一个固定端进行数据节点的插入和删除操作

## 队列


## 数组

## 链表

## 树

## 图

## 堆积

## 散列表







## 一、十大经典排序算法
**排序算法是算法中最基本算法之一**

首先我们要知道几个相关的概念：

**1. 时间复杂度（平均时间复杂度、最好情况、最坏情况）**

**2. 空间复杂度**

**3. 排序方式**

**4. 稳定性**

时间复杂度： 执行算法需要的计算工作量

空间算法：执行算法所需的内存空间

排序方式：内部排序和外部排序

稳定性：排序后 2 个相等键值的顺序和排序之前它们的顺序相同
![image](https://raw.githubusercontent.com/FlameDream/Learn_Algorithm/main/resource/sort_img.png)

关于时间复杂度：
1.平方阶（O(n2)）：冒泡排序、选择排序和插入排序
2.线性对数阶（O(nlog2n)）: 归并排序、快速排序、堆排序和希尔排序
3.O（n+k）：计数排序、桶排序
4.O(nxK):基数排序

稳定性：

稳定的排序方法：冒泡排序、插入排序，归并排序和基数排序、计数排序、桶排序
不稳定的排序方法： 选择排序、快速排序、希尔排序、堆排序

<br>

**十大排序具体内容**

1. [冒泡排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/1.BubblingSort.md)
2. [选择排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/2.ChooceSort.md)
3. [插入排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/3.InsertSort.md)
4. [希尔排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/4.HillSort.md)
5. [归并排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/5.MergeSort.md)
6. [快速排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/6.FastSort.md)
7. [堆排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/7.HeapSort.md)
8. [桶排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/8.BucketSort.md)
9. [计数排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/9.CountSort.md)
10. [基数排序](https://github.com/FlameDream/Learn_Algorithm/blob/main/sort/10.BaseSort.md)




## 二、七大经典查找算法

查找算法：是在信息中找到特定的信息元素。

1. 查找算法分类：

+ 1) 静态查找 和 动态查找

&emsp;&emsp;**注：静态或动态是针对被查找表而言的，动态查找：被查找数组（表）中有删除和插入等操作**

+ 2) 无序查找 和 有序查找

&emsp;&emsp;**无序查找：被查找的数组（表）有序无序均可。**

&emsp;&emsp;**有序查找：被查找的数组（表）必须是有序**


2. 平均查找长度（Average Search Length ASL）:查找的值Value 和 比较的关键值的个数的期望值（简单说：查找成功次数的期望值）

查找成功的平均查找长度为：

**ASL = Pi*Ci;**

&emsp;&emsp;**Pi：查找表中第i个数据元素的概率。**

&emsp;&emsp;**Ci：找到第i个数据元素时已经比较过的次数。**


<br><br>
**七大查找具体内容**

1. [顺序查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
2. [二分查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
3. [插值查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
4. [斐波那契查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
5. [树表查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
6. [分块查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)
7. [哈希查找](https://github.com/FlameDream/Learn_Algorithm/blob/main/seek/seek.md)



**本仓库持续更新中……**

## Donate

如果本仓库对你有帮助，可以请作者喝杯速溶咖啡

![感谢🙏](https://raw.githubusercontent.com/FlameDream/Learn_Algorithm/main/resource/pay.jpg)

