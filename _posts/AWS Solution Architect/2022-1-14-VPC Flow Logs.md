---
title:  "[AWS Solution Architect] VPC Flow Logs"
date: 2022-1-14 3:50PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-14 3:50PM
---

## VPC Flow Logs

<img width="1440" alt="Screen Shot 2022-01-14 at 3 31 42 PM" src="https://user-images.githubusercontent.com/83699657/149462856-44c41792-22dc-4905-aecf-8f9c1b13402b.png">

- to capture IP traffic information in-and-out of Network interfaces within your VPC.

You can turn on VPC Flow Logs at three different levels
- turn it on in VPC level : which doing it here
- turn it on at a specific Subnet
- turn it on for a specific network interface

- To find VPC flow logs, just go to the VPC console

- if you once turn flow log on, you can't edit it. all you can do is <b>delete it.</b>

---

## Example of VPC flow logs

<img width="1440" alt="Screen Shot 2022-01-14 at 3 38 25 PM" src="https://user-images.githubusercontent.com/83699657/149462886-02163bc3-7a74-457e-9bf4-dc4e378d5994.png">

- ⭐️ srcaddr
- ⭐️ dstaddr

`Questions`
- Does VPC flow logs contain host names? N
- Does VPC flow logs contain IP addresses? Y 

---
## Summary

<img width="1440" alt="Screen Shot 2022-01-14 at 3 42 36 PM" src="https://user-images.githubusercontent.com/83699657/149464035-0dd5e664-9a43-4e05-b8e9-97407cac7b15.png">

---
## Words
- trickle down :　흘러내리다

---

The copyright of all material here is on the video <https://www.youtube.com/watch?v=Ia-UEYYR44s>
This post is just for studying AWS SAA.