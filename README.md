# CCNP
- 헷갈리거나 몰랐던 내용들

---------------------------------
- Directed Broadcast : 허용하면 서브넷 범위의 브로드캐스트 주소를 이용하여, 브로드캐스트 요청이 가능함. ex) 192.168.154.0/24 범위의 192.168.154.255 주소로 ping을 요청하면 해당 서브넷의 모든 노드들이 응답을 함.
- MAC 주소 계산 및 요청등의 기본은 Next Hop 이다.
- FIB (Forward Information Base)는 route table의 핵심(목적지, 출력 인터페이스, 다음 홉 등)을 하드웨어칩 (ASIC)에 복사해뒀다가, 패킷이 들어오면 CPU를 거치지 않고 포워딩함




# OSPF
------------------------------------
- ip ospf 는 기존 v4 에서 쓰이고, 그냥 ospf 는 ospfv4나 v6 에서 쓰이는 명령어
- 




# Qos
------------------------------------
- Bandwidth : 시간당 전송 가능한 데이터 양
- Latency : 데이터가 출발지부터 목적지까지 걸리는 시간
- Jitter : 데이터 전송의 시간 간격이 일정하지 않고 변하는 현상
- Baudrate : 초당 변조되는 신호의 변화 횟수

- Qos 과정
  - marking/classify - queueing - policing/shaping

- Cos
  - 2계층 우선순위 마킹하는 기술 
  - Vlan tag ( 802.1q 내부의 priority code point - 3bit ) 사용
  - 0 부터 7까지 (7이 가장 우선 순위) 지정 가능
  - LAN 이나 VLAN 내부에서만 유효하며, WAN으로 이동시 이더넷 헤더가 바뀌면서 Cos 정보는 삭제

- DSCP
  - 3계층 우선순위 마킹 기술
  - IP 헤더의 Type of service필드 중 6bit 사용
  - 0 부터 63까지 지정 가능
  - WAN을 넘어가도 End to End로 정보 유지
 
- DSCP 세부
  - EF : 최고 우선 순위 전송 (Voip 등) , 대표 코드 (46)
  - AF : 트래픽을 클래스와 드롭 순위를 세분화 함
    - 클래스는 1 - 4번까지, 4번이 높은 우선 순위
    - 드롭 순위는 1 - 3번까지, 3번이 가장 낮은 우선 순위
  - BF : 기본 전송
 


# MTU
-----------------------------------------
<img width="853" height="340" alt="image" src="https://github.com/user-attachments/assets/2bcbe940-52e5-47e3-9d15-4984222fdda6" />

- Ethernet MTU : 이더넷 프레임에서, 이더넷 헤더와 트레일러를 제외한 페이로드의 크기
- 
