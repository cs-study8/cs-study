# TCP와 UDP의 차이점



# 1. TCP(Transmission Control Protocol)

> 두 종단 간 연결을 설정한 후 세크먼트 단위 데이터를 전송하는 **연결형** 프로토콜

<img src="https://media.vlpt.us/images/sangmin7648/post/1990e2f9-b466-4223-84da-1134ab1a53f9/image.png" alt="img" style="zoom:80%;" />

- OSI 7계층 기준으로 전송 계층 프로토콜에 해당한다
- 프로세스 간 메시지 전달을 위해 포트 번호를 이용하고 다중연결을 허용해 여러 프로세스가 동시에 연결 가능하다
- 흐름제어와 혼잡제어를 수행한다
- TCP의 연결지향형 방식을 신뢰성 스트림 서비스라고도 한다 

<img src="https://media.vlpt.us/images/sangmin7648/post/a9a0fb84-c7dd-4ec9-97d4-ef5e065c0903/image.png" alt="img" style="zoom:80%;" />



## 1-1. TCP 세그먼트 데이터 전송

> 슬라이딩 윈도우를 사용한 피기백 방식의 흐름 제어 지원

- 슬라이딩 윈도우 : 흐름제어 기법. 전송한 프레임에 대한 ACK 프레임을 수신하지 않더라도 여러 프레임을 연속적으로 전송하도록 허용한다

  - 송신 측에서 프레임에 번호를 붙여 윈도우 크기만큼 프레임을 전송하고 대기. 전송 프레임 버퍼에 저장

  - 수신 측에서 프레임을 수신하면 ACK + 프레임 번호를 송신 측에 통보

  - 송신 측은 ACK를 확인하면 해당 프레임을 버퍼에서 지우고 다음 차례의 프레임 수신 측에 전송 

    

- 피기백 : 양방향 전송을 지원하는 경우, 송수신 측 구분 없이 모두 정보 프레임과 응답을 전송

  - 상대방의 정보 프레임에 대한 ACK를 별도의 응답으로 보내지 않고 정보 프레임에 담아 보내 전송 회수 줄임

<img src="https://media.vlpt.us/images/sangmin7648/post/23a3a04f-3395-4adc-9b3d-96019c78edc5/image.png" alt="img" style="zoom:80%;" />

- TCP의 흐름제어 :
  - 송신 측 세그먼트 번호와 데이터 크기를 데이터와 함께 전송
  - 수신 측 세그먼트를 수신할 겨우 ACK 응답과 다음 세그먼트 번호 전송
  - 피기백 방식으로 송수신 동시에 처리



## 1-2. TCP의 오류 처리

- 데이터 전송 오류

  - 수신 측에서 변형된 프레임을 받으면 분실로 간주하고 NAK 응답 없이 대기
  - 송신 측에서 ACK를 받지 못해 타임아웃이 발생, 동일한 번호의 프레임 재전송

- ACK 전송 오류

  - 수신 측에서 번호가 동일한 프레임을 받으면 중복으로 판단하여 버리고 ACK 응답 

  

<hr>

# 2. UDP(User Datagram Protocol)

> 두 종단 간 연결을 설정하지 않고 데이터를 고속으로 교환하는 **비연결형** 프로토콜

- OSI 7계층 기준으로 전송 계층 프로토콜에 해당한다
- 프로세스 간 메시지 전달을 위해 포트 번호를 이용하고 다중연결을 허용해 여러 프로세스가 동시에 연결 가능하다
- 수신 측에 데이터가 도착했는지 확인하지 않음
- 신뢰성이 비교적 낮으며 **흐름 제어 및 오류 검출 기능이 없어** 패킷을 빠르게 전송해야하는 응용 계층에서 사용
- 오버헤드의 크기가 크지 않으며, 연결 등에 대한 상태 정보를 저장하지 않음
- 단방향 전송으로 데이터를 일방적으로 보낸다

![img](https://media.vlpt.us/images/sangmin7648/post/0b003f7e-cd03-4d25-a7ad-7d07406f776b/image.png)

- 영상 스트리밍, VoIP 같이 데이터 신뢰성보다 지속적으로 많은 데이터를 받는 것이 중요한 서비스를 위해 제시됐다



<hr>



# 3. TCP vs UDP

![img](https://media.vlpt.us/images/sangmin7648/post/8a1f9e39-699b-41f4-abe9-f0e67f97463d/image.png)



<hr>



# 4. 포트번호

> TCP가 상위 계층으로 또는 상위 계층에서 TCP/UDP로 데이터를 전송할 때 상호 간 사용하는 데이터의 이동 경로

- IP를 통해 두 종단 간 컴퓨터를 연결한다면, 프로세스와 연결하기 위해선 포트번호가 필요하다 
- 0~65535번 포트가 사용 가능하다
- 0~1023번 포트는 주요 인터넷 서비스에 고정 할당 되어있다
- **소켓 주소 : IP주소 + 포트 번호**. 각 프로세스를 구분한다

![img](https://media.vlpt.us/images/sangmin7648/post/47328c89-7ff9-477a-9ad3-636988d53b9b/image.png)

- UDP와 TCP의 포트 번호는 별개이다

