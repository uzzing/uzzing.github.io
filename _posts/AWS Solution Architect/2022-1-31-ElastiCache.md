---
title:  "[AWS Solution Architect] ElastiCache"
date: 2022-1-31 2:32PM
excerpt: "aws"

author: Yuha
categories: [Development, AWS]
tags: [aws, certification, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-1-31 2:32PM
---

## ElastiCache 

- Introduction
- Caching Comparison

<img width="1440" alt="Screen Shot 2022-01-31 at 2 17 38 PM" src="https://user-images.githubusercontent.com/83699657/151743706-1adadcd0-26df-4043-877d-c49184aed730.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 2 18 38 PM" src="https://user-images.githubusercontent.com/83699657/151743719-af686ddc-3340-41ba-9832-b043884d7b8b.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 2 19 43 PM" src="https://user-images.githubusercontent.com/83699657/151743723-b1ac6398-5381-4aec-87a1-8cb4fa13b392.png">
<img width="1440" alt="Screen Shot 2022-01-31 at 2 21 17 PM" src="https://user-images.githubusercontent.com/83699657/151743727-babca8ec-4725-41ba-afc7-078a4acf89b8.png">



---

<img width="877" alt="Screen Shot 2022-01-24 at 3 11 16 PM" src="https://user-images.githubusercontent.com/83699657/151743143-eb49164d-6c68-4b22-baaa-f250ba3f184d.png">

- 같은 vpc안에 있는 리소스에만 접근 가능
- 걸리는 부하를 줄이기 위해서 반복되는 쿼리가 날려질 때, 매번 DB에서 가져오는 게 아니라, <b>가운데에 ElastiCache를 놓고 동일한 쿼리가 날려지는 경우, 이전에 동일한 쿼리의 캐시가 있으면 그 결과를 보내줌. 없으면 DB로 가서 결과를 가져옴.</b>

<img width="875" alt="Screen Shot 2022-01-24 at 3 11 58 PM" src="https://user-images.githubusercontent.com/83699657/151743146-0baa1e56-08b7-434f-992b-36cfcb185e86.png">

- <b>Memcached</b>
    - multi core를 가지고 있는 시스템에서 빠른 성능 제공
    - 기능은 단촐한 대신, <b>속도와 안정성</b>이 뛰어남 
    - key-value만 지원
- <b>Redis</b>
    - 지속성 : reboot하더라도 데이터가 남아있을 수 있음
    - 원자 조작 : 데이터를 업데이트 시킬 때
    - pub/sub 기능으로 데이터를 메세지로 보냄
    - 클러스터 모드 : 여러개의 shard에 데이터가 중복되어서 저장되게 해서 <b>high durability, performance</b>

    

<img width="880" alt="Screen Shot 2022-01-24 at 3 15 21 PM" src="https://user-images.githubusercontent.com/83699657/151743160-451077d0-4164-4ef2-a715-3b2f2446a838.png">

- Answer : b, c

---

<img width="1068" alt="Screen Shot 2022-01-31 at 2 05 48 PM" src="https://user-images.githubusercontent.com/83699657/151742116-3a2d5b5d-d57e-41b9-b4cd-1acc8b5907bf.png">

- caching 
    : 일반적으로 RAM(Random Access Memory)과 같이 빠르게 액세스할 수 있는 하드웨어에 저장

- 캐시 계층을 구현할 때는 <b>캐싱되는 데이터의 유효성을 이해하는 것이 중요</b>합니다. <b>성공적인 캐시</b>는 높은 적중률로 이어집니다. 즉, <b>가져온 데이터가 캐시에 존재합니다.</b> 가져온 데이터가 캐시에 존재하지 않을 때 캐시 비적중이 발생합니다.
    - <b>TTL(Time To Live)</b>과 같은 제어 항목을 적용하여 이에 따라 <b>데이터를 만료</b>되도록 할 수 있습니다. 
- 다른 고려 사항은 <b>캐시 환경이 고가용성</b>이어야 할 필요가 있는지 여부인데, 
    - 이는 <b>Redis와 같은 인 메모리 엔진</b>을 사용하여 충족할 수 있습니다. 
    - 기본 위치에서 데이터를 캐싱하는 것과는 달리, 경우에 따라 인 메모리 계층을 <b>독립형 데이터 스토리지 계층</b>으로 사용할 수 있습니다. 이 시나리오에서는 인 메모리 엔진에 상주하는 데이터에 대해 적절한 <b>RTO</b>(복구 목표 시간 – 가동 중단으로부터 복구하는 데 걸리는 시간)와 <b>RPO</b>(목표 복구 시점 – 복구 시 캡처된 최종 시점 또는 트랜잭션)를 정의하여 이것이 적합한지를 파악하는 것이 중요합니다. 다른 인 메모리 엔진의 설계 전략 및 특성들을 적용하면 대부분의 RTO와 RPO 요구 사항을 충족시킬 수 있습니다.

** Reference : AWS <https://aws.amazon.com/ko/caching/>

---


---
#### Reference
AWS Certified Solutions Architect - Associate 2020 (PASS THE EXAM!), Youtube, uploaded by freeCodeCamp.org, 12/24/2019, 
<https://www.youtube.com/watch?v=Ia-UEYYR44s>