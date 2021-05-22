# REST

REST API가 무엇인지 알아본다. 비바 리퍼블리카 이응준 개발자님이 Naver DEVIEW에서 강연하신 내용을 듣고 요약했으며, 일부 예제는 김영한님의 HTTP 강의를 참고했다.
해당 자료에 대한 링크는 포스트 하단에 명시했다.

# REST API란 무엇인가

REST(REpresentational State Transfer)는 로이 필딩(Roy Fielding)이 '어떻게하면 웹을 망가뜨리지 않으면서 HTTP를 개선할 수 있을까'에 대한
고민을 하며 제안한 "분산 하이퍼미디어 시스템(ex.웹)을 위한 아키텍쳐 스타일"이다. 2000년에 [자신의 박사 논문](https://www.ics.uci.edu/~fielding/pubs/dissertation/fielding_dissertation.pdf) 에서 REST를 처음으로 제안하였다.

**즉 REST API란 이 REST 아키텍쳐 스타일을 따르는 API를 말한다.** 

아키텍쳐 스타일은 **제약 조건의 집합**이다. REST는 하이브리드 아키텍쳐라고도 불리는데, 이는 REST가 **아키텍쳐 스타일의 집합**이기 때문이다.

REST는 다음 여섯 가지의 아키텍쳐 스타일의 집합이다. 아래 여섯 가지 아키텍쳐 스타일을 모두 지켜야 RESTful하다고 할 수 있다.

1. Client-Server: 서버와 클라이언트가 서로간에 어떤 의존성도 없이 각각 독립적으로 진화할 수 있어야한다.

2. Stateless: 서버는 최근 HTTP 요청에 대한 어떠한 것도 저장하지 않는다. 만약 클라이언트 어플리케이션이 유저가 로그인해서 다른 인증이 필요한 동작들을
수행할 수 있기를 원한다면, 클라이언트 쪽에서 해당 정보를 모두 포함해서 요청을 보내야한다.

3. Cacheable: 캐시 가능해야한다. 모든 서버 응답은 캐싱이 될 수 있는지 아닌지를 명시적 혹은 묵시적으로 표현해야한다.

4. Layered system: 계층적으로 구성 가능해야하며, 각 레이어의 구성요소는 인접한 레이어를 넘어서는 레이어는 볼 수 없어야한다.

5. Uniform interface: 구성요소(클라이언트, 서버 등) 사이의 인터페이스는 균일(uniform)해야한다. 인터페이스를 일반화함으로써, 전체 시스템 아키텍처가 단순해지고, 상호작용의 가시성이 개선되며, 구현과 서비스가 분리되므로 독립적인 진화가 가능해진다.

6. Code on demand(optional): 이 제약은 선택적이다. 서버에서 생성한 코드가 클라이언트에서 실행가능해야 한다(ex. 자바스크립트).

# Uniform interface

HTTP만 잘 따라도 Uniform interface를 제외한 다른 제약 조건들은 대부분 만족시킬 수 있다. 

대부분의 API들이 REST를 만족하지 못하는 것은 Uniform interface의 제약 조건을 만족하지 못하기 때문이다. 

Uniform interface도 아키텍쳐 스타일이기 때문에 여러 제약 조건들로 이루어져있는데, 다음과 같다.

* identification of resources: 리소스가 URI로 식별되어야 한다.
* manipulation of resources through representations: 리소스를 조작(CRUD)할 때 HTTP 메시지에 해당 내용을 담아서 보내야한다.
* self-descriptive messages: 메시지는 스스로를 설명해야한다.
* hypermedia as the engine of application state(HATEOAS): 애플리케이션의 상태는 하이퍼링크로 전이되어야 한다.

## Identification of resources

회원 정보 관리 API를 만든다고 해보자. 다음과 같은 요구사항이 정의되어 있다.

* 회원 목록 조회
* 회원 조회
* 회원 등록
* 회원 수정
* 회원 삭제

위 요구조건에 따른 API URI를 다음과 같이 설계했다.

* 회원 목록 조회: /read-member-list
* 회원 조회: /read-member-by-id
* 회원 등록: /create-member
* 회원 수정: /update-member
* 회원 삭제: /delete-member

<br>

위 API URI는 첫 번째 제약 조건을 만족시키는가? 즉 URI로 리소스 식별이 가능한가? 아니다.

위 예제에서 리소스는 '회원'이다. **회원을 조회하고 등록하고 수정하고 삭제하는게 리소스가 아니다.**
위 설계의 문제점은 URI가 회원을 식별하는게 아니라 조회, 등록, 수정, 삭제같이 리소스에 대한 조작 행위를 식별하고 있다.

즉 위 설계를 `identification of resources` 제약 조건을 만족하도록 바꾸면 다음과 같다.

* 회원 목록 조회: /members
* 회원 조회: /members/{id}
* 회원 등록: /members
* 회원 수정: /members/{id}
* 회원 삭제: /members/{id}

위 URI는 오로지 '회원'이라는 리소스만 식별하고 있다. /members는 회원 전체 집합을, 나머지는 {id}를 추가해서 단일 회원을 식별한다.

그런데 회원 조회, 등록, 수정, 삭제는 URI가 모두 같다. 리소스 조작(manipulation of resources)에 대한 정보는 HTTP 메서드를 이용한다.

## Manipulation of resources through representations

HTTP 메서드를 통해 HTTP 메시지에 해당 리소스에 대해 어떤 조작을 하는지 명시한다.

회원 조회
```HTTP
GET /members/100 HTTP/1.1
Host: localhost:8080

```

<br>

회원 등록
```HTTP
POST /members HTTP/1.1
Content-Type: application/json

{
    "username": "kim",
    "age": 20
}
```

<br>

회원 수정
```HTTP
PATCH /member/100 HTTP/1.1
Content-Type: application/json

{
    "age": 25
}
```

> 수정에는 PUT 또는 PATCH를 사용할 수 있는데, PUT의 경우 해당 리소스가 존재하지 않으면 새로 생성하고 리소스가 존재하면
> 리소스를 완전히 대치한다. 위 예시에서 만약 메서드만 PUT으로 바꾸면 /member/100은 username이 날아가고 age 정보만 남게된다.

<br>

회원 삭제
```HTTP
DELETE /member/100 HTTP/1.1
Host: localhost:8080

```

## Self-descriptive messages

메시지는 스스로를 설명해야한다. 즉 HTTP 메시지만 보고도 해당 메시지가 무엇을 하려는건지 정확히 알 수 있어야한다. 

다음과 같은 HTTP 요청 메시지가 있다고 해보자

```HTTP
GET / HTTP/1.1

```
위 메시지는 self-descriptive한가? 루트에 대한 정보를 조회하려는 것 같은데 어떤 루트에 대한 것인지 명시되어 있지 않다. 따라서
다음과 같이 Host 헤더를 추가해줘야 self-descriptive해진다.

```HTTP
GET / HTTP/1.1
Host: www.example.org

```
이제 이 메시지를 보면 '아 www.example.org의 루트 경로에 대한 정보를 조회하려는 것이구나'하고 해석할 수 있다.

<br>

또 다른 예로 다음과 같은 HTTP 응답 메시지가 있다고 해보자.

```HTTP
HTTP/1.1 200 OK

[ { "op": "remove", "path": "/a/b/c" } ]

```

요청이 성공한 것 같긴한데, 메시지 바디에 담긴 정보가 무엇인지 알 수 없다. 따라서 다음과 같이 컨텐트 타입을 명시해줘야 한다.

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json

[ { "op": "remove", "path": "/a/b/c" } ]
```

이제 메시지 바디의 정보가 json 타입인 걸 알 수 있으니 파싱이 가능하다. 그런데 이것만으로는 부족하다. json 메시지인건 알겠는데,
"op"가 뭔지, "path"는 무얼 의미하는지 알 수 없다. 따라서 self-descriptive해지려면 정보를 더 추가해야한다.

```HTTP
HTTP/1.1 200 OK
Content-Type: application/json-patch+json

[ { "op": "remove", "path": "/a/b/c" } ]
```
이제 클라이언트는 json-patch+json이라는 명세를 찾아보고 해당 메시지를 정확하게 이해할 수 있다.

## HATEOAS

HATEOAS는 애플리케이션의 상태가 항상 Hyperlink를 통해서 전이되어야 한다는 제약조건이다.

![image](https://user-images.githubusercontent.com/63030569/119233675-21e9e600-bb65-11eb-8e7d-ddd03a934070.png)

HTML은 a tag의 하이퍼링크를 통해 다음 상태로 전이가 가능하다.
```HTTP
HTTP/1.1 200 OK 
Content-Type: text/html 

<html> 
<head></head> 
<body><a href="/test">test</a></body> 
</html>
```

<br>

json으로도 HATEOAS를 만족할 수 있다.
```HTTP
HTTP/1.1 200 OK
Content-Type: application.json 
Link : </articles/1>; rel="previous", 
       </articles/3>; rel="next"; 
       
{ "title" : "The second article", "contents" : "blah blah ..." }
```
Link 헤더를 통해 이전 게시물과 다음 게시물의 URI를 표현하고 있다. Link 헤더는 이미 표준으로 명세가 되어있기 때문에 이 메시지를 받은 클라이언트는
온전히 이 메시지를 해석해서 하이퍼링크를 타고 다른 상태로 전이할 수 있다.

# REST를 꼭 따라야하는가

앞서 말했듯이 6가지 아키텍쳐 스타일을 모두 따르는 API가 REST API이다. 근데 대부분의 HTTP API들이 자신이 REST API라고 말하면서도
Uniform interface의 self-descriptive messages와 HATEOAS 제약조건을 만족하지 못하고 있다.

그럼 꼭 저 두 제약 조건을 따라야하는가? 이를 위해 왜 self-descriptive messages와 HATEOAS가 필요한지 먼저 알아보자.

## 독립적인 진화

Uniform interface는 서버와 클라이언트의 독립적인 진화를 위해서 필요한 조건이다.

* 서버나 클라이언트가 변경되더라도 오고가는 메시지가 항상 self-descriptive하다면 해석하는데 아무런 문제가 없다.
* HATEOAS는 애플리케이션 상태 전이의 late binding을 가능하게 한다. 즉 어떤 상태로 전이되고 나서야 그 다음 전이될 수 있는 상태가 결정된다.
따라서 서버가 링크를 바꾸더라고 클라이언트는 바뀐 링크를 보고 따라가기만 하면된다.
  
<br>

## 결론

REST는 긴 시간에 걸쳐 진화하는 웹을 위해 만들어진 아키텍쳐이다. 

REST API는 REST의 여섯 가지 아키텍쳐 스타일을 모두 만족하는 API를 말한다.

많은 API들이 REST를 따르고 있다고 말하지만 주로 Uniform interface의 self-descriptive messages와 HATEOAS를 만족하지 못하고 있다. 

실제로 저 두가지 조건을 만족시키는 것에는 큰 비용이 따른다. 따라서 API 개발자들은 각자 상황에 따라서 REST를 따를지 말지를 판단해야 한다.

<br>

### 참고 자료

Naver DEVIEW, 이응준님 강연 - [그런 REST API로 괜찮은가?](https://www.youtube.com/watch?v=RP_f5dMoHFc&t=2s)

이응준님 블로그 - [바쁜 개발자들을 위한 REST 논문 요약](https://blog.npcode.com/2017/03/02/%EB%B0%94%EC%81%9C-%EA%B0%9C%EB%B0%9C%EC%9E%90%EB%93%A4%EC%9D%84-%EC%9C%84%ED%95%9C-rest-%EB%85%BC%EB%AC%B8-%EC%9A%94%EC%95%BD/)

김영한님 인프런 강의 - [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)

https://restfulapi.net/

