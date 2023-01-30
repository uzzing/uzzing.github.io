---
title:  "[Medium] Merge Nodes in Between Zeros"
date: 2023-1-30 10:00AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 10:00AM
---

# 'Merge Nodes in Between Zeros (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/merge-nodes-in-between-zeros/>


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
    public ListNode mergeNodes(ListNode head) {

        ListNode result = new ListNode(0);
        ListNode resultNode = result;
        
        int sum = 0;
        while (head.next != null) {
            head = head.next;

            if (head.val != 0) sum += head.val;
            else {
                result.val = sum;
                if (head.next != null) {
                    result.next = new ListNode(0);
                    result = result.next;
                }
                sum = 0;
            }
        }

        return resultNode;
    }
}
```

```java
class Solution {
    public ListNode mergeNodes(ListNode head) {
        ListNode dummy = new ListNode(Integer.MIN_VALUE), prev = dummy;
        while (head != null && head.next != null) {
            prev.next = head; // prev connects next 0 node.
            head = head.next; // head forward to a non-zero node.
            
            while (head != null && head.val != 0) { // traverse all non-zero nodes between two zero nodes.
                prev.next.val += head.val; // add current value to the previous zero node.
                head = head.next; // forward one step.
            }
            prev = prev.next; // prev point to the summation node (initially 0).
        }
        prev.next = null; // cut off last 0 node.

        return dummy.next;
    }
}

```

- reference
: <https://leetcode.com/problems/merge-nodes-in-between-zeros/solutions/1784766/java-python-3-one-pass-two-pointers-copy-sum-to-0-nodes/?orderBy=most_votes&languageTags=java>