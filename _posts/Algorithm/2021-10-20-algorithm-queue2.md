---
title:  "[Algorithm] Queue2"
date: 2021-10-20 10:50PM
excerpt: "coding test"

author: Yuha
categories: [Development, DataStructure, Algorithm]
tags: [datastructure, java, eng, algorithm, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-20 10:50PM
---
# Queue

## Task
### **`2. 프린터`** in Programmers (Level 2)
<https://programmers.co.kr/learn/courses/30/lessons/42586>

#### **`⭐️ The point`**
- Code that is often used when using queue 
```java
while (!queue.isEmpty()) {
        int num = queue.poll();
        // blah blah blah
}
```
- Used custom class
- Input class to queue
- Used boolean flag

#### **` Answer`**
```java
import java.util.Queue;
import java.util.LinkedList;

class Solution {
    
    class Task {
        int index;
        int priority;
        
        public Task(int index, int priority) {
            this.index = index;
            this.priority = priority;
        }
    }
    
    public int solution(int[] priorities, int location) {
        
        int answer = 0;
        
        // make queue of printing
        Queue<Task> queue = new LinkedList<>();
        
        for (int i = 0; i < priorities.length; i++) {
            queue.add(new Task(i, priorities[i]));
        }
        
        int nowIndex = 0;
        
        while (!queue.isEmpty()) {
            // get first task
            Task currTask = queue.poll();
            boolean flag = false;
            
            // true if there are bigger priorities in remaining queue
            for (Task t : queue)
                if (t.priority > currTask.priority) flag = true;
            
            if (flag) queue.add(currTask);
            else { // if it's the biggest priority

                // to skip big priority in order from next time
                nowIndex++;
                
                // if it's my print
                if (currTask.index == location) {
                    answer = nowIndex;
                    break;
                }
            } 
        }
        return answer;
    }
}
/**
중요도가 높은 문서를 먼저 인쇄하는 프린터
[Logic]
1. 인쇄 대기목록의 가장 앞에 있는 문서(J)를 대기목록에서 꺼냅니다.
    
2. 나머지 인쇄 대기목록에서 J보다 중요도가 높은 문서가 한 개라도 존재하면, J를 대기목록의 가장 마지막에 넣습니다.
    
3. 그렇지 않으면 J를 인쇄합니다.
    
return 내가 인쇄를 요청한 문서가 몇 번째로 인쇄되는지

[Condition]
- priorities : 문서의 중요도 배열 (value : 1~9)
- location : 내가 인쇄를 요청한 문서가 현재 대기목록의 어떤 위치에 있는지 (0~99 like index of array)
    ** the number of documents : 1 ~ 100

- ex. priorities : 1 1 9 1 1 1 -> print by order 'C D E F A B'
**/

// [Test case]
// 2 1 3 2 -> 1 3 2 2 -> 3 2 2 1 -> return 1
// 9 1 1 1 1 1 -> return 5
// 3 5 1 2 4 2, 4(4) 
```
---
My head can't work well anymore....