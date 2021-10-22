---
title:  "[Algorithm] Brute-force Search 2"
date: 2021-10-22 4:23PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-22 4:23PM
---
# Brute-force Search
---

# Task
[Previous task](https://uzzing.github.io/posts/algorithm-brute-force/)

## 2. 소수 찾기 in Programmers (Level 2)
### 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42839>

### 📌 The point
Use backtracking (dfs -> recursion)

### 📌 Answer

```java
// backtracking -> use recursion
import java.util.List;
import java.util.ArrayList;

class Solution {

    private boolean[] checked;
    private List<Integer> nums;
    
    public int solution(String numbers) {
        int answer = 0;
        
        nums = new ArrayList<>();
        checked = new boolean[numbers.length()]; // string.length()
        
        for (int i = 1; i <= numbers.length(); i++)
            dfs(numbers, i, ""); // 자리수 증가시키기

        for (int i = 0; i < nums.size(); i++)
            if (isPrimeNum(nums.get(i))) answer++;

        return answer;
    }
    
    private void dfs(String numbers, int len, String tmp) {
        if (tmp.length() == len) {
            int n = Integer.parseInt(tmp);
            if (!nums.contains(n)) nums.add(n);
            return;
        }
        
        for (int i = 0; i < numbers.length(); i++) {
            if (!checked[i]) {
                tmp += numbers.charAt(i);
                checked[i] = true;
                dfs(numbers, len, tmp);
                tmp = tmp.substring(0, tmp.length() - 1);
                checked[i] = false;
            }
        } 
    }

    private boolean isPrimeNum(int n) {
        
        // case1. 0 or 1
        if (n == 0 || n == 1) return false;
        
        // case2. it can be divided with other number
        for (int i = 2; i < n; i++) 
            if (n % i == 0) return false;
        
        return true;
    }
}
/**
[Question]
- make primary number by using numbers(string) 
** what is primary number?
    : the number can be only divided with 1 and itself.

[Condition]
- numbers : length = 1 ~ 7 (value = 0 ~ 9)
**/
```
The source : <https://blog.naver.com/PostView.naver?blogId=seop1284&logNo=222450982972&parentCategoryNo=&categoryNo=9&viewDate=&isShowPopularPosts=true&from=search>

---

It's quite difficult!
Let's resolve it afterwards.