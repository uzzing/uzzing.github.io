---
title:  "[Algorithm] Add Two Numbers"
date: 2021-10-25 2:57PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Leetcode]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 2:57PM
---

# 'Min Stack' in LeetCode (Easy)
---
## 📌 Problem
<https://leetcode.com/problems/add-two-numbers/>

## 📌 Answer

[Result](https://leetcode.com/submissions/detail/576791361/)

```java
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        
        ListNode node = new ListNode(0); // first node
        ListNode result = node;
        int sum = 0;
        
        while (l1 != null || l2 != null || sum > 0) {
            
            if (l1 != null) {
                sum += l1.val;
                l1 = l1.next;
            }
            
            if (l2 != null) {
                sum += l2.val;
                l2 = l2.next;
            }
            
            node.next = new ListNode(sum % 10);
            sum /= 10;
            
            node = node.next;
        }

        return result.next;
    }
}
// Add the two numbers and return the sum as a linked list.

/**
 * Definition for singly-linked list.
 * public class ListNode { // linked lists
 *     int val; ->.  non-negative integers, reverse order
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
```
The source : <https://leetcode.com/problems/add-two-numbers/discuss/735511/Java-So-clear.>
