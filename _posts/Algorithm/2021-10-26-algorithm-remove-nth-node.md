---
title:  "[Algorithm] Remove Nth Node From End of List"
date: 2021-10-26 7:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-26 7:00PM
---
# 'Remove Nth Node From End of List' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/remove-nth-node-from-end-of-list/>

## 📌 Answer
### Two-Pointer
#### The point
- For a singly linked list, used two pointer **'fast', 'slow'**

The time and space complexity is quite good.

<img width="424" alt="Screen Shot 2021-10-26 at 7 05 36 PM" src="https://user-images.githubusercontent.com/83699657/138857045-df4a2e27-ee9e-409c-91bb-f2ac803b1cff.png">


[Result](https://leetcode.com/submissions/detail/577435403/)

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        
        ListNode start = new ListNode(0);

        // two pointer
        ListNode slow = start, fast = start;
        start.next = head;
        
        
        for (int i = 1; i <= n + 1; i++) {
            fast = fast.next;
        }
        
        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
        }

        slow.next = slow.next.next;

        return start.next;
    }
}
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
/**
[Question]
- remove the nth node from the end of the list
- return its head.

[Condition]
- The number of nodes in the list is sz. 
**/
```
The source : <https://leetcode.com/problems/remove-nth-node-from-end-of-list/discuss/589304/CLEAR-JAVA-SOLUTION-WITH-DETAILED-EXPLANATION!>
And ⭐️ it's the best explanation

---
I'm not good at singly linked list.... <br>
Let's search it.