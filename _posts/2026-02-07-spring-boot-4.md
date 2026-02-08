---
title: Spring Boot 4.0
date: 2026-02-07 15:22 +000
categories: [BE, Spring]
tags: [SpringBoot]
---


# Spring Boot 4.0 
> Release Note: https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-4.0-Release-Notes

## Upgrading from Spring Boot 3.5 

기존 하위 버전을 사용중이었다면 우선 3.5로 먼저 업그레이드 후 순차적으로 마이그레이션을 추천 


## Gradle 9
`Gradle 9` 지원. 기존 Gradle 8.x (8.14 or later) 도 지원 유지.


## HTTP Service Clients

> [HTTP Service Interface Clients](https://docs.spring.io/spring-boot/4.0-SNAPSHOT/reference/io/rest-client.html#io.rest-client.httpservice)

HTTP 클라이언트 Auto-configuration/설정 기능 제공. HTTP Service Client 를 사용해서 interface 로 구현  
아마도 외부 API 호출을 복잡하고 반복적인 RestTemplate 이나 WebClient, FeignClient 를 대체하고, 간단하게 구현할 수 있을 것으로 보임

```java
@HttpExchange(url = "https://echo.zuplo.io")
public interface EchoService {

  @PostExchange
  Map<?, ?> echo(@RequestBody Map<String, String> message);

}
```


## API Versioning

> [Spring MVC API Versioning](https://docs.spring.io/spring-boot/4.0-SNAPSHOT/reference/web/servlet.html#web.servlet.spring-mvc.api-versioning)  
> [Spring Webflux API Versioning](https://docs.spring.io/spring-boot/4.0-SNAPSHOT/reference/web/reactive.html#web.reactive.webflux.api-versioning)

API 버전 관리 Auto-configuration 지원 (Spring MVC, Spring WebFlux)
- properties 로 간단하게 설정 : `spring.mvc.apiversion.*` or `spring.webflux.apiversion.*`
- 혹은 고급제어를 위해 다음 Bean 을 정의해서 사용 : `ApiVersionResolver`, `ApiVersionParser`, `ApiVersionDeprecationHandler`


## JmsClient
> [JmsClient](https://docs.spring.io/spring-framework/docs/7.0.x-SNAPSHOT/javadoc-api/org/springframework/jms/core/JmsClient.html)

JMS auto-configuration 에 JmsClient API 지원 포함. JmsTemplate, JmsMessagingTemplate 에 대한 지원은 기존 유지  

JMS 가 뭔지 몰랐어서 간단 내용 정리

### JMS (Java Message Service) 
- Java application 간 비동기 메세징 API
- [jms](https://docs.spring.io/spring-framework/reference/integration/jms.html)
- Kafka 는 JMS 가 아닌듯함 


