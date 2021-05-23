# 1. REpresentational State Transfer

> 분산 하이퍼미디어 시스템을 위한 소프트웨어 아키텍처 스타일

- 아키텍처 스타일 : 제약조건의 집합

- 2000년 로이 필딩의 논문에서 소개된 개념
  - 기존 웹과 충돌/문제 없이 HTTP를 개선하기 위해 고안
  - 독립적 진화를 위해 적용
- 자원을 표현(URI)하고 상태 전달(HTTP Method)을 하는 아키텍처
- REST 아키텍처 스타일의 제약조건을 모두 만족하는 시스템을 RESTful하다고 한다



<hr>



# 2. REST의 제약조건(아키텍처 스타일)

> 1. Client - Server
> 2. Stateless
> 3. Cache
> 4. Uniform Interface
>    1. Identification of Resources
>    2. Manipulation of Resources through Representation
>    3. Self-Descriptive Messages
>    4. Hypermedia As The Engine Of Application State
> 5. Layered System
> 6. Code on Demand(Option)



## 2-1) Client - Server

- 클라이언트가 요청을 서버가 응답을하는 구조
- 서버는 API 제공과 비즈니스 로직을 처리하거나 저장
- 클라이언트는 사용자 인증이나 컨텍스트등을 관리
- 명확한 분리를 통해 각각의 역할에 집중할 수 있다



## 2-2) Stateless

- 클라이언트와 서버의 통신에는 상태가 없어야 한다 
- 모든 요청은 필요한 모든 정보를 담고 있어야 한다



## 2-3) Cache

- 클라이언트는 응답을 캐싱할 수 있어야 한다
- 잘 관리되는 캐싱은 클라이언트-서버 간 상호작용을 줄여 확장성과 성능을 향상시킨다



## 2-4) Uniform Interface

### 1. Identification of Resources

- 자원은 URI를 통해 유일하게 식별 가능해야한다

### 2. Manipulation of Resources through Representation

- Representation의 형태는 content-type으로 결정. 일관된 타입을 써야한다
  - text/html, application/xml, application/json 등
- HTTP Method를 통해 표현을 나타낸다
- 안전한 오퍼레이션과 그렇지 않은 오퍼레이션 간 강한 분리를 제공해야한다 
  - 일반적 서비스에서 60~80% 가량 트랜잭션이 조회이다
  - GET은 얼마든지 호출해도 같은 결과를 내므로 캐싱이 가능하다 

### 3. Self-Descriptive Messages

- 메시지는 요청 작업을 완료할 수 있도록, 응답을 이해할 수 있도록 충분한 정보들을 HTTP Method, Status Code, Header 등을 활요하여 전달 해야한다 

### 4. Hypermedia As The Engine Of Application State

- HATEOAS로 자주 부른다
- 클라이언트가 서버로부터 어떠한 요청을 할 때, 요청에 필요한 URI를 응답에 포함시켜 반환하는 것
- 애플리케이션의 상태는 Hyperlink를 이용해 전이되어야한다
- 예) 예약 성공 시 예약 취소/ 시간 변경 같은 다른 URI를 클라이언트가 사용 가능하도록 응답 body에 포함
- 요청 URI가 변경되어도 서버에서 동적으로 URI를 생성하기 때문에 클라이언트에서 코드를 변경할 필요가 없다



## 2-5) Layered System

- 계층으로 구성이 가능해야한다
- 클라이언트 입장에서는 서버만 호출
- 서버는 다중 계층으로 구성 가능
  - 비즈니스 로직 수행 서버, 암호화, 로드밸런싱 계층추가
  - 프록시, 게이트웨이 같은 중간 매체 사용 



## 2-6) Code on Demand (Option)

- 서버가 네트워크를 통해 클라이언트에 프로그램을 전달하면 이를 클라이언트에서 실행할 수 있어야한다. ie) Javascript



<hr>



# 3. RESTful 해야하는 이유

- 독립적 진화를 위해 RESTful 해야한다!!
- REST API라고 부르면서 Uniform Interface 제약조건을 만족하지 못하는 경우가 많다



## 3-1) self-descriptive messages

> 서버나 클라가 변경되어도 메시지는 언제나 self-descriptive 하므로 해석이 가능하다

잘못된 예

```
GET / HTTP/1.1  # 목적지가 지정되지 않음


HTTP/1.1 200 OK  # body 표현 방법을 알 수 없음
[ { "op": "remove", "path": "/a/b/c" } ]
```

옳은 예

```
GET / HTTP/1.1
Host: www.example.org


HTTP/1.1 200 OK
Content-Type: application/json-patch+json
[ { "op": "remove", "path": "/a/b/c" } ]
```



## 3-2) HATEOAS

> 애플리케이션 상태 전이의 late binding. 상태 전이가 완료되고 나서야 다음 전이될 수 있는 상태가 결정된다. 덕분에 링크는 동적으로 변경될 수 있다.

```
HTTP/1.1 200 OK
Content-Type: text/html

<html>
<head></head>
<body><a href="/test">test</a></body>
</html>


HTTP/1.1 200 OK
Content-Type: application/json
Link: </articles/1>; rel="previous",
      </articles/3>; rel="next";
      
{
    "title": "2nd article",
    "contents": "..."
}
```



<hr>



# 4. RESTful

- 모든 제약조건을 만족해야한다
- 모든 원격 API가 REST API일 필요는 없다
  - 시스템 통제가 가능하거나 독립적 진화가 필요 없다면 필요없다



## 4-1) REST API가 잘 안되는 이유

- media-type

|            | 웹 페이지 | HTTP API  |
| :--------- | :-------: | :-------: |
| 프로토콜   |   HTTP    |   HTTP    |
| 통신       | 사람-기계 | 기계-기계 |
| Media Type | **HTML**  | **JSON**  |

HTML은 a태그로 하이퍼링크를 통해 다음 상태로 전이될 수 있고 HTML에 대한 명세가 존재한다. 하지만 JSON은 최소한의 파싱법만 존재한다.

|                  | HTML | JSON |
| :--------------- | :--: | :--: |
| Self-descriptive |  ✔️   |  ✖️   |
| HATEOAS          |  ✔️   |  ✖️   |



## 4-2) Restful 하게 만들기

### Self-descriptive

- **방법 1. Media Type**
  - Media type을 정의하고 문서를 작성한다
  - IANA에 미디어 타입을 등록한다
  
```
HTTP/1.1 200 OK
Content-Type: application/vnd.todos+json

[
    {"id": 1, "title": "회사 가기"},
    {"id": 2, "title": "집에 가기"}
]

```

- **방법 2. Profile**
  - 명세를 작성하고 Link 헤더에 profile relation으로 링크한다 
```
HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

[
    {"id": 1, "title": "회사 가기"},
    {"id": 2, "title": "집에 가기"}
]
```

### HATEOAS

- **방법 1. data**
  - 다양한 방법으로 json 데이터 내에 하이퍼링크를 추가한다

예1)
```
HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

[
  {
    "link": "https://example.org/todos/1",
    "title": "회사 가기"
  },
  {
    "link": "https://example.org/todos/2",
    "title": "집에 가기"
  }
]
```
예2)
```
HTTP/1.1 200 OK
Content-Type: application/json
Link: <https://example.org/docs/todos>; rel="profile"

{
  "links": {
    "todo": "https://example.org/todos/{id}"
  },
  "data": [{
    "id": 1,
    "title": "회사 가기"
  }, {
    "id": 2,
    "title": "집에 가기"
  }]
}
```


- **방법 2. HTTP 헤더**
  - Link, Location 등의 헤더로 링크를 표현한다
```
HTTP/1.1 204 No Content
Location: /todos/1
Link: </todos/>; rel="collection"
```

