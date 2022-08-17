---
title:  "[Easy] Remove Duplicates from Sorted Array"
date: 2022-8-5 1:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-5 1:30PM
---

# 'Remove Duplicates from Sorted Array' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/remove-duplicates-from-sorted-array/>

## 📌 Answer
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i = 0;
        
        for (int n : nums) {
            if (i == 0 || n > nums[i-1]) nums[i++] = n;
        }
        
        return i;
    }
}
```

`The point`
- O(1) extra memory
    - Do not allocate extra space for another array.
- return a array size that you modified

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        
        int j = 0;
        for (int i = 1; i < nums.length; i++) {
            if (nums[j] != nums[i]) {
                j++;
                nums[j] = nums[i];
            }
        }
        
        return j + 1;
    }
}
```


### Custom Judge
```java
int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i < k; i++) {
    assert nums[i] == expectedNums[i];
}
```