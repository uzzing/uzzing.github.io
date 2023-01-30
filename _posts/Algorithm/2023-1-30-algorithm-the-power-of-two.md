---
title:  "[Easy] Power of Two"
date: 2023-1-30 3:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, recursion]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 3:00PM
---

# 'Power of Two (Easy)`

---

## 📌 Problem
<https://leetcode.com/problems/power-of-two/>


## 📌 Answer

```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if (n == 1) return true;
        if (n == 0) return false;
        if (n % 2 != 0) return false;
        return isPowerOfTwo(n / 2);
    }
}
```