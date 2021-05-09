1. # 1. HTTP vs HTTPS

   > HTTP와 HTTPS의 가장 큰 차이는 SSL 인증서이다

   - HTTP 프로토콜의 문제점은 서버에서부터 브라우저로 전송되는 정보가 암호화되지 않는다는 것이다

     - 데이터가 쉽게 도난당할 수 있다

   - HTTPS 프로토콜은 이 문제를 해결하기 위해 만들어졌다

     - SSL은 서버와 브라우저 사이에 안전하게 암호화된 연결을 만들 수 있게 도와주고, 서버 브라우저가 민감한 정보를 주고받을 때 이것이 도난당하는 것을 막아준다

       

   | Parameter        | HTTP                          | HTTPS                                                        |
   | ---------------- | ----------------------------- | ------------------------------------------------------------ |
   | 이름             | hypertext transfer protocol   | hypertext transfer protocol with secure                      |
   | 보안성           | 낮음                          | 높음                                                         |
   | 포트             | 80                            | 443                                                          |
   | 도메인 네임 검증 | SSL 인증서를 필요 하지 않는다 | SSL 인증서를 필요로 한다                                     |
   | 암호화           | X                             | O                                                            |
   | 검색 랭킹        |                               | 구글에서 HTTPS를 사용하는 사이트에 더 높은 점수를 주는 등 검색 랭킹에 도움을 준다 |
   | 속도             | 빠름                          | 상대적으로 느림                                              |

   

   # 2. SSL

   > 네트워크로 연결된 컴퓨터간에 인증되고 암호화 된 링크를 설정하기위한 프로토콜

   ![](https://images.velog.io/images/sangmin7648/post/b1b0d7ff-f41a-40bc-a0fc-08b1d91f624c/Screenshot%20from%202021-05-09%2017-18-46.png)

   - CA(Certificate Authority)에게 인증서 사인 받는 과정

   ![](https://images.velog.io/images/sangmin7648/post/b08f4286-a389-4b06-8aef-5101665a6026/Screenshot%20from%202021-05-09%2017-22-26.png)

   - self-signed certificate authority에게 인증서 사인 받는 과정

   ![](https://images.velog.io/images/sangmin7648/post/638d6572-2415-41fc-bc60-ecc9873ddd17/Screenshot%20from%202021-05-09%2017-25-24.png)