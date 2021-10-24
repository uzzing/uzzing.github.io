---
title:  "[Algorithm] Hash2"
date: 2021-10-24 5:36 PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-24 5:36 PM
---
# Hash
`HashMap<Key, Value>`

---

# Task
# 2. 위장 in Programmers (Level 2)
---
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42578>

## 📌 The point
- Use **number of cases**
    - ex. If {hat=3, shirt=2, pants=1}, 
        it must be calculated like `(3*2*1) + (3*2) + (3*1) + (1*2) + 3 + 2 + 1`
        If the formula, it's **`(n + 1) * (m + 1) * (o + 1) - 1`** (⭐️⭐️⭐️ Do remember)

- Use **HashMap**

    - HashMap.containsKey(String)
    - HashMap.put(key, value)
    - **HashMap.get(key)**
    - **HashMap.keySet()** : iterator of keys


## 📌 Answer
```java
import java.util.HashMap;

class Solution {
    public int solution(String[][] clothes) {
        
        // for multiplication
        int answer = 1;
        
        // save <type, count>
        HashMap<String, Integer> map = new HashMap<>();
        
        for (int i = 0; i < clothes.length; i++) {
            String type = clothes[i][1];
            if (!map.containsKey(type)) 
                map.put(type, 1);
            else 
                map.put(type, map.get(type) + 1);
        }
        // result : ex. {eyewear=1, headgear=2}
        
        // calculate number of cases
        // ex. (eyewear1 + 1) * (headgear2 + 1) - 1 = 5
        for (String keys : map.keySet())
            answer *= (map.get(keys) + 1);
        answer -= 1;
        
        return answer;
    }
}
/**
[Condition]
- 매일 다른 옷을 조합 
- clothes[i] : ["name", "type"]
- clothes.length : 1 ~ 30
- clothes.[i].length : 1 ~ 20
- 하루에 최소 한 개의 의상
- return 서로 다른 옷의 조합의 수
**/
```

The source : <https://sas-study.tistory.com/215>

---
## 📌 Words
- number of cases : 경우의 수
- formula : 公式　공식 
- factor : 因数　인수
- factorize : 因数分解 인수분해
- multiplication : 곱셈
- plus / minus / time / divided by : + / - / * / /

--- 
Why I almost forgot math I learned when I was in high school? lol
Of course it also is needed knowledge of the basic math in coding test.
But it's so interesting and funny because I like math and can feel I go back to young moment 🤭
I'll be the genious of math!!! Keep doing hard!