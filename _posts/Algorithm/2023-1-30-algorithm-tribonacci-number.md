---
title:  "[Easy] N-th Tribonacci Number"
date: 2023-1-30 5:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, recursion]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 5:00PM
---

# 'N-th Tribonacci Number (Easy)`

---

## 📌 Problem
https://leetcode.com/problems/n-th-tribonacci-number/>


## 📌 Answer

```java
class Solution {
    public int tribonacci(int n) {

        if (n == 0)
            return 0;
        if (n == 1 || n == 2)
            return 1;
        
        int[] Tribonacci = new int[n + 1];
        Tribonacci[0] = 0;
        Tribonacci[1] = 1;
        Tribonacci[2] = 1;
        
        for (int i = 3; i < n + 1; i++) {
            Tribonacci[i] = Tribonacci[i-1] + Tribonacci[i-2] + Tribonacci[i-3];
        }

        return Tribonacci[n];
    }
}
```