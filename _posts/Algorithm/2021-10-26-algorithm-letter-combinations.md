---
title:  "[Algorithm] Letter Combinations of a Phone Number"
date: 2021-10-26 9:37AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm]
tags: [algorithm, java, eng, leetcode]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-26 9:37AM
---
# 'Letter Combinations of a Phone Number' in LeetCode (Medium)
---
## 📌 Problem
<https://leetcode.com/problems/letter-combinations-of-a-phone-number/>

## 📌 Answer
### 1. Backtracking
#### The point
- recursion `void backtrack()`
- for (char letter : dict[digit].**toCharArray()**)


The time and space complexity is so nice!

<img width="458" alt="Screen Shot 2021-10-26 at 9 34 07 AM" src="https://user-images.githubusercontent.com/83699657/138789135-cb16d4fe-bbf5-46b5-9739-1e12320ffd1c.png">

[Result](https://leetcode.com/submissions/detail/577201287/)

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        
        List<String> list = new ArrayList<>();
        
        if (digits.length() == 0) return list;
        
        String[] dict = new String[] {"", "", "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz" };
        
        backtrack(list, digits.toCharArray(), "", dict);
        
        return list;
    }
    
    public void backtrack(List<String> list, char[] digits, String s, String[] dict) {
        
        if (s.length() == digits.length) { 
            list.add(s); 
            return; 
        }
        
        int i = s.length();
        int digit = digits[i] - '0';
        
        for (char letter : dict[digit].toCharArray())
            backtrack(list, digits, s + Character.toString(letter), dict);
    }
}
```
The source : <https://leetcode.com/problems/letter-combinations-of-a-phone-number/discuss/402087/Backtracking-Java-Solution-(100-runtime-98-memory)>

### 2. Simple answer
#### The point
- `int num = digits.charAt(i) - '0';`
    - convert char to int


The time and space complexity is slower than backtracking.

<img width="444" alt="Screen Shot 2021-10-26 at 9 27 18 AM" src="https://user-images.githubusercontent.com/83699657/138788837-69957863-1705-44b4-b8c9-6e13e42eb88d.png">

[Result](https://leetcode.com/submissions/detail/577198701/)

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        String digitletter[] = {"","","abc","def","ghi","jkl","mno","pqrs","tuv","wxyz"};
        List<String> result = new ArrayList<String>();
    
        if (digits.length() == 0) return result;
            
        result.add("");
        
        for (int i = 0; i < digits.length(); i++) {
            int num = digits.charAt(i) - '0';
            result = combine(digitletter[num], result);
        }
            
        return result;
    }
        
    public List<String> combine(String digit, List<String> l) {
        
        List<String> result = new ArrayList<String>();
            
        for (int i = 0; i< digit.length(); i++) 
            for (String x : l) 
                result.add(x + digit.charAt(i));
    
        return result;
    }
}
```
The source : <https://leetcode.com/problems/letter-combinations-of-a-phone-number/discuss/8118/Easy-understand-Java-Solution>


###  3. Without using input specific datas
- I defined a function for this pattern : String getLetters()

<img width="210" alt="Screen Shot 2021-10-26 at 9 12 30 AM" src="https://user-images.githubusercontent.com/83699657/138787529-652e0948-7ad6-415b-8345-7c049481f93e.png">

Let's check.

```java
import java.util.List;
import java.util.ArrayList;
import java.util.Collections;

class Solution {
    public List<String> letterCombinations(String digits) {
        
        if (digits.length() == 0) return Collections.emptyList();
        
        List<String> list = new ArrayList<>();
        
        // condition : 0 <= digits.length <= 4
        String[] arr = new String[4];
        
        for (int i = 0; i < digits.length(); i++) {
            int num = digits.charAt(i) - '0'; // char to int

            int count = 3; // default
            if (num == 7 || num == 9) count = 4;
            
            arr[i] = getLetters(num, count);
        }

        // combine datas of arr
        // I've not declared yet
        
        return list;
    }
    
    private String getLetters(int num, int count) {

        String letters = "";
        int start = 3 * (num - 2);
        int end = start + count;
        
        for (int i = start; i < end; i++)
            letters += String.valueOf((char) ('a' + i));
        
        return letters;
    }
}
/**
[Question]
- Return the answer in any order.
- condition
    - 1 does not map to any letters.
    - 0 <= digits.length <= 4
**/
```

---

## 📌 Word
|Declaration|Definition|
|:---:|:---:|
|You are declaring that **something exists**, such as a class, function or variable. <br> You don't say anything about what that class or function looks like, you just say that it exists.|You define **how something is implemented**, such as a class, function or variable, i.e. <br> you say what it actually is.|

The source : <https://stackoverflow.com/questions/11715485/what-is-the-difference-between-declaration-and-definition-in-java>