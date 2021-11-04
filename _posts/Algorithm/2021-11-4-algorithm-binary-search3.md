---
title:  "[Binary Search] Search in Rotated Sorted Array"
date: 2021-11-4 1:08AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-4 1:08AM
---

# 'Search in Rotated Sorted Array' in LeetCode (Medium)

---

## 📌 Problem
<https://leetcode.com/problems/search-in-rotated-sorted-array/>

## 📌 Answer
### The point
- set **judgement** to check two points
    - whether which part is ordered
    - whether target is in that range
- and move
- there is an constraint <br> `You must write an algorithm with O(log n) runtime complexity.`

```java
class Solution {
    public int search(int[] nums, int target) {
        
        int start = 0;
        int end = nums.length - 1;
        int mid;
        
        while (start <= end){
            mid = (start + end) / 2;
            
            if (nums[mid] == target) return mid;
            
             // 1. check whether which part is ordered 
            if (nums[start] <= nums[mid]) {
                
                 // 2. check whether target is in that range
                 if (target < nums[mid] && target >= nums[start]) 
                    end = mid - 1;
                 else
                    start = mid + 1;
                
            }
            
            // 1. check whether which part is ordered
            if (nums[mid] <= nums[end]) {
                
                // 2. check whether target is in that range
                if (target > nums[mid] && target <= nums[end])
                    start = mid + 1;
                 else
                    end = mid - 1;
                
            }
        }
        return -1;
    }
}
```
The source : <https://leetcode.com/problems/search-in-rotated-sorted-array/discuss/14472/Java-AC-Solution-using-once-binary-search>