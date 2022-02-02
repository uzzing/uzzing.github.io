---
title:  "[AWS Solution Architect] CloudFront"
date: 2022-1-31 2:13PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-31 2:13PM
---

## CloudFront 
- Introduction
- Core Components
- Distributions
- Lambda@Edge
- Protection
- CloudFront Cheat Sheet


<img width="1440" alt="Screen Shot 2022-01-31 at 1 22 57 PM" src="https://user-images.githubusercontent.com/83699657/151740526-bfa46970-7800-4bfa-bab8-8896052ae765.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 1 23 03 PM" src="https://user-images.githubusercontent.com/83699657/151740534-02ba8377-19b2-4a5b-969c-44fbfcd04d89.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 1 24 05 PM" src="https://user-images.githubusercontent.com/83699657/151740537-ee2e7128-44ad-4f76-9ed2-35e4004ca055.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 1 25 10 PM" src="https://user-images.githubusercontent.com/83699657/151740539-cf636c95-aa8f-4283-9200-33ba2da88350.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 1 29 10 PM" src="https://user-images.githubusercontent.com/83699657/151740542-a2ffe3d3-0f95-4220-be13-4f1b05e6796c.png">

- presigned URL : for S3
- signed URL : for CloudFront

<img width="1440" alt="Screen Shot 2022-01-31 at 1 40 11 PM" src="https://user-images.githubusercontent.com/83699657/151740544-ba797aae-a972-4976-948a-966343573850.png">

---

- Create a Distribution
<img width="1440" alt="Screen Shot 2022-01-31 at 1 33 10 PM" src="https://user-images.githubusercontent.com/83699657/151740597-50cb6206-4399-4a2b-8a6b-c7a7f0869bc9.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 1 34 44 PM" src="https://user-images.githubusercontent.com/83699657/151740614-dc1b06e4-dc61-4034-9306-50ac93a4b0ba.png">

- Invalidation after updating files
<img width="1440" alt="Screen Shot 2022-01-31 at 1 39 50 PM" src="https://user-images.githubusercontent.com/83699657/151740618-c5aee590-eb2d-4fab-8f53-41e5ca4eee0e.png">

---
<img width="880" alt="Screen Shot 2022-01-24 at 3 10 11 PM" src="https://user-images.githubusercontent.com/83699657/151742000-14ac9c8f-df18-4095-b52e-5e31a87f5401.png"> by AWS (01/24/2022)

- CloudFront edge-location : has cached copies

---

<img width="1068" alt="Screen Shot 2022-01-31 at 2 05 48 PM" src="https://user-images.githubusercontent.com/83699657/151742116-3a2d5b5d-d57e-41b9-b4cd-1acc8b5907bf.png">

- <b>Caching</b>
    - 오랜시간 걸리는 작업의 결과를 저장하는 것 for high performance
    - origin storage에 access하는 것보다 더 빠르게 요청 가능
    - 일반적으로 RAM(Random Access Memory)과 같이 빠르게 액세스할 수 있는 하드웨어에 저장

- 캐시 계층을 구현할 때는 <b>캐싱되는 데이터의 유효성을 이해하는 것이 중요</b>합니다. <b>성공적인 캐시</b>는 높은 적중률로 이어집니다. 즉, <b>가져온 데이터가 캐시에 존재합니다.</b> 가져온 데이터가 캐시에 존재하지 않을 때 캐시 비적중이 발생합니다.
    - <b>TTL(Time To Live)</b>과 같은 제어 항목을 적용하여 이에 따라 <b>데이터를 만료</b>되도록 할 수 있습니다. 
- 다른 고려 사항은 <b>캐시 환경이 고가용성</b>이어야 할 필요가 있는지 여부인데, 
    - 이는 <b>Redis와 같은 인 메모리 엔진</b>을 사용하여 충족할 수 있습니다. 
    - 기본 위치에서 데이터를 캐싱하는 것과는 달리, 경우에 따라 인 메모리 계층을 <b>독립형 데이터 스토리지 계층</b>으로 사용할 수 있습니다. 이 시나리오에서는 인 메모리 엔진에 상주하는 데이터에 대해 적절한 <b>RTO</b>(복구 목표 시간 – 가동 중단으로부터 복구하는 데 걸리는 시간)와 <b>RPO</b>(목표 복구 시점 – 복구 시 캡처된 최종 시점 또는 트랜잭션)를 정의하여 이것이 적합한지를 파악하는 것이 중요합니다. 다른 인 메모리 엔진의 설계 전략 및 특성들을 적용하면 대부분의 RTO와 RPO 요구 사항을 충족시킬 수 있습니다.

** Reference : AWS <https://aws.amazon.com/ko/caching/>

---

<img width="877" alt="Screen Shot 2022-01-24 at 3 14 16 PM" src="https://user-images.githubusercontent.com/83699657/151742145-35cf4bce-cd64-404c-af74-1ebeff0712fe.png"> by AWS (01/24/2022)

- Answer : a, b, c
    - d. 은행 계정 잔액 : consistency가 가장 중요하기 때문에 캐시 저장은 좋지 않음 (캐시는 업데이트가 늦어지기 때문에 은행 잔고는 늦게 갱신되면 안됨)


---
#### Reference
AWS Certified Solutions Architect - Associate 2020 (PASS THE EXAM!), Youtube, uploaded by freeCodeCamp.org, 12/24/2019, 
<https://www.youtube.com/watch?v=Ia-UEYYR44s>