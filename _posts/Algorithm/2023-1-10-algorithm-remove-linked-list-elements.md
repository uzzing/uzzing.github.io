---
title:  "[Easy] Remove Linked List Elements"
date: 2023-1-10 4:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-10 4:30PM
---

# 'Remove Linked List Elements' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/remove-linked-list-elements/>


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
public class Solution {
    public ListNode removeElements(ListNode head, int val) {
        while (head != null && head.val == val) head = head.next;
        ListNode curr = head;
        while (curr != null && curr.next != null) {
            // System.out.println("curr before : " + curr.val);
            if (curr.next.val == val) curr.next = curr.next.next; // remove next
            else curr = curr.next; // go next
            // System.out.println("curr after : " + curr.val);
            // System.out.println();
        }
        return head;
    }
}

/**
Input: head = [1,2,6,3,4,5,6], val = 6
Output: [1,2,3,4,5]

Stdout
curr before : 1
curr after : 2

curr before : 2
curr after : 2

curr before : 2
curr after : 3

curr before : 3
curr after : 4

curr before : 4
curr after : 5

curr before : 5
curr after : 5
**/
```

```java
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) return null;
        head.next = removeElements(head.next, val);
        return head.val == val ? head.next : head;
    }
}
```

- Reference
    - <https://leetcode.com/problems/remove-linked-list-elements/solutions/57323/iterative-short-java-solution/?orderBy=most_votes&languageTags=java>

    - <https://leetcode.com/problems/remove-linked-list-elements/solutions/57306/3-line-recursive-solution/?orderBy=most_votes&languageTags=java>

