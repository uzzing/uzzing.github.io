---
title:  "[Medium] Maximum Twin Sum of a Linked List"
date: 2023-1-30 10:00AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 10:00AM
---

# 'Maximum Twin Sum of a Linked List (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/>


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
    public int pairSum(ListNode head) {
        
        // check size
        ListNode checkSize = head;
        int size = 1;
        while (checkSize.next != null) {
            checkSize = checkSize.next;
            size++;
        }

        // put the value of 0 ~ size/2 to stack
        Stack<Integer> stack = new Stack<>();
        for (int i = 0; i < size / 2; i++) {
            stack.push(head.val);
            head = head.next;
        }
        
        // make sum pop plus head.val / head = head.next;
        // compare prev sum with curr sum
        // - if curr sum is bigger, sum will be changed
        int sum = 0;
        while (head != null) {
            int curr = stack.pop() + head.val;
            if (sum < curr) sum = curr;
            head = head.next;
        }
        
        return sum; 
    }
}
```

```java
class Solution {
    public int pairSum(ListNode head) {
        if (head == null) {
            return 0;
        }
        if (head.next == null) {
            return head.val;
        }
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        slow = reverse(slow);
        fast = head;
        int sum = Integer.MIN_VALUE;
        while (slow != null) {
            sum = Math.max(slow.val + fast.val, sum);
            slow = slow.next;
            fast = fast.next;
        }
        return sum;
    }
    
    public ListNode reverse(ListNode node) {
        if (node == null) {
            return null;
        }
        ListNode current = node;
        ListNode previous = null;
        while (current != null) {
            ListNode next = current.next;
            current.next = previous;
            previous = current;
            current = next;
        }
        return previous;
    }
}
```

- reference
: <https://leetcode.com/problems/maximum-twin-sum-of-a-linked-list/solutions/1675791/my-java-solution-using-the-concepts-of-linkedlist/?orderBy=most_votes&languageTags=java>