---
title: 记录一次练习当中遇到的HashSet的相关问题
date: 2020-12-15 13:15:08
categories: 随记分享
tags:
	- java
	- HashSet
description: HashSet的顺序问题
cover: https://upyun-cdn.mistill.com/img/post_cover/post_cover_031.webp
abbrlink: record-201215
---



# 背景

在练习`java` `Set`时，遇到了很奇怪的问题。我们都知道，`Set`是无序的并且不能有重复元素的，利用随机数随机存入多个`Integer`类型的数据，却发生了有序的情况。

```java
// 使用一个set集合，存储0-16的数字
Set<Integer> set = new HashSet<>();
while (set.size() < 16) {
    int num = (int) (Math.random() * 16);
    if (!set.contains(num)) {
        set.add(num);
    }
}
System.out.println(set);
```

运行结果：

```java
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15]
```

明明`Set`是无序的，怎么存进去就自动进行了排序？



# 解决

依旧是万能的百度。

从https://bbs.csdn.net/topics/393667463获取到了想要的答案。

总结一句话：`HashSet`的是计算对象的`hash`值，并映射到数组的下标。

一般来说的`Set`**无序是指不按照我们存入的顺序**。

接下来引用大佬的解答。



---



 `HashSet`的原理是：计算对象的`hash`值，并映射到数组的下标。

再看一下`String`的`hashCode()`方法的源码

![img](https://upyun-cdn.mistill.com/img/post_img/aHR0cHM6Ly9vc2NpbWcub3NjaGluYS5uZXQvb3NjbmV0LzBjMTIyMTM3MjlhNWUwOGNkMTQ1M2MxZTMzYTVjOGRjYjI4LmpwZw)


哈希值是通过`char`对应的`int`值计算出来的，即：`char`对应的`int`值越大，`hash`值就越大。 

而在拉丁字母A、B、C、D的`char`字符对应的`int`值**恰巧是递增的**，所以他们的`hash`值也恰巧是递增的，所以最终映射到`HashSet`内的数组的位置也是顺序的。 

![img](https://upyun-cdn.mistill.com/img/post_img/295f40b351e1b93abff04f192a9bf7fb03f.jpg)

![img](https://upyun-cdn.mistill.com/img/post_img/cc4e0c7bdfb468c038e5b3000c9477bc645.jpg)



---



`HashSet` 元素的存储(地址)是无序的。一般来讲，通过进行迭代的迭代器也是依次将各个元素(字符串)，无序地输出。 

  楼主所示的"有序结果"，其实是一种**极其特殊案例**：**每个元素都仅是一(单)个字符，或都是数字字符，或都是小写英文字符，或都是大写英文字符。** 

  **元素的存储地址，视这个元素的哈希值而定。**由于元素仅有一个字符，其哈希值的计算结果，就会是这个给定字符的 ascii 码(参见: 哈希算法)的值。结果， 打印出的 `HashSet` 列表，就会是貌似经过排序后的结果。但要注意构成这种案例的条件：元素必须 都是单个数字字符、或都是单个英文小写字符、或都是单个英文大写字符。


  下列代码显示每个元素的哈希值，以及最终调用` toString()` 输出 `HashSet hs` 的结果。输出结果显示，单个字符元素的哈希值，就是它的 ASCII值。 

```java
import java.util.HashSet;

public class HashSetDemo {
	static void showHashSet(String[] s) {
		HashSet<String> hs = new HashSet<String>();
		for (int i = 0; i < s.length; i++) {
			hs.add(s[i]);
			System.out.println(s[i] + "的哈希值：" + s[i].hashCode() + " ");
		}
		System.out.println("toString的结果：" + hs);
	}

	public static void main(String args[]) {
		String data[][] = new String[5][6];
		String dat[] = { "B", "A", "D", "E", "C", "F", // 可以打印出貌似排序的结果
				"6", "4", "3", "1", "2", "5", // 可以打印出貌似排序的结果
				"BB", "AA", "DD", "EE", "CC", "FF", "42", "41", "45", "46", "44", "43", "Base", "Alberta", "Done",
				"End", "Coding", "Factory" };
		for (int i = 0; i < dat.length; i++)
			data[i / 6][i % 6] = dat[i];
		for (int i = 0; i < data.length; i++)
			showHashSet(data[i]);
	}
}
```

输出结果：

```java
B的哈希值：66 
A的哈希值：65 
D的哈希值：68 
E的哈希值：69 
C的哈希值：67 
F的哈希值：70 
toString的结果：[A, B, C, D, E, F]
6的哈希值：54 
4的哈希值：52 
3的哈希值：51 
1的哈希值：49 
2的哈希值：50 
5的哈希值：53 
toString的结果：[1, 2, 3, 4, 5, 6]
BB的哈希值：2112 
AA的哈希值：2080 
DD的哈希值：2176 
EE的哈希值：2208 
CC的哈希值：2144 
FF的哈希值：2240 
toString的结果：[BB, AA, DD, EE, CC, FF]
42的哈希值：1662 
41的哈希值：1661 
45的哈希值：1665 
46的哈希值：1666 
44的哈希值：1664 
43的哈希值：1663 
toString的结果：[44, 45, 46, 41, 42, 43]
Base的哈希值：2063089 
Alberta的哈希值：743772625 
Done的哈希值：2135970 
End的哈希值：69819 
Coding的哈希值：2023747466 
Factory的哈希值：572770538 
toString的结果：[Done, Alberta, Coding, Factory, End, Base]

```

