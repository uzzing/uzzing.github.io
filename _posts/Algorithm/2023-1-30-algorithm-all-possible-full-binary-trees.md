---
title:  "[Medium] All Possible Full Binary Trees"
date: 2023-1-30 5:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, recursion]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 5:00PM
---

# 'All Possible Full Binary Trees(Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/all-possible-full-binary-trees/>


## 📌 Answer

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    Map<Integer , List<TreeNode>> map = new HashMap<>();
    
    public List<TreeNode> allPossibleFBT(int n) {
        
        if (!map.containsKey(n)) {
            List<TreeNode> res = new ArrayList<>();

            if (n == 1) {
                res.add(new TreeNode(0,null,null));
            } else {
                for (int i = 1 ; i < n ; i += 2) {
                    List<TreeNode> leftSubtree = allPossibleFBT(i);
                    List<TreeNode> rightSubtree = allPossibleFBT(n - i - 1);

                    for (TreeNode left : leftSubtree) {
                        for (TreeNode right : rightSubtree) {
                            res.add(new TreeNode(0,left,right));
                        }
                    }
                }
            }
            map.put(n , res);
        }
        
        return map.get(n);
    }
}
```

- reference 
: <https://leetcode.com/problems/all-possible-full-binary-trees/solutions/1556987/simple-java-dfs-memoization-solution/?orderBy=most_votes&languageTags=java>