---
title:  "[Easy] Reverse Linked List"
date: 2023-1-10 3:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-10 3:30PM
---

# 'Reverse Linked List' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/reverse-linked-list/>


## 📌 Answer

![linkednode](https://user-images.githubusercontent.com/83699657/211478452-336a8fe5-258d-404e-ab37-e13ee3cad00f.jpeg)

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
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null) return head;
        ListNode curr = head;
        ListNode prev = null;
        ListNode next;
        while (curr != null) {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
}
```

- Reference
    - <https://leetcode.com/problems/reverse-linked-list/solutions/1866153/java-2-solutons-in-place-operation-beats-100-and-create-a-new-linked-list-beats-100/?orderBy=most_votes&languageTags=java>

