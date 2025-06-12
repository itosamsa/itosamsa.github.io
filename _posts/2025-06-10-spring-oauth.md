---
title: OAuth2 소셜 로그인 
date: 2025-06-10 21:32 +000
categories: [SpringBoot, Security]
tags: [SpringBoot, SpringBootOauth2]
---



https://console.cloud.google.com > 프로젝트 생성 

API 및 서비스 > OAuth 동의 화면 > [시작하기] 

클라이언트 

- 승인된 리디렉션 URI 입력: `http://localhost:8080/login/oauth2/code/google`




spring

```kotlin
implementation("org.springframework.boot:spring-boot-starter-oauth2-client")
```

```yaml
spring:
  security:
    oauth2:
      client:
        registration:
          google:
            client-id: ${client-id}
            client-secret: ${client-secret}
```


config
```java
@Configuration
public class SecurityConfig {

  @Bean
  public SecurityFilterChain filterChain(HttpSecurity http) throws Exception{
    http.authorizeHttpRequests(authorizeRequests ->
            authorizeRequests.anyRequest().authenticated())
        .oauth2Login(Customizer.withDefaults());
    return http.build();
  }

}
```



