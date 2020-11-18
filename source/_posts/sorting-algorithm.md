---
title: 常用的排序算法
date: 2020-06-10 11:51:46
tags: [算法&数据结构,Python]
---
最近在leetcode上刷题，想回顾一下计算机编程的基本功排序。常用的排序算法（内部排序），按大类分可分为以下几种：插入排序、交换排序、选择排序、归并排序和计数排序五大类。下面用python代码简单实现一下这几种排序算法。

## 插入排序
[插入排序](https://zh.wikipedia.org/wiki/插入排序)（Insertion Sort）比较简单直观，原理是将为排序数据，在已排序序列中从后往前扫描，找到相应位置插入。

### 直接插入排序（Straight Insertion Sort）
```python
def insertion_sort(nums):
    for i in range(1, len(nums)):
        j, key = i - 1, nums[i]
        while j >= 0 and key < nums[j]:
            nums[j+1] = nums[j]
            j = j - 1

        nums[j+1] = key
```

### 其他插入排序

## 交换排序
交换排序也是一种非常基础的算法，主要包含冒泡排序和快速排序。

### 冒泡排序（Bubble Sort）

```python
def bubble_sort(nums):
    for i in range(0, len(nums)-1):
        for j in range(0, len(nums)-1-i):
            if nums[j] > nums[j+1]:
                nums[j], nums[j+1] = nums[j+1], nums[j]
```

### 快速排序（Quick Sort）
快速排序，又称分区交换排序，简称快排，是对冒泡排序的一种改进。
```python
def quick_sort(nums, low, high):
    if low >= high: return

    pivot = nums[low]  # 选数列第一个元素作为"基准"
    i, j = low, high
    while i < j:
        while i < j and nums[j] >= pivot:
            j = j - 1
        nums[i] = nums[j]

        while i < j and nums[i] <= pivot:
            i = i + 1
        nums[j] = nums[i]
    nums[i] = pivot

    quick_sort(nums, low, i-1)
    quick_sort(nums, i+1, high)
```

## 选择排序
### 堆排序（Heap Sort）
```python
def heap_sort(nums):
    # 堆调整
    def max_heapify(nums, i, length):
        parent = i
        child = 2 * i + 1
        if child >= length:
            return
        if child + 1 < length and nums[child] < nums[child+1]:
            child += 1
        if nums[parent] < nums[child]:
            nums[parent], nums[child] = nums[child], nums[parent]
            max_heapify(nums, child, length)
    
    # 初始化，构造大顶堆
    for i in range(len(nums) // 2 - 1, -1, -1):
        max_heapify(nums, i, len(nums))

    # 堆排序
    for j in range(len(nums) - 1, 0, -1):
        nums[0], nums[j] = nums[j], nums[0]
        max_heapify(nums, 0, j)
```

## 归并排序（Merge Sort）
快速排序虽然排序效率高，但是不稳定，时间复杂度介于O(nlogn)跟O(n2)之间。
而归并排序可以稳定在O(nlogn)。
```python
def mergeSort(nums):
    if len(nums) == 1: 
        return nums

    mid = len(nums) // 2
    left = mergeSort(nums[:mid])
    right = mergeSort(nums[mid:])
    result = []
    while left and right:
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    if left:
        result += left
    if right:
        result += right
    return result
```

### 参考
1. 《数据结构（C语言版）》——严蔚敏、吴伟民
2. https://zh.wikipedia.org/wiki/快速排序
3. https://blog.csdn.net/wthfeng/article/details/78037228
