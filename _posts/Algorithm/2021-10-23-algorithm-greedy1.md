---
title:  "[Algorithm] Greedy1"
date: 2021-10-23 1:20PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-23 1:20PM
---
# Greedy algorithm
---

# Task
# 1. 큰 수 만들기 in Programmers (Level 2)
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42883>

## 📌 The point
- Compare the size of numbers and save the result to Stack
    -> so, it's quite fast because of stack

## 📌 Answer
```java
import java.util.Stack;

class Solution {
    public String solution(String number, int k) {
        
        char[] result = new char[number.length() - k];
        Stack<Character> stack = new Stack<>();
        
        for (int i = 0; i < number.length(); i++) { 
            char now = number.charAt(i);
            
            // make stack empty
            // important condition : stack.peek() < now
            // = if (the top of stack < now) delete top 
            while (!stack.isEmpty() && stack.peek() < now && k > 0) {
                stack.pop();
                k--;
                
                // System.out.println("k : " + k);
            }
            
            stack.push(now);
            
            // System.out.println("now : " + now);
            // System.out.println("stack : " + stack);
            // System.out.println();
        }
        
        // get the data in the order
        for (int i = 0; i < result.length; i++)
            result[i] = stack.get(i);
        
        // make char array to string
        return new String(result);
    }
}
/**
[Logic]
- greedy algorithm : choose the best answer at each moment
- compare the numbers
**/
```
The source : <https://wpioneer.tistory.com/110>

There are so many genius in the world,,,,
I'll study all ways how they solve the problem.
