---
title:  "[HashSet] Find the Duplicate Number"
date: 2021-11-4 10:59PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, binary search]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-11-4 10:59PM
---

# 'Find the Duplicate Number' in LeetCode (Medium)

---

## 📌 Problem
<https://leetcode.com/problems/find-the-duplicate-number/>

## 📌 Answer
### The point

- contains()
- Time complexity : O(n)
- Space complexity : O(n)

```java

class Solution {
    public int findDuplicate(int[] nums) {
        
        Set<Integer> seen = new HashSet<Integer>();
        
        for (int num : nums) {
            if (seen.contains(num))
                return num;
            seen.add(num);
        }

        return -1;
    }
}
```

## 📌 Other answer
### The point

- Time complexity : O(n)
- Space complexity : O(1)

<img width="438" alt="Screen Shot 2021-11-04 at 10 55 44 PM" src="https://user-images.githubusercontent.com/83699657/140326470-b8eb19d4-8404-4b19-ba12-cd03aadcfc0d.png">


```java
class Solution {
    public int findDuplicate(int[] nums) {

        while (nums[0] != nums[nums[0]]) {
            int nxt = nums[nums[0]];
            nums[nums[0]] = nums[0];
            nums[0] = nxt;
        }

        return nums[0];
    }
}
```


The source : <https://leetcode.com/problems/find-the-duplicate-number/solution/>


---
## 📌 Words

- intuitive : 직관적인