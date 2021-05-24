

#### Request Line

<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_G308xZBor8/CleanShot 2021-05-23 at 14.11.47@2x.png" alt="CleanShot 2021-05-23 at 14.11.47@2x" style="zoom:33%;" />



#### URI vs. URL

URI: 인터넷 서비스를 전제로 하여 인터넷 응용 정보자원에 대한 통일적 식별체계를 지칭하는 개념적 용어 ([참고](http://www.ktword.co.kr/abbr_view.php?nav=&m_temp1=2340&id=637))

* URI는 **URL** (*Uniform Resource Locator*; 인터넷 콘텐츠에 대한 프로토콜/서비스/접근방법/경로 등 자원의 위치를 나타냄), **URN** (*Uniform Resource Name*; 인터넷 도메인명과는 독집적으로 특정 콘텐츠에 대한 고유 식별, 특정이름이나 네임스페이스, 도서번호인 ISBN 등), **URC** (*Uniform Resource Characteristic*; 특정 콘텐츠의 저자, 제목 등의 특성 정보) 를 총칭하는 용어

<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_ANRUs1DxPD/CleanShot 2021-05-23 at 14.13.11@2x.png" alt="CleanShot 2021-05-23 at 14.13.11@2x" style="zoom: 25%;" />



#### Query Strings

<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_TyGjhpCo3g/CleanShot 2021-05-23 at 14.14.22@2x.png" alt="CleanShot 2021-05-23 at 14.14.22@2x" style="zoom:33%;" />





# HTTP request methods

HTTP의 요청 메서드란 클라이언트가 웹 서버에게 사용자 요청의 목적/종류를 알리는 수단이다.

### GET

URI 형식으로 서버측 데이터 (예. 웹페이지, 이미지, 영상 등)를 요청하고 본문형식을 넘겨받음

```
GET [request-uri]?query_string HTTP/1.1
Host:[Hostname] 혹은 [IP]
```



<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_l8mwIoCia9/CleanShot 2021-05-23 at 14.20.10@2x.png" alt="CleanShot 2021-05-23 at 14.20.10@2x" style="zoom:50%;" />

* URL에 query string 형식으로 데이터 전송하기 때문에 서버로 넘기는 파라미터가 표시됨
* URL에 최대 길이 존재, 초과된 데이터는 절단되어 보내짐



### HEAD

서버 리소스의 헤더 (메타 데이터)를 확인

```
HEAD [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
```



<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_Xq52Oirg4y/CleanShot 2021-05-23 at 14.08.38@2x.png" alt="CleanShot 2021-05-23 at 14.08.38@2x" style="zoom:50%;" />

* 실제 문서를 요청하는 것이 아니라 문서 정보를 요청하는 것이라 HTTP응답 메세지에 본문 (body)없이 HTTP 헤더 정보만을 보냄
* 이럴 때 사용:
  * 리소스를 가져오지 않고도, 그에 대해 **무엇인가**(타입이라거나)를 알아낼 때
  * 응답의 상태 코드를 통해, 개체가 존재하는지 확인할 때
  * 헤더만을 확인하여 리소스가 변경되었는지 검사할 때
  * 큰 용량의 리소스를 다운로드 받을지 말지 결정하기 위해서 사전 요청하는 용도로 사용할 때



### POST

서버에 데이터를 추가, 작성 등 (파일 포함 내용 전송)

```
POST [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
Content-Lenght:[Length in Bytes]
Content-Type:[Content Type]
[데이터] 
```

> ```html
> // 예시
> POST / HTTP/1.1
> Host: foo.com
> Content-Type: application/x-www-form-urlencoded
> Content-Length: 13
> 
> say=Hi&to=Mom
> ```

<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_nn9ACHEEle/CleanShot 2021-05-23 at 14.23.04@2x.png" alt="CleanShot 2021-05-23 at 14.23.04@2x" style="zoom:50%;" />

<img src="/Users/eugene/Library/Application Support/CleanShot/media/media_DLSecAizt0/CleanShot 2021-05-23 at 16.03.10@2x.png" alt="CleanShot 2021-05-23 at 16.03.10@2x" style="zoom: 33%;" />



* 예를 들어 블로그 게시글을 올릴 때와 같이 새로운 리소스에 데이터를 만들 때 사용됨
* 기존의 데이터를 수정할 때 사용되기도 함
* 브라우저에 기록 남지 않음
* 데이터 길이에 제한 없음



### PUT

서버의 데이터를 갱신 (파일 전송 가능)

```
PUT [request-uri] HTTP/1.1
Host:[Hostname] 혹은 [IP]
Content-Lenght:[Length in Bytes]
Content-Type:[Content Type]
[데이터] 
```

> ```html
> // 예시
> PUT /new.html HTTP/1.1
> Host: example.com
> Content-type: text/html
> Content-length: 16
> 
> <p>New File</p>
> ```

* POST처럼 정보를 서버로 제출하는 형식이긴 하나 데이터 갱신 위주
  	- 따라서 POST와는 달리 서버측 응답메세지의 HTTP 헤더 항목 중에 'Location: '을 보내지 않아도 됨



### DELETE

서버의 데이터를 삭제

```
DELETE [request-uri] HTTP/ 1.1
Host:[Hostname] 혹은 [IP]
```

* 서버에서 클라이언트의 요청 무시 가능
  예. 실제로 삭제되지 않았지만 클라이언트는 삭제된 것으로 간주하는 경우



### OPTIONS

리소스가 지원하고 있는 메소드의 취득

```html
OPTIONS [request-uri] HTTP/ 1.1
Host: [Hostname] 혹은 [IP]
```

* 가능한 메소드 옵션에 대한 질의
* 응답 메세지에 HTTP 헤더 항목 중 'Allow: GET, POST, HEAD' 처럼 보내짐



### TRACE

요청 리소스가 수신되는 경로 표시

```
TRACE [request-uri] HTTP/ 1.1
Host: [Hostname] 혹은 [IP]
```

* 자기 앞으로 요청 메세지를 반환해서 자신의 요청이 서버에 도달했을 때 어떻게 보이는지 알려줌
* 원격시 서버에 루프백 메세지 호출하기 위해 테스트용으로 사용 (즉 요청이 의도한 요청.응답 연쇄를 거쳐가는지 검사할 수 있음)



#### GET & POST

---

**GET**

먹등하게 설계됨

* 서버에게 동일한 요청을 여러 번 전송하더라도 동일한 응답이 돌아와야 하기 때문

```
GET /some/resource HTTP/1.1
Header:[value]
...
(none)	
```

**POST**

먹등하지 않음

* 서버의 상태나 데이터를 변경시킬 때 사용되기 때문에 (예. 게시글 작성하면 서버에 게시글이 저장되고 게시글을 삭제하면 해당 데이터가 없어지는 등 서버의 무언가를 변경) 서버에게 동일한 요청을 여러번 전송해도 응답은 항상 다를 수 있음

```
POST /some/resource HTTP/1.1
Header:[value]
...
[request body]
```



#### POST와 PUT의 차이

---

* POST는 보통 **INSERT**의 개념, PUT은 **UPDATE**개념으로 사용

* POST는 멱등하지 않고 PUT은 멱등함 (동일한 자원을 여러번 POST 하면 서버자원에는 변화가 생기지만, 여러번 PUT하는 경우는 변화가 생기지 않음)

예를들어 POST의 경우 클라이언트가 리소스의 위치를 지정하지 않는 경우 사용됨 (/dogs). 따라서 아래와 같은 요청이 여러번 수행되는 경우 매번 새로운 dog가 생성되어 dogs/3, dogs/4 등 매번 새로운 자원이 생성됨 (멱등하지 않음)

​			POST **/dogs** HTTP/1.1
​			{ "name": "blue", "age": 5 }
​			HTTP/1.1 201 Created

반면 PUT의 경우는 클라이언트가 명확하게 리소스의 위치를 지정함 (/dogs/3). 따라서 아무리 많이 수행되더라도 리소스의 위치가 지정되어 새로운 자원이 생성되지 않으며 동일한 리소스(/dogs/3)를 수정하기 때문에 여러번 요청하더라도 멱등함

​			PUT **/dogs/3** HTTP/1.1
​			{ "name": "blue", "age": 5 }



##### 	참고) 멱등성, 캐시 가능성

![CleanShot 2021-05-23 at 14.00.58@2x](/Users/eugene/Library/Application Support/CleanShot/media/media_LLzUxG4MyR/CleanShot 2021-05-23 at 14.00.58@2x.png)

* 멱등성 (Idempotent): 특정 메소드의 요청을 여러 번 했을 경우, 한 번 요청했을 때와 결과가 같다면 멱등으로 간주
* 캐시 가능성 (Cachable): 향후 재사용을 위해 이에 대한 응답을 저장할 수 있음을 나타냄
  * 일반적으로 현재 시점의 응답이나 권한 있는 응답에 의존하지 않는 안전(safe)한 메소드는 캐시 가능한 것으로 정의

