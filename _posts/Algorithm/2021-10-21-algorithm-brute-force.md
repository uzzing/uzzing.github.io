---
title:  "[Algorithm] Brute-force Search"
date: 2021-10-22 2:17PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-22 2:17PM
---
# Brute-force Search
```text
enumerate all possible candidates for the solution and check whether each candidate satisfies the problem's statement.
```
It is often used with BFS / DFS

---

# Task
## 1. 타겟 넘버 in Programmers (Level 2)
### 📌 Problem 
<https://programmers.co.kr/learn/courses/30/lessons/43165>

### 📌 The point
You must visit all nodes and check all possibility.

### 📌 Answer

#### Case 1. Used BFS (Queue)
**The point**
- Brute-force search + BFS(Queue)
- make a variable 'index' for depth
- But, BFS is slower than DFS -> so DFS is more preferable than BFS.

```java
import java.util.Queue;
import java.util.LinkedList;

class Solution {

    class Pair {
        int index;
        int number;

        Pair(int index, int number) {
            this.index = index;
            this.number = number;
        }
    }

    public int solution(int[] numbers, int target) {
        int answer = 0;

        Queue<Pair> queue = new LinkedList<>();

        queue.add(new Pair(0, numbers[0]));
        queue.add(new Pair(0, -numbers[0])); // -> at first, start the negative number (ex. -1)

        while (!queue.isEmpty()) {
            Pair now = queue.poll(); // get data and delete it

            // if it is last index
            if (now.index == numbers.length - 1) {

                // if it is same with target
                if (now.number == target) answer++;
                continue;
            }

            // case1. add
            int newNum1 = now.number + numbers[now.index + 1]; 
            queue.add(new Pair(now.index + 1, newNum1));

            // case2. minus
            int newNum2 = now.number - numbers[now.index + 1];
            queue.add(new Pair(now.index + 1, newNum2));
        }

        return answer;
    }
}
```

#### Case 2. Used DFS (Recursion)
##### The point
- Brute-force search + DFS(Recursion)
- DFS is **faster and more space-efficient** than BFS -> you must select this way to solve it

```java
class Solution {

    // main function
    public int solution(int[] numbers, int target) {
        int answer = 0;
        
        // recursion
        // case1. add
        answer += dfs(numbers, target, numbers[0], 1);

        // case2. minus
        answer += dfs(numbers, target, -numbers[0], 1);
        
        return answer;
    }
    
    private int dfs(int[] numbers, int target, int pre, int index) {

        if (index >= numbers.length) {
            if (pre == target) return 1; // answer++;
            return 0;
        }

        int answer = 0;

        // case1. add
        int cur1 = pre + numbers[index];
        answer += dfs(numbers, target, cur1, index + 1);

        // case2. minus
        int cur2 = pre - numbers[index];
        answer += dfs(numbers, target, cur2, index + 1);

        return answer;
    }
}
``` 
The source : <https://www.pymoon.com/entry/Programmers-타겟-넘버-BFSDFS-Java-풀이>

---
