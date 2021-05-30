
# 1. Same-Origin Policy
> 어떤 출처에서 불러온 리소스가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안 정책. 스크립트에만 적용된다. 동일한 출처의 웹페이지일때만 리소스에 접근하는 것을 허용한다.

- **동일한 출처(same-origin) :** 두 URL의 프로토콜, 호스트, 포트가 동일

예) http://store.company.com/dir/page.html 페이지의 스크립트가 아래 페이지에서 리소스 접근시
![](https://images.velog.io/images/sangmin7648/post/258327e0-86f8-4438-b1f8-362494493470/image.png)

- 어떤 페이지의 악의적인 스크립트가 다른 페이지의 DOM를 통해 데이터에 접근하는 것을 방지한다 

- 이미지, CSS 같은 리소스는 HTML 태그를 통해 다른 출처여도 접근할 수 있다.

⚠️  **사용자를 보호하기 위한 클라이언트 측 정책으로 요청이 들어오면 서버에서는 다른 출처여도 정상적으로 응답하지만 브라우저 단에서 SOP를 확인해 처리한다. 따라서 서버 간 통신에는 적용되지 않는다** ⚠️

<hr>

# 2. SOP가 없다면?
- **SOP가 없을 때 발생가능한 문제 예 :**
가짜 은행 피싱사이트의 페이지에 iframe으로 진짜 은행 사이트가 로드됐다. iframe 내 진짜 은행 사이트에 로그인 했을 때 가짜 사이트가 간단한 스크립트로 진짜의 DOM 요소에 접근 가능하다. 요청을 조작해 누군가에게 송금하게 하는것도 가능할 수 있다. 

- SOP가 없다면 이런 다른 사이트간 요청이 악의적으로 실행될 수 있다

<hr>

# 3. CORS(Cross-Origin Resource Sharing)

> HTTP-header 기반 방식으로 서버가 브라우저에서 리소스 로딩을 할 수 있는 다른 출처를 허용할 수 있게한다

- 오픈된 웹 환경에서 흔히 있는 다른 출처 간 리소스 사용을 무조건 막을 수는 없다. 

- 따라서 제한된 설정을 통해 부합하는 출처에서 통신을 허용한다

- **작동방식 :** 
1) 클라이언트가 다른 출처의 리소스를 요청할 때 헤더에 <code>Origin</code> 필드에 요청을 보내는 출처를 함께 보낸다. 
2) 이후 서버가 응답할 때 응답 헤더의 <code>Access-Control-Allow-Origin</code> 필드에 해당 리소스에 접근이 허용된 출처를 보낸다. 
3) 응답을 받은 클라이언트는 보냈던 요청의 <code>Origin</code>과 응답의 <code>Access-Control-Allow-Origin</code>을 비교해 유효한 응답인지를 결정한다

- CORS의 세세한 동작 방식은 **Preflight, Simple, Credentialed** 3가지 시나리오에 따라 조금씩 다르다

⚠️  **사용자를 보호하기 위한 클라이언트 측 정책으로 요청이 들어오면 서버에서는 다른 출처여도 정상적으로 응답하지만 브라우저 단에서 CORS를 확인해 처리한다. 따라서 서버 간 통신에는 적용되지 않는다** ⚠️

## 3-1. Preflight Request

- 브라우저가 요청을 한번에 보내지 않고 예비 요청과 본 요청으로 나눠 서버로 전송한다. 이때 예비요청을 preflight이라 부른다.

![](https://images.velog.io/images/sangmin7648/post/72d92441-eba0-4476-801a-f11a5d5f1913/image.png)

## 3-2. Simple Request

- 예비요청 없이 바로 본 요청을 보내고, 응답에 따라 CORS 정책 위반 여부를 검사한다.

![](https://images.velog.io/images/sangmin7648/post/0158320a-5b79-44b7-8c75-5b79583d13fb/image.png)

- 단, simple request 시나리오를 위해선 특정 조건을 만족해야한다
i) 요청 메소드 = <code> GET, HEAD, POST</code> 중 하나
ii) <code> Accept, Accept-Language, Content-Language, Content-type, DPR, Downlink, Save-Data, Viewport-Width, Width </code> 이외의 헤더를 사용 X
iii) Content-Type 사용하는 경우 <code> application/x-www-form-urlencoded, multipart/form-data, text/plain</code>만 허용

## 3-3. Credentialed Request

- 다른 출처 간 통신의 보안을 강화하고 싶을 때 사용

- 비동기 리소스 요청은 쿠키나 인증 관련 헤더를 별도 옵션 없이 헤더에 담지 않는다. 요청에 인증 관련 정보를 담게 해주는 옵션이 credentials이다

![](https://images.velog.io/images/sangmin7648/post/f7ee9148-4f04-4323-ba3f-ee22b5e69368/image.png)

```js
// credentials include 옵션 예시
fetch('https://test.com', {
  credentials: 'include',
});
```

- include의 경우 다음 조건이 충족돼야한다
i) <code>Access-Control-Allow-Origin</code>에 <code>*</code> 사용 X, URL 명시
ii) 응답 헤더에 <code>Access-Control-Allow-Credentials: true</code> 존재

참고 : https://evan-moon.github.io/2020/05/21/about-cors/

<hr>

# 4. flask-cors
> CORS 처리를 위한 Flask 익스텐션

- CORS를 가능하게 하고 싶다면, 모든 곳에서 헤더 상관없이 가능케하는걸 모토로하는 패키지이다

- 기본설정은 모든 엔드포인트에 모든 origin과 method에 대해 cors를 허용한다

```py
from flask import Flask
from flask_cors import CORS

app = Flask(__name__)
CORS(app)
```

- 특정 리소스 CORS : 리소스를 특정해 CORS 옵션을 설정할 수 있다

```py
app = Flask(__name__)
cors = CORS(app, resources={r"/api/*": {"origins": "*"}})

@app.route("/api/v1/users")
def list_users():
  return "user example"
```

- 특정 엔드포인트 CORS : 데코레이터를 통해 특정 엔드포인트만 CORS를 가능케 할 수 있다

```py
@app.route("/")
@cross_origin()
def helloWorld():
  return "Hello, cross-origin-world!"
```

참고 : https://flask-cors.corydolphin.com/en/latest/index.html