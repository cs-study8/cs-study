# 1. HTTP

> HTML 문서와 같은 리소스들을 가져올 수 있도록 하는 프로토콜



- 웹에서 이뤄지는 모든 데이터 교환의 기초
- 클라이언트-서버 어플리케이션 계층 프로토콜

<img src="https://mdn.mozillademos.org/files/13677/Fetching_a_page.png" alt="A Web document is the composition of different resources" style="zoom: 67%;" />

- 개별적인 메시지 교환에 의해 통신 
  - 클라이언트가 전송하는 메시지 : 요청
  - 서버가 전송하는 메시지 응답
- 신뢰 가능한 전송 프로토콜이라면 무엇이든 사용할 수 있으나 주로 TCP 혹은 TLS로 전송
- 필요 때마다 웹 페이지를 갱신하기 위해 문서 일부를 가져오는데 사용 가능



<hr>

# 2. HTTP 기반 시스템의 구성요소

- 클라이언트 : 사용자 에이전트
  - 사용자 에이전트 : 사용자를 대신해 동작하는 모든 도구 ex) 브라우저
  - 브라우저는 HTML 문서를 가져와 다양한 처리를 통해 완전한 웹 페이지 표시
- 웹 서버
  - 클라이언트 요청에 대한 문서를 제공하는 서버
  - 논리적으로 단일 기계
  - 여러 개 서버가 HTTP/1.1과 Host 헤더를 이용해 동일한 IP 주소를 공유할 수도 있음
- 프록시
  - 클라이언트와 서버 사이에서는 많은 컴퓨터가 HTTP 메시지를 이어 받고 전달함
  - 이런 컴퓨터들은 대부분 전송/네트워크/물리 계층에서 동작
  - HTTP 계층에서는 어떻게 동작하는지 보이지 않음
  - 이런 컴퓨터 중에 애플리케이션 계층에서 동작하는 것들을 프록시라고 부름
  - 다양한 기능 수행
    - 캐싱
    - 필터링
    - 로드 밸런싱
    - 인증
    - 로깅



<hr>



# 3. HTTP의 기초적인 측면

- 간단성 : 
  - HTTP는 사람이 읽을 수 있게 고안 (HTTP/2.0부터는 캡슐화로 불가)
- 확장성 : 
  - HTTP 헤더의 고안으로 헤더 클라-서버 간 시맨틱에 대한 합의만 있다면 새로운 기능 추가 가능
- 상태x, 세션o : 
  - 각 HTTP 통신은 독립적
  - **장점 :** 효과적 서버 디자인과 간결화. 각 HTTP 요청에 대해 독립적으로 응답만 전송
    _(상태를 서버에서 저장 X, 통신 간 진행/연결 상태 처리 및 저장 구현/관리 X 때문)_
  - **단점 :** 요청 시 필요 데이터를 매번 포함시켜 전송. 이를 위해 쿠키와 세션을 사용해 통신상 데이터 저장
- HTTP와 연결 :
  - 신뢰성 있는 연결을 요구하기 때문에 TCP 표준에 의존
  - TCP가 요구되지는 않음 ex) 구글의 UDP 기반 QUIC
  - 메시지 교환 전 TCP 연결을 설정해야함
  - HTTP/1.0 : 각 메시지에 대해 별도의 TCP 연결 생성
  - HTTP/1.1 : 파이프라이닝과 지속적 연결 개념 도입. Connection 헤더를 사용해 부분적으로 TCP 연결 제어 가능
  - HTTP/2.0 : 단일 연결 상에서 메시지를 다중 전송하여 연결이 더 지속되고 효율적으로 유지하게 함



<hr>



# 4. HTTP로 제어할 수 있는 것

- 캐시 : 문서 캐싱 방식 제어

  - 서버는 캐시 대상과 기간을 프록시와 클라이언트에 지시 가능
  - 클라이언트는 저장된 문서를 무시하도록 중간 캐시 프록시에게 지시 가능

- origin 제약사항 완화

  - 문서는 다른 도메인으로부터 전달된 정보를 패치워크할 수 있음

- 인증

  1. WWW-Authenticate 또는 유사 헤더

  2. 쿠키를 통한 세션 설정

  - 을 통해 접근 제어 가능
  
- 프록시와 터널링

  - 서버, 클라이언트 모두 종종 인트라넷에 위치해 다른 개체에게 실제 주소를 숨기기도 함
  - HTTP 요청은 프록시들을 지나 이런 장벽을 통과함 

- 세션 

  - 쿠키를 사용해 요청과 서버 상태를 연결 가능
  - 이를 통해 세션을 만듬



<hr>



# 5. HTTP 흐름

1. TCP 연결 열기
   - 새 연결을 설립하거나 기존 연결을 사용하거나 여러 TCP 연결을 열 수 있음
2.  HTTP 메시지 전송
3. 서버가 전송한 응답을 읽음
4. 연결을 닫거나 다른 요청을 위해 재사용 



# 6. HTTP 메시지

> ![](https://images.velog.io/images/sangmin7648/post/cfc88650-17b6-4e32-a90d-a8113c499e7b/image.png)

## 6-1. 요청 메시지 구조

**3 부분으로 구성**

**1. Start Line : HTTP 메소드, 요청 타겟, HTTP 버전으로 구성**
- 메소드 : GET, POST, PUT, DELETE, OPTIONS 등 요청이 의도하는 동작을 정의하는 부분
- 요청 타겟 : 요청이 전송되는 목표 주소 
- HTTP 버전 : 서버가 요청의 HTTP 버전에 맞춰 응답할 수 있도록 명시

**2. Headers : HTTP 요청 자체에 대한 정보. 키와 값으로 구성 **

- Host : 요청이 전송되는 타겟의 호스트의 URL 주소
- User-Agent : 요청을 보내는 클라이언트의 대한 정보
- Accept : 요청이 받을 수 있는 응답 body 데이터 타입. MIME type이 값으로 지정
- Connection : 요청이 끝난 후 클라이언트와 서버 네트워크 연결 유지 여부
- Content-Type : 요청이 보내는 메시지 body의 타입. MIME type이 값으로 지정
- Content-Length : 요청이 보내는 메시지 body의 총 사이즈

_MIME type : 인터넷상 전송되는 파일 포멧과 컨텐츠를 위한 식별자. "type/subtype" 형태로 이뤄짐. 
현재 Media type으로 명칭 변경_

**3. Body : 요청이 전송하는 데이터 부분**
- 전송 데이터가 없다면 비어 있음



## 6-2. 응답 메시지 구조

**3 부분으로 구성**

**1. Status Line : HTTP 버전, Status Code, Status Text로 구성**
- HTTP 버전 : 응답이 사용하는 HTTP 버전
- Status Code : 응답 상태를 나타내는 숫자로 된 코드
- Status Text : Status Code를 글로 설명한 부분

**2. Headers : 요청의 Headers와 동일하나 요청과 응답에서 사용되는 헤더가 다를 수 있음**
- 요청에서 User-Agent 헤더를 사용한다면 응답에선 Server 헤더 사용

**3. Body : 응답이 전송하는 데이터 부분 **



<hr>



# 7. 대표적인 HTTP 메소드
> 요청이 의도하는 동작을 정의하는 부분

**1. GET**

- 데이터를 서버로부터 요청할 때 사용
- 데이터 생성/수정/삭제 없이 단순히 받아 오는 요청 메소드

**2. POST**
- 데이터를 생성/수정/삭제 요청할 때 사용하는 메소드

**3. OPTIONS**
- 특정 엔드포인트에서 허용하는 메소드들이 무엇이 있는지 알고자 하는 요청에서 사용
- 엔드포인트는 허용하는 메소드가 지정되어있고, 허용하지 않는 메소드의 요청이 들어오면 405 응답

**4. PUT**
- 데이터를 생성/수정할 때 사용하는 메소드
- POST와 달리 멱등성을 가짐
- POST로 통일하는 시스템 많아지는 중

**5. DELETE**
- 데이터 삭제 요청을 할때 사용하는 메소드
- POST와 달리 멱등성을 가짐
- POST로 통일하는 시스템 많아지는 중

이외에도 CONNECT, TRACE 등 메소드 존재



<hr>



# 8. HTTP Status Code

> HTTP 요청 처리 결과를 표시하기 위한 코드

**1. 200 OK : 요청 성공적으로 처리**

**2. 301 Moved Permanently : 요청을 보낸 엔드포인트의 URL 주소가 바뀜**

- 엔드포인트의 새로운 주소가 담긴 Location 헤더를 포함해 응답
- 301 응답을 받은 클라이언트는 Location헤더의 새로운 주소에 요청 재전송
- 이 과정을 redirection이라 함

**3. 400 Bad Request : 잘못된 요청일 때 보내는 응답 코드**

- 주로 요청에 포함된 input 값들이 잘못된 값일 때 사용

**4. 401 Unauthorized : 요청을 보내는 주체의 신분 확인이 요구되나 확인할 수 없음 **

- ex) 로그인이 필요한 기능에 로그인하지 않은 사용자 접근 시

**5. 403 Forbidden : 요청을 보내는 주체가 해당 요청에 대한 권한이 없음**

- ex) 게시글/댓글 작성자가 아닌 사용자가 삭제 요청

**6. 404 Not Found : 요청을 보내고자 하는 URI가 존재하지 않음**

**7. 500 Internal Server Error : 요청 처리 과정에서 서버 오류로 처리할 수 없음**

이외에도 다양한 Status Code 존재



<hr>



# 9. HTTP의 발전 과정

- WWW가 만들어질때 4개의 빌딩 블록으로 구성
  1. HTML
  2. HTTP
  3. 브라우저
  4. httpd

## 9-1. HTTP/0.9 : 원-라인 프로토콜

> 초기 버전에는 버전 번호가 없었음. 이후 버전이 생기고 나서 초기 버전을 0.9로 명명 

- 요청은 **한줄로 구성**
- GET 메소드만 사용가능
- 리소스 경로(URL x)로 요청. 프로토콜, 서버, 포트는 서버에 연결되면 불필요했기 때문에

```
GET /mypage.html
```

- 응답은 HTML 파일 자체

```
<HTML>
A very simple HTML page
</HTML>
```

- 헤더 존재 x, HTML 파일만 전송 가능
- 상태 코드 존재 x, 문제 발생 시 HTML에 내부 문제에 대한 설명과 함께 전송



## 9-2. HTTP/1.0 : 확장성 만들기

- 버전 정보가 각 요청에 명시
- 상태 코드가 응답에 붙어 전송 
- **헤더의 개념이 요청과 응답에 도입**, 메타데이터 전송이 가능하고 프로토콜이 확장 가능해짐
- 헤더의 생성으로 HTML 외 문서 전송이 가능해짐
- 다양한 HTTP 메소드 도입

```
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```



## 9-3. HTTP/1.1 : 표준 프로토콜

> 첫번째 HTTP 표준 버전

- 연결 재사용 가능. 문서 내 임베드된 리소스를 가져오는 시간 절약
- 파이프라이닝 추가. 이전 요청에 대한 응답을 완전히 받기 전에 요청 전송 가능
- 청크 응답 지원 ex) 이미지 로딩

- 추가적인 캐시 제어 방법들
- 언어, 인코딩, 타입등에 대한 컨텐츠 협상 도입. 클라-서버 간 교환에 가장 적합한 컨텐츠 동의
- Host 헤더로 동일 IP 주소에 다른 도메인을 호스트하는 기능이 추가

```
GET /en-US/docs/Glossary/Simple_header HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header

200 OK
Connection: Keep-Alive
Content-Encoding: gzip
Content-Type: text/html; charset=utf-8
Date: Wed, 20 Jul 2016 10:55:30 GMT
Etag: "547fa7e369ef56031dd3bff2ace9fc0832eb251a"
Keep-Alive: timeout=5, max=1000
Last-Modified: Tue, 19 Jul 2016 00:59:33 GMT
Server: Apache
Transfer-Encoding: chunked
Vary: Cookie, Accept-Encoding
```



## 9-4. HTTP/1.1 ~ HTTP/2.0 사이 주요 변화들

- HTTPS : 더 많은 데이터가 HTTP를 이용해 전달되면서 IP/TCP 스택보다 보안성이 뛰어난 프로토콜이 필요로 해짐
- REST : HTTP 사용 패턴. 새로운 메소드 작성 없이 기본 HTTP/1.1 메소드로 URI 접근
- WebSocket : 클라-서버 간 양방향 상호작용 통신을 가능하게함



## 9-5. HTTP/2 : 성능

- 웹이 발전하며 발생한 문제들
  - 웹 페이지가 복잡해 지면서 애플리케이션까지 됨
  - 많은 데이터가 수 많은 HTTP 요청으로 전송됨
  - HTTP/1.1 연결에서 요청은 올바른 순서로 전송돼야함
  - 여러 병렬 연결이 가능해 복잡하고 오버헤드가 큼
- HTTP/2 특징
  - 텍스트가 아닌 바이너리 프로토콜
  - 멀티플렉스 프로토콜 : 병렬 요청을 동일 연결에서 보낼 수 있음
  - 헤더 압축 : 데이터의 중복과 오버헤드 해결. 요청들의 헤더에 중복값이 존재하면 헤더 테이블 index 값만 전송한다
  - 서버 푸쉬 : 클라이언트가 요청하지도 않은 리소스를 보낼 수 있음
    - ex) 문서에 포함된 CSS, 사진 등의 리소스

- 대부분의 경우 웹 사이트나 애플리케이션 측의 변화 없이 최신 서버와 브라우저가 통신하면 쓸 수 있어 빠르게 보급되었다



## 9-6. HTTP/3 : QUIC

- 전송 계층 프로토콜에 TCP/TLS 대신 UDP 기반 QUIC을 이용해 통신하는 프로토콜
- 아직 실험적인 기술. 표준안 완성이 되지 않았다
- 기본적으로 HTTP/3를 활성화한 최초의 브라우저는 macOS 빅서의 사파리

