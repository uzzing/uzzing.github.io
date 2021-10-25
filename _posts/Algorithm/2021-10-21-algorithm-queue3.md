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

### 📌 3. 다리를 지나는 트럭 in Programmers (Level 2)
#### ⭐️ The point
- Used **while loop and break**

#### 📌 Answer
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
- 트럭 여러 대가 정해진 순으로 건넘
- return 모든 트럭이 다리를 '순서대로 최단 시간 안에' 건너려면 최소 몇 초?

[Condition]
- 다리
    - 트럭이 최대 bridge_length대 올라갈 수 있으며
    - weight 이하까지의 무게를 견딜 수 있습니다
    - 단, 다리에 완전히 오르지 않은 트럭의 무게는 무시
    
- bridge_length, weight, truck_weights : 1 ~ 10,000

[Example]
- 트럭 2대 + 무게 총 합 10kg까지
- 트럭 [7, 4, 5, 6]
-> 최소 8초
**/
```
---
Let's keep it simple always.