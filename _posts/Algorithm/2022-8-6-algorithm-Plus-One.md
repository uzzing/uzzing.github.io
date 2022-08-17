---
title:  "[Easy] Plus One"
date: 2022-8-5 2:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-17 6:00PM
---

# 'Plus One' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/plus-one/>

## 📌 Answer
```java
class Solution {
    public int[] plusOne(int[] digits) {
        
        for (int i = digits.length - 1; i >= 0; i--) {
            if (digits[i] != 9) {
                digits[i]++;
                break;
            } else {
                digits[i] = 0;
            }
        }
        
        if (digits[0] == 0) {
            int[] res = new int[digits.length + 1];
            res[0] = 1;
            return res;
        }
        
        return digits;
    }
}
```