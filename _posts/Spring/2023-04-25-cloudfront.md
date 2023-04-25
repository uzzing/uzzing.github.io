---
title:  "[AWS] Cloudfront"
date: 2023-04-25 1:00PM
excerpt: "Dev"

author: Yuha
categories: [Development]
tags: [eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2023-04-25 1:00PM
---

# Cloudfront
- Edge Location을 활용해서 정적/동적 콘텐츠를 유저들에게 보다 빠르게 전달해주는 서비스
  - Edge Location : 콘텐츠가 캐시(Cache)되고 유저에게 제공하는 곳
  - 원리 : Cloudfront는 여러 나라의 Edge를 보유하고있음 >> 
    - 만약 요청 받은 컨텐츠가 Edge Location에 있다면 >> 바로 유저들에게 콘텐츠를 제공
    - 만약 요청 받은 컨텐츠가 Edge Location에 없다면 >> 가장 가까운 Edge에 접근하여, origin에서 정보를 제공받고, TTL(Time to Live)만큼 Edge Location에 캐싱 >> 유저들에게 콘텐츠를 제공 
      - Edge와 Origin 사이의 **데이터 전송의 지속적인 연결을 유지**하기에 콘텐츠 전송 속도의 향상이 증가됩니다.
  - origin  (ex. AWS service(EC2 Instance, S3 Bucket), On-Premise etc...)
    - static contents : S3 (캐싱으로 접근 속도 최적화)
    - dynamic contents : 네트워크 최적화, 연결 유지, Gzip 압축 등을 사용

## Content Delivery Network(CDN) 
- 만약 특정 웹 페이지를 서버에 요청할 때 현재 어디에서 불려지는지, 웹 페이지를 불러오려고 하는 사용자가 **어디에 거주하는지에 근거**하여 콘텐츠 웹 페이지에 전달해주는 **분산 네트워크**
- 대부분 CDN은 보통 정적/동적 컨텐츠를 분리해서 사용
  - 동적 컨텐츠는 App Server에서 구동되고, 그 안에 정적 컨텐츠는 CDN Server를 통해 End-Point를 구분지어 컨텐츠를 전달

- 정적 컨텐츠 파일
  - html, css, js, image, etc... (서버(EC2)가 필요하지 않은, 자주 바뀌지 않는 정적 파일들)
  - **여러 CDN Server에 올려** 사용자가 좀 더 빠르게 콘텐츠를 전달받을 수 있게 해준다.
  - origin : S3
    - S3에 넣어 호스팅하는것이 훨씬 저렴하게 먹힌다.
    - 수천, 수만명 사람들에게 한꺼번에 서비스 되어도 상관 없을 정도로 견고하기 때문에 따로 **오토스케일링이나 로드밸런서 작업이 필요없다.**

- 동적 컨텐츠
  - 서버가 필요한 콘텐츠 (Node.js 웹서버, PHP, Go, Python 등 서버에서 매번 바뀌는 컨텐츠, DB조회 등 ex. 로그인, 게시판)
  - 자주 변경되는 정보, 사용자가 보낸 요청에 포함된 요인에 따라 그 내용이 변경되는 컨텐츠
  - 정적 캐싱한다면 TTL 시간 동안 사용자는 새롭게 추가/수정된 데이터를 볼 수 없게 된다.


## Example
<img width="689" alt="Screen Shot 2023-04-25 at 10 55 02 AM" src="https://user-images.githubusercontent.com/83699657/234155465-c0656786-f438-441a-ac4e-94c220a16345.png">
서버(EC2)의 연산이 필요한 동적 콘텐츠의 요청을 EC2로 향하게 Distribution 처리하고 서버가 필요하지 않은 정적 콘텐츠는 S3 버킷 등으로  Distribution 처리하는 구성을 고려해볼 수 있다.

  - <https://blog.bespinglobal.com/post/cloudfront%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EC%BD%98%ED%85%90%EC%B8%A0-%EA%B0%80%EC%86%8D%ED%99%94%ED%95%98%EA%B8%B01/>


## Recommend
- 특별한 이유가 없는 한 Cloudfront를 **App Server 앞단**에 배치하여 보안 및 성능 증가를 권장한다. 또한 Cloudfront Traffic의 경우 사용량에 따라 비용을 절감하기를 바란다. (CloudFront의 경우 사용량에 따라 비용을 할인 받을 수 있다.)


- reference
  - <https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-S3-%EC%A0%95%EC%A0%81-%EC%9B%B9-%EC%82%AC%EC%9D%B4%ED%8A%B8-%ED%98%B8%EC%8A%A4%ED%8C%85-%EB%8F%84%EB%A9%94%EC%9D%B8-%EC%84%A4%EC%A0%95Route-53>
  - <https://medium.com/wizpace/aws-cloudfront%EB%A5%BC-%EC%82%AC%EC%9A%A9%ED%95%98%EC%97%AC-%EB%8F%99%EC%A0%81-%EC%BB%A8%ED%85%90%EC%B8%A0-%EC%A0%84%EC%86%A1%ED%95%98%EA%B8%B0-dynamic-content-delivery-c249da4b269b>
  - <https://overcome-the-limits.tistory.com/378>
  - <https://blog.leedoing.com/35>
  - <https://bosungtea9416.tistory.com/entry/AWS-CloudFront>
  - <https://velog.io/@ragnarok_code/Amazon-CloudFront%EB%9E%80>