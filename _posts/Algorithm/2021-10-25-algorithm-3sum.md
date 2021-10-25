---
title:  "[Algorithm] 3Sum"
date: 2021-10-25 10:27PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Leetcode]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 10:27PM

---

# '3Sum' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/3sum/>

## 📌 Answer
### The point
- **Sort** array first
- Used **Two-pointers technique**
    - **i and j**

[More detail about 'Two pointers algorithm'](https://leetcode.com/articles/two-pointer-technique/)


[Result](https://leetcode.com/submissions/detail/576925503/)

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        
        Arrays.sort(nums);
        
        List<List<Integer>> list = new ArrayList<>();
    
        for (int i = 0; i < nums.length - 2; i++) {
            
            // avoid duplicates
            if (i > 0 && (nums[i] == nums[i-1])) continue;
            
            // start : i, j , , , , , k
            int j = i + 1;
            int k = nums.length-1;
            
            while (j < k) {

                int sum = nums[i] + nums[j] + nums[k];

                if (sum == 0) {
                    
                    list.add(Arrays.asList(nums[i], nums[j], nums[k]));

                    // move again to make new list
                    j++;
                    k--;

                    // avoid duplicates
                    while ((j < k) && (nums[j] == nums[j - 1])) j++;
                    while ((j < k) && (nums[k] == nums[k + 1])) k--;

                }
                else if (sum > 0) k--;
                else if (sum < 0) j++;
            }
        }

        return list;
    }
}
/**
[Question]
- return all the triplets [nums[i], nums[j], nums[k]]
- condition
    - i != j, i != k, j != k (index)
    - nums[i] + nums[j] + nums[k] == 0 (value)
    - the solution set must not contain duplicate triplets.
**/
```

The source : <https://leetcode.com/problems/3sum/discuss/7631/Simple-Java-Solution-Without-using-HashSet>
