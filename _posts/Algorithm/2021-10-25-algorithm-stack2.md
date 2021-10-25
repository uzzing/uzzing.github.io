---
title:  "[Algorithm] Stack2"
date: 2021-10-25 10:03AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 10:03AM
---
# Stack
---

# Task
# 'Min Stack' in LeetCode (Easy)
---
## 📌 Problem
<https://leetcode.com/problems/min-stack/submissions/>

## 📌 Answer
###  1. Use Stack
#### The point
- If a inputted data is minimum, push two times.
- Pop two times when pop is same as min

[Result](https://leetcode.com/submissions/detail/576657616/)

```java
class MinStack {
    
    private Stack<Integer> stack;
    private int min;

    // constructor
    public MinStack() {
        stack = new Stack<>();
        min = Integer.MAX_VALUE;
    }
    
    public void push(int val) {

        // important
        if (min >= val) {
            stack.push(min);
            min = val;
        }
        stack.push(val);
    }
    
    public void pop() {
        int top = stack.pop();
        if (top == min) min = stack.pop(); // pop again
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int getMin() {
        return min;
    }
}
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack obj = new MinStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.top();
 * int param_4 = obj.getMin();
 */
```
The source : <https://leetcode.com/problems/min-stack/discuss/49014>

Well, its efficiency is not bad

<img width="665" alt="Screen Shot 2021-10-25 at 9 42 15 AM" src="https://user-images.githubusercontent.com/83699657/138620023-0b0903b1-08a3-45ad-b118-c95bc59dea24.png">


### 2. Implementation by yourself
#### The point
- Make the custom class in the class -> incredible 😲

[Result](https://leetcode.com/submissions/detail/576661377/)

```java
class MinStack {

    ListNode top;
    
    public class ListNode {
        int data;
        int min;
        ListNode next;
        
        ListNode(int data) {
            this.data = data;
            next = null;
            min = Integer.MAX_VALUE;
        }
    }
    
    /** initialize your data structure here. */
    public MinStack() {
        top = null;
    }
    
    public void push(int val) {
        ListNode t = new ListNode(val);
        t.next = top;
        if (top == null) {
            t.min = t.data; // SecondStack.Push(t.data);
        }
        else {
            if (t.data < top.min) {
                t.min = t.data; // SecondStack.Push(t.data);
            } else {
                t.min = top.min; // SecondStack.Push(top.min);
            }
        }
        top = t;
    }
    
    public void pop() {
        if (top == null) {
            System.err.println("Empty Stack");
            return;
        }
        top = top.next;
    }
    
    public int top() {
        return top.data;
    }
    
    public int getMin() {
        return top.min;
    }
}
```
The source : <https://leetcode.com/problems/min-stack/discuss/509793/Java-Solution-one-Stack-O(1)-time-solution>

It's almost same efficient as first answer.

---
It's the first time I use LeetCode.<br>
It's so useful site because I can check the other answers easily after I submit mine.<br>
So interesting!