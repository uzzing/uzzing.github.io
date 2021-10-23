---
title:  "[Algorithm] Greedy3"
date: 2021-10-23 6:17PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-23 6:17PM
---
# Greedy algorithm
---

# Task
# 3. 조이스틱 in Programmers (Level 2)
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42860>

## 📌 The point
- Use the greedy
    - Check the condition
    - Choose the best at each moment
        - move up vs down
            - compare the length of movement
        - move left vs right
            - compare the length of movement

## 📌 Answer
```java
class Solution {
    public int solution(String name) {
        int answer = 0;
        int len = name.length();
        
        // if name only consists of 'A' 
        //      -> the minimum movement = just go right continuously 
        int min = len - 1;
        
        for (int i = 0; i < len; i++) {
            
             // get each char from String
            char c = name.charAt(i);
            
            // decide to move 'up or down'
            // up : c - 'A'
            // down : 'Z' - c + 1
            int move = (c - 'A' < 'Z' - c + 1) ? (c - 'A') : ('Z' - c + 1);
            answer += move;
            
            // decide to move 'right or left'
            
            // 1. first, go right -> count index by using nextIndex
            int nextIndex = i + 1;
            while (nextIndex < len && name.charAt(nextIndex) == 'A') 
                nextIndex++;
            
            // 2. compare which is the minimum value and update 'min'
            // - go right : min
            // - go back to left : (i * 2) + len - nextIndex
            //           -> i * 2 : go right + go back to left
            //           -> len - nextIndex : count from last index
            min = Math.min(min, (i * 2) + len - nextIndex);
        }
        
        answer += min;
        
        return answer;
    }
}
```
The source : <https://hellodavid.tistory.com/4a>

It is not difficult code, but I think it takes long time to come up with the way to solve.


And I have a heavy stomachache these days, so I make a reservation on hostipal on next wednesday 🥲
I hope I'm fine.