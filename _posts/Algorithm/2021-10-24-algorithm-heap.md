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
# λ λ§΅κ² in Programmers (Level 2)
---
## π Problem
<https://programmers.co.kr/learn/courses/30/lessons/42626>

## π The point
- Use **PriorityQueue & Min-Heap**
    - `PriorityQueue<Integer> heap = new PriorityQueue<>();`
    - to pick the minimum value


`When I face problems which need to get the minimum value or the maximum value,`
`It's more efficient if I use PriorityQueue! Let's apply it afterwards π`

## π Answer
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
- scoville : λͺ¨λ  μμμ μ€μ½λΉ μ§μ (value : 2 or more and 1,000,000 or less)
- K : μ€μ½λΉ μ§μ (value : 0 or more and 1,000,000 or less)
- return : μμ΄μΌ νλ μ΅μ νμ for λͺ¨λ  μμμ μ€μ½λΉ μ§μ >= K
    - λ§λ€ μ μλ κ²½μ°μλ -1
    
- μμ μμμ μ€μ½λΉ μ§μ = κ°μ₯ λ§΅μ§ μμ μμμ μ€μ½λΉ μ§μ 
                    + (λ λ²μ§Έλ‘ λ§΅μ§ μμ μμμ μ€μ½λΉ μ§μ * 2)
**/
```

The source : <https://velog.io/@peppermint100/Algoνλ‘κ·Έλλ¨Έμ€-λ-λ§΅κ²-in-Java>
