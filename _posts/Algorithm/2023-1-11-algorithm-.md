---
title:  "[Easy] Rotate List"
date: 2023-1-11 4:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-11 4:00PM
---

# 'Rotate List (Medium)'

---

## 📌 Problem
<https://leetcode.com/problems/rotate-list/>


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
    public ListNode rotateRight(ListNode head, int k) {

        if (head == null || head.next == null) return head;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode fast = dummy, slow = dummy;
        
        int i;
        // Get the total length
        for (i = 0; fast.next != null; i++) fast = fast.next;
        
        // Get the i - k % i th node
        for (int j = i - k % i; j > 0; j--) slow = slow.next;
        
        // Do the rotation
        fast.next = dummy.next;
        dummy.next = slow.next;
        slow.next = null;
        
        return dummy.next;
    }
}
```


- Reference
    - <https://leetcode.com/problems/rotate-list/solutions/22715/share-my-java-solution-with-explanation/?orderBy=most_votes&languageTags=java>

