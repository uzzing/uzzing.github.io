---
title:  "[Algorithm] Queue1"
date: 2021-10-20 4:02PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [datastructure, java, eng, algorithm, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-21 7:39PM
---
# Queue
[Explain](https://uzzing.github.io/posts/stack-queue/)

---

## Task
### 1. κΈ°λ₯κ°λ° in Programmers (Level 2)
<https://programmers.co.kr/learn/courses/30/lessons/42586>

#### π The point
- Code that is often used when using queue 
```java
while (!queue.isEmpty()) {
        int num = queue.poll();
        // blah blah blah
}
```
- Convert List<Integer> to int[] array
: listname.stream().mapToInt(x -> x).toArray();

#### π Answer
```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.List;
import java.util.ArrayList;

class Solution {
    
    public int[] solution(int[] progresses, int[] speeds) {

        List<Integer> answer = new ArrayList<>();
        
        // 1. make a queue which has the days of each progresses
        Queue<Integer> queue = new LinkedList<>();
        int n = progresses.length;
        
        for (int i = 0; i < n; i++) {
            int day = 0;
            while (progresses[i] + speeds[i] * day < 100) day++;
            queue.add(day);
        }
       
        // 2. find the release day
        // case1 : day1 < day2
        // case2 : day1 >= day2
        int day1 = queue.poll();
        int day2 = 0;
        int count = 1;

        while (!queue.isEmpty()) {
            day2 = queue.poll();
            if (day1 >= day2) count++;
            else {
                answer.add(count);
                count = 1; // initialization
                day1 = day2; // switch
            }
        }
        answer.add(count); // important
        
        return answer.stream().mapToInt(x -> x).toArray();
    }
}
// [condition]
// 1. λ°°ν¬ μ μμ μ§λ : progresses (<=100) (value : 1~99)
// 2. μμλ³ 'κ°λ° μλ' : speeds (<=100) (value : 1~100)
// 3. λ°°ν¬λ νλ£¨μ ν λ²λ§, λ§€μΌ νλ£¨ λμ
// return κ° λ°°ν¬λ§λ€ λͺ κ°μ κΈ°λ₯μ΄ λ°°ν¬?
    
// [Logic]
// κ°μ₯ μμ μλ κΈ°λ₯μ΄ κ°λ° μλ£λ  λ, μ΄λ―Έ κ°λ° μλ£ λ λ€μ μλ κΈ°λ₯μ΄ κ°μ΄ λ°°ν¬λκ³  out -> λ€μ κΈ°λ₯λ€μ΄ μ¬μ λ ¬λ¨ -> λ°λ³΅
//    ---> Use LinkedList (Queue : FIFO)

// dynamic programming
// 1. λͺ¨λ  κΈ°λ₯μ΄ κ°λ° μλ£λλ λ μ§ κ΅¬νκΈ°
// -> κ°λ° μλ£λλ λ μ§λ₯Ό linkedlistμ μ μ₯νκΈ° ok
// 2. day1 < day2 λΌλ©΄, answer.add(count), queueμμ poll()
//      μλλΌλ©΄, (day1 >= day2)
// 3. day1 < day2κ° λ λκΉμ§ count++, queueμμ poll()
// 4. answer.add(count)
// 5. μλ‘ λ§λ€μ΄μ§ queueλ‘ λ€μ 1, 2, 3μ λ°λ³΅

// [Test case]
// 7 3, 9 -> [2, 1]
// 5, 10 1 1, 20 1 -> [1, 3, 2]
// 5, 10 1 1 1, 20 -> [1, 4, 1]
// 5, 10 1 1, 3, 5 -> [1, 3, 1, 1]

/**
System.out.println("day1 : " + day1);
System.out.println("day2 : " + day2);
System.out.println("in loop : " + queue);
System.out.println("count : " + count);
System.out.println("answer : " + answer);
System.out.println();
**/
```

---
## Important words
- natural number : μμ°μ (1~)
- positive integer : μμ μ μ
- negative integer : μμ μ μ

---
Solving problem by using queue is quite fun π
