# CCNP
- 헷갈리거나 몰랐던 내용들

---------------------------------
- ARP 테이블은 자기 대역 내에서만 올라온다. 네트워크가 넘어가면 어차피 GW로 타야하니까.
- Directed Broadcast : 허용하면 서브넷 범위의 브로드캐스트 주소를 이용하여, 브로드캐스트 요청이 가능함. ex) 192.168.154.0/24 범위의 192.168.154.255 주소로 ping을 요청하면 해당 서브넷의 모든 노드들이 응답을 함.
- MAC 주소 계산 및 요청등의 기본은 Next Hop 이다.
- control plane : 라우팅 프로토콜 및 테이블 구축
- data plane : 경로 찾기 및 실제 데이터 포워딩
- 패킷 스위칭 : L3 포워딩
- 프레임 스위칭 : L2 포워딩
- 재귀경로 : ip route 192.168.2.0 255.255.255.0 10.1.1.2 등으로, Next hop을 ip 주소로 지정하는 방식
  - 192.168.2.0/24로 나가는 경로를 10.1.1.2 주소의 인터페이스로 잡기위해, 10.1.1.2 를 가지고있는 인터페이스를 다시 RIB에서 검색하는 재귀적 방법
  - 10.1.1.2와 인터페이스 방향 하나만 테이블에 올라와, ARP 테이블이 간결함
- 직접연결 정적 경로 : ip route 192.168.2.0 255.255.255.0 GigabitEthernet0/1 등으로, netx hop을 인터페이스로 지정하는 방식
  - 192.168.2.0/24로 나가는 경로를 특정 인터페이스로 지정함. PtoP 환경에서 주로 사용함.
  - next hop에 대한 주소를 모르기 때문에, 목적지 주소에 대해 바로 ARP를 수행함 (직접 연결로 간주하는 상태) 상대 장비가 Proxy ARP를 안해주면 통신 불가능
  - 목표 IP 주소 하나마다 ARP 테이블이 채워지기 때문에, 테이블 고갈 가능성이 있음
- 완전지정 정적 경로 : next hop을 ip와 인터페이스 둘다 지정하여, 빠르게 포워딩도 하면서 ARP 대상도 명시하는 방법 (권장)
- logging monitor , console , buffer (terminal monitor)

- ethernet
<img width="1774" height="887" alt="image" src="https://github.com/user-attachments/assets/2aa9ddf3-71dc-4c83-8a4e-b527ef388045" />


- IP
<img width="1402" height="1122" alt="image" src="https://github.com/user-attachments/assets/7f78b82a-6aaf-4a8a-a7ee-854bd2334b42" />






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
 


# MTU (2 ~ 3계층)
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
- Runt : 최소 크기보다 작은 프레임
- PMTUD : 조각화가 필요없는 경로를 찾는 절차.
    - DF bit를 set 하고 패킷을 보냈을때, 받는쪽의 MTU보다 패킷이 크다면 drop 해버리고 크기를 더 작게 보내라고 메시지를 보내어 drop 되지 않을때까지 패킷 크기를 조절함
    - 하지만 상대가 보안상 ICMP 응답을 deny 하면 ICMP 단편화 필요 응답을 받을수 없기 때문에 불가능 함


# MSS (4계층 전용 (TCP 등))
------------------------------------------------
- TCP MSS : 순수 데이터의 크기 (1500 - IP,TCP 헤더 20 20 = 1460)
- 전송 가능한 TCP 메시지의 크기를 정함
- 기본값으로, 로컬네트워크는 1460byte, 타네트워크는 536byte이다.


# TCP
-------------------------------------------------
- TCP/UDP
<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/5342d1ea-f96f-4681-a879-c13e59af5e8c" />

- Window Size : host가 Ack 받기전에 수신 가능한 데이터의 크기


# CEF (FIB)
---------------------------------------------------
- FIB (Forward Information Base)는 route table의 핵심(목적지, 출력 인터페이스, 다음 홉 등)을 하드웨어칩 (ASIC)에 복사해뒀다가, 패킷이 들어오면 CPU를 거치지 않고 포워딩함
- ASIC : 패킷을 고속 처리하는 전용 칩. CPU와 다르게 패킷 포워딩 작업 처리에 특화됨
- CAM : 콘텐츠 주소 지정메모리. 스위치가 MAC 주소를 빠르게 조회하는 데 사용하는 메모리
- TCAM : CAM이 L2 주소를 처리한 후에, L3 주소를 확인하는 메모리. FIB가 저장됨

- 패킷 포워딩기반
  - 소프트웨어 : 범용 CPU를 사용하여 포워딩 함. control 및 data plane이 공유됨. 느리지만 프로그래밍이 가능하고 유연함
  - 하드웨어 : CPU가 control plane을 처리하고, ASIC이 data plane 처리함
  - 하이브리드 : CPU가 control plane을 처리하고, Network Processor가 data plane 처리함
    - NP : 패킷 전달 및 기타 네트워크 관련 기능을 위한 프로세서. 프로그래밍 가능하고 유연함. NP가 처리 불가능한 패킷은 CPU가 처리함

- 패킷 포워딩 방법
  - process switching : 라우터가 각 패킷에 대해 CPU를 사용하여, 라우팅 테이블 조회를 수행함
  - fast switching : 라우터가 메모리에 고속 전환 캐시를 구축하여, 후속 캐시에 대해 빠른 조회 및 포워딩 지원
  - CEF : data plane에 구축된 두 개의 캐시를 이용하여 빠른 포워딩
    - FIB : control plane에 있는 RIB를 기반으로, data plane에 재구성. L3 정보 제공
    - adjancency table : ARP 테이블 기반으로 구축함. L2 정보 제공

- 로드 밸런싱
  - per-destination : 패킷의 src/des IP를 참조하여 암호 생성함. 그것과 같은 암호들은 같은 회선으로 이동
  - per-packet : 패킷을 RR 방식으로, 정확히 분배함

- DCEF
  - 분배형CEF
  - CPU가 만든 FIB / 인접 테이블의 복사본을 각 슬롯, 라인 카드등에 탑재하여, 개개인의 ASIC과 TCAM, 인접 테이블등을 가지고 빠른 처리 가능


# L2
-----------------------------------------------------
- mac address-table aging-time : 기본 300초
- mac address-table static 0c84.639c.0000 vlan [] int [] : 인터페이스에 mac 주소를 static 매핑
  - vlan을 지정 하는 이유
    - 동일한 MAC 주소가 다른 vlan에 있을수 있기 때문(vlan 마다 mac table 존재)
    - 스위치의 동작 방식이 MAC 주소 보다 vlan을 먼저 확인하기 때문
    - Trunk port 등

# L3
-----------------------------------------------------
- 라우팅 테이블 올릴때, AD를 고려하여 올린다. 경로를 결정할땐 LPM을 우선 고려하고 값이 같다면 Metric을 비교한다.
- show ip route [ip] : RIB 기반으로 경로 출력
- show ip cef [ip] : FIB 기반으로 경로 출력

# ARP
-----------------------------------------------------
- show logging : logging level 확인 및 log 확인
- logging console [] : logging level 설정
- debug arp

# Memory
-----------------------------------------------------
- ROM : 컴퓨터의 BIOS. 하드웨어 부팅 (POST) , ROMMON 담당.
- DRAM : 컴퓨터의 RAM. running config , RIB, 로그 등 실시간 설정
- SRAM : DRAM보다 작고 빠름. 인접테이블 및 캐시 버퍼 등
- NVRAM : start config 저장
- flash : SSD. OS등 저장
- EEPROM : 장비 DNA 확인

# Switch stacking
-----------------------------------------------------
- 여러 대의 스위치를 논리적인 하나로 묶는 기술
- 장비 config 관리 및 STP로 인한 대역폭 차단을 완화하기 위해 사용. Control plane은 활성 스위치에 의해 관리되고, data plane은 분산됨
- MEC : 멀티 섀시 이더채널, 서로 다른 스위치를 하나의 논리적 스위치로 묶어서, 이더채널을 사용함
  - 채널을 각기 스위치 A,B에 나누어 꽂아도 STP로 인한 block이 없음
  - 이중화 가능 및 대역폭 + 로드밸런싱 온전히 사용 가능
- Interface Numbering : Switch/Slot/Port

- StackWise : 전용 스태킹 포트에 연결하여 1대의 Master와 나머지의 Member로 묶음
  - SDP : Stack/StackWise Discovery Protocol : 이웃 찾는 프로토콜

- VSS : 레거시 기술, VSL (virtual switch link)로 상호 연결. 2대만 연결 가능하며, Active/Standby로 나뉨
  - VSLP : VSL 제어 프로토콜
    - LMP : Link Management Protocol, 이웃 장비와 케이블 상태 확인. 단방향 링크 거부함
    - RRP : Role Resolution Protocol, priority 기반으로 Active/Standby를 결정함
  - RPR :  Standby로 전환시, RIB와 OSPF 상태 등을 reboot하여 처음부터 시작하는 프로토콜, Standby는 기본적으로 최소한의 가동 준비만 하고있음
  - SSO : Standby가 Active와 동일한 정보를 실시간으로 복사하여 대기하는 상태, Active down시 즉시 넘겨받음
- StackWiseVirtual : VSS와 마찬가지로, 2대만 상호 연결. SVL (stackwise virtual link)로 연결하며, Activa/Standby로 나뉨
  - VSS와 차이 : DAD (Dual-Active Detection)
  - Active와 연결이 끊겼을때, 서로 Active가 되려고 하는 SplitBrain 현상을 막기위한 기술
  - 별도의 백업 감시선을 연결하여, SVL이 끊겨도 Active의 생존을 알림

# SSO (고가용성)
----------------------------------------------------
- Active가 Down 됐을때, Standby로 넘어가는 방법
- SSO : Stateful SwitchOver, Standby가 Active의 MAC 주소, 인터페이스 정보, FIB 등을 복사해 뒀다가, Active 사망시 바로 전환하여 Forwarding을 멈추지 않음
  - OSPF 상태등을 알지는 못함
- NSF : Non-Stop Forwarding, SSO와 함께 움직이는 기술. 라우팅 프로토콜이 죽은동안, FIB를 지우지 않고 계속 포워딩함. (라우팅 프로토콜 재부팅동안 FIB를 지우지 않는 역할이 메인)
- GR : Graceful-Restart, NSF를 달성하기 위한 기술. 주변 helper 들의 도움을 받아 OSPF 인접을 끊지 않고 패킷 포워딩 수행 가능하게 함
- NSR : Non-Stop Routing, Standby가 Active의 control plane 전체를 실시간 동기화 해뒀다가, 장애시 이어받음. helper 필요 없음

- cold standby : 백업이 전원만 켜져있고, OS 등을 올리지 않은 상태
- warm standby : OS 등은 올려놨지만, FIB/MAC 등은 올리지 않은 상태
- hot standby : Active와 완전 동기화되어 대기하는 상태

# 부팅 타입
-----------------------------------------------------
- Cold boot : 장비의 전원이 꺼진 상태부터, 하드웨어와 소프트웨어를 부팅
- warm boot : 전원은 켜져있고, reload 등으로 시스템만 재시작

# SDM
----------------------------------------------------
- Swithcing Database Manager : ASIC 내부의 CAM과 TCAM에 할당할 장부 등록 제한 설정
  - 스위치가 L2 위주라면 CAM을, L3 위주라면 TCAM 위주로 장부를 등록한다

# ICMP
----------------------------------------------------
<img width="1472" height="825" alt="image" src="https://github.com/user-attachments/assets/1d860af9-a4ea-4125-b0e7-63d386acee45" />


- L3 프로토콜
- IP 헤더의 protocol 번호 1번
- payload에 ICMP 헤더와 ICMP data 포함됨
- Header
  - 8byte 고정 값
  - 1byte : type , 1byte : code , 2byte : checksum, 4byte : rest of header
  - type
    - 0 : reply
    - 3 : Unreachable
    - 5 : redirect
    - 8 : request
    - 11 : time exceeded
  - Unreachable code
    - type 3일때, 그 사유를 설명해주는 code
    - code 0 : network unreachable, 해당 network의 route가 없음
    - code 1 : host unreachable , 해당 network의 route는 찾았지만, 대상 장비의 응답이 없음
    - code 2 : protocol unreachable, 장비와 Ping 연결은 성공했지만 프로토콜 처리가 안되는 경우
    - code 3 : port unreachable, 장비가 해당 서비스를 거부하고 있는 경우
    - code 4 : DF bit set , MTU를 초과하는 패킷을 분할 거부하는 경우
    - code 13 : administratively prohibit , ACL 등에 거부당하는 경우
  - redirect
    - 호스트에게 목적지를 향한 다른 경로를 사용하도록 알리는 데 사용
  - time exceeded
    - TTL 또는 단편화 재조립 대기 시간 초과 등
    - code 0 : TTL 만료
    - code 1 : 단편화 재조립 대기 시간 초과
  - rest of header
    - type 0 , 8 : 핑 송수신때, 앞의 2byte가 프로세스 구분, 뒤의 2byte가 순서 구분
    - type 3의 code 4 : 앞의 2byte는 unuse, 뒤의 2byte는 netx-hop MTU 삽입
    - type 5 : 지름길의 IP 주소 삽입
- ping
  - icmp type 0 , 8 이며, code 는 항상 0이다.
  - rest of header : Identifier / Sequence Number
  - Identifier : 명령어 한번 기준의 식별자, "ping" 이란 명령 한번의 request / reply 는 같은 식별자를 가진다
  - Sequence Number : request / reply 의 순서, ping 명령에서 각 request 와 reply는 같은 짝의 번호를 가진다
  - 최소 크기인 46byte를 위해, 18byte의 padding을 추가 하기도함
- ICMPv6
  <img width="1468" height="824" alt="image" src="https://github.com/user-attachments/assets/c1f77a4b-0543-426c-938a-d01c029171b9" />

# Traceroute
---------------------------------------------------------------------------
- TTL 감소를 기반으로한 route 파악
- window에선 tracert 명령어 및 ICMP로 송신 및 응답 받음
- cisco, linux 등에선 UDP로 송신하고, ICMP로 응답 받음
  - 사용하지 않는 UDP 포트로 송신하여, ICMP type 3 의 code 3인 port unreachable 을 받아옴
- 중간 홉 응답은 ICMP type 11 code 0 인 time exceeded를 받고, 마지막 응답은 window에선 reply, 다른 장비들은 port unreachable
- 한계
  - 비대칭 경로에 의해 순방향 전송은 성공했는데, 역방향에서 다른 경로로 오다가 끊겨버리는 경우
  - ECMP에 의해 패킷이 각기 다른 루트로 전송 및 수신되는 경우
  - ICMP rate-limit에 의해 바쁜 라우터가 ICMP 응답을 늦게 하는 경우
  - ACL이나 방화벽등에 의해 drop 되는 경우
  - ip unreachable 응답을 안하는 경우

# debug
-----------------------------------------------------------------------------
- 전체적인 debug와 condition debug로 나뉨
- 대표
  - debug ip ospf adjacencies : OSPF 이웃맺기 단계 감시
  - debug ip packet : 해당 장비를 통과하거나, 자신을 대상으로 하는 패킷들의 L3 헤더를 모두 보여줌 (하드웨어 스위칭되는 패킷은 안잡힘)
  - debug condition
  - service timestamps debug datetime msec : 디버그 로그를 0.001초 단위로 찍음


# VLAN
-----------------------------------------------------------------------------
- Stretched vlan : site 마다 같은 vlan과, 같은 대역을 부여하고, trunk로 site간 연결하는 구세대 방식
  - broadcast storm 발생시, 다른 site의 vlan 까지 마비됨
- local vlan : site 마다 다른 대역으로, L3를 통해 site간 연결하는 현대 표준
- multiple subnets vlan : 일반적으로 하나의 서브넷에 하나의 vlan이 정석
  - 하나의 vlan에 primary , secondary 대역을 넣어서 다른 서브넷도 같은 vlan에 포함시킴
- vlan shutdown , suspend
  - vlan 명령어 내부에서 shutdown시, local 에서 포워딩을 중단하는 효과 (VTP domain 에선 살아있음)
  - vlan 명령어 내부에서 state suspend시, VTP 도메인 전체에 영향을 끼침
- internal vlan
  - L3급 switch 에서, no switchport를 issue 했을 때 생기는 숨겨진 vlan.
  - port 에 ip 를 부여하면, 숨겨진 vlan의 SVI에 IP가 부여된다. 트래픽이 오고갈때, 이 port 에 인입되는 패킷들은 숨겨진 vlan의 tag 를 달고 들어와, 내외부와 라우팅 가능해짐
  - ++ ip routing 명령어는 스위치 내부의 FIB 와 CEF 등의 기능을 활성화 시킴
- access port
  - untagged port
  - access port 는 untagged frame이 수신 되어야 함.
  - VoIP 같은 특수 상황에선 access port 라도 전용 vlan 할당 가능
- trunk port
  - tagged port
  - 802.1q 가 Source mac과 ether type 사이, 4byte 크기로 삽입됨
  - native vlan은 trunk port 에서도 untagged로 나갈수있다.
    - native 인척 속이면서 다른 vlan에 침투하는 double tag 공격에 이용될수 있으니, native는 안쓰는 번호로 지정해야함
    - 인터페이스마다 다른 native vlan을 가질수있음
    - allowed vlan == add [] tagged
- PVID
  - 패킷이 포트로 인입될때, 어떤 vlan에 속할지 구별함. 반대로 포트에서 나갈땐 untagged/tagged (access/trunk)가 기능함
  - native vlan과 동일한 개념
  - access vlan 10 untagged 는 포트에서 나갈때, PC가 이해할수 있게 tag를 떼는것
  - add vlan 99 1 set pvid 99 는 포트 1번에 PC가 보낸 untagged 프레임이 들어올 때, vlan 99번에 속하게 하는것


# DTP
-------------------------------------------------------------------------------------
- Dynamic Trunking Protocol
- nego를 통해, ISL/dot1q , trunk/access 등을 자동 협상하는 프로토콜
- VTP 도메인이 일치하지 않으면, 협상하지 못함
- switch mode access , 또는 switch nonegotiate 명령어로 DTP를 disable 가능
<img width="1279" height="720" alt="image" src="https://github.com/user-attachments/assets/b145beb2-10b4-4787-bbef-21adbaac90b2" />
 - O : operation, 현재 상태
 - A : administrative, 내가 입력한 상태
 - N : negotiate, 협상 결과
 - S : status, 포트모드 (trunk or access)
 - T : type, encapsulation 형태 (ISL or dot1q)

# VTP
------------------------------------------------------------------------------------
- 스위치가 VTP domain 내의 스위치들과 vlan 정보를 공유하는 프로토콜
- vlan 생성 , 삭제 , 수정 등의 정보를 공유하며, 할당 등은 하지않음
- vtp domain이 NULL인 스위치는 기본적으로 광고를 송신하지 않지만, vtp domain을 수신 받으면, 그 domain 에 속하게된다
- 버전 1의 스위치가 버전 2의 정보를 수신 받으면, 스스로 버전2로 업데이트함
- vtp packet은 trunk port 에서만 전송됨
- revision number : 장부를 수정 할 때마다 증가하는 번호. 클 수록 최신의 정보로 판단함
  - 수신 받은 vtp packet의 number가 높으면, 그 정보로 동기화함
  - vtp bomb 등의 참사 원인
- 버전 1,2는 vlan 0 ~ 1005 까지, 버전 3은 0 ~ 4094 까지 지원함
- VTP mode
  - v1/v2 : server , client , transparent
  - v3 : server , client , transparent , off
    - v3의 server는 primary / secondary 로 나뉜다.
    - vtp primary 로 설정된 한 대의 스위치만 vlan 수정이 가능함.
  - transparent : 자신이 NULL 일때 모든 vtp packet forward
    - 자신의 domain이 있을 때, 일치하는 domain forward
    - 평소엔 자신의 local vlan 권한
    - revision number가 항상 0 이다.
  - off : transparent 와 기본적으로 동일하지만, VTP packet을 forward도 하지 않음.
- VTP 인증
  - vtp password [비밀번호] : 비밀번호 MD5 암호화. 받은 vtp packet 과 동일할 경우 동기화함
  - transparent 는 단순히 forward 하기 때문에, password 일치 여부는 상관안하고 바로 forwarding
  - VTPv3
    - hidden : 평문을 16진수 암호문으로 변경
    - secret : hidden 된 암호문을 다른 장비에 복사할때, "이미 암호화된 상태임"을 알려주는 키워드
- VTP 비교
  - v1과 v2는 v2에서 tokken ring과 자잘한 기능 몇가지 추가된것 이외엔 큰 차이가 없음
  - v3 에선 hidden , secret이 추가 되었고, 확장 vlan 사용이 가능하다.
  - v3 에선 primary / secondary server가 나뉘어져 있다.
    - 장비 리부팅 / 도메인 및 암호 변경 / 다른 스위치에서 primary 명령어 입력시 / 기존의 primary server 권한이 박탈됨



