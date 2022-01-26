---
title:  "[AWS Solution Architect] EC2 Pricing"
date: 2022-1-26 3:41PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-26 3:41PM
---

## EC2 Pricing

<img width="1440" alt="Screen Shot 2022-01-26 at 12 50 57 PM" src="https://user-images.githubusercontent.com/83699657/151112004-1fd0149e-ab35-4214-ad64-0cf28eca5712.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 12 51 15 PM" src="https://user-images.githubusercontent.com/83699657/151112016-83a086e7-373f-498f-a513-7bd15da21ef9.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 12 51 50 PM" src="https://user-images.githubusercontent.com/83699657/151112018-a5390f92-91a0-4d2b-92e0-68c6ad10b8e8.png">

- Discount
    : All Upfront > Partial Upfront > No Upfront

- All Upfront
: Pay full amount for the reservation term in one single payment

- Partial Upfront: Pay portion of amount for part of the reservation term in an upfront payment and pay the remaining in installments every month for the duration of the term. 

- No Upfront: Pay for the reservation in installments throughout the term’s duration every month. This payment offers the lowest savings rate.


<https://www.botmetric.com/blog/aws-ec2-reserved-instances-choosing-right-one-fits/>

<https://aws.amazon.com/ko/blogs/korea/simplified-reserved-instances/>


<img width="1440" alt="Screen Shot 2022-01-26 at 12 54 31 PM" src="https://user-images.githubusercontent.com/83699657/151112022-bb04c275-d44a-45cc-8105-9614e0f821fa.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 12 56 09 PM" src="https://user-images.githubusercontent.com/83699657/151112023-8201f09c-8d59-4d13-a6ca-7a47f93faf36.png">

<https://aws-diary.tistory.com/84>
<https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/dedicated-hosts-overview.html>

- An important difference between a Dedicated Host and a Dedicated instance
    - Dedicate Host
        - cost <b>a physical server(host) with EC2 instance capacity</b> fully dedicated to your use.
        - it gives you additional visibility and control over how instances are placed on a physical server, and you can consistently deploy your instances to the same physical server over time.
        -  인스턴스 실행을 전담하는 실제 호스트 비용을 지불하며, 기존의 소켓, 코어 또는 VM 소프트웨어별 라이선스를 가져와 비용을 절감합니다.

    - Dedicate Instance
        - 단일 테넌트 하드웨어에서 실행되는 인스턴스 비용을 시간 단위로 지불합니다


- <b>Support for multiple instance sizes on the same Dedicated Host</b> is available for the following instance families: T3, A1, C5, M5, R5, C5n, R5n, and M5n.
    - Other instance families support only <b>a single instance size on the same Dedicated Host.</b>


<img width="1440" alt="Screen Shot 2022-01-26 at 12 57 41 PM" src="https://user-images.githubusercontent.com/83699657/151112025-4441830a-8988-4c66-8867-e7ee380563cc.png">
<img width="1440" alt="Screen Shot 2022-01-26 at 12 59 34 PM" src="https://user-images.githubusercontent.com/83699657/151112030-e8841fc6-4dab-4446-88d0-c4c0b146f2da.png">

<https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html>

---


The copyright of all material here is on this video
<https://www.youtube.com/watch?v=Ia-UEYYR44s>

<br>
This post is just for studying AWS SAA.