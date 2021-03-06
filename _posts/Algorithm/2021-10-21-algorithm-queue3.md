---
title:  "[Algorithm] Queue3"
date: 2021-10-21 7:39PM
excerpt: "coding test"

author: Yuha
categories: [Development, Algorithm, Programmers]
tags: [algorithm, java, eng, programmers]

#toc: true
#toc_sticky: true
 
last_modified_at: 2021-10-21 7:39PM
---
# Queue
[Explain](https://uzzing.github.io/posts/stack-queue/)

---
## Task
[Previous task 1](https://uzzing.github.io/posts/algorithm-queue/)
[Previous task 2](https://uzzing.github.io/posts/algorithm-queue2/)

### π 3. λ€λ¦¬λ₯Ό μ§λλ νΈλ­ in Programmers (Level 2)
#### β­οΈ The point
- Used **while loop and break**

#### π Answer
```java
import java.util.Queue;
import java.util.LinkedList;
    
class Solution {
    
    private Queue<Integer> queue;
    
    public int solution(int bridge_length, int weight, int[] truck_weights) {
        
        int time = 0;
        int sumOfWeight = 0;
        queue = new LinkedList<>(); 
        
        for (int i = 0; i < truck_weights.length; i++) {
            int truck = truck_weights[i];
            
            while (true) {
                
                // case1. just add truck, don't need to consider sum of weights
                if (queue.isEmpty()) {
                    queue.add(truck);
                    sumOfWeight += truck;
                    time++;
                    break; // already added truck, so go out whlie loop
                }
                // case2. add truck and need to consider sum of weights
                else if (!queue.isEmpty() && queue.size() == bridge_length) {
                    int arrived = queue.poll();
                    sumOfWeight -= arrived;
                }
                // case3. 
                else if (!queue.isEmpty()) {
                    
                    // Let's consider sum of weights
                    // case2-1. 
                    if (sumOfWeight + truck > weight) {
                        queue.add(0); // add nothing
                        time++;
                    }
                    // case2-2.
                    else {
                        queue.add(truck);
                        sumOfWeight += truck;
                        time++;
                        break;
                    }
                }
            }
        }
        // have to + bridge_length because the remained trucks also must be arrived
        return time + bridge_length; // important 
    }
}

/**
[Question]
- νΈλ­ μ¬λ¬ λκ° μ ν΄μ§ μμΌλ‘ κ±΄λ
- return λͺ¨λ  νΈλ­μ΄ λ€λ¦¬λ₯Ό 'μμλλ‘ μ΅λ¨ μκ° μμ' κ±΄λλ €λ©΄ μ΅μ λͺ μ΄?

[Condition]
- λ€λ¦¬
    - νΈλ­μ΄ μ΅λ bridge_lengthλ μ¬λΌκ° μ μμΌλ©°
    - weight μ΄νκΉμ§μ λ¬΄κ²λ₯Ό κ²¬λ μ μμ΅λλ€
    - λ¨, λ€λ¦¬μ μμ ν μ€λ₯΄μ§ μμ νΈλ­μ λ¬΄κ²λ λ¬΄μ
    
- bridge_length, weight, truck_weights : 1 ~ 10,000

[Example]
- νΈλ­ 2λ + λ¬΄κ² μ΄ ν© 10kgκΉμ§
- νΈλ­ [7, 4, 5, 6]
-> μ΅μ 8μ΄
**/
```
---
Let's keep it simple always.