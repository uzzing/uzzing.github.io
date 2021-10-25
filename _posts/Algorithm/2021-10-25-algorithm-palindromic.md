---
title:  "[Algorithm] Longest Palindromic Substring"
date: 2021-10-25 6:49PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Leetcode]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-25 6:49PM

---

# 'Longest Palindromic Substrings' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/longest-palindromic-substring/>

## 📌 Answer

### 1. Simple answer
#### The point

- **`for ( ; 0 <= i && j < s.length(); i--, j++) {}`**
    - This expression can check all datas from start to end

[Result](https://leetcode.com/submissions/detail/576871410/)

```java
class Solution {
    public String longestPalindrome(String s) {
        
        String max = "";
        
        for (int i = 0; i < s.length(); i++) {
            
            String s1 = extend(s, i, i); // 0 0
            String s2 = extend(s, i, i + 1); // 0 1
            
            if (s1.length() > max.length()) max = s1; // s1 = b
            if (s2.length() > max.length()) max = s2; // 
        }
        
        return max;
    }
    
    private String extend(String s, int i, int j) {
        
        for ( ; 0 <= i && j < s.length(); i--, j++) // core idea : i--, j++
            if (s.charAt(i) != s.charAt(j)) break;
        
        return s.substring(i + 1, j); // i : -1, j : 1
    }
}
/**
[Question]
- s consist of only digits and English letters.
- return the longest palindromic substring in s.
    - palindromic? ex. abba, samsung
- 
**/
```

The source : <https://leetcode.com/problems/longest-palindromic-substring/discuss/2928/Very-simple-clean-java-solution>



### 2. Use Dynamic programming

#### The point

- **`boolean[][] dp = new boolean[len][len];`**
    - the way to **record the datas** which are already checked in Dynamic programming <br> (⭐️⭐️⭐️ Don't forget **purpose** of dp)

But...this way is quite slow and less efficient

[Result](https://leetcode.com/submissions/detail/576871655/)

```java
public class Solution {
    public String longestPalindrome(String s) {
        
        if (s == null || s.length() == 0)
            return "";
        
        int len = s.length();
        boolean[][] dp = new boolean[len][len]; // dp
        int start = 0;
        int end = 0;
        int max = 0;

        for (int i = 0; i < s.length(); i++) {
            for (int j = 0; j <= i; j++) { // important : j <= i

                // i - j : length of substring
                if (s.charAt(i) == s.charAt(j) && (i - j <= 2 || dp[j + 1][i - 1]))
                    dp[j][i] = true; // the way of dp
                                   
                
                if (dp[j][i] && max < i - j + 1) {
                    max = i - j + 1; // i - j + 1 : length of substring
                    start = j;
                    end = i;
                }
            }
        }

        return s.substring(start, end + 1);
    }
}
```
The source : <https://leetcode.com/problems/longest-palindromic-substring/discuss/2987/Clean-Java-solution-using-DP-yet-the-time-complexity-is-O(N2)>

---

Let's use debugger! <br>
And let's eat dinner 🍱