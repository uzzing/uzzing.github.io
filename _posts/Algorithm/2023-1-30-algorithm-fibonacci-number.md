---
title:  "[Easy] Fibonacci Number"
date: 2023-1-30 2:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, recursion]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 2:00PM
---

# 'Fibonacci Number (Easy)`

---

## 📌 Problem
<https://leetcode.com/problems/fibonacci-number/>


## 📌 Answer

```java
class Solution {
    public int fib(int n) {
        if (n == 0) return 0;
        if (n == 1) return 1;
        return fib(n - 2) + fib(n - 1); 
    }
}
```