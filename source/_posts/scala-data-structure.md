---
title: Scala 中几种常用集合操作符
date: 2016-08-12 19:55:41
tags: [Scala]
---
### Scala 中的几种常用的集合操作符
* ::
* :+/+:
* ++
* :::

### 几种操作符的说明以及用法
一、::
两个冒号，表示往一个集合的头部添加元素，构造一个新的集合。x::list 表示往 list 队列的头部添加元素 x
```
//创建一个List
scala> val list = List(1,2)
list: List[Int] = List(1, 2)

//创建不变量x
scala> val x = 3
x: Int = 3

//将x插入到list头部
scala> x::list
res16: List[Int] = List(3, 1, 2)

// :: 的另一种使用形式
scala> list.::(x)
res17: List[Int] = List(3, 1, 2)
```

二、:+ 和 +:
冒号和加和组合的操作符，冒号在左边和冒号在右边的区别是分别是：1. list:+x 在集合尾部添加元素；2. x+:list在集合头部添加元素。
```
//将x插入到list尾部
scala> list:+x
res18: List[Int] = List(1, 2, 3)

//将x插入到list头部
scala> x+:list
res19: List[Int] = List(3, 1, 2)

//也可以这样使用
scala> list.+:(x)
res20: List[Int] = List(3, 1, 2)

scala> list.:+(x)
res21: List[Int] = List(1, 2, 3)

//创建一个 Seq 类型集合
scala> val seq = Seq(1, 2, 3)
seq: Seq[Int] = List(1, 2, 3)

//seq调用 :+
scala> seq.:+(5)
res29: Seq[Int] = List(1, 2, 3, 5)
```
其中 +: 和 :: 类似，但是 :: 可以用于 pattern match，而 +： 不支持。

三、++
两个加号，表示连接两个集合。例如，list++list1
```
scala> list1
res25: List[Int] = List(3, 4)

//list 加上 list1 中的元素
scala> list++list1
res26: List[Int] = List(1, 2, 3, 4)

//list1 加上 list 中的元素
scala> list1++list
res27: List[Int] = List(3, 4, 1, 2)
```

四、:::
三个冒号，表示连接两个 List 类型的集合。
```
//创建seq1
scala> val seq1 = Seq(4, 5)
seq1: Seq[Int] = List(4, 5)

//seq调用 ::: 去连接seq1，报错
scala> seq:::seq1
<console>:10: error: value ::: is not a member of Seq[Int]
              seq:::seq1
                 ^

//::: 只能用于连接两个 List 类型的集合
scala> list:::list1
res31: List[Int] = List(1, 2, 3, 4)
```
