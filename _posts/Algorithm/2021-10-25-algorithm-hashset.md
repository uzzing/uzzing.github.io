---
title:  "[Algorithm] Longest Substring Without Repeating Characters"
date: 2021-10-25 6:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Leetcode]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 6:00PM
---
# HashSet
[Detail](https://uzzing.github.io/posts/hashset/)

---

# 'Longest Substring Without Repeating Characters' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/longest-substring-without-repeating-characters/>

## 📌 Answer

### The point
- HashSet.contains(Object)
    - Object ex. Character, String...

- String.charAt(int index)

- import java.lang.Math;


```java
import java.util.Set;
import java.util.HashSet;
import java.lang.Math;

class Solution {
    public int lengthOfLongestSubstring(String s) {
        
        int i = 0, j = 0, max = 0;
        Set<Character> set = new HashSet<>();

        while (j < s.length()) { // make the set without duplication
            
            // if there is no duplicate element in set
            if (!set.contains(s.charAt(j))) {
                
                set.add(s.charAt(j++)); // add to set
                max = Math.max(max, set.size()); // get max length
                
            } 
            else set.remove(s.charAt(i++)); // if not, remove the duplicate element in set
        }

        return max;
    }
}
/**
[Question]
- find the length of the longest substring without repeating characters.
**/
```

The source : <https://leetcode.com/problems/longest-substring-without-repeating-characters/discuss/1812/Share-my-Java-solution-using-HashSet>