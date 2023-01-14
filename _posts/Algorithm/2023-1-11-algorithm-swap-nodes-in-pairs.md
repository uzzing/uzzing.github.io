---
title:  "[Medium] Swap Nodes in Pairs"
date: 2023-1-11 2:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-11 2:00PM
---

# 'Swap Nodes in Pairs (Medium)

---

## 📌 Problem
<https://leetcode.com/problems/swap-nodes-in-pairs/>


## 📌 Answer

- Iterative
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
    public ListNode swapPairs(ListNode head) {

        ListNode temp = head;
        
        while (head != null && head.next != null) {
            int curr = head.val;
            int next = head.next.val;
            head.next.val = curr;
            head.val = next;
            head = head.next.next;
        }

        return temp;
    }
}
```

- Recursive
```java
class Solution {
    public ListNode swapPairs(ListNode head) {
        if (head == null || head.next == null) return head;
        
        ListNode nxt = head.next;
        head.next = swapPairs(nxt.next);
        nxt.next = head;
        
        return nxt;
    }
}
```

- Reference
    - <https://leetcode.com/problems/swap-nodes-in-pairs/solutions/11204/java-recursive-and-iterative-solutions/?orderBy=most_votes&languageTags=java>

