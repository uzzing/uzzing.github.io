---
title:  "[AWS Solution Architect] Create VPC, IGW, Route Tables and Subnets"
date: 2022-1-15 2:17PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-15 2:17PM
---

## Create VPC and Core Components(IGW, Route table, Subnets)

<img width="1440" alt="Screen Shot 2022-01-15 at 1 05 31 PM" src="https://user-images.githubusercontent.com/83699657/149608483-679b471f-c991-4f1f-9a61-239ec369be22.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 11 39 PM" src="https://user-images.githubusercontent.com/83699657/149608485-0d1cde84-98d6-43c8-9c15-e949f0732da9.png">

- IPv4 CIDR
    - 10.0.0.0 is commonly chosen one.
    - this is saying how many IP addresses you want to allocate.

- IPv6 CIDR block
    - it's supported on AWS.
    - it's the future of our IP protocol.
    - so it's definitely something you might want to turn on.
    - just be prepared for the future there

- Tenancy
    - dedicated host is quite expensive


- we don't have any DNS hostnames
    - we definitely want to <b>turn that on.</b>
    - if we launch EC2 instance, it's not going to get a DNS hostname, that's just like a URL.
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 14 44 PM" src="https://user-images.githubusercontent.com/83699657/149608468-5c564bbc-1e2b-481e-9564-15028b4fdc2c.png">
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 15 31 PM" src="https://user-images.githubusercontent.com/83699657/149608474-c17fb843-e009-45b3-91fe-4dcf480846ce.png">

<br>

- Create internet gateways
<img width="1440" alt="Screen Shot 2022-01-15 at 1 18 07 PM" src="https://user-images.githubusercontent.com/83699657/149608635-a4d8c66e-8d6f-4f98-9ebc-e402e698c3a7.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 18 38 PM" src="https://user-images.githubusercontent.com/83699657/149608636-cb0e0f53-f3f6-4876-8d55-bdd0c55378ce.png">
<br>

- internet gateways can only be attached to a very specific VPC
    - it's a <b>one-to-one relationship</b>
<img width="1440" alt="Screen Shot 2022-01-15 at 1 19 00 PM" src="https://user-images.githubusercontent.com/83699657/149608637-1c8dbf22-0d5b-4514-ad04-c4a4bf0aea4f.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 20 14 PM" src="https://user-images.githubusercontent.com/83699657/149608638-459e9344-8988-46be-a8e0-b0bcd9065d21.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 20 36 PM" src="https://user-images.githubusercontent.com/83699657/149608640-d77d4731-fb4a-427f-bd55-12d89ddc469b.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 20 50 PM" src="https://user-images.githubusercontent.com/83699657/149608642-b80d15cf-e2e0-44a4-b34d-74d0dc6fccd8.png">


- but that still doesn't mean that things within our network can reach the internet
    - because we have to <b>add a route to our route table</b>

- see that <b>there already is a route table associated with our VPC</b>
    - because it did create us <b>a default route table</b>

    <img width="1440" alt="Screen Shot 2022-01-15 at 1 27 29 PM" src="https://user-images.githubusercontent.com/83699657/149608816-9d8575f1-5ae1-40a9-8467-61081d62fce5.png">

<br>

- But let's create a route table
<img width="1440" alt="Screen Shot 2022-01-15 at 1 30 02 PM" src="https://user-images.githubusercontent.com/83699657/149608890-6ccaad53-89cd-4bd2-8cf2-037b2284e2d9.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 30 42 PM" src="https://user-images.githubusercontent.com/83699657/149608893-1b1413b6-8c37-40f6-bb30-875ad2e3072d.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 31 15 PM" src="https://user-images.githubusercontent.com/83699657/149608895-e79b7cbc-2c96-4436-a0e2-a1916984b509.png">

You can see by default, it has the full scope of our local network here.

<img width="1440" alt="Screen Shot 2022-01-15 at 1 34 08 PM" src="https://user-images.githubusercontent.com/83699657/149608971-23898b19-8774-4cda-afef-cd87d8e2a00a.png">

- Let change this one to our main.
    - main route table is whenever what is going to be used by default.
<img width="1440" alt="Screen Shot 2022-01-15 at 1 37 28 PM" src="https://user-images.githubusercontent.com/83699657/149609066-14cf8753-95a9-4f35-b7d8-652924585181.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 37 36 PM" src="https://user-images.githubusercontent.com/83699657/149609067-ec785dc9-11cf-4a8a-970d-fcef3c0c5d4c.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 38 13 PM" src="https://user-images.githubusercontent.com/83699657/149609074-eaee038a-7ca6-4748-8064-369202483c8e.png">

- we're gonna <b>add a route</b> for the internet gateway.
    - 0.0.0.0/0 which means let's take anything from anywhere.
    - select internet gateway
    - save 
    - now we have a way for our subnets to reach the internet.
<img width="1440" alt="Screen Shot 2022-01-15 at 1 39 59 PM" src="https://user-images.githubusercontent.com/83699657/149609193-86d3e82f-d0c2-43c8-a778-5f19c67f7468.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 41 28 PM" src="https://user-images.githubusercontent.com/83699657/149609194-e14a3785-1a8d-4f5b-bd8c-c9ed73de4211.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 41 33 PM" src="https://user-images.githubusercontent.com/83699657/149609195-6a6da70e-2e6c-400d-8885-67f28dcfa62b.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 1 41 37 PM" src="https://user-images.githubusercontent.com/83699657/149609196-e5c2849b-57b5-47ca-ad71-452f409f4504.png">



- it's time to create some subnets.
- these are default ones created with your default VPC
    - there's exactly one for every availability zone within each region
    - my region is seoul, which has 4 public subnets.
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 46 50 PM" src="https://user-images.githubusercontent.com/83699657/149609317-7fbef0b2-d158-4841-bb08-e9d4c404bf9a.png">


- check the auto assign to Yes
    - if this is set to Yes, that means any EC2 instance launch in the subnet is going to get a public IP address.
    - Hence, it's going to be considered a public subnet.
<img width="1440" alt="Screen Shot 2022-01-15 at 1 50 39 PM" src="https://user-images.githubusercontent.com/83699657/149609409-b239d580-a94f-4e02-851d-762468a77a63.png">

- a lot of companies wants to run on at least three availability zones for high availability.
    - because one goes out, if you have another one, what happens if two goes out.
    - so commonly create at least two additionals.

- we're gonna make 3 subnets and 1 private subnet
- first of all, make subnet for A.
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 54 42 PM" src="https://user-images.githubusercontent.com/83699657/149609599-4823ba51-c2fb-424c-bdae-71bd00005d50.png">
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 55 21 PM" src="https://user-images.githubusercontent.com/83699657/149609600-2855562a-10b4-45a2-9627-7633e1f950d1.png">
    <img width="1440" alt="Screen Shot 2022-01-15 at 1 58 09 PM" src="https://user-images.githubusercontent.com/83699657/149609601-36fe3b1c-b54a-4f25-b936-828f6cfa7cae.png">

- this CIDR range is smaller than the one up here.
    - the number is larger, but from the perspective of how many IP addresses it allocates, there's actually a fewer here.
    - you can set this as 16, it's always goint to be less, I mean a higher number than 16.


- the auto sign is going to be set to No.
    - modify this and set it is considered <b>a public subnet.</b>
<img width="1440" alt="Screen Shot 2022-01-15 at 1 59 38 PM" src="https://user-images.githubusercontent.com/83699657/149609645-0ae7d26e-06a4-46ae-a1a3-be430288ae2d.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 2 00 10 PM" src="https://user-images.githubusercontent.com/83699657/149609648-0996c143-81f4-4d78-a854-0de63bef0d2f.png">

- make subnets for B and C and private A too.
<img width="1440" alt="Screen Shot 2022-01-15 at 2 03 39 PM" src="https://user-images.githubusercontent.com/83699657/149609756-3f924d64-4b5d-4721-b225-2c5b073f1dd9.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 2 04 54 PM" src="https://user-images.githubusercontent.com/83699657/149609758-a3f57973-a66e-4f5f-8e86-08c7e9971a75.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 2 06 48 PM" src="https://user-images.githubusercontent.com/83699657/149609782-9c340d0f-5742-4a35-b23e-a88a272f0658.png">

- public A, B, C are already automatically asscociated with main route table by default.
- but for our private one, we're not gonna wanting to really use the main route table there. 
    - so we probably would want to <br>create our own route table for our private subnets</b>.

- we don't need the subnet to reach the internet.
- so just change the association here.
<img width="1440" alt="Screen Shot 2022-01-15 at 2 11 31 PM" src="https://user-images.githubusercontent.com/83699657/149609906-40686d38-a2c7-44da-9b3c-613121f1b4c2.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 2 12 51 PM" src="https://user-images.githubusercontent.com/83699657/149609918-a131aa60-7465-4fb4-9d6f-a929b857cab1.png">
<img width="1440" alt="Screen Shot 2022-01-15 at 2 12 57 PM" src="https://user-images.githubusercontent.com/83699657/149609920-9e0ad7bb-fd38-445b-8152-253aa3634ef7.png">

---
## Words
- on the left hand side : 왼쪽에

---

The copyright of all material here is on this video <https://www.youtube.com/watch?v=Ia-UEYYR44s>
<br>
This post is just for studying AWS SAA.