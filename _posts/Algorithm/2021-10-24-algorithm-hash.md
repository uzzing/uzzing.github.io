---
title:  "[Algorithm] Hash"
date: 2021-10-24 1:58PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-24 1:58PM
---
# Hash

`HashMap(Key, Value)`

---

# Task
# 전화번호 목록 in Programmers (Level 2)
---
## 📌 Problem
<https://programmers.co.kr/learn/courses/30/lessons/42577>

## 📌 Answer
### 1. Use HashMap
#### The point
- HashMap.containsKey(String)
- String.substring(start, end);
- Check the splited number is in map
- HashMap is super quick lol
    so, if hashmap, multi for loop was also okay...

<img width="682" alt="Screen Shot 2021-10-24 at 1 47 21 PM" src="https://user-images.githubusercontent.com/83699657/138581422-f9a0499f-14cf-4b19-b09b-38e8a9efafdb.png">


```java
import java.util.HashMap;

class Solution {
    public boolean solution(String[] phone_book) {
        
        // put datas of phone_book to HashMap
        // Q : why number is key?
        // A : because we're gonna use 'HashMap.containsKey(String)''
        HashMap<String, Integer> map = new HashMap<>();
        for (int i = 0; i < phone_book.length; i++)
            map.put(phone_book[i], i);
        
        // check there are num in the map
        for (String num : phone_book) {
            for (int i = 1; i < num.length(); i++) {
                if (map.containsKey(num.substring(0, i)))
                    return false;
            }
        }
        
        return true;
    }
}
```

The source : <https://coding-grandpa.tistory.com/entry/프로그래머스-전화번호-목록-해시-Lv-2-자바-Java>

### 2. Use Arrays.sort()
#### The point 
- Arrays.sort(String[]) 
    ```
    ex. before sorting 
        { "99", "7894", "123", "123456", "789" }
        after sorting
        { "123", "123456", "789", "7894", "99"}
    ```

- String.startsWith(String)
- But it was slower than HashMap

<img width="679" alt="Screen Shot 2021-10-24 at 1 56 56 PM" src="https://user-images.githubusercontent.com/83699657/138581411-ecac3f8c-b7ac-4fe7-97ca-deec698701ac.png">


```java
import java.util.Arrays;

class Solution {
    public boolean solution(String[] phone_book) {

        Arrays.sort(phone_book);

        // you only need to compare the current number and the next number
        // because Arrays.sort();
        for (int i = 0; i < phone_book.length - 1; i++) 
            if (phone_book[i + 1].startsWith(phone_book[i])) return false;
        
        return true;
    }
}
```
The source : <https://sso-feeling.tistory.com/318?category=922139>

---
## 📌 Words 
- 2 or more, more than 2: 以上
- 2 or less : 以下
- over 2, above 2, grater than 2 : 超過（ちょうか）
- under 2, below 2, less than 2 : 未満（みまん）

