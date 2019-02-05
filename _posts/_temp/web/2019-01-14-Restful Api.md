---
layout: temp
comments: true
categories: Web
tag : rest, restful, rest Api
---

# RESTFUL API - 리소스 지향적 아키텍쳐

## Rest Api 개념
![network.PNG](./../../assets/restapi.png)
> Rest하다는건 무슨 뜻일까?

    Rest란 웹에 존재하는 모든 자원(이미지, 동영상, DB 자원)에 고유한 URI를 부여해 활용하는 것으로, 자원을 정의하고 자원에 대한 주소를 지정하는 방법론이다.
    
    Rest Api는 Rest의 특징을 잘 지키면서 API를 제공하는 것을 이야기 한다.

> Rest 개념이 왜 대두되었을까?

    제일 큰 특징으로는 '애플리케이션 분리 및 통합', '다양한 클라이언트의 등장' 이다.
    - 애플리케이션 분리 및 통합
        애플리케이션의 복잡도가 증가하면서 애플리케이션을 어떻게 분리하고 통합하느냐가 주요 이슈가 되었고, 이에 SOA(Service Oriented Architecture)에 이어 MSA(Micro Service Architecture)와 함께 Rest가 떠오르고 있다.
    - 다양한 클라이언트의 등장
        모바일과 같은 다양한 클라이언트의 등장으로 Backend가 하나로 다양한 Device를 대응하기 위해 rest의 필요성이 증대되었다.

## 구조 살펴보기

    Rest의 구성
        - 자원 (Resource) - URI
        - 행위 (Verb) - Http Method
        - 표현 (Representation)

## Restful 이점

1. 직관적인 표현, 프론트엔드와 백엔드의 분리
    - View 영역이 포함되지 않은 서버 사이드 개발 진행
    - 플랫폼 종속적이지 않은 API 제공 가능

## Rest Api 특징

1. **유니폼 인터페이스(uniform Interface)**
    HTTP 표준에만 따른다면, 안드로이드/ios 플랫폼이든, 특정 언어나 기술에 종속되지 않고 모든 플랫폼에서 사용 가능하다.
2. **무상태성(Stateless)**
    HTTP는 Stateless Protocol 이므로, Rest 역시 무상태성을 갖는다. 즉, HttpSession과 같은 컹텍스트 저장소에 상태정보를 따로 저장하고 관리 하지 않고, API 서버는 들어오는 요청만을 단순 처리한다. 세션과 같은 처리를 하지 않기 때문에 구현이 단순해 진다.
3. **캐슁 가능 (Chacheable)**
    Http의 기존 웹 표준을 그대로 사용하여, 웹에서 사용하는 기존의 인프라를 그대로 활용 가능하다. HTTP 프로토콜 기반의 로드 밸런서나 SSL은 물론, HTTP가 가진 강력한 특징중 캐슁 기능을 적용할 수 있다. 네트워크 응답시간 뿐만 아니라, 자원 사용율을 비약적으로 향상 시킬 수 있다.
4. **자체 표현 구조 (self-destructive)**
    api 메세지 자체만 보고도 API를 이해할 수 있는 SELF-DESTRUCTIVE 구조를 가진다. 리소스와 메서드를 이용하여 어떤 메서드에 무슨 행위를 하는지를 알 수 있다.
5. **클라이언트 / 서버 구조 (client-Server Architecture)**
    Rest 서버는 API를 제공하고, 제공된 API를 이용하여 비지니스 로직 처리 및 저장을 책임진다. 서버사이드와 클라이언트 사이드가 명확하게 구별된다.
6. **계층형 구조 (Layered System)**
    서버는 다중 계층으로 구성될 수 있다. 순수 비지니스 로직을 수행하는 api 서버와 그 앞단에 사용자 인증, 암호화, 로드 밸런싱등을 하는 계층을 추가하여 구조상의 유연성을 둘 수 있다.
    
## Richardson Maturity Model (RMM)
![network.PNG](./../../assets/rmmrest.png)

## Rest Api 설계 가이드

### URI 구성은 직관적으로! 심플하게!
- 리소스는 **명사** 를 사용하여 표현
- / 을 사용하여 계층 표현 가능

### 자원에 대한 행위 정의
- 리소스에 대한 행위는 메소드가 되며, Get, Post, Put, Delete로 표현할 수 없는 동작은 URI와 문맥을 함께 구성한다.
- Self-descriptiveness 속성을 사용하여 rest uri와 메서드 그러고 쉽게 정의된 메시지 포멧에 의해 쉽게 API를 이해 할 수 있어야 한다.

### 에러 처리
- HTTP Response Code를 사용한 후, Response body에 error detail을 서술하는 것이 좋다. 

## Rest Api 단점
- 자원 중심의 설계가 선행 되어야 함.
- 무상태성을 지향하는 구조
    - 세션등 상태정보를 기반으로 정보 접근 권한을 부여하는 시스템에는 부합하지 않는 구조.
- 표쥰 규약이 없다.


참고
- http://bcho.tistory.com/953
- https://brainbackdoor.tistory.com/53
- https://www.slideshare.net/SangBaekLee3/restful-api-67239776?qid=9ecf9123-24e5-47ab-b4f9-48bbaa00c2a7&v=&b=&from_search=12
