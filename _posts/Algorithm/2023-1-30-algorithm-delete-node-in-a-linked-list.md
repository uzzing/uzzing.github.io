---
title:  "[Medium] Delete Node in a Linked List"
date: 2023-1-30 10:00AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 10:00AM
---

# 'Delete Node in a Linked List (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/delete-node-in-a-linked-list/>


## 📌 Answer

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {

    // input node will be deleted node
    public void deleteNode(ListNode node) {
        ListNode nextNode = node.next;
        node.val = nextNode.val;
        node.next = nextNode.next;
        nextNode.next = null;
    }
}
```

- reference
: <https://leetcode.com/problems/delete-node-in-a-linked-list/solutions/2506192/delete-node-in-a-linked-list/?orderBy=most_votes>