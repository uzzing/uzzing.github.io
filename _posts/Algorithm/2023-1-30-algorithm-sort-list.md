---
title:  "[Medium] Sort List"
date: 2023-1-30 10:00AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-1-30 10:00AM
---

# 'Sort List (Medium)`

---

## 📌 Problem
<https://leetcode.com/problems/sort-list/>


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
    public ListNode sortList(ListNode head) {
        //bottom case
        if (head == null) {
            return head;
        }
        if (head.next == null) {
            return head;
        }
        
        //p1 move 1 step every time, p2 move 2 step every time, pre record node before p1
        ListNode p1 = head;
        ListNode p2 = head;
        ListNode pre = head;
        
        while (p2 != null && p2.next != null) {
            pre = p1;
            p1 = p1.next;
            p2 = p2.next.next;
        }
        //change pre next to null, make two sub list(head to pre, p1 to p2)
        pre.next = null;
        
        //handle those two sub list
        ListNode h1 = sortList(head);
        ListNode h2 = sortList(p1);
        
        return merge(h1, h2);
    }

    //merge two sorted list, return result head
    public ListNode merge(ListNode h1, ListNode h2) {
        if (h1 == null) {
            return h2;
        }
        if (h2 == null) {
            return h1;
        }
        
        if (h1.val < h2.val) {
            h1.next = merge(h1.next, h2);
            return h1;
        }
        else {
            h2.next = merge(h1, h2.next);
            return h2;
        }   
    }
}
```

- reference
: <https://leetcode.com/problems/sort-list/solutions/46716/basically-it-seems-like-merge-sort-problem-really-easy-understand/?orderBy=most_votes&languageTags=java>


```java
class Solution {
    public ListNode sortList(ListNode head) {
        
        ListNode temp=head;
        int count=0;
        while(temp!=null){
            count++;
            temp=temp.next;
        }
        temp=head;
        int a[]=new int[count];
        count=0;
        while(temp!=null){
            a[count++]=temp.val;
            temp=temp.next;
        }
        temp=head;
        Arrays.sort(a);
        int k=0;
        while(temp!=null){
            temp.val=a[k++];
            temp=temp.next;
        }
        return head;
        
    }
}
```

- reference
: <https://leetcode.com/problems/sort-list/solutions/3027781/simple-java-code/?orderBy=most_votes&languageTags=java>