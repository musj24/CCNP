# CCNP
- 헷갈리거나 몰랐던 내용들

---------------------------------
- Directed Broadcast : 허용하면 서브넷 범위의 브로드캐스트 주소를 이용하여, 브로드캐스트 요청이 가능함. ex) 192.168.154.0/24 범위의 192.168.154.255 주소로 ping을 요청하면 해당 서브넷의 모든 노드들이 응답을 함.
- MAC 주소 계산 및 요청등의 기본은 Next Hop 이다.
- FIB (Forward Information Base)는 route table의 핵심(목적지, 출력 인터페이스, 다음 홉 등)을 하드웨어칩 (ASIC)에 복사해뒀다가, 패킷이 들어오면 CPU를 거치지 않고 포워딩함

- ethernet
<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/2aa9ddf3-71dc-4c83-8a4e-b527ef388045" />


- IP
<img width="1402" height="1122" alt="image" src="https://github.com/user-attachments/assets/7f78b82a-6aaf-4a8a-a7ee-854bd2334b42" />

- TCP/UDP
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/5342d1ea-f96f-4681-a879-c13e59af5e8c" />




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

- Ethernet MTU : 이더넷 프레임에서, 이더넷 헤더와 트레일러를 제외한 페이로드의 크기 (1500) , 인터페이스에서 수신 가능한 페이로드의 최대 크기를 지정


<img width="1406" height="343" alt="image" src="https://github.com/user-attachments/assets/cab2f8aa-092f-425a-9d41-2c821f2f5c69" />

- IP MTU : IP, TCP 헤더와 데이터를 합한 크기 (1500) , 조각화 되기전의 최대 크기를 지정 (L2 에선 조각화가 불가능하고, 드롭만 가능함) , IP MTU는 Ethernet MTU의 값보다 작거나 같다

<img width="1898" height="352" alt="image" src="https://github.com/user-attachments/assets/687405ca-5111-4a67-80aa-db0c94e63981" />

- system MTU : 시스템 전체에 MTU 적용 (인터페이스에 적용하는 MTU가 우선순위가 더 높음)
 - system mtu : 1/100mbps 이더넷 인터페이스에 적용되는 MTU
 - system jumbo mtu : 1g/10gbps 이더넷 인터페이스에 적용되는 MTU
 - system alternate mtu : 또 다른 옵션
 - system routing mtu : 시스템 전체에 적용되는 IP MTU

<img width="996" height="442" alt="image" src="https://github.com/user-attachments/assets/c775278f-5b3f-4299-b182-12e04c390bab" />

- GRE 환경 MTU
  - GRE 터널 환경에선 기존 IP 패킷에 GRE 헤더 (4byte)와 Outer IP 헤더 (20byte)가 추가 되기 때문에, 기존 패킷에 24byte가 더해진다.
  - 따라서 터널의 MTU는 기존 MTU보다 24byte 적게 설정해야 한다.



- baby giant : 1500 보단 크고, 점보 보단 작음
- jumbo : 1500 보다 훨씬 큼
- super jumbo : 데이터 센터등에 사용되는 매우 큰 프레임
- Runt : 최소 크기보다 작은 프레
- PMTUD : 조각화가 필요없는 경로를 찾는 절차.
    - DF bit를 set 하고 패킷을 보냈을때, 받는쪽의 MTU보다 패킷이 크다면 drop 해버리고 크기를 더 작게 보내라고 메시지를 보내어 drop 되지 않을때까지 패킷 크기를 조절함


# MSS
------------------------------------------------
- TCP MSS : 순수 데이터의 크기 (1500 - IP,TCP 헤더 20 20 = 1460)
- 
