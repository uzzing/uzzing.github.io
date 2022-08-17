---
title:  "[] Implement strStr()"
date: 2022-8-5 1:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-4 1:30PM
---

# 'Remove Duplicates from Sorted Array' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/implement-strstr/>

## 📌 Answer

### The Point 
- String methods : `contains()`, `indexOf()`

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle == "" || haystack == "") return 0;
	    else if (haystack.contains(needle)) return haystack.indexOf(needle);
	    else return -1;
    }
}
```

```java
class Solution {
    public int strStr(String haystack, String needle) {
        for (int i = 0; ; i++) {
            for (int j = 0; ; j++) {
            if (j == needle.length()) return i;
            if (i + j == haystack.length()) return -1;
            if (needle.charAt(j) != haystack.charAt(i + j)) break;
            }
        }
    }
}
```
