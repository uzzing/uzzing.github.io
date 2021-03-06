---
title:  "[Algorithm] Sort2"
date: 2021-10-24 11:50AM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-24 11:50PM
---
# Sort
---

# Task
# 2. H-Index in Programmers (Level 2)
---
## ð Problem
<https://programmers.co.kr/learn/courses/30/lessons/42747>

## ð Answer
###  1. Use Arrays.sort()

```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        int answer = 0;

        Arrays.sort(citations);
        
        for (int i = 0; i < citations.length; i++) {
            int h = citations.length - i; // from last
            
            if (citations[i] >= h) {
                answer = h;
                break;
            }
        }
   
        return answer;
    }
}
/**
[Question]
- ë¼ë¬¸ ní¸ (1 <= n <= 1000)
    -> hë² ì´ì ì¸ì©ë ë¼ë¬¸ = hí¸ ì´ì : h <= n (0 <= h <= 10000)
    -> ëë¨¸ì§ ë¼ë¬¸(hë² ì´í ì¸ì©) : n - h
    -> H-Index : hì ìµëê°
- citations : ë¼ë¬¸ì ì¸ì© íì
- return H-Index
```
The source : <https://ju-nam2.tistory.com/74>

### 2. Use Binary Search
But this way takes **longer** than `1. Use Arrays.sort()`
```java
import java.util.Arrays;

class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        
        Arrays.sort(citations);
        int len = citations.length;
        int h = 0;
        int low = 0;
        int high = len - 1;
        
        while (low <= high) {
            int mid = (low + high) / 2;
            h = len - mid;
            
            if (citations[mid] >= h) {
                if (mid == 0) {
                    answer = h;
                    break;
                }
                
                if (mid != 0 && citations[mid - 1] <= h) {
                    answer = h;      // update
                    high = mid - 1;  // move to the left
                }
                else high = mid - 1;  // move to the left
            }
            else low = mid + 1; // move to the right
        } 
        
        return answer;
    }
}
```
The source : <https://leetcode.com/problems/h-index-ii/discuss/1325353/java-binary-search-solution-ologn-time-o1-space>

---
Actually, I came up with all of two ways. But, I couldn't apply those....
I have to learn more examples and get used to it.

I ate Chueotang in the morning, but it tasted not good compared to the other restaurant I often go hh.
I'm gonna solve two more problems and go to bakery to buy sandwichs consisted of a half of basil chicken sandwich and a half of sweet pumpkin sandwich!
It sounds like nnyami ð
