---
title:  "[AWS Solution Architect] VPC Endpoints"
date: 2022-1-14 3:30PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-14 3:30PM
---

## VPC Endpoints

<img width="1440" alt="Screen Shot 2022-01-14 at 3 09 53 PM" src="https://user-images.githubusercontent.com/83699657/149461761-0ad31508-5e9d-4233-bfd9-c6a3c8c3f811.png">

- you have an EC2 instance, and you want to get something from your s3 bucket.
so you normally do is use the AWS SDK and you would make that call, and it would go out of your IGW to the internet and back into the AWS network to get that file or object out of s3. 
SOo, it wouldn't be more convenient if we could just keep the traffic within the AWS network. That is the purpose of a VPC endpoint.
It helps you keep traffic within the AWS network.
<br>

`The idea`
- because it does not leave a network, not required a public IP address to communicate with these services.
to get to s3, we can now eliminate the need for an internet gateway and keep everything private.

`Type`
- Interface Endpoint
- Gateway Endpoint

---
## Interface Endpoints

<img width="1440" alt="Screen Shot 2022-01-14 at 3 18 07 PM" src="https://user-images.githubusercontent.com/83699657/149461206-6fd22a1d-9d21-49eb-a31e-46771c3f9060.png">

---

## Gateway Endpoint

<img width="1440" alt="Screen Shot 2022-01-14 at 3 21 22 PM" src="https://user-images.githubusercontent.com/83699657/149461244-0910f88d-2a2e-4495-9e1d-9a8b197956b8.png">

---
## Summary

<img width="1440" alt="Screen Shot 2022-01-14 at 3 24 00 PM" src="https://user-images.githubusercontent.com/83699657/149461970-dd60e058-e498-4d7f-9c01-fc9d21d6074d.png">

---
## Words

- elastic
- provision : supply, 供給, 공급

---

The copyright of all material here is on the video <https://www.youtube.com/watch?v=Ia-UEYYR44s>
This post is just for studying AWS SAA.