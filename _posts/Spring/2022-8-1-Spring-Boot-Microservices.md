---
title:  "[Spring] Microservices in Spring Boot"
date: 2022-7-29 3:02PM
excerpt: "spring"

author: Yuha
categories: [Development, Spring]
tags: [spring, eng]

#toc: true
#toc_sticky: true
 
last_modified_at: 2022-8-1 3:05PM
---

# How to communicate microservices 
- @FeignClient (ApiClient)
- Kafka (Use Event)
- RestTemplate (communicate with REST API)
- Circuit Breaker (Fault Tolerant Design Pattern)

---

# Spring Cloud
a framework for building robust cloud(strong and healthy) applications. (= microservices)

## Spring Cloud Stream

A lightweight <b>event-driven</b> microservices framework to quickly build applications that can connect to external systems.
Simple declarative model to send and receive messages using <b>Apache Kafka(middleware)</b> or RabbitMQ
between Spring Boot apps.

---

# @FeignClient
- Microservices communication method in Spring Boot
- @EnableFeignClients 

user-service
## build.gradle
```java
dependencies {
    implementation group: 'org.springframework.cloud', name: 'spring-cloud-starter-openfeign', version: '2.1.1.RELEASE'
}
```

### user-service
```java
@EnableFeignClients
public class ApiClientConfiguration {
    ...
}
```

### departments-service
```java
@FeignClient(name = "user", contextId = "userEnvironmentSetting", url = "${...}")
@RequestMapping(path="/users", consumes = "application/json")
interface UserEnvironmentSettingClient {

    @Override
    @GetMapping("/users/environmentSetting")
    Map<String, String> getEnvironmentSetting();
}
```
- name : LoadBalancer client name
- contextId : bean name instead of name if present
    - issue : 동일 name 으로 두개의 class 에서 지정하면 오류 발생



- reference: <https://techblog.woowahan.com/2630/>

---

# RestTemplate
- Spring Http communication template (Rest API 서비스를 요청 후 응답받을 때 주로  사용)
- For communiating over the microservices
- Synchronize (Async : org.springframework.web.client.AsyncRestTemplate)
- will be deprecated

## build.gradle
```java
implementation 'org.springframework.boot:spring-boot-starter-web'
```

## RestTemplate VS WebCLient

||RestTemplate|WebCLient|
|:---:|:---:|:---:|
||Sync|Async (= AsyncRestTemplate)|
|Dependency|implementation <br> 'org.springframework.boot:spring-boot-starter-web'|implementation <br> 'org.springframework.boot:spring-boot-starter-webflux'|

- reference
<https://backtony.github.io/spring/2021-07-12-spring-basic-8/>
<br>
<https://blog.naver.com/hj_kim97/222295259904> 
<br>
<https://sjh836.tistory.com/141>

## Blocking VS Non-Blocking VS Sync VS Async
- Blocking / Non-blocking 
: 다른 주체가 작업할 때 자신에게 자신의 작업에 대한 제어권이 있는지 없는지

||Blocking|Non-blocking|
|:---:|:---:|:---:|
||호출된 함수가 자신의 작업을 모두 마칠 때까지 <br> 호출한 함수에게 제어권을 넘겨주지 않고 대기하게 만든다면 <br> (executes "in series")|호출된 함수가 바로 리턴해서<br>  호출한 함수에게 제어권을 넘겨주고, <br> 호출한 함수가 다른 일을 할 수 있는 기회를 줄 수 있으면 <br> (executes in parallel)|
|Example|직원이 상사에게 서류를 제출하고, <br> 상사가 서류를 다 읽을 때까지 자리에서 기다리는 상황|직원이 상사에게 서류를 제출했지만, <br> 상사가 서류를 다 읽어볼 동안 자리에 가서 자신의 일을 처리하는 상황|


- Sync / Async
: 그것을 요청한 순서가 지켜지는가 아닌가 (호출되는 함수의 작업 완료 여부를 누가 신경쓰냐)


||Synchronous|Asynchronous|
|:---:|:---:|:---:|
||작업을 동시에 수행하거나, 동시에 끝나거나, 끝나는 동시에 시작함 <br> (결과를 리턴받았을 때 바로 그 결과에 집중함 / scheduled, real-time)|시작, 종료가 일치하지 않으며 끝나는 동시에 시작을 하지 않음 <br> (결과를 바로 처리하지 않아도 됨 / on your own time, no need schedule / use callback)|
||When a work is requested, <br> the result value of the request is `directly` returned.|When a work is requested, <br> the result value of the request is `indirectly` received|
||요청을 보낸 후 응답을 받아야지만 다음 동작이 이루어짐|웹 페이지 전체를 새로고침 하지않고 데이터를 불러오는 방식|
||비동기 방식에 비해 설계가 매우 간단하고 직관적이지만 <br> <b>결과가 주어질 때 까지 아무 것도 못하고 대기해야함</b>|비동기 방식을 이용할 경우, 필요한 부분의 데이터만 불러와 사용 가능. <br> 결과가 주어지는데 시간이 걸리더라도 <br> 그 시간동안 다른 작업을 할 수 있으므로 <b>자원의 효율적 사용 가능</b>|
|**Example**|상사가 서류를 다 읽고 결과를 리턴해주면 <br> 직원은 바로 그 결과에 관심을 갖게 됩니다.| 상사가 리턴한 결과를 바로 처리할지, <br> 나중에 처리할지를 결정할 수 있습니다. |



- common used : sync-blocking, sync-nonblocking, async-nonblocking (most efficient)
![img (1)](https://user-images.githubusercontent.com/83699657/181702149-5b6923f5-cb06-4e5b-8688-68b96a781fc9.png)

- reference
<https://studyandwrite.tistory.com/486>
<br>
<https://baek-kim-dev.site/38>


---

# CircuitBreaker (Design pattern using netfilx hystrix)
- Hystrix
: library form Netflix (spring-cloud-starter-netflix), isolates the points of access between the services, stops cascading failures across thhem and provides the fallback options
     - Fallback 
    : provides an alternative solution during a service request failure
- Circuit Breaker Pattern
: <b>prevents failure</b> cascading and gives a default behavior when services fail
  - Netflix Hystrix
    : allows us to introduce fault tolerance and latency tolerance by isolating failure and by preventing them from cascading into the other part of the system building a more robust distributed application.


<img width="731" alt="Screen Shot 2022-08-01 at 2 02 28 PM" src="https://user-images.githubusercontent.com/83699657/182075856-a4357993-4c62-4ad8-8188-c407fabf6ce9.png">


<img width="716" alt="Screen Shot 2022-08-01 at 2 01 15 PM" src="https://user-images.githubusercontent.com/83699657/182075727-1e77e44f-b617-439b-8960-37e23fa4d848.png">


```java
@Service
public class GreetingService {

    @HystrixCommand(fallbackMethod = "defaultGreeting")
    public String getGreeting(String username) {
        return new RestTemplate()
          .getForObject("http://localhost:9090/greeting/{username}", 
          String.class, username);
    }
 
    private String defaultGreeting(String username) {
        return "Hello User!";
    }
}
```

- @EnableCircuitBreaker
: will scan the classpath for any compatible Circuit Breaker implementation.

```java
@SpringBootApplication
@EnableCircuitBreaker
public class RestConsumerApplication {
    public static void main(String[] args) {
        SpringApplication.run(RestConsumerApplication.class, args);
    }
}
```

## Hystrix VS Resilience4J

-  common feature : fault tolerant library

|Hystrix|Resilience4J|
|:---:|:---:|
|embraces an Object-Oriented design <br> where calls to external systems have to be wrapped in a HystrixCommand <br> offering multiple functionalities.|relies on function composition <br> to let you stack the specific decorators you need.|

<img width="683" alt="Screen Shot 2022-08-01 at 11 10 27 AM" src="https://user-images.githubusercontent.com/83699657/182059121-bc791208-47a0-4f7b-a216-a22d595469d6.png">


- reference 
<https://engineering.linecorp.com/ko/blog/circuit-breakers-for-distributed-services/> <br>
<https://www.baeldung.com/spring-cloud-netflix-hystrix> <br>
<https://digitalvarys.com/what-is-circuit-breaker-design-pattern/>

---

# API Gateway (Load balancing)
Service : Cloud-gateway


## spring-cloud-starter-gateway
## bulid.gradle
```java
dependencies {
    compile 'org.springframework.cloud:spring-cloud-starter-gateway:2.1.0.RELEASE'
}
```

## application.yml
```java
server:
    port: 9191

spring:
  cloud:
    gateway:
      routes:
        - id: USER-SERVICE
          url: ${cloud-gateway.user-url}
          predicates:
            - Path=/users/ **
        - id: DEPARTMENT-SERVICE
          url: ${cloud-gateway.department-url}
          predicates:
            - Path=/departments/ **
          filter:
            - name: CircuitBreaker
              args:
                name: USER-SERVICE
                fallbackuri: forward:/userServiceFallBack

cloud-gateway:
    user-url: http://cloud-user-service:9001
    department-url: http://cloud-department-service:9002
```
Meaning:
- when you call <b>http://localhost:9191/users/1</b>, it goes to http://localhost:9001/users/1

- when you call <b>http://localhost:9191/departments/1</b>, it goes to http://localhost:9002/departments/1





- reference : <https://cloud.spring.io/spring-cloud-gateway/reference/html/#configuration>

# Spring-boot-starter-actuator
## bulid.gradle
```java
dependencies { 
  compile("org.springframework.boot:spring-boot-starter-actuator")
}
```

## application.yml
From spring boot 2.x, you have to custom `management` part in application.yml because the default setting is not exposing most datas.
```java
management:
  endpoints:
    web:
      exposure:
        include: health
```
Meaning : expose the `health` information

```java
management:
    endpoints:
        web:
            exposure:
                exclude: env, beans
```
Meaning : expose the information except for env, beans

the property `exclude` is prior than `include`, so if you declared some information on exclude, you can't see it even if you declared that on include.

- reference : <https://jeong-pro.tistory.com/160>




---

# Spring Cloud Stream
- 이벤트 중심 microservcie를 구축하기 위한 프레임워크
- Apache Kafka 또는 RabbitMQ 등을 사용하여 Spring Boot 어플리케이션과 메세지를 보내고 받음.

<https://saramin.github.io/2019-08-28-2/>



---
# Eureke Client

- reference : <https://www.baeldung.com/spring-cloud-netflix-eureka>