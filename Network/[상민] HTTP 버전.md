# HTTP 버전

HTTP는 1989년~1991년 사이에 발명되었는데, 본래의 단순함의 대부분을 지키면서 확장성 위에서 만들어지도록 수많은 수정을 거쳐왔다. 월드 와이드 웹의 발명부터 시작하여 오늘날의 HTTP/2까지의 버전들을 알아보자.

## 1. 월드 와이드 웹(WWW)의 발명

1989년에 **인터넷 상의 하이퍼텍스트 시스템을 만들기 위한 제안**에 따라 작성된 Mesh는, 1990년 구현 과정에서 <i>월드 와이드 웹</i>으로 이름을 바꿨고, 기존의 TCP/IP 프로토콜 상에서 만들어지면서 4개의 빌딩 블록으로 구성되었다.

1. 하이퍼텍스트 문서를 표현하기 위한 텍스트 형식의 HTML(HyperText Markup Language)
2. 문서 같은 것을 교환하기 위한 간단한 프로토콜인 HTTP(HyperText Transfer Protocol)
3. 문서를 디스플레이하기 위한 클라이언트인 WWW(World Wide Web)이라 불리우는 첫 번째 브라우저
4. 문서에 접근하도록 해주는 httpd의 초기 버전

1990년 말에 완료된 이 네 개의 빌드 블록은, 1991년 9월 6일에 공식적인 WWW의 출발점을 형성하였다.

이렇게 초기에 사용되던 HTTP 프로토콜은 매우 간단했으며, 이후 HTTP/0.9 버전을 부여했고 때로는 원라인 프로토콜로 불리기도 했다.

## 2. HTTP/0.9: 원라인 프로토콜

처음부터 0.9라는 버전을 달고 나오지는 않았다. 초기엔 버전 이름이 없었으나 이후 버전과의 구별을 위해 초기 버전을 0.9로 부르게 되었다.
HTTP/0.9에서 **요청은 단일 라인으로 구성**되며 리소스에 대한 경로로 가능한 메소드는 **GET**이 유일했다. 단, 프로토콜, 서버, 포트는 서버가 연결되고 나면 필요하지 않으므로 URL이 아닌 경로에 한정한다.

> GET /mypage.html

응답 또한 오로지 파일 내용 자체로 구성되었다.

```html
<html>
  A very simple HTML page
</html>
```

이 때에는, HTTP의 헤더가 없었다. 이 말인 즉슨 HTML 파일만 전송할 수 있었다는 뜻이다. 또한, 초기 버전 답게 상태와 오류 코드 또한 없었다. 문제가 발생했다면, 문제에 대한 설명과 함께 파일이 되돌려 보내졌었다.

## 3. HTTP/1.0: 확장성 만들기

HTTP/0.9에서, **브라우저 및 서버 모두가 좀 더 융통성을 갖도록** 빠르게 확장되었다.

1. 버전 정보가 각 요청 사이내로 전송되기 시작했다. (`HTTP/1.0`이 `GET`에 붙은 형태로)
2. 상태 코드 라인 또한 응답의 시작 부분에 붙어 전송되어, 브라우저가 요청에 대한 성공과 실패를 알 수 있고 그 결과에 대한 동작(특정 방법으로 그것의 로컬 캐시를 갱신하거나 사용하는 것과 같은)을 할 수 있게 되었다.
3. HTTP 헤더 개념이 요청과 응답 모두를 위해 도입되었고, 메타데이터 전송이 가능해졌고 프로토콜을 유연하게 확장할 수 있도록 만들어줬다.
4. 새로운 HTTP 헤더의 도움으로(`Content-type`의 등장 덕분에) 평이한 HTML 파일들 외에 다른 문서들을 전송하는 기능이 추가되었다.

HTTP/1.0 하에서의 일반적인 요청 및 응답이다.

```
GET /mypage.html HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Data: Tue, 15 Nov 1994 08:12:31 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/html
<HTML>
A page with an image
  <IMG SRC="/myimage.gif">
</HTML>
```

두 번째 커넥션에 의한 이미지를 내려받기 위한 요청과 그에 대한 응답이다.

```
GET /myimage.gif HTTP/1.0
User-Agent: NCSA_Mosaic/2.0 (Windows 3.1)

200 OK
Date: Tue, 15 Nov 1994 08:12:32 GMT
Server: CERN/3.0 libwww/2.17
Content-Type: text/gif
(image content)
```

이런 새로운 기능들은 합의된 노력들로써 도입되지는 않았지만 1991년부터 1995년까지의 기간 동안 일단 해보자는 접근법으로 이루어졌다: 서버와 브라우저에 기능을 추가한 뒤, 그것이 관심을 끄는지 지켜봤다. 수많은 상호작용 문제가 발생했다. 1996년 11월에, 이런 괴로운 문제를 해결하기 위해, 일반적인 실제 내용을 설명하는 정보 문서는 RFC 1945에 공개되었다. 이것이 HTTP/1.0이 되었다.

## 4. HTTP/1.1: 표준 프로토콜

1995년부터 다양한 HTTP/1.0 구현이 동시에 진행되었고, 그 이듬해 HTTP/1.0 문서 출간 전까지 합당한 표준화를 진행하고 있었다. HTTP의 첫 번째 표준 버전인 HTTP/1.1은 HTTP/1.0이 나온지 몇 달 지나지 않은 1997년 초에 공개되었다.

HTTP/1.1은 모호했던 점들을 명확하게 했고, 많은 개선사항을 도입했다.

- 파이프라이닝을 추가하여, 첫번째 요청에 대한 응답이 완전히 전송되기 이전에 두번째 요청 전송을 가능하게 하였고, 이에 따라 communication latency를 늦췄다.
- 추가적인 캐시 제어 매커니즘이 도입되었다.
- 언어, 인코딩 혹은 타입을 포함한 컨텐츠 협상이 도입되었고, 클라이언트와 서버로 하여금 교환하려는 가장 적합한 컨텐츠에 대한 동의를 가능하게 했다.
- Host 헤더 덕분에, 동일 IP 주소에 다른 도메인을 호스트하는 기능인, server collocation이 가능해졌다.

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

(content)


GET /static/img/header-background.png HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: */*
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/en-US/docs/Glossary/Simple_header

200 OK
Age: 9578461
Cache-Control: public, max-age=315360000
Connection: keep-alive
Content-Length: 3077
Content-Type: image/png
Date: Thu, 31 Mar 2016 13:34:46 GMT
Last-Modified: Wed, 21 Oct 2015 18:27:50 GMT
Server: Apache

(image content of 3077 bytes)
```

## 15년 넘게 진행된 확장

새로운 헤더와 메소드를 생성하기 쉬워졌다는 확장성 덕분에 1999년부터 15년이 넘도록 매우 높은 안정성을 유지해왔다.

### 보안 전송을 위한 HTTP 사용

HTTP에 일어났던 가장 큰 변화는 1994년 말에 이미 완료되었다. 기본적인 TCP/IP 스택을 통해 HTTP를 전송하는 대신에, 넷스케이프 커뮤니케이션은 그것의 토대 위에 추가적인 암호화된 전송 계층인 SSL을 만들어냈다. SSL 1.0은 회사 외부로 릴리즈된 적이 없으며, SSL 2.0과 후속 버전인 SSL 3.0과 SSL 3.1은 서버와 클라이언트 간에 교환된 메시지 인증을 암호화하고 보장하여 e-커머스 웹 사이트를 만들어내도록 했다. SSL은 표준 트랙 상에 놓여져 있었고 마침내 TLS가 되어, 성공적으로 취약성을 종식시키는 1.0, 1.1 그리고 1.2 버전이 나와있고, TLS 1.3은 현재 진행 중에 있다.

같은 시간 동안, 암호화된 전송 계층에 대한 필요성이 대두되었다: 웹은 광고주, 불특정 개인, 혹은 범죄자가 다른 사람인척 가장하거나 전송된 데이터를 수정된 데이터로 대치시키고자, 개인 정보를 빼내려고 경쟁하는 정글 속에, 거의 학문적인 네트워크의 상대적인 신뢰를 남겨두었습니다. HTTP 상에서 만들어진 애플리케이션들이 주소록, 이메일 혹은 사용자의 지리적 위치와 같은 수 많은 개인 정보에 접근하는 등 점점 더 강력해짐에 따라, TLS의 필요성은 e-커머스 사용 케이스 외에 여기 저기서 나타나게 되었습니다.

### 복잡한 어플리케이션을 위한 HTTP 사용

웹에 대한 Tim Berners-Lee의 본래 비전은 읽기 전용의 매체는 아니었다. 그는 사람들이 문서를 원격으로 추가하거나 이동시킬 수 있는, 분산된 파일 시스템의 한 종류로 웹을 상상했다. 1996년도 쯤에, HTTP는 저작을 허용하도록 확장되었으며 WebDAV라고 불리는 표준이 만들어졌다. 그것은 주소록 개체들을 다루기 위한 CardDAV 그리고 달력을 다루기 위한 CalDav와 같은 특정 애플리케이션들로 더 확장되었다. 그러나 이런 모든 DAV 확장들은 한 가지 결점을 갖고 있었다: 꽤 복잡한, 사용하고 있는 서버에 의해 구현되어야만 한다는 것이었다. 웹 영역에서 그것들을 사용하는 것은 극비로 남겨져 있었다.

2000년에, HTTP 사용에 대한 새로운 패턴이 고안되었다: representational state transfer (혹은 REST). API에 의해 유도되는 액션들은 새로운 HTTP 메서드 뿐만 아니라, 기초적인 HTTP/1.1 메서드를 이용한 특정 URI 접근에 의해서도 더 이상 전달되지 않았다. 이것은 모든 웹 어플리케이션으로 하여금 브라우저나 서버의 갱신없이 데이터 탐색과 수정을 허용하는 API 제공을 가능케 했다: 필요로 하는 모든 것은 표준 HTTP/1.1을 통해 웹 사이트에 의해 서브되는 파일 내로 임베드되는 것이었다. REST 모델의 단점은 각각의 웹사이트가 자신의 비표준 RESTful API를 정의하고 그에 대한 전권을 가진다는 사실에 있다; *DAV 확장과는 다르게 클라이언트와 서버들은 상호작용이 가능하다. RESTful API들은 2010년에 들어 표준으로 자리잡았다.

2005년부터, 웹 페이지에서 사용 가능한 API 집합들이 급격히 늘어나게 되었고 이들 API 중 몇몇은, 거의 새로운 특성화된 HTTP 헤더로, 특정한 목적을 위해 HTTP 프로토콜에 확장을 만들어냈다:

1. 서버 전송 이벤트, 서버가 브라우저로 이따금씩 보내는 메시지를 푸시할 수 있는 곳
2. 웹소켓, 기존 HTTP 커넥션을 업그레이드하여 만들 수 있는 새로운 프로토콜


### 웹의 보안 모델 완화

HTTP는 웹의 보안 모델인 same-origin 정책에서 독립되어 있다. 사실, 현재의 웹 보안 모델은 HTTP이 만들어진 이후에 개발되어 왔다. 몇 년에 걸쳐, 이 정책의 몇 가지 정책을 고무시키기 위해 확실한 제약사항 아래 허용함으로써, 좀 더 관대해지도록 하는 것이 유용하다는 것을 증명해왔다. 제약사항이 얼마나 그리고 언제 리프트될지는 HTTP 헤더의 새로운 묶음들을 사용하는 서버부터 클라이언트에 의해 전도된다. 이러한 내용들은 Cross-Origin 리소스 공유 (CORS) 혹은 컨텐츠 보안 정책 (CSP)과 같은 스펙 내에 정의되어 있다.

이런 커다란 확장에 덧붙여, 다른 많은 헤더들이, 때로는 실험적으로만, 추가되어 오고 있다. 주목할 만한 헤더들은 프라이버시를 제어하기 위한 Do Not Track (DNT) 헤더, X-Frame-Options, 혹은 Upgrade-Insecure-Request이 있고, 그 외에도 수많은 헤더들이 존재한다.

## HTTP/2: 더 나은 성능을 위한 프로토콜

몇 년에 걸쳐, 웹 페이지는 진정한 어플리케이션이 되는 과정에서 매우 복잡해졌다. 디스플레이되는 시각적 미디어의 양에 덧붙여 상호작용을 추가하기 위한 스크립트의 양과 크기는 점점 더 많이 증가하고 있다: 더 많은 데이터들이 더 많은 요청 너머로 전송되고 있다. HTTP/1.1 커넥션은 올바른 순서로 전송되는 요청을 필요로 한다. 또한, 몇몇 병렬 커넥션이 이론적으로 사용 가능한 경우(일반적으로 5와 8 사이에서), 여전히 많은 양의 오버헤드와 복잡도가 남아 있다.

2010년 전반기에, Google은 실험적인 SPDY 프로토콜을 구현하여, 클라이언트와 서버 간의 데이터 교환을 대체할 수단을 실증하였다. 그것은 브라우저와 서버 측 모두에 있어 많은 관심을 불러일으켰다. 응답성 증가 능력을 입증하고 전송된 데이터 중복에 관한 문제를 해결하면서, SPDY는 HTTP/2 프로토콜의 기초로써 기여했다.

HTTP/2 프로토콜은 HTTP/1.1 버전과 다른 몇가지 근본적인 차이점을 가지고 있다:

1. 텍스트 프로토콜이라기 보다는 이진 프로토콜이다. 더 이상 읽을 수도 없고 수작업을 만들어낼 수 없다; 이런 결점에 대한 보상으로, 새로운 최적화 기술이 구현될 수 있다.
2. 병렬 요청이 동일한 커넥션 상에서 다루어질 수 있는 다중화 프로토콜로, 순서를 제거해주고 HTTP/1.x 프로토콜의 제약사항을 막아준다.
3. 전송된 데이터의 분명한 중복과 그런 데이터로부터 유발된 불필요한 오버헤드를 제거하면서, 연속된 요청 사이의 매우 유사한 내용으로 존재하는 헤더들을 압축시킨다.
4. 서버로 하여금 사전에 클라이언트 캐시를 서버 푸쉬라고 불리는 메커니즘에 의해, 필요하게 될 데이터로 채워넣도록 허용한다.

2015년 5월에 공식적으로 표준화된, HTTP/2는 큰 성공을 거뒀다: 2016년 6월, 모든 웹 사이트 중 8.7%가 이미 사용 중에 있고, 이것은 모든 요청의 68% 이상을 나타낸다. 인터넷 상에서 전송 오버헤드 감소로 많은 돈을 절약하는 높은 트래픽의 웹 사이트들은 이 프로토콜을 급속히 받아들이고 있다.

이러한 급격한 채택은 HTTP/2가 웹 사이트와 애플리케이션의 채택이 필요하지 않았기에 가능했다: HTTP/1.1을 사용할지 HTTP/2를 사용할지 고민할 필요가 없어졌다. 최신 브라우저와 통신하는 최신의 서버를 갖는 것은 프로토콜 사용을 활성화하는 것만으로 충분하다: 어느 정도의 제한된 액터 세트만이 HTTP/2 채택을 불러일으키는데 필요했으며 브라우저와 서버 버전이 교체됨에 따라, 웹 개발자의 투입없이도 HTTP/2의 사용은 자연스럽게 증가했다.

## 차세대: HTTP/2로의 진화

HTTP는 HTTP/2의 릴리즈와 함께 진화를 멈추지 않았다. HTTP/1.x처럼, 확장성은 여전히 새로운 기능들을 추가하는데 사용되고 있다. 주목할 만한 중요성에 있어 2016년에 나타난 HTTP의 새로운 확장들을 들 수 있다:


1. Alt-Svc (en-US) 지원은 좀 더 영리한 CDN (en-US) 메커니즘을 따라, 신분 증명의 개념과 주어진 자원의 위치를 분리하도록 해 준다.
2. Client-Hints의 도입으로 브라우저 혹은 클라이언트가 요구사항이나 서버의 하드웨어 제약사항에 관한 정보를 사전에 미리 주고 받을 수 있게 되었다.
3. Cookie 내에 보안 관련 접두사 도입은 보안 쿠키가 변경되지 않았다는 것을 보장하는데 도움을 준다.

HTTP의 진화는 그것의 확장성과 단순함이 예측 불가능한 애플리케이션과 프로토콜 채택을 만들어내고 있다는 것을 보여준다. 오늘날 HTTP가 사용되는 환경은 1990년 초에 상상하던 것과는 완전히 다르다. HTTP 본래의 설계가 걸작이 되었음을 지난 25년 넘게 호환되지 않는 진화의 요구없이 웹을 진화시킴으로 증명했다. 25년 넘게 HTTP의 성공을 만들어 온 유연함과 확장성을 유지하는 동시에, 수년 넘게 밝혀진 많은 결함들을 수정한 덕택에, HTTP/2의 등장은 프로토콜에 대한 밝은 미래를 암시하는 것으로 봐도 무방하다.

