# TCP란?

> 연결 지향형 프로토콜로, 연속성 있는 데이터 패킷을 주고 받을 때 사용 

- 전송되는 데이터의 신뢰성 보장 (흐름 제어, 혼잡 제어, 오류 제어)
- 파일전송에 주로 사용
- <u>가상 회선</u>을 만들어 신뢰성을 보장



## TCP 3 way handshake

> 장치들 사이에 논리적 접속을 성립하기 위해 사용하는 연결 확인 방식



1. A -> B : 내 말 들려?
2. B -> A : 잘 들려. 내 말은 들려?
3. A -> B : 잘 들려!

<img src="https://goodgid.github.io/assets/img/network/tcp_ip_3way_4way_1.png" alt="스크린샷 2021-05-08 오후 10.49.13" style="zoom:50%;" />

SYN = synchronize sequence numbers : 연결 확인을 위해 무작위의 숫자를 보냄 (내 말 잘 들려?)

ACK = acknowledgements : Client 혹은 Server로부터 받은 SYN에 1을 더해 SYN을 잘 받았다는 ACK 전송 (잘 들려)

ISN = Initial sequence numbers : Client와 Server가 각각 처음으로  생성한 SYN



* SYN의 값에 무작위 수를 사용하는 이유?

  > Connection을 맺을 때 사용하는 포트는 유한 범위 내에서 사용하고 시간이 지남에 따라 재사용된다. 따라서 두 통신 호스트가 과거에 사용된 포트 번호 쌍을 사용할 가능성이 존재한다. 서버 측에서 패킷의 SYN을 보고 패킷을 구분하게 되는데 난수가 아닌 순차적인 숫자가 전송된다면 이전의 connection으로부터 오는 패킷으로 인식할 수 있어 이러한 문제 발생 가능성을 줄이기 위해 ISN을 무작위 난수로 사용하는 것이다.

<img src="/Users/pro/Library/Application Support/typora-user-images/스크린샷 2021-05-08 오후 11.17.08.png" alt="스크린샷 2021-05-08 오후 11.17.08" style="zoom:50%;" />

<img src="/Users/pro/Library/Application Support/typora-user-images/스크린샷 2021-05-08 오후 10.59.51.png" alt="스크린샷 2021-05-08 오후 10.59.51" style="zoom:50%;" />

1. Client가 연결하고자 하는 Server에게 seq port (2915269997) 전송

2. Server가 해당 seq port를 받고 해당 숫자에 1을 더한 ack port (2915269998) + Client의 연결을 확인하고자 하는 seq port (1458477026) 전송

3. Client가 Server의 seq port를 받고 해당 숫자에 1을 더한 ack port (1458477027)을 Server에 전송

   

   

## TCP 4 way handshake

> 가상 회선 연결을 해제



1. A -> B: 나는 다 보냈어. 이제 끊자! 
2. B -> A: 알겠어! 잠시만~
3. B -> A: 나도 끊을게!
4. A -> B: 알겠어!

<img src="/Users/pro/Library/Application Support/typora-user-images/스크린샷 2021-05-08 오후 11.59.24.png" alt="스크린샷 2021-05-08 오후 11.59.24" style="zoom:35%;" />



​	FIN = Finish : TCP 연결을 종료하겠다는 메시지

 <img src="/Users/pro/Library/Application Support/typora-user-images/스크린샷 2021-05-09 오전 12.01.44.png" alt="스크린샷 2021-05-09 오전 12.01.44" style="zoom:40%;" />



#### Time-Wait

>  먼저 연결을 끊는 (active closer) 쪽에 생성되는 소켓으로, 혹시 모를 패킷 전송 실패에 대비하기 위하여 존재하는 소켓



### Time-wait이 없다면?

##### EX) Passive closer에서 보낸 FIN 메시지에 대해 Active closer가 보낸 ACK를 Passive closer가 받지 못한 경우

1. Passive Closer의 FIN 메시지 전송
2. Active Closer가 수신 후 ACK 메시지 전송 후, 통신 끊음 (Time-wait X)
3. Passive Closer가 ACK를 수신하지 못함 

4. 일정 시간 후, ACK를 수신하지 못한 Passive Closer가 다시 FIN 메시지 전송.
5. Active Closer는 이미 Closed 상태이기 때문에 FIN 메시지 수신 불가
6. TCP 통신이 제대로 끊기지 않음
