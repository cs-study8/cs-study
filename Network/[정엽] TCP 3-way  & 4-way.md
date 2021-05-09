# TCP 연결 설정과 해제

## 3-way handshake

 TCP 통신을 이용해 데이터를 전송하기 위해 네트워크 연결을 설정하는 과정

- 양쪽 모두 데이터를 전송할 준비가 되어있다는 것 보장

![img](https://gmlwjd9405.github.io/images/network/3-way-handshaking.png)

1. A -> B 
   - 접속 요청 프로세스 A가 연결 요청 메시지 전송 (SYN)
   - 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고 SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다
   - 포트 상태 - A : CLOSED - 포트가 닫힌 상태 , B : LISTEN - 포트가 열린 상태로 연결 요청 대기 중
2. B -> A 
   - 접속 요청을 받은 프로세스 B가 요청을 수락하고 접속 요청 프로세스인 A도 포트를 열어달라는 메시지 전송(SYN + ACK)
   - 수신자는 Acknowledgement Number 필드를 (Sequence + 1)로 지정하고, SYN과 ACK 플래그 비트를 1로 설정한 세그먼트를 정성한다
   - 포트 상태 - A: CLOSED, B : SYN_RCV - SYNC 요청을 받고 상대방의 응답을 기다리는 중 
3. A -> B 
   - 포트 상태 - A: ESTABLISHED, B: SYN_RCV
   - 마지막으로 접속 요청 프로세스 A가 수랑 확인을 보내 연결을 맺는다 (ACK)
   - 포트 상태 - A : ESTABLISHED, B: ESTABLISHED - 포트 연결 상태

## 4-way handshake

- TCP 연결 해제

![img](https://blog.kakaocdn.net/dn/cOOd6d/btqxrWdWGha/9K8vKCDGBPIeOoV8AJHr9K/img.png)

1. A -> B : FIN
   - 프로세스 A가 연결을 종료하겠다는 FIN 플래그를 전송
   - 프로세스 B가 FIN 플래그로 응답하기 전까지 연결을 계속 유지
   - A 포트 FIN_WAIT1 상태, 통신을 위한 자료구조등 필요한 정보를 폐기하기 때문에 더 이상 서버에게 데이터를 전달할 수 없는 상태 
2. B -> A : ACK 
   - 일단 확인 메시지를 보내고 자신의 통신이 끝날 때까지 기다린다
   - 수신자는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다
   - 그리고 전송할 데이터가 남아있다면 이어서 계속 전송한다
   - A 포트 FIN_WAIT2 상태
3. B -> A : FIN
   - 프로세스 B가 통신이 끝났으면 연결 종료 요청에 합의한다는 의미로 프로세스 A에게 FIN 플래그를 전송한다
4. A -> B : ACK
   - 프로세스 A는 확인했다는 메시지 전송

### TCP HEADER안의 플래그 정보

TCP Header에는 Control Bit(플래그 비트, 6bit)가 존재하며, 각각의 bit는 "URG-ACK-PSH-RST-SYN-FIN"의 의미를 가진다

- 해당 위치의 비트가 1이면 해당 패킷이 어떤 내용을 담고 있는지 알 수 있다.