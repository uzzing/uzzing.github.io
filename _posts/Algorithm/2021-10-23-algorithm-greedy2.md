---
title:  "[Algorithm] Greedy2"
date: 2021-10-23 2:20PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-23 2:20PM
---
# Greedy algorithm
---

# Task
# 2. ๊ตฌ๋ช๋ณดํธ in Programmers (Level 2)
## ๐ Problem
<https://programmers.co.kr/learn/courses/30/lessons/42885>

## ๐ The point
- Use the greedy
    - Check the condition
    - Choose one from the below
        - Count the number of persons who can ride a boat
        - Count that person who will ride a boat alone

- Sort an array

## ๐ Answer
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] people, int limit) {
        int answer = 0;
    
        Arrays.sort(people);
        
        int min = 0; // the number of people who can ride a boat
    
        for (int max = people.length - 1; min <= max; max--) {
            if (people[min] + people[max] <= limit) min++;
            
            answer++; // ride a boat alone
            
            // System.out.println("min : " + min);
            // System.out.println("max : " + max);
            // System.out.println("answer : " + answer);
            // System.out.println();
        }
        
        return answer;
    }
}
/**
[Condition]
- ์ต๋ 2๋ช์ฉ
- ๊ตฌ๋ช๋ณดํธ๋ฅผ ์ต๋ํ ์ ๊ฒ ์ฌ์ฉ, ๋ชจ๋  ์ฌ๋์ ๊ตฌ์ถ

[Test case]
-[70kg, 50kg, 80kg, 50kg], limit : 100kg

[Logic]
- greedy algorithm
**/
```
The source : <https://velog.io/@ajufresh/ํ๋ก๊ทธ๋๋จธ์ค-๊ตฌ๋ช๋ณดํธ-๋ฌธ์ ํ์ด-Java>

I can't come up with good greedy algorithm which can be the best choice at each moment when I solve the problem yet....