---
title:  "[AWS Solution Architect] Follow Along - VPC Clean up"
date: 2022-1-17 4:39PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-17 4:39PM
---

## VPC Clean up
- terminate instances
- delete endpoint for s3
- release elastic IPs (be created when we created NAT gateways, Ips not being utilized cost use money)
- double check NAT gateway, make user nothing is running under there
- delete subnets
- delete route tables
- detach internet gateways
- delete VPC

--- 
## Words
- free credits
- incur cost : 비용을 발생하다
---

The copyright of all material here is on this video
<https://www.youtube.com/watch?v=Ia-UEYYR44s>

<br>
This post is just for studying AWS SAA.