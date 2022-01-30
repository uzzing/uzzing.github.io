---
title:  "[AWS Solution Architect] DynamoDB"
date: 2022-1-31 12:07AM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-31 12:07AM
---

## DynamoDB
- Introduction
- Table Structure
- Consistent Reads ⭐️ 
- DynamoDB Cheat Sheet

<img width="1440" alt="Screen Shot 2022-01-30 at 11 55 51 PM" src="https://user-images.githubusercontent.com/83699657/151705099-1942e729-cd0a-45af-9f67-c14d811b25c6.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 56 07 PM" src="https://user-images.githubusercontent.com/83699657/151705109-10730aa2-f6cb-4fa7-955d-a7e1a431be76.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 56 43 PM" src="https://user-images.githubusercontent.com/83699657/151705111-bcb412fe-ef44-4a00-ae44-8fa8b3ba6a8e.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 57 59 PM" src="https://user-images.githubusercontent.com/83699657/151705113-aa1ed6de-e650-4649-8f7c-99000a4b181e.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 58 40 PM" src="https://user-images.githubusercontent.com/83699657/151705114-80696b86-477e-4c60-9868-ef36ba3c7d16.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 12 00 12 AM" src="https://user-images.githubusercontent.com/83699657/151705115-46a9cba4-6154-4571-a771-e171cdfc71b2.png">

---
- ⭐️ ⭐️ ⭐️ 
<img width="882" alt="Screen Shot 2022-01-24 at 3 00 19 PM" src="https://user-images.githubusercontent.com/83699657/151691940-9e8d0d3a-ed5b-4ef1-8c6e-7528f383ed48.png">

    - 여러 리전의, 테이블 간, 비동기 복제 : 여러 region의 table을 서로 동기화시킬 수 있음 (비동기로)

<img width="876" alt="Screen Shot 2022-01-24 at 3 03 07 PM" src="https://user-images.githubusercontent.com/83699657/151691945-5e89610a-67a5-45f0-ad4f-1e42ff095965.png">
from AWS (01/24/2022)

- Reading / Writing 용량을 각각 돈을 주고 구입함
    - 요구 사항에 따라 용량을 각각 provision해서 사용 가능
- 1번 시점 : 데이터가 저장됨
- 2번 시점 : 데이터 목록이 나오는 시점
    - Eventually consistent read (default) : 1번 시점, 2번 시점이 1초정도 늦게 동기화됨, 더 저렴함
        - use case : 싱크가 중요하지 않은 경우 충분히 잘 사용 가능
    - Strongly consistent read : 1번 시점, 2번 시점이 거의 비슷
        - use case : 은행! 은행간 거래에서 물건값 결제 등 잔고에 대해서 사용
            - eventually consistent read를 사용하면 2번 이상의 transaction을 발생시킬수도 있어서 두번 돈이 나갈 수 있음



---
<img width="881" alt="Screen Shot 2022-01-24 at 3 06 22 PM" src="https://user-images.githubusercontent.com/83699657/151691880-dfdc6054-7ba5-4b45-b86a-2b26b83114b8.png">
<img width="877" alt="Screen Shot 2022-01-24 at 3 06 44 PM" src="https://user-images.githubusercontent.com/83699657/151691882-476a4b59-e66a-48ee-94b3-5870dff65daa.png">
from AWS (01/24/2022)

- Key point : Unrelational database
- Answer : D
    - Redshift : rds -> X
    - RDS -> X
    - Glacier -> no database

<img width="878" alt="Screen Shot 2022-01-24 at 3 07 56 PM" src="https://user-images.githubusercontent.com/83699657/151691684-880ff843-29fa-497e-9665-2eb3450d2058.png">
from AWS (01/24/2022)

---
#### Reference
AWS Certified Solutions Architect - Associate 2020 (PASS THE EXAM!), Youtube, uploaded by freeCodeCamp.org, 12/24/2019, 
<https://www.youtube.com/watch?v=Ia-UEYYR44s>