---
title:  "[AWS Solution Architect] Security Groups, NACL and Bastion"
date: 2022-1-17 2:54PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-17 2:54PM
---

## Security Groups

- there's IPv4 DNS and the public IP address for the public
- there's nothing for the private 

    <img width="1440" alt="Screen Shot 2022-01-15 at 4 09 34 PM" src="https://user-images.githubusercontent.com/83699657/149613065-e1ff1147-1cf1-4aa0-8308-d2187e466d8c.png">


Let's check our website is working
- `case1` public instance
    - copy the public IP address
    - or we can take the DNS when it doesn't matter
    <img width="1275" alt="Screen Shot 2022-01-17 at 12 33 52 PM" src="https://user-images.githubusercontent.com/83699657/149704156-e71cf7c0-0dcd-4644-afa9-8f759f3823a0.png">

- `case2` private instance
    - there's nothing on the public ID address
    - we can use Private IPs
    - <b>there's no one of accessing that website running on the private one.</b>
    <img width="1283" alt="Screen Shot 2022-01-17 at 12 34 14 PM" src="https://user-images.githubusercontent.com/83699657/149704147-23820d6d-d0bb-4d23-bb3b-d7341d261d87.png">

- the reason why we were able to access the instance, publicly was that in our security group, <b>we had an inbound rule on port 80.</b>
    - Port 80 is what websites run on.
        - when we're accessing through the web browser, we're allowing my IP here. 
        - that's why I was allowed to access it.
    <img width="1288" alt="Screen Shot 2022-01-17 at 12 36 46 PM" src="https://user-images.githubusercontent.com/83699657/149704986-0b5f6e80-fbb3-40d5-bcd0-b6b90bff97b2.png">

- let's change my IP
    - I have a VPN
        - it's a service you can buy a lot of people use it so that they can watch Netflix in other regions.
    - I have a VPN from brazil shortly once it connects.
    -> it shouldn't work, it's hanging because I'm not using that IP.

-> that's how security groups work for inbound rules.


- for outbound rules, that's traffic going out to the internet. it's almost always open like this.
    <img width="1268" alt="Screen Shot 2022-01-17 at 12 57 46 PM" src="https://user-images.githubusercontent.com/83699657/149705945-ee42f64c-6acd-4f14-a822-135d8bcd9f50.png">

---
## NACL (Network ACL)

- we would like to show off how NACLs work compared to security groups.

- <b>security groups, by default, only can allow things so everything is denied.</b>
    - you're adding allow rules only 
    - <b>you can't add an explicit deny rule.</b>

⭐️ <b>NACLs are very useful, is that you can use it to block a very `specific IP` addresses or IP ranges.</b> ⭐️

- ⭐️ <b>security groups</b> are associated with <b>the actual EC2 instance</b>
- ⭐️ <b>NACLs are associated with the subnets.</b>
- Q. how do we figure out the NACLs?

- A. 
    - in order to block individual IP address, we have to determine what subnet it runs in.
    <img width="1440" alt="Screen Shot 2022-01-17 at 1 12 43 PM" src="https://user-images.githubusercontent.com/83699657/149707100-b249f243-0cc6-4586-b0be-6bd977629184.png">
    <img width="1440" alt="Screen Shot 2022-01-17 at 1 13 05 PM" src="https://user-images.githubusercontent.com/83699657/149707127-1065b326-2ec9-4457-8c64-eef251db2260.png">
    <img width="1440" alt="Screen Shot 2022-01-17 at 1 13 34 PM" src="https://user-images.githubusercontent.com/83699657/149707129-f8d4bf93-8afd-490e-8ba5-94aa9aa39360.png">

    - check grab that IP address and paste it.
        - it works!

---
## Bastion

- how do we actually <b>get access to the private subnet.</b>
    - we have our private EC2 instance
    - we don't have an public IP address on it
        - there's no direct way to gain access to it.
    - So we can't just easily SSH into it.
-> this is where we're gonna need a bastion

- launch new instance
    1. go to marketplace and type in Bastion.
        - use Guacamole Bastion Host
            - there's an associated cost
            - they do have a trial version (you can get it without paying anything for it)
            <img width="1440" alt="Screen Shot 2022-01-17 at 1 24 19 PM" src="https://user-images.githubusercontent.com/83699657/149707926-da99001a-18a5-417f-8a26-55aec9383eb6.png">
            <img width="1440" alt="Screen Shot 2022-01-17 at 1 24 27 PM" src="https://user-images.githubusercontent.com/83699657/149707927-9363c7e9-cdf4-4ee3-829e-7d1c72181eef.png">

    2. we're gonna need a small, this one doesn't allow you to go into micros. (There's an assciated cost)
        <img width="1440" alt="Screen Shot 2022-01-17 at 1 25 10 PM" src="https://user-images.githubusercontent.com/83699657/149707932-dd5301fa-39b2-4c50-a087-736bcf8a96aa.png">


    3. Configure instance detail
        - select the network as private one.
        - select the public subnet.
        - create a new IAM role and set it
            - you need to give it some access so that it can auto discover instances.
            - it's gonna give us permissions to cloud watch and STS
            - EC2ReadOnlyAccess & Guaws

        <img width="1440" alt="Screen Shot 2022-01-17 at 1 27 31 PM" src="https://user-images.githubusercontent.com/83699657/149708241-4b9e51df-b42d-4fee-837c-0f2f03658aeb.png">
        <img width="1440" alt="Screen Shot 2022-01-17 at 1 29 02 PM" src="https://user-images.githubusercontent.com/83699657/149708244-6cd66147-947e-40d6-a831-01778ef8b8ee.png">

        <img width="1440" alt="Screen Shot 2022-01-17 at 1 32 53 PM" src="https://user-images.githubusercontent.com/83699657/149708623-f1cb162b-82b1-4498-b36e-9550a7243d25.png">
        <img width="1440" alt="Screen Shot 2022-01-17 at 1 33 51 PM" src="https://user-images.githubusercontent.com/83699657/149708665-7b1539fd-f3ef-4f59-abf9-cd25ef6275b4.png">
        <img width="984" alt="Screen Shot 2022-01-17 at 1 37 02 PM" src="https://user-images.githubusercontent.com/83699657/149709081-d9dc50a8-ac4f-41e2-b3fd-13c995d04817.png">
        <img width="1440" alt="Screen Shot 2022-01-17 at 1 38 31 PM" src="https://user-images.githubusercontent.com/83699657/149709084-4912512c-3548-45d1-9c9c-32343a03cf52.png">
        <img width="987" alt="Screen Shot 2022-01-17 at 1 39 30 PM" src="https://user-images.githubusercontent.com/83699657/149709086-675c93a9-212d-4e11-a849-708016b8d9e6.png">
        <img width="980" alt="Screen Shot 2022-01-17 at 1 39 51 PM" src="https://user-images.githubusercontent.com/83699657/149709091-9aa2913a-37bb-486a-be05-7bb756f62fb1.png">
        <img width="984" alt="Screen Shot 2022-01-17 at 1 40 19 PM" src="https://user-images.githubusercontent.com/83699657/149709092-5c01a2e7-872d-4318-9990-3c53e5c2b6a7.png">
        <img width="971" alt="Screen Shot 2022-01-17 at 1 41 40 PM" src="https://user-images.githubusercontent.com/83699657/149709205-fd18b68b-69ec-42fc-ab66-3640bd745b25.png">
        <img width="982" alt="Screen Shot 2022-01-17 at 1 42 22 PM" src="https://user-images.githubusercontent.com/83699657/149709206-f3adbbb2-b98a-4d7f-85b2-e2b060541e69.png">

    - result
    <img width="984" alt="Screen Shot 2022-01-17 at 1 44 27 PM" src="https://user-images.githubusercontent.com/83699657/149709358-ee6f204b-dbc3-4550-b429-bd227715b797.png">

- Grap the public DNS and paste it
    - hit hide advanced
    - hit allow on the top left
    - login default admin
        - id : guacadmin
        - password : the name of the instance ID
    <img width="984" alt="Screen Shot 2022-01-17 at 1 46 05 PM" src="https://user-images.githubusercontent.com/83699657/149714978-b04003a2-86f3-4cf8-b2b8-85f4c3f074fd.png">
    <img width="985" alt="Screen Shot 2022-01-17 at 1 46 36 PM" src="https://user-images.githubusercontent.com/83699657/149709558-56a93441-63f2-4519-8520-23b7176fe973.png">
    <img width="985" alt="Screen Shot 2022-01-17 at 1 48 32 PM" src="https://user-images.githubusercontent.com/83699657/149709691-a5951168-16d3-4b93-92e3-78d8ad013a21.png">
    <img width="984" alt="Screen Shot 2022-01-17 at 1 48 48 PM" src="https://user-images.githubusercontent.com/83699657/149709694-168af98d-19f6-4d6c-812e-34c7a3014b69.png">

- now it has auto discovered the instances which are in the VPC that is launched 
    <img width="981" alt="Screen Shot 2022-01-17 at 1 50 21 PM" src="https://user-images.githubusercontent.com/83699657/149709808-3c8374e6-04c7-478c-b2c3-7d0a27713e08.png">

- connect it and login, make the shell here
    - login : that's the way to gain access to the private instance.
        <img width="517" alt="Screen Shot 2022-01-17 at 1 52 13 PM" src="https://user-images.githubusercontent.com/83699657/149709945-7386308c-cb51-4236-bd79-b090e6901700.png">
    - before doing something, I'm gonna configure something that's why we use Bastions (you can see those in setup )
        - it's a hardened instance.
        - it does allow you to <b>authenticate via multiple methods</b>
            - so you can enable multi factor authentication to use this
        - it also has the ability to do <b>screen recordings</b>
            - you can do show what people are up to
        - we can also use <b>a sessions manager</b> which does a lot of this for us with the exception of screen recording within the AWS.

---
## Words
- explicit : 明示的
- grab it here : copy it

--- 
The copyright of all material here is on this video 
<br>

<https://www.youtube.com/watch?v=Ia-UEYYR44s>
<br>
This post is just for studying AWS SAA.