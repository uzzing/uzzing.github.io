---
title:  "[Medium] Merge In Between Linked Lists"
date: 2023-1-30 10:00AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 10:00AM
---

# 'Merge In Between Linked Lists (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/merge-in-between-linked-lists/>


## 📌 Answer

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode mergeInBetween(ListNode list1, int a, int b, ListNode list2) {
        ListNode left = list1;
        for (int i = 1; i < a; i++)
            left = left.next;

        ListNode middle = left;
        for (int i = a; i <= b; i++)
            middle = middle.next;
        
		left.next = list2;
        while (list2.next != null)
            list2 = list2.next;
        
        list2.next = middle.next;
        
        return list1;
    }
}
```

- reference 
: <https://leetcode.com/problems/merge-in-between-linked-lists/solutions/993116/java-easy-solution-beats-100-time-o-n-space-o-1/?languageTags=java>