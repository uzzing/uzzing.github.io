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
### 1. 기능개발 in Programmers (Level 2)
<https://programmers.co.kr/learn/courses/30/lessons/42586>

#### 📌 The point
- Code that is often used when using queue 
```java
while (!queue.isEmpty()) {
        int num = queue.poll();
        // blah blah blah
}
```
- Convert List<Integer> to int[] array
: listname.stream().mapToInt(x -> x).toArray();

#### 📌 Answer
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
// 1. 배포 순 작업 진도 : progresses (<=100) (value : 1~99)
// 2. 작업별 '개발 속도' : speeds (<=100) (value : 1~100)
// 3. 배포는 하루에 한 번만, 매일 하루 끝에
// return 각 배포마다 몇 개의 기능이 배포?
    
// [Logic]
// 가장 앞에 있는 기능이 개발 완료될 때, 이미 개발 완료 된 뒤에 있는 기능이 같이 배포되고 out -> 뒤의 기능들이 재정렬됨 -> 반복
//    ---> Use LinkedList (Queue : FIFO)

// dynamic programming
// 1. 모든 기능이 개발 완료되는 날짜 구하기
// -> 개발 완료되는 날짜를 linkedlist에 저장하기 ok
// 2. day1 < day2 라면, answer.add(count), queue에서 poll()
//      아니라면, (day1 >= day2)
// 3. day1 < day2가 될때까지 count++, queue에서 poll()
// 4. answer.add(count)
// 5. 새로 만들어진 queue로 다시 1, 2, 3을 반복

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
- natural number : 자연수 (1~)
- positive integer : 양의 정수
- negative integer : 음의 정수

---
Solving problem by using queue is quite fun 😆
