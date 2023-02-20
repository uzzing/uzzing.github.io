---
title:  "[Medium] Swapping Nodes in a Linked List"
date: 2023-2-20 5:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode, recursion]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-2-20 5:00PM
---

# 'Swapping Nodes in a Linked List (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/swapping-nodes-in-a-linked-list/>


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
    public ListNode swapNodes(ListNode head, int k) {
        ListNode fast = head;
        ListNode slow = head;
        ListNode first = head, second = head;
        
		// Put fast (k-1) nodes after slow
        for (int i = 1; i < k; i++)
            fast = fast.next;
            
		// Save the node for swapping
        first = fast;

		// Move until the end of the list
        while (fast.next != null) {
			slow = slow.next;
            fast = fast.next;
        }
        
        // Save the second node for swapping
		// Note that the pointer second isn't necessary: we could use slow for swapping as well
		// However, having second improves readability
        second = slow;
		
		// Swap values
        int temp = first.val;
        first.val = second.val;
        second.val = temp;
        
        return head;
    }
}
```

Reference 
: <https://leetcode.com/problems/swapping-nodes-in-a-linked-list/solutions/1009918/java-two-pointers-detailed-explanation-o-n-time-o-1-space/?orderBy=most_votes&languageTags=java>