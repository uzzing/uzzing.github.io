---
title:  "[Algorithm] Stack"
date: 2021-10-21 9:6PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-21 9:6PM
---
# Stack
[Explain](https://uzzing.github.io/posts/stack-queue/)

---

## Task
#### π Previous task 
[Queue task 1](https://uzzing.github.io/posts/algorithm-queue/)
[Queue task 2](https://uzzing.github.io/posts/algorithm-queue2/)
[Queue task 3](https://uzzing.github.io/posts/algorithm-queue3/)


### 1. μ£Όμκ°κ²© in Programmers (Level 2)
#### π Problem 
<https://programmers.co.kr/learn/courses/30/lessons/42584> 
#### π The point
- Used **custom class**
- Used **stack** efficiently

#### π Answer
```java
import java.util.Stack;

class Solution {
    
    private class Price {
        int index;
        int price;
        
        public Price(int index, int price) {
            this.index = index;
            this.price = price;
        }
    }
    
    private Stack<Price> stack;
    
    public int[] solution(int[] prices) {
        
        int[] answer = new int[prices.length];
        stack = new Stack<>(); // Object 'Price' 1 ~ (i - 1)
        
        
        for (int i = 0; i < prices.length; i++) {
            
            int currentPrice = prices[i];
            
            while (!stack.isEmpty()) {
                Price top = stack.peek(); // get only data
                if (top.price > currentPrice) {
                    answer[top.index] = i - top.index;
                    stack.pop(); // delete top data
                }
                else break; // do nothing
            }
            
            stack.push(new Price(i, currentPrice)); // add data
        }
        
        while (!stack.isEmpty()) {
            Price top = stack.pop(); // get top data and remove it
            answer[top.index] = prices.length - 1 - top.index; // '-1' is important that it catch the condition the last object's price is not down
        }
        
        return answer;
    }
}
/**
[Question]
- prices : μ£Όμκ°κ²© (μ΄ λ¨μ) -> values: 1 ~ 10,000, length: 2 ~ 100,000
- return κ°κ²©μ΄ λ¨μ΄μ§μ§ μμ κΈ°κ°μ λͺ μ΄?
**/
```
The source : <https://hongjw1938.tistory.com/10>

---
It is first time to solve a problem by using stack algorithm, so it was quite difficult...

I think I know how to use queue well, but I didn't get used to stack.

Don't forget a quote **`From zero to hero`**
You can do it.