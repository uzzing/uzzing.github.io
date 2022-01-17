---
title:  "[AWS Solution Architect] VPC Flow logs"
date: 2022-1-17 4:23PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-17 4:23PM
---

## VPC Flow logs 

`Instruction`
<https://uzzing.github.io/posts/VPC-Flow-Logs/>

- Flow logs will track all the traffic that is going through your VPC

- Create flow log
    - we can have it to accept, reject or all. 
    <img width="925" alt="Screen Shot 2022-01-17 at 4 08 19 PM" src="https://user-images.githubusercontent.com/83699657/149723298-cabbe743-2854-47b1-9c2c-da4115924d5a.png">

    - it can either be delivered to cloudwatch logs or s3
        - cloud watch is very good destination for that.
    
    - in order to deliver that, we're going to need a destination log group.
        - go to `cloudwatch` and create a new cloudwatch log
        <img width="748" alt="Screen Shot 2022-01-17 at 4 11 02 PM" src="https://user-images.githubusercontent.com/83699657/149723626-f00edb1d-7497-4eca-a4a7-15f9a0467587.png">
        <img width="909" alt="Screen Shot 2022-01-17 at 4 16 57 PM" src="https://user-images.githubusercontent.com/83699657/149724369-2af6605a-4ed6-4596-82d1-4c522dd8d46c.png">
        
    <img width="690" alt="Screen Shot 2022-01-17 at 4 09 37 PM" src="https://user-images.githubusercontent.com/83699657/149723440-b88fa0d4-d785-4515-8e98-da22b0648858.png">
    <img width="665" alt="Screen Shot 2022-01-17 at 4 17 27 PM" src="https://user-images.githubusercontent.com/83699657/149724429-51132f16-eaa3-4358-b74c-0288324685d8.png">

    - we need a IAM role to publish to cloud watch logs.


- under our VPC, we can see that we have flow logs enabled, we had just created that a log there 

- just took public instances's IP addresses and test enter enter enter
<img width="940" alt="Screen Shot 2022-01-17 at 4 20 44 PM" src="https://user-images.githubusercontent.com/83699657/149724903-eeec57be-28d3-4e70-8688-ce8efb9c44b4.png">
<img width="943" alt="Screen Shot 2022-01-17 at 4 21 39 PM" src="https://user-images.githubusercontent.com/83699657/149725023-704ab4f8-1907-486e-916a-9b40f32c2694.png">
    - source, destination

--- 

?????

The copyright of all material here is on this video
<https://www.youtube.com/watch?v=Ia-UEYYR44s>

<br>
This post is just for studying AWS SAA.