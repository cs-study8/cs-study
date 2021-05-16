# GET

`리소스 조회`를 위한 메서드. 서버에 전달하고 싶은 데이터는 query(쿼리 파라미터 or 쿼리 스트링)를 통해서 전달한다.

다음과 같은 형태
```HTTP
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

## 특징

* 리소스 조회가 목적이다.
* 데이터를 헤더에 쿼리 스트링으로 전달한다.
    * 따라서 대용량 데이터를 보내기에 적절하지 않으며 보안에도 취약하다. 
* POST 방식보다 빠르다.
    * 브라우저에 캐싱이 가능하기 때문에 같은 요청의 경우 서버로 보내지 않고 캐싱된 정보를 보내준다.
* Message Body를 사용하지 않는다.
    * 메시지 바디를 통해서 데이터를 전달할 수도 있다. 하지만 이를 지원하지 않는 서버가 많기 때문에 사용하지 않는 것이 좋다.
    

# POST

데이터 처리를 요청하기 위한 메서드. 클라이언트에서 데이터를 줄테니 서버가 처리해달라는 뜻.

예를 들어 새로운 멤버를 등록하고 싶은 경우

```HTTP
POST /members HTTP/1.1
Content-Type: application/json

{
    "username": "awesomeo184",
    "age": 50
}
```
위와 같이 요청을 보내면

서버에서 신규 리소스 식별자(예를 들어 members/100)를 생성한 후 다음과 같이 응답 데이터를 보낸다.

```HTTP
HTTP /1.1 201 Created
Content-Type: application/json
Content-Length: 34
Location: /members/100

{
    "username": "awesomeo184",
    "age": 50
}
```

## 특징
* 처리를 원하는 데이터를 메시지 바디에 전달한다.
    * 데이터 길이의 제한이 없다.
    * GET보다 보안상 안전하다(물론 중요한 정보는 추가적인 보안이 필요하다).

'처리' 한다는게 무슨 뜻일까? [HTTP 스펙](https://datatracker.ietf.org/doc/html/rfc7231#section-4.3.3) 을 보면 POST를 다음과 같은 기능에 사용한다고 소개하고 있다.

* HTML 폼에 입력된 데이터 블록을 처리할 때
* 블로그, 뉴스 등을 포스팅할 때(ex. 게시판 글쓰기, 댓글 달기)
* 서버가 아직 식별하지 않은 새 리소스를 생성할 때(ex. 신규 주문 생성)
* 기존 자원에 데이터를 추가할 때

즉 한마디로 딱히 정해진 것이 없다. 리소스 URI에 POST 요청이 오면 요청 데이터를 어떻게 처리할지는 리소스마다 따로 정해야 한다.


### 참고자료

김영한님 인프런 강의 - [모든 개발자를 위한 HTTP 웹 기본 지식](https://www.inflearn.com/course/http-%EC%9B%B9-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC/dashboard)
