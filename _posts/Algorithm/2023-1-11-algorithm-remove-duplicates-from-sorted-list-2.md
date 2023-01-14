---
title:  "[Medium] Remove Duplicates from Sorted List II"
date: 2023-1-11 2:00PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-11 2:00PM
---

# 'Remove Duplicates from Sorted List II (Medium)'

---

## 📌 Problem
<https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/>


## 📌 Answer


```java
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        // sentinel
        ListNode sentinel = new ListNode(0, head);

        // predecessor = the last node 
        // before the sublist of duplicates
        ListNode pred = sentinel;
        
        while (head != null) {
            // if it's a beginning of duplicates sublist 
            // skip all duplicates
            if (head.next != null && head.val == head.next.val) {
                // move till the end of duplicates sublist
                while (head.next != null && head.val == head.next.val) {
                    head = head.next;    
                }
                // skip all duplicates
                pred.next = head.next;     
            // otherwise, move predecessor
            } else {
                pred = pred.next;    
            }
                
            // move forward
            head = head.next;    
        }  
        return sentinel.next;
    }
}
```


- Reference
    - <https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/solutions/952302/remove-duplicates-from-sorted-list-ii/?orderBy=most_votes>

