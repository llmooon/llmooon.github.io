---
layout: post
comments: true
categories: Spring

---

# Spring security



## Spring Security 란?

> 스프링에서 사용하는 강력하고 고도로 커스터마이징 할 수 있는 인증과 접근 제어 프레임워크

스프링 시큐리티는 스프링 기반의 애플리케이션에선 보안에 대한 표준이라고 할수 있다. Java Application에 Authentictication(인증) 과 Authorization(인가) 를 제공하는데 초점을 맞추고 있다. 



### 인증 VS 인가

- 인증 : 시스템 접근 시, 등록된 사용자인지 여부를 확인하는것
- 인가 : 시스템 접근 후, 인증된 사용자에게 **권한** 을 부여하는것. 권한에 따라 사용 가능한 기능이 제한된다.



## Spring Security 구조



### 인증 관련 Architecture

![1548773216608](./../../assets/spring_security_authentication_architecture.png)

- AuthenticationManager
  - 사용자 비밀번호를 인증한다.
- ProviderManager
  - AuthenticationManager의 구현체
- AuthenticationProvider
  - 인증 구현을 Authentication Provider interface에 위임.
  - AuthenticationProvider의 authenticate 메소드에서 유저 비밀번호와 대조한다. 인증에 성공하면 Authentication 객체 리턴후 인증 종료한다.
- UserDetailsService
  - user가 로그인하면 UserDetailService의 loadByUserName으로 유저를 조회하여 AuthenticationProvider로 리턴.
  - 
- UserDetails
  - userDetails 에서 제공되는 메서드
    - ![1548773216608](./../../assets/spring_security_userdetailsservice.png)
  - 

##  인증 방법

### 1. HTTP 기본 인증

Basic authentication is often used with stateless clients which pass their credentials on each request. It’s quite common to use it in combination with form-based authentication where an application is used through both a browser-based user interface and as a web-service.





---

참고

- https://sjh836.tistory.com/165
- http://egloos.zum.com/springmvc/v/504862 (조금 더 읽어보기!)
- https://okky.kr/article/382738