## **REST란**

---

1. **REST의 정의**

“Representational State Transfer” 의 약자
자원을 이름(자원의 표현)으로 구분하여 해당 자원의 상태(정보)를 주고 받는 모든 것을 의미한다. 즉, 자원(resource)의 표현(representation) 에 의한 상태 전달

  - **자원(resource)의 표현(representation)**
        자원: 해당 소프트웨어가 관리하는 모든 것
             -> Ex) 문서, 그림, 데이터, 해당 소프트웨어 자체 등
        자원의 표현: 그 자원을 표현하기 위한 이름
             -> Ex) DB의 학생 정보가 자원일 때, ‘students’를 자원의 표현으로 정한다.

 - **상태(정보) 전달**

데이터가 요청되어지는 시점에서 자원의 상태(정보)를 전달한다.
JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.
월드 와이드 웹(www)과 같은 분산 하이퍼미디어 시스템을 위한 소프트웨어 개발 아키텍처의 한 형식
REST는 기본적으로 웹의 기존 기술과 HTTP 프로토콜을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.

2.   **REST의 구체적인 개념**

HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.

즉, **REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계**의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.

웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 ID인 HTTP URI를 부여한다.
CRUD Operation
Create : 생성(POST)
Read : 조회(GET)
Update : 수정(PUT)
Delete : 삭제(DELETE)

## REST 구성 요소

---

1. **자원(Resource): URI**
모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
자원을 구별하는 ID는 ‘/groups/:group_id’와 같은 HTTP URI 다.
Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
2. **행위(Verb): HTTP Method**
HTTP 프로토콜의 Method를 사용한다.
HTTP 프로토콜은 GET, POST, PUT, DELETE 와 같은 메서드를 제공한다.
3. **표현(Representation of Resource)**
Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
REST에서 하나의 자원은 JSON, XML, TEXT, RSS 등 여러 형태의 Representation으로 나타내어 질 수 있다.
JSON 혹은 XML를 통해 데이터를 주고 받는 것이 일반적이다.

    header에 직접적으로 content-type을 명시하여 정보를 왔다갔다 할 수 있음!

- URL vs URI

    ![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/599ae4a6-19c7-4a59-b6e4-75eef6025d28/_2021-05-16__8.21.57.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/599ae4a6-19c7-4a59-b6e4-75eef6025d28/_2021-05-16__8.21.57.png)

    [[네트워크📶] URI 란 ? / URI VS URL VS URN 차이 /](https://programming119.tistory.com/194)

## REST 특징

1. **Server-Client(서버-클라이언트 구조)**
자원이 있는 쪽이 Server, 자원을 요청하는 쪽이 Client가 된다.
REST Server: API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
Client: 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
서로 간 의존성이 줄어든다.
2. **Stateless(무상태)**
HTTP 프로토콜은 Stateless Protocol이므로 REST 역시 무상태성을 갖는다.
Client의 context를 Server에 저장하지 않는다.
즉, 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해진다.
Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
각 API 서버는 Client의 요청만을 단순 처리한다.
즉, 이전 요청이 다음 요청의 처리에 연관되어서는 안된다.
**물론 이전 요청이 DB를 수정하여 DB에 의해 바뀌는 것은 허용한다.**
Server의 처리 방식에 일관성을 부여하고 부담이 줄어들며, 서비스의 자유도가 높아진다.
3. **Cacheable(캐시 처리 가능)**
웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용할 수 있다.
즉, HTTP가 가진 가장 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
HTTP 프로토콜 표준에서 사용하는 Last-Modified 태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.
대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다.
캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상시킬 수 있다.
4. **Layered System(계층화)**
Client는 REST API Server만 호출한다.
REST Server는 다중 계층으로 구성될 수 있다.
API Server는 순수 비즈니스 로직을 수행하고 그 앞단에 보안, 로드밸런싱, 암호화, 사용자 인증 등을 추가하여 구조상의 유연성을 줄 수 있다.(nginx, apache 등을 활용한 다양한 기능)
또한 로드밸런싱, 공유 캐시 등을 통해 확장성과 보안성을 향상시킬 수 있다.
PROXY, 게이트웨이 같은 네트워크 기반의 중간 매체를 사용할 수 있다.
5. **Code-On-Demand(optional)**
Server로부터 스크립트를 받아서 Client에서 실행한다.
반드시 충족할 필요는 없다.
6. **Uniform Interface(인터페이스 일관성)**
URI로 지정한 Resource에 대한 조작을 통일되고 한정적인 인터페이스로 수행한다.
HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용이 가능하다.
특정 언어나 기술에 종속되지 않는다.

### REST API

- 정의 : Representational State Tranfer, URI를 이용해 자원을 표시하고 HTTP METHOD를 지용하여 자원의 행위를 정하여 요청을 보내고 그 결과를 받는 것.
- 원칙
    - URI는 자원을 표현하는데 집중해야 하며 리소스명은 **동사보다는 명사**를 이용해서 표현되어야 한다. 행위에 대한 표현이 들어가서는 안 된다.
    - 자원에 대한 행위는 HTTP METHOD로만 표현해야 한다.
    - 이 외의 형식 규칙으로는 슬래시는 계층관계 나타내는데 쓰며 마지막엔 쓰면 안되고 하이픈은 쓸 수 있지만 언더바나 밑줄은 쓰지 않고 소문자 쓰면 좋고 파일 확장자는 URI에 포함시키지 말고 accept header을 이용해야함.
- 구성 : Resource-자원, URI  /  Verb - 자원에 대한 행위, HTTP METHOD / Represesntational : 자원의 행위에 대한 내용, payload, 파라미터
- RESTful하다 : 상기한 규칙이 잘 지켜질 때 레스트풀하다고 함. CRUD기능을 전부 POST로만 처리하는 API나(메소드로 동작 표현이 안됨), URI에 자원과 id외의 정보가 들어가는 API는 레스트풀하지 못하다.
- 장점, 왜 쓰는지
    - 유니폼 인터페이스 : HTTP 표준만 따른다면 어떤 언어 혹은 플랫폼에서 사용하여도 사용이 가능하다. 모바일이든 웹이든 요청을 보내면 정보를 가져올 수 있어 범용적이다.
    - 자체 표현 구조 : 메시지만 보고도 자원의 이동을 쉽게 표현할 수 있는 구조
    - 클라이언트-서버 : 클라이언트는 자원만 받고 렌더링이나 사용자 인터렉션을 클라이언트에서 알아서 처리하기 때문에  서버와 클라이언트간의 의존성을 줄이고 전통적으로 서버가 해왔던 일도 줄어든다.
    - 계층화 : 레스트 서버는 다중 계층으로 구성될 수 있으며 로드 밸런싱, 암호화, 사용자 인증등을 추가하여 구조상의 유연성을 둘 수 있다.