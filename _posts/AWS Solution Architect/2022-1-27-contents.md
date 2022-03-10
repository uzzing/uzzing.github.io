---
title:  "[AWS Solution Architect] Contents & I finally got pass! "
date: 2022-1-27 3:00PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-2-10 1:10PM
---

## Certification
<img width="800" alt="3" src="https://user-images.githubusercontent.com/83699657/157660120-e17ad887-09fc-4f9b-9a74-759b2e170b76.png">

<img width="530" alt="1" src="https://user-images.githubusercontent.com/83699657/157660182-b2b6fc7b-eb4b-487e-b11a-fee449e44b67.png">
<img width="530" alt="2" src="https://user-images.githubusercontent.com/83699657/157660184-f6d94794-319b-44f9-8bac-0bd74059cfee.png">


- Study period 
    : 2022.01.10 ~ 2022.02.09 (30days)

---

## Content Outline
<img width="879" alt="Screen Shot 2022-01-24 at 1 37 32 PM" src="https://user-images.githubusercontent.com/83699657/151293518-c0afd9ca-0686-4c13-83ae-08d4460e5432.png">

- Module1 
    : Design <b>Resilient</b> Architectures (30%)
    <img width="878" alt="Screen Shot 2022-01-24 at 1 50 16 PM" src="https://user-images.githubusercontent.com/83699657/151293527-d765e186-9af7-4c89-b29e-9e78830c55bb.png">
    <img width="880" alt="Screen Shot 2022-01-24 at 2 27 49 PM" src="https://user-images.githubusercontent.com/83699657/151688429-d3710c4c-c853-4d54-a5b5-a7b7e3c5a656.png">

    - single AZ : not for scalability, availability 
    - managing service : for redundancy, availability in region
    - 내결함성 : 성능상의 요구조건을 충족시키지 못한 것
        - ex. 어떤 서비스가 반드시 성능을 만족시키기 위해 4대가 동작해야함. 하지만 2개의 AZ에 instance가 2개씩 있음. <b>1개의 AZ가 다운 되더라도 나머지 AZ는 돌아감. -> 내구성 O</b> 
        - 고가용성 O, but <b>내결함성은 X</b> (결함 발생한 거라서)
            - 가용성 : 시스템의 내구성을 측정하는 방법
    - ex. 2 AZ에 각각 4개의 instance가 있음. -> 고가용성 O, 내결함성 O
    - 모든 구성요소에서 장애가 발생할 수 있음
        - 자동으로 복구되거나
        - multi machine이 동작할 수 있도록 분산해서 처리하도록 설계하는 것이 중요


- Module2 
    : Define <b>Performant</b> Architectures (28%)
    <img width="876" alt="Screen Shot 2022-01-24 at 2 41 47 PM" src="https://user-images.githubusercontent.com/83699657/151293563-99aba429-9545-44c6-9120-8973dcd9eda8.png">
- Module3 
    : Specify <b>Secure</b> Applications and Architectures (24%)
    <img width="877" alt="Screen Shot 2022-01-24 at 3 43 36 PM" src="https://user-images.githubusercontent.com/83699657/151293571-af881589-7830-4e9d-80c7-9fb3682b7d64.png">
- Module4 
    : Design <b>Cost-Optimized</b> Architectures (18%)
    <img width="873" alt="Screen Shot 2022-01-24 at 4 38 37 PM" src="https://user-images.githubusercontent.com/83699657/151293601-70fe5cc5-bbda-42e2-8c73-433dd22547bc.png">

---

## Contents

- 📓 (0:58:39) S3 - 2022/01/10, 2022/01/31
- 📓 (1:09:27) Snowball - 2022/01/14
- 📓 (1:26:19) VPC Endpoints - 2022/01/14 (module3)
- 📓 (1:29:09) VPC Flow Logs - 2022/01/14 (module3)
- 📓 (1:32:30) NACL - 2022/01/15 (module3)
- 📓 (1:38:39) Security Groups - 2022/01/15 (module3)
- 📓 (1:42:45) NAT - 2022/01/15
- 📓 (2:50:37) IAM - 2022/01/18 (module3)
- 📓 (2:58:12) Cognito 
           - 2022/01/31
- 📓 (3:20:41) CLI & SDK - 2022/01/31
- 📓 (3:30:00) DNS - 2022/01/31
- 📓 (3:45:07) Route 53 - 2022/01/31
<br>

- 📓 (3:56:12) EC2 - 2022/01/26 (module1)
- 📓 (4:04:49) EC2 Pricing - 2022/01/26 (module1)
- 📓 (4:13:46) AMI - 2022/01/26 (module1)
- 📓 (4:23:36) Autoscaling Groups - 2022/01/29 (module2)
- 📓 (4:35:28) ELB - 2022/01/29 (module2)
- 📓 (5:49:50) EFS - 2022/01/27 (module1)
- 📓 (6:02:27) EBS - 2022/01/27 (module1)
<br>

- 📓 (7:00:11) RDS - 2022/01/30 (module2)
- 📓 (7:07:58) Redshift - 2022/01/30 (module2)
- 📓 (7:06:56) Aurora - 2022/01/30 (module2)
- 📓 (7:23:54) DynamoDB - 2022/01/30 (module2)
<br>

- 📓 (7:31:40) CloudFormation - 2022/01/26
- 📓 (7:51:56) CloudWatch - 2022/01/29 (module2)
- 📓 (8:06:30) CloudTrail - 2022/01/30 (module1)
- 📓 (8:18:16) Lambda - 2022/01/30 (module1)
- 📓 (8:28:30) SQS - 2022/01/29 (module1)
- 📓 (8:37:01) SNS - 2022/01/29
<br>

- 📓 (6:21:02) CloudFront - 2022/01/31 (module2)
- 📓 (8:42:21) ElastiCache - 2022/01/31 (module2)
- 📓 (8:43:03) High Availability (HA) - 2022/01/31 (module1)
- 📓 (9:02:49) Elastic Beanstalk - 2022/01/31 (module4)
- 📓 (9:12:41) API Gateway - 2022/01/31 (module3)
- 📓 (9:20:26) Kinesis - 2022/01/31
- 📓 (9:28:52) Storage Gateway(File Gateway) - 2022/01/31

Reference :
AWS Certified Solutions Architect - Associate 2020 (PASS THE EXAM!), Youtube, uploaded by freeCodeCamp.org, 12/24/2022, 
<https://www.youtube.com/watch?v=Ia-UEYYR44s>

---
## Dump
I studied <b>examtopic dump(574 questions)</b> twice and tried to analyze and remember some keywords on each question. Some questions have the specific pattern like having same keywords. But I heard there are not similar questions on the real test. I felt I need to study and get used to many kinds of situation of efficient AWS solutions. And When I take a test, I exactly felt it and I did good study.

For studying AWS SAA, I could know and understand flow of AWS and how to use many AWS solutions easily and efficiently.
I totally can sure that AWS SAA will help our backend development skill improve.