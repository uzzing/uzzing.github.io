---
title:  "[Easy] Convert Binary Number in a Linked List to Integer"
date: 2023-1-11 1:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-11 1:30PM
---

# 'Convert Binary Number in a Linked List to Integer (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/>


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
    public int getDecimalValue(ListNode head) {
        int num = head.val;
        while (head.next != null) {
            num = num * 2 + head.next.val;
            head = head.next;    
        }
        return num;
    }
}
```

- Reference
    - <https://leetcode.com/problems/convert-binary-number-in-a-linked-list-to-integer/solutions/851040/convert-binary-number-in-a-linked-list-to-integer/?orderBy=most_votes>

