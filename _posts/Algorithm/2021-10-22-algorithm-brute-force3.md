---
title:  "[Algorithm] Brute-force Search 3"
date: 2021-10-22 5:16PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-22 5:16PM
---
# Brute-force Search
---

# Task
[Previous task1](https://uzzing.github.io/posts/algorithm-brute-force/)<br>
[Previous task2](https://uzzing.github.io/posts/algorithm-brute-force2/)


## 3. 카펫 in Programmers (Level 2)
### 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42842>

### 📌 The point
Used recursion

### 📌 Answer
```java
class Solution {

    public int[] solution(int brown, int yellow) {
        int[] answer = new int[2];
        
        int sum = brown + yellow; // 12
        int hori, verti = 0;
        
        // find the possibility of hori and verti
        // condition : hori >= verti -> so i--
        for (int i = sum / 2; i > 2; i--) {
            if (sum % i == 0) {
                hori = i;
                if (check(hori, brown, yellow)) {
                    answer[0] = hori;
                    answer[1] = sum / hori;
                    break;
                }
            }
        }
        return answer;
    }
    
    private boolean check(int hori, int brown, int yellow) {
        int y_hori = hori - 2;
        
        if (yellow % y_hori != 0) return false;
        
        return true;
    }
}
/**
[Question]
return { horizontal length, vertical length }

[Condition]
- 8 <= brown <= 5000
- 1 <= yellow <= 2,000,000
- horizontal length >= vertical length

[Algorithm]
- Brute-force search : dfs (recursion)

[Logic]
- the goal : get hori, verti
- it's okay only know one variable, hori or verti
- brown must be 2 * hori + (verti - 2)
- yello must be hori - 2
**/
```
