---
layout: post
comments: true
categories: Spring

---

# Spring security



## Spring Security 란?

>  (+ 앞으로 더 추가하기)



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



---

참고

- https://sjh836.tistory.com/165