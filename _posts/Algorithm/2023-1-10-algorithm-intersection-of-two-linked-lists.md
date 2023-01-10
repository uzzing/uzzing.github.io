---
title:  "[Easy] Intersection of Two Linked Lists"
date: 2023-1-10 5:30PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-10 5:30PM
---

# 'Intersection of Two Linked Lists' in LeetCode (Easy)

---

## 📌 Problem
<https://leetcode.com/problems/intersection-of-two-linked-lists/>


## 📌 Answer

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode p1 = headA, p2 = headB;
        int len1 = 0, len2 = 0;
        
        while (p1 != null) {
            p1 = p1.next;
            len1++;
        }
        while (p2 != null) {
            p2 = p2.next;
            len2++;
        }

        p1 = headA;
        p2 = headB;

        if (len1 > len2) {
            for (int i = 0; i < len1 - len2; i++) {
                p1 = p1.next;
            }
        } else {
            for (int i = 0; i < len2 - len1; i++) {
                p2 = p2.next;
            }
        }

        while (p1 != p2) {
            // System.out.println("p1 : " + p1.val);
            // System.out.println("p2 : " + p2.val);
            // System.out.println();
            
            p1 = p1.next;
            p2 = p2.next;
        }
        return p1;
    }
}
```

- Reference
    - <https://leetcode.com/problems/intersection-of-two-linked-lists/solutions/49902/java-beats-99-56/?orderBy=most_votes&languageTags=java>

