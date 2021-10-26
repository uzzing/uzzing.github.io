---
title:  "[Algorithm] Generate Parentheses"
date: 2021-10-26 8:20PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-26 8:20PM
---
# 'Generate Parentheses' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/generate-parentheses/>

---

## 📌 Insight
|Recursion|Backtracking|DFS|
|:---|:---|:---|
|In recursion, **the function calls itself** until it reaches a base case.|In backtracking, we **use recursion to explore all the possibilities** until we get the best result for the problem.||
|| - Backtracking is a **more general algorithm** that doesn't necessarily even relate to trees. <br> <br>- Backtracking is usually **implemented as DFS** plus search pruning (backtracking is **the general form of DFS.**) <br><br> - If we extend DFS to general problems, we can call it backtracking. | - DFS is **the special form of backtracking** <br><br> - If we use backtracking to tree/graph related problems, we can call it DFS.

The source : <https://stackoverflow.com/questions/1294720/whats-the-difference-between-backtracking-and-depth-first-search>

---

## 📌 Answer
### 1. Use DFS
The time and space complexity is very nice.

<img width="482" alt="Screen Shot 2021-10-26 at 7 54 24 PM" src="https://user-images.githubusercontent.com/83699657/138864649-57e71f74-a6f0-474e-a0cc-0b24a4a06f79.png">


[Result](https://leetcode.com/submissions/detail/577447127/)

```java
class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> output = new ArrayList<>();
        dfs(n, "", output, n, n);
        return output;
    }
    
    public void dfs(int n, String cur, List output, int left, int right) {
        if (left > right) return;
        
        if (left == 0 && right == 0) {
            output.add(cur);
            return;
        }
        
        if (left > 0)
            dfs(n, cur + "(", output, left - 1, right);
        
        
        if (right > 0)
            dfs(n, cur + ")", output, left, right - 1);
    }
}
```
The source : <https://leetcode.com/problems/generate-parentheses/discuss/248359/Extremely-simple-Java-DFS-(beats-100)>

---

### 2. Use Backtracking
`Backtracking is usually implemented as DFS plus search pruning.`

#### The point

The time and space complexity is bad....

<img width="457" alt="Screen Shot 2021-10-26 at 7 53 35 PM" src="https://user-images.githubusercontent.com/83699657/138866396-f2dd12c8-c658-4aa0-b675-9752cae0ab58.png">


[Result](https://leetcode.com/submissions/detail/577446930/)

```java
import java.util.List;
import java.util.ArrayList;

class Solution {
    public List<String> generateParenthesis(int n) {
        List<String> list = new ArrayList<>();
        backtrack(list, "", 0, 0, n);
        return list;
    }
    
    private void backtrack(List<String> list, String s, int open, int close, int n) {
        
        System.out.println(s);
        
        // end backtracking
        if (s.length() == n * 2) {
            list.add(s);
            return;
        }
        
        if (open < n) {
            System.out.println("open < max");
            backtrack(list, s + "(", open + 1, close, n);
        }
        
        if (close < open) {
            System.out.println("close < open");
            backtrack(list, s + ")", open, close + 1, n);
        }
    }
    
}
```
The source : <https://leetcode.com/problems/generate-parentheses/discuss/10100/Easy-to-understand-Java-backtracking-solution>

---

## 📌 Words
- Parentheses : 괄호
- discard : ~를 버리다
- constraints : 제약
- interpret : 해석하다
- prefix : 접두사
- concatenation : 연속
- traverse : 가로지르다
- extend : 확장하다
- search pruning : 검색 가지치기 🍆

---

But I think two codes are not so different....?
Let's know step by step 🐤