---
title:  "[AWS Solution Architect] Redshift"
date: 2022-1-30 11:55PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-30 11:55PM
---

## Redshift

<img width="1440" alt="Screen Shot 2022-01-30 at 11 38 29 PM" src="https://user-images.githubusercontent.com/83699657/151704793-5ee3af5d-896a-4ce6-9a84-a00029d68779.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 38 44 PM" src="https://user-images.githubusercontent.com/83699657/151704799-5ad40aa8-c281-4849-a806-aa99e27806d3.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 40 53 PM" src="https://user-images.githubusercontent.com/83699657/151704800-c86d1a54-edec-4d3a-99b2-f1bb081d8482.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 41 53 PM" src="https://user-images.githubusercontent.com/83699657/151704801-08f899f9-8005-4339-9c97-8be817d77980.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 42 43 PM" src="https://user-images.githubusercontent.com/83699657/151704802-ba3f69f5-1421-42e9-a002-f3de16a94fef.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 43 35 PM" src="https://user-images.githubusercontent.com/83699657/151704804-eeda9fae-2703-4b1b-a26d-864932490e44.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 44 31 PM" src="https://user-images.githubusercontent.com/83699657/151704805-15742535-b8eb-4f70-87ef-5130d2fa37e9.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 45 04 PM" src="https://user-images.githubusercontent.com/83699657/151704806-b342f193-6245-41cf-9a73-2273755ac7c2.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 45 45 PM" src="https://user-images.githubusercontent.com/83699657/151704807-d8fc1c81-9bba-43e9-8a0a-0956e4b0e7fd.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 46 08 PM" src="https://user-images.githubusercontent.com/83699657/151704808-3ccf391c-6e45-455b-8dc2-2927f4b6eae2.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 46 41 PM" src="https://user-images.githubusercontent.com/83699657/151704809-9fe7a2d9-34ea-4ba9-94b8-818d3992470e.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 47 18 PM" src="https://user-images.githubusercontent.com/83699657/151704810-cf5bb1b9-9b96-4c34-adc3-366ce87e3d80.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 47 34 PM" src="https://user-images.githubusercontent.com/83699657/151704813-bbffe7f9-7469-484d-bef1-da0e93cbe1a2.png">
<img width="1440" alt="Screen Shot 2022-01-30 at 11 48 06 PM" src="https://user-images.githubusercontent.com/83699657/151704814-fb98798f-cf6c-4e3d-bbfe-c61d743ea336.png">

---

<img width="878" alt="Screen Shot 2022-01-24 at 3 07 56 PM" src="https://user-images.githubusercontent.com/83699657/151691684-880ff843-29fa-497e-9665-2eb3450d2058.png">
from AWS (01/24/2022)

- Key point : 4TB의 초기 storage capacity, 관계형 데이터베이스, 매일 10GB씩 증가, read replica
    - Answer : Aurora
        - 자동으로 storage capacity가 increase
    - dynamoDB : no rds / noSQL
    - S3 : object storage
    - Redshift : data warehouse / no read replica / no automatic scalable

---
#### Reference
AWS Certified Solutions Architect - Associate 2020 (PASS THE EXAM!), Youtube, uploaded by freeCodeCamp.org, 12/24/2019, 
<https://www.youtube.com/watch?v=Ia-UEYYR44s>