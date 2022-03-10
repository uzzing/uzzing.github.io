---
title:  "[AWS Solution Architect] Follow Along - NAT Gateway, VPC Endpoints"
date: 2022-1-17 3:56PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-17 3:56PM
---

## NAT Gateway (Network Address Translation)

`Instruction`
<https://uzzing.github.io/posts/NAT/>

- ⭐️ If you have <b>a private networking need to help gain outbound access to the internet</b>, you need to use a NAT gateway to rempat the Private IPs.

- ⭐️ NAT Gateways is a managed service which launches redundant instances within the selected AZ.

- ⭐️ You have to launch a NAT gateway per AZ
    - NAT gateway doesn’t do launch them automatically across other AZs for you.

---
## Follow along

the way we're going to get a route to the internet is by creating a NAT instacne or a NAT gateway.
Generally you wanna use a NAT gateway.
If you were trying to save mondy, you can definitely save money by having to manage a NAT instance by itself.

But we're gonna learn how to do NAT gateway, let's do it!

- switch over to VPC
    - because that's where the NAT gateway is.
    <img width="941" alt="Screen Shot 2022-01-17 at 3 04 23 PM" src="https://user-images.githubusercontent.com/83699657/149716611-0e3dc1af-04e7-4865-b54b-34c3355b91a9.png">
    <img width="941" alt="Screen Shot 2022-01-17 at 3 05 16 PM" src="https://user-images.githubusercontent.com/83699657/149716615-b95ec0b9-7fa6-478b-ab04-fdd891ec6f53.png">

- launch a NAT gateway in a public subnet
    - NAT gateway do cost money, but they're not terribly expensive.
    - Create NAT gateway
        1. select public one subnet
        2. Create Elastic IP 
    - Edit route table
    <img width="942" alt="Screen Shot 2022-01-17 at 3 06 07 PM" src="https://user-images.githubusercontent.com/83699657/149716618-fa31da61-7836-480e-9a36-79e0d034858b.png">
    <img width="937" alt="Screen Shot 2022-01-17 at 3 06 49 PM" src="https://user-images.githubusercontent.com/83699657/149716622-8016e085-7537-45e6-9e4b-a0670e6cfb20.png">
    <img width="943" alt="Screen Shot 2022-01-17 at 3 07 11 PM" src="https://user-images.githubusercontent.com/83699657/149716625-d122901f-e78b-4235-afda-c301f1409ba4.png">

- test
    <img width="619" alt="Screen Shot 2022-01-17 at 3 09 00 PM" src="https://user-images.githubusercontent.com/83699657/149716693-55889888-0371-4a11-b7c7-e6a78dd1f43e.png">

- we have one inbound traffic, but we definitely want outbound, because we wold probably want to update packages on our EC2 instance.
    - if we did 'sudo yum update', we wouldn't be able to do this without a outbound connection.
    <img width="916" alt="Screen Shot 2022-01-17 at 3 12 09 PM" src="https://user-images.githubusercontent.com/83699657/149716908-7e2f4fc1-650c-4732-a818-52b453398708.png">

- it's a way of getting access to the internet, only for the thing that we need for outbound connections. 

---
## VPC Endpoints

- how we can set an outbound connection to the internet.
    - let's talk about how we could access other AWS services via our private EC2 instances here.
    - so s3 would be a very common one to utilize.

`Instructions`
<https://uzzing.github.io/posts/VPC-Endpoints/>

- switch over to s3
    - we get a IAM role permissions to access that stuff there.
    <img width="941" alt="Screen Shot 2022-01-17 at 3 16 26 PM" src="https://user-images.githubusercontent.com/83699657/149717804-84948021-2c56-4b5a-8165-715afdbe8247.png">

- aws s3 ls
    - we can definitely see that we have a way of accessing s3 via the CLI
    <img width="369" alt="Screen Shot 2022-01-17 at 3 19 40 PM" src="https://user-images.githubusercontent.com/83699657/149717815-b5a13c11-348b-4213-9879-bebafc01692f.png">

    - Q. what it happen when we remove that NAT gateway, would we still be able to access s3?
    - A. No. it no longer has anyway to access s3.
    <img width="841" alt="Screen Shot 2022-01-17 at 3 21 39 PM" src="https://user-images.githubusercontent.com/83699657/149718040-4aece0a9-a906-4e0a-8d28-332548c2482b.png">
    - So the way to use EC2 instance through CLI is it's going to go out to the internet and come back into AWS network to access s3.
    - <b>since there's no outbound way of connection to the internet, there's no way we're gonna be able to connect to s3.</b>

    - Q. why doesn't you just keep the traffic within the network?
    - A. because we're already on EC2 within AWS network and s3 is with Eva's network.
    - that bring us to endpoints which is how we can create our own private tunnel within AWS network, we don't have to leave up the internet.

- we can connect to s3 without having outbound connect.

- Create a new Endpoints
    - select VPC
        <img width="937" alt="Screen Shot 2022-01-17 at 3 29 04 PM" src="https://user-images.githubusercontent.com/83699657/149718888-92114c75-ed19-4707-9484-d32af82c9e8a.png">
    - select S3
        <img width="937" alt="Screen Shot 2022-01-17 at 3 29 04 PM" src="https://user-images.githubusercontent.com/83699657/149718962-4dac3eed-25f2-4f2b-bb00-e5329bc1d4b5.png">
    - selete a route table associated with private subnet
        <img width="658" alt="Screen Shot 2022-01-17 at 3 34 11 PM" src="https://user-images.githubusercontent.com/83699657/149719373-47281a3e-6d9a-42e2-b271-85d005e7da0f.png">

    - result
        <img width="848" alt="Screen Shot 2022-01-17 at 3 35 52 PM" src="https://user-images.githubusercontent.com/83699657/149719564-dce27ec0-70e1-416f-bcdc-d93ab58b8a9d.png">
        <img width="345" alt="Screen Shot 2022-01-17 at 3 36 40 PM" src="https://user-images.githubusercontent.com/83699657/149719653-41fcd2db-5edb-495f-982e-22080a0a5bcf.png">

---
## Words
- switch over to N

--- 

.....???!!!

The copyright of all material here is on this video 
<br>

<https://www.youtube.com/watch?v=Ia-UEYYR44s>
<br>
This post is just for studying AWS SAA.