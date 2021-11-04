---
title:  "[Data Structure] HashSet vs TreeSet"
date: 2021-11-3 1:58PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-4 2:41PM
---

## 📌 Common feature
- No duplicate elements
- Only one null element

## 📌 Comparison
- Most important difference between HashSet and TreeSet is **ordering.**

|HashSet|TreeSet|
|:---:|:---:|
| HashSet **doesn't guaranteed any order**| TreeSet **maintains objects in Sorted order** defined by either Comparable or Comparator method in Java.|
|HashSet is **faster** than a TreeSet. ||

## 📌 Time complexity
||HashSet|TreeSet|
|:---:|:---:|:---:|
|**Add**|O(1)|O(log n)|
|**Contains**|O(1)|O(log n)|
|**Next**|O(h/n)|O(log n)|

`Tips`
**O(1) < O(log n) < O(n) < O(n * log n) < O(n²) < O(n³) < O(2^n) < O(n!)**

---
The source :
<https://soft.plusblog.co.kr/74>