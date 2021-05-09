# TCP 3, 4 Way Handshake



# 1. TCP 헤더

<img src="https://s3.ap-south-1.amazonaws.com/afteracademy-server-uploads/what-is-a-tcp-3-way-handshake-process-tcp-header-b4e17a1675ac1e86.jpg" alt="img" style="zoom: 67%;" />

- TCP 헤더의 구성은 위 그림과 같다. 이중 아래 요소들이 TCP 연결 수립/종료에 사용된다 
  1. Sequence number : 무작위 32비트 숫자. 한 연결에 한번만 사용된다. 같은 연결에 다른 데이터 전송 시 다른 숫자가 사용된다
  2. Acknowledgement number : acknowledgement를 전송하는 기기가 기대하는 숫자. 보통 전송 받은 sequence number보다 1 크다. ACK flag가 1일때만 유효한데, ACK flag가 1이 아닐 때는 연결 수립 때 만이다. 
  3. Window size : 버퍼 사이즈
  4. Maximum segment size : 수용 가능한 최대 데이터 세그먼트 크기
  5. SYN flag : 연결 수립 요청을 위한 플래그 (SYN = 1, 연결 요청)
  6. ACK flag : SYN에 응답을 위한 플래그 (ACK = 1, SYN에 응답)
  7. FIN flag : 연결 종료를 위한 플래그 (FIN = 1, 연결 종료)



# 2. TCP 연결 수립

> 가상회선을 수립하는 단계. 3 way handshake로 이뤄진다

- 클라이언트는 서버에 요청을 전송할 수 있는지, 서버는 클라이언트에게 응답을 전송할 수 있는지 확인하는 과정

<img src="https://s3.ap-south-1.amazonaws.com/afteracademy-server-uploads/what-is-a-tcp-3-way-handshake-process-three-way-handshaking-establishing-connection-6a724e77ba96e241.jpg" alt="img" style="zoom:67%;" />

- SYN과 ACK 패킷을 주고 받으며, 데이터 전송 전 두 기기 간 연결을 수립한다

  1. 클라이언트에서 SYN 요청을 보낸다. SYN flag를 1로 하여 서버에 보낸다. 

  2. 서버가 SYN 요청을 받고 SYN + ACK를 한 패킷에 보낸다. ACK flag를 1로하고 클라이언트에 보낸다. acknowledgement number는 seq(m) + 1이다. SYN flag도 1이다. 이때 seq은 클라이언트에서 보낸 요청 때 숫자와 다른 숫자이다. 이 단계에서 클라이언트에서 서버로 연결이 수립된다

  3. 클라이언트가 SYN 요청을 받고 ACK를 보낸다. ACK flag를 1로하고 서버에 보낸다. acknowledgement number는 seq(n)+1이다. SYN flag는 0이다. 이 단계에서 서버에서 클라이언트로 연결이 수립된다. 양쪽의 max segment size중 더 작은 값이 데이터 전송 시 사용된다.  

     

- seq에 랜덤 숫자를 사용하는 이유

  - TCP 연결에 포트 넘버는 수가 제한적이어서 seq이 없을 시 다른 연결의 전송과 혼동될 수 있기 때문에 seq이 필요하다

  1. 다른 연결 간 seq 충돌을 피하기 위해 랜덤 숫자를 사용한다

  2. seq이 예측 가능하면 보안 문제가 발생할 수 있다. ie) TCP seq prediction attack

     https://en.wikipedia.org/wiki/TCP_sequence_prediction_attack



# 3. TCP 연결 종료

> 일반적으로 4 way handshake로 이뤄지지만 3 way도 가능하다

- 연결 종료는 양쪽에서 일어날 수 있기 때문에 연결 해제 요청 측(Active close)과 연결 해제 요청을 받은 측(Passive close)으로 나뉜다

![TCP의 3 way Handshake과 4 way Handshake](https://img1.daumcdn.net/thumb/R720x0.q80/?scode=mtistory2&fname=http%3A%2F%2Fcfile23.uf.tistory.com%2Fimage%2F2301313E5815FF5A277878)



- FIN과 ACK 패킷을 주고 받으며, 데이터 전송 전 두 기기 간 연결을 종료한다

  1. A에서 FIN 요청을 보낸다. FIN flag를 1로 하여 B에 보낸다. 
  2. B에서 FIN 요청을 받고 ACK로 응답한다
  3. B에서 FIN 요청을 보낸다
  4. A에서 ACK로 응답한다

- 각각 한쪽의 연결을 종료하는 FIN-ACK 쌍으로 이뤄져 있어. 한쪽만 연결을 종료한 상태인 Half-open 상태도 가능하다

  

# 4. TCP 연결 상태

> TCP 연결은 생성 후 종료 시까지 여러 상태를 거친다. 

![TCP state transition diagram](https://www.ibm.com/docs/en/SSLTBW_2.1.0/com.ibm.zos.v2r1.halu101/dwgl0004.gif)



| 상태        | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| CLOSE       | 커넥션 없음                                                  |
| LISTEN      | Passive open, SYN을 기다리는 상태                            |
| SYN-SENT    | SYN을 보내고 ACK를 기다리는 상태                             |
| SYN-RCVD    | SYN+ACK을 보내고 ACK를 기다리는 상태                         |
| ESTABLISHED | 커넥션이 생성된 상태, 데이터를 전송할 수 있다.               |
| FIN-WAIT-1  | 첫 FIN이 보내진 상태, ACK를 기다리고 있다.                   |
| FIN-WAIT-2  | 첫 FIN에 대한 ACK를 받은 상태, 2번째 FIN을 기다리고 있다.    |
| CLOSE-WAIT  | 첫 FIN을 받고 ACK를 보낸 상태, 어플리케이션의 종료를 기다리고 있다. |
| TIME-WAIT   | 2번째 FIN을 받고 ACK를 보낸 상태, 동일 포트와 주소에 커넥션이 생성되지 않도록 하는 시간(2MSL time out)을 기다리는 상태 |
| LAST-ACK    | 2번째 FIN을 보내고 ACK를 기다리는 상태                       |
| CLOSING     | 양쪽이 동시에 닫기로 한 상태                                 |



# 5. TCP 연결 종료의 다양한 상황들

> 연결 수립은 통신을 하고자 할 때 발생한다. 종료는 조금 더 복잡하다.



## 5-1. 일반적인 종료 상황

- 4 way handshake(혹은 3 way)를 통해 위에서 설명한 과정대로 연결을 종료한다



## 5-2. TCP Half Close

- 한쪽만 연결을 종료한 상태. 장애로 발생한 문제일 수도 있고 의도적이 기능일 수도 있다
- 장애 발생 시 : half close 상태로 있을 수 있는 시간 제한이 있기 때문에 그 시간 이후 종료된다
  - DoS 공격으로 악용될 수도 있다
  - 완벽한 half close 연결 관리를 TCP가 지원하지 않기 때문에 애플리케이션 수준에서 관리해야한다

![graphics/18fig10.gif](https://flylib.com/books/3/223/1/html/2/files/18fig10.gif)

- 의도적 기능 : 클라이언트는 서버가 언제까지 데이터를 전송할지 모르기 때문에 필요하다

![img](https://postfiles.pstatic.net/MjAxOTA0MTFfMjMg/MDAxNTU0OTMzNjI4ODYy.9njHtB7ljEChY4ididDc1TjNfr0y3qElZC4_hE8rlRUg.lcNa93IDD2GzyPwgtNDM3j8pz03SLzuRjMinHaoYUCog.PNG.ihp0001/image.png?type=w773)

## 5-3. TCP Simultaneous Close

- 양쪽에서 FIN을 받기 전 서로 FIN을 요청한 경우 아래와 같이 연결 종료가 진행된다 

![img](http://www.tcpipguide.com/free/diagrams/tcpclosesimul.png)

- MSL : TCP 세그먼트가 네트워크에서 존재할 수 있는 최대 시간. 기본적으로 2분이지만 변경 가능하다