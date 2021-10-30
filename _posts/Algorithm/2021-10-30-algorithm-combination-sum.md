---
title:  "[Algorithm] Combination Sum"
date: 2021-10-30 1:15PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-30 1:15PM
---

# 'Combination Sum' in LeetCode (Medium)

---

## 📌 Problem
<https://leetcode.com/problems/combination-sum/>

## 📌 Answer
### The point
- backtracking

```java
import java.util.List;

class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        
        List<List<Integer>> result = new ArrayList<>();
        
        Arrays.sort(candidates);
        
       
        backtrack(result, new ArrayList<>(), candidates, target, 0);
        
        return result;
    }
    
    private void backtrack(List<List<Integer>> list, List<Integer> temp, int[] nums, int remain, int start) {
        if (remain < 0) return;
        else if (remain == 0) {
            // System.out.println("when? ");
            list.add(new ArrayList<>(temp));
        }
        else {
            for (int i = start; i < nums.length; i++) {
                // System.out.println(temp);
                temp.add(nums[i]);
                backtrack(list, temp, nums, remain - nums[i], i); // check again until remain become minus
                temp.remove(temp.size() - 1);
                // System.out.println(temp);
                // System.out.println();
            }
        }
    }
}
/**
[Question]
- candidates : distinct integers
- target : a target integer
- return : a list of all unique combinations of candidates where the chosen numbers sum to target
**/
```
The source : <https://leetcode.com/problems/combination-sum/discuss/16502/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partitioning)>

---
I'm gonna eat sandwich 🥪🥪🥪