---
title:  "[Algorithm] Heap"
date: 2021-10-24 7:08PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-24 7:35PM
---
# Heap
In Java, **PriorityQueue** can be used as a Heap. <br>

[Detail](https://uzzing.github.io/posts/heap/)

---

# Task
# 더 맵게 in Programmers (Level 2)
---
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42626>

## 📌 The point
- Use **PriorityQueue & Min-Heap**
    - `PriorityQueue<Integer> heap = new PriorityQueue<>();`
    - to pick the minimum value


`When I face problems which need to get the minimum value or the maximum value,`
`It's more efficient if I use PriorityQueue! Let's apply it afterwards 🎃`

## 📌 Answer
```java
import java.util.PriorityQueue;

class Solution {
    
    public int solution(int[] scoville, int K) {
        int answer = 0;

        // Used min-heap
        PriorityQueue<Integer> heap = new PriorityQueue<>();

        // convert int array to PriorityQueue
        // ex. scoville [1, 2, 9, 3, 10, 12] -> heap [1, 2, 3, 9, 10, 12]
        for (int i = 0; i < scoville.length; i++)
            heap.offer(scoville[i]);
        

        while (heap.peek() < K) {

            if (heap.size() < 2) return -1; // if all datas can't be K or more

            int f1 = heap.poll(); // get the minimum value and remove
            int f2 = heap.poll();

            int newFood = f1 + (f2 * 2);
            heap.offer(newFood); // add data
            answer++;
        }

        return answer;
    }
}
/**
[Question]
- scoville : 모든 음식의 스코빌 지수 (value : 2 or more and 1,000,000 or less)
- K : 스코빌 지수 (value : 0 or more and 1,000,000 or less)
- return : 섞어야 하는 최소 횟수 for 모든 음식의 스코빌 지수 >= K
    - 만들 수 없는 경우에는 -1
    
- 섞은 음식의 스코빌 지수 = 가장 맵지 않은 음식의 스코빌 지수 
                    + (두 번째로 맵지 않은 음식의 스코빌 지수 * 2)
**/
```

The source : <https://velog.io/@peppermint100/Algo프로그래머스-더-맵게-in-Java>
