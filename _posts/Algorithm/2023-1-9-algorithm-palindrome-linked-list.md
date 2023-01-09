---
title:  "[Easy] Panlindrome Linked List"
date: 2023-1-9 4:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-9 4:30PM
---

# 'Panlindrome Linked List' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/palindrome-linked-list/>


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
    public boolean isPalindrome(ListNode head) {

        // 1. Copying the Linked List into an Array.
        List<Integer> vals = new ArrayList<>();
        ListNode currentNode = head;

        while (currentNode != null) {
            vals.add(currentNode.val);
            currentNode = currentNode.next;
        }

        // 2. Checking whether or not the Array is a palindrome.
        int front = 0;
        int back = vals.size() - 1;
        while (front < back) {
            if (!vals.get(front).equals(vals.get(back))) {
                return false;
            }
            front++;
            back--;
        }

        return true;
    }
}
```

- Reference
: <https://leetcode.com/problems/palindrome-linked-list/solutions/433547/official-solution/>