---
title:  "[Easy] Middle of the Linked List"
date: 2023-1-10 6:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-10 6:30PM
---

# 'Middle of the Linked List' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/middle-of-the-linked-list/>


## 📌 Answer

When traversing the list with a pointer slow, make another pointer fast that traverses twice as fast. When **fast** reaches **the end of the list**, **slow** must be **in the middle**.

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
    public ListNode middleNode(ListNode head) {
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
}
```

- Reference
: <https://leetcode.com/problems/middle-of-the-linked-list/solutions/154715/middle-of-the-linked-list/?orderBy=most_votes>