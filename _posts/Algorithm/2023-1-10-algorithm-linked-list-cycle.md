---
title:  "[Easy] Linked List Cycle"
date: 2023-1-10 1:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-10 1:00PM
---

# 'Linked List Cycle' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/linked-list-cycle/>


## 📌 Answer
```java
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public boolean hasCycle(ListNode head) {
        if (head == null || head.next == null) return false;

		Set<ListNode> set = new HashSet<>();

        while (head != null) {
            if (set.contains(head)) return true;

            set.add(head);
            head = head.next;
        }
        
        return false;
    }
}
```

- Reference
    - <https://leetcode.com/problems/linked-list-cycle/solutions/44614/java-11ms-solution-with-hashset-and-1ms-solution-without-extra-space/?orderBy=most_votes&languageTags=java>

    - <https://leetcode.com/problems/reverse-linked-list/solutions/1866153/java-2-solutons-in-place-operation-beats-100-and-create-a-new-linked-list-beats-100/?orderBy=most_votes&languageTags=java>

