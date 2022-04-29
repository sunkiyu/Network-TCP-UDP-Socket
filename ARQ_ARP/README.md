출처 http://www.ktword.co.kr/

# ARQ (Automatic Repeat Request) 자동 재전송 요구, 검출후 재전송 방식
ㅇ 정지대기방식 (Stop and Wait, Idle ARQ)
     - 한 번에 하나씩 긍정 확인응답(ACK)을 받고, 후속 데이터 전송
     - 가장 단순하나, 다소 비효율적
     - 반이중 방식에서도 가능
 
  ㅇ Go Back n ARQ (GBN) 또는 Continuous ARQ(연속적 ARQ)
     - 한번에 여러 개를 보낸후 하나의 긍정 확인응답(ACK)을 받고, 후속 데이터 전송.
     - NAK(부정 확인응답)를 수신할 때까지 계속하여 데이터를 송신함.
     - 전이중방식에서 동작함
     * `슬라이딩 윈도우 (Sliding Window) 방식` 이라고도 불리움
# ARP
* ARP(Address Resolution Protocol)   
-> 논리적인 IP 주소 -> 물리적 MAC 주소로 바꾸는 역할을 하는 주소 해석 프로토콜   

* 라우터 상의 ARP 동작   
1. ARP 요청   
* LAN의 라우터에 외부로부터 데이터 패킷이 전달되어 목적지 호스트를 찾을 때, 라우터가 최초로 하는 일은   
* ARP Request Packet(ARP 요청 패킷)을 LAN 전체에 브로드캐스팅 함.    
* 이때, ARP 요청 메세지는 자신의 MAC/IP 주소, 목적지 IP 주소를 채우고 목적지 MAC 주소는 0으로 넣음   

2. ARP 응답   
* ARP 요청 패킷에 포함된 IP 주소와 일치하는 Host는 자신의 IP/물리 주소를 채워넣은 ARP 응답패킷을 해당 라우터에게 송출하여 물리/IP 주소 상호간의 정보를 얻음   

