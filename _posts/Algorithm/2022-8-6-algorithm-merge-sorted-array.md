---
title:  "[Tail] Merge Sorted Array"
date: 2022-8-5 6:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-17 6:00PM
---

# ' Merge Sorted Array' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/merge-sorted-array/>

## 📌 Answer
### The point
- put data from the last index to first index (descending order)

```java
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        
        int tail1 = m - 1, tail2 = n - 1, finished = m + n -1;
        while (tail1 >= 0 && tail2 >= 0)
            nums1[finished--] = nums1[tail1] > nums2[tail2] ? nums1[tail1--] : nums2[tail2--];
        
        while (tail2 >= 0)
            nums1[finished--] = nums2[tail2--];
    }
}
```