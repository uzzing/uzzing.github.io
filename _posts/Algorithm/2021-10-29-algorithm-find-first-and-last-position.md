---
title:  "[Binary Search] Find First and Last Position of Element in Sorted Array"
date: 2021-10-29 3:22PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, binary search]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-4 2:40PM
---
# 'Find First and Last Position of Element in Sorted Array' in LeetCode (Medium)

---

## 📌 Problem
<https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/>

## 📌 Answer
### The point
- binary search : time complextiy is O(logN)

[Result](https://leetcode.com/submissions/detail/578910776/)

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int[] result = new int[2];
        result[0] = findFirst(nums, target);
        result[1] = findLast(nums, target);
        return result;
    }

    private int findFirst(int[] nums, int target) {
        
        int idx = -1;
        int start = 0;
        int end = nums.length - 1;
        
        while (start <= end) {
            
            int mid = (start + end) / 2;
            
            // here is difference
            if (nums[mid] >= target)
                end = mid - 1;
            else
                start = mid + 1;
            
            if (nums[mid] == target) idx = mid;
        }
        return idx;
    }

    private int findLast(int[] nums, int target) {
        
        int idx = -1;
        int start = 0;
        int end = nums.length - 1;
        
        while (start <= end) {
            
            int mid = (start + end) / 2;
            
            // here is difference
            if (nums[mid] <= target)
                start = mid + 1;
            else
                end = mid - 1;
            
            if (nums[mid] == target) idx = mid;
        }
        return idx;
    }
}
/**
[Question]
- Find First and Last Position of Element in Sorted Array
- find the starting and ending position of a given target value.
- If target is not found in the array, return [-1, -1].

[Condition]
- 0 <= nums.length <= 10.5
- 10.9 <= nums[i] <= 10.9
- -10.9 <= target <= 10.9
**/
```
The source : <https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/discuss/14734/Easy-java-O(logn)-solution>
