# CCNP2
-----------------------------------------------------------------
network switching and forwarding - packet forwading
----------------------------------------------------------------
- L1 ~ L2

- enhanced TCP/IP model
  - OSI 계층과 L1 - L4 까지 동일하게 매핑
  - OSI 계층의 L5 - L7 부터, TCP/IP model은 L5로 매핑한다.

<img width="1910" height="937" alt="image" src="https://github.com/user-attachments/assets/1fb96bfd-d698-4c7b-9a1f-96766ee2437a" />

- Dot1q tag (4 byte)
  - TPID, 0x8100 (2byte)
  - TCI (2byte)
    - PCP(Cos), priority code point, 3bit. 000 to 111
    - DEI(CFI), drop eligible indicator, 혼잡시 드랍 여부 flag, 1bit
    - vlan id, 12bit-

<img width="1865" height="910" alt="image" src="https://github.com/user-attachments/assets/239b8243-6b2b-4b70-ba3f-8bf633659119" />

- MAC address table은 논리적, control plane 영역이고,
- MAC table 기반으로 제작된 CAM은 물리적인 data plane 영역이고, 사실상 MAC과 CAM은 같은 개념임
- show interface [ ] switchport , show interface status
- mac address static은 특정 mac 주소로 향하는 트래픽을 특정 포트로 보내는 기술, 특정 mac을 특정 포트로 고정하는건 port security
<img width="878" height="454" alt="image" src="https://github.com/user-attachments/assets/0f425e56-635b-48d2-b3b0-4c08fcf6c323" />

------------------------------------------------------------------
- packet forwarding architecture

<img width="1780" height="767" alt="image" src="https://github.com/user-attachments/assets/558fc377-c11b-4fbd-b4cb-1b852ce633f3" />

- flow : source , destination IP 및 port 와 프로토콜이 같은 모든 패킷

<img width="1911" height="842" alt="image" src="https://github.com/user-attachments/assets/cff15805-6a86-4fa7-9b8f-5135a6d410d7" />

<img width="1904" height="826" alt="image" src="https://github.com/user-attachments/assets/6f1c41bd-b6a4-4390-915a-abe7cb1c2774" />

<img width="1901" height="824" alt="image" src="https://github.com/user-attachments/assets/19d7dffa-7eb8-4436-a9b9-1495c49a91ef" />
- ASIC은 유연성이 없는 고정 역할, NPU는 재프로그래밍이 가능함

<img width="1904" height="823" alt="image" src="https://github.com/user-attachments/assets/295c9ed3-6554-4ffb-9f91-46786e568b02" />

<img width="1907" height="821" alt="image" src="https://github.com/user-attachments/assets/86a21f4d-e57c-4d35-931f-3baad048ddb4" />

--------------------------------------------------------------------
# STP - 802.1D
--------------------------------------------------------------------
- PVST , PVST+ 는 cisco 독자 프로토콜
- 802.1W (RSTP), 802.1S (MSTP)는 표준

<img width="1901" height="917" alt="image" src="https://github.com/user-attachments/assets/95866a3e-3a0e-47fb-97ba-00bd66b74aca" />
<img width="1901" height="915" alt="image" src="https://github.com/user-attachments/assets/35a6f814-1a26-4b22-aeae-57a0c5d4e46a" />

--------------------------------------------------------------------
# PVST+
--------------------------------------------------------------------
<img width="1878" height="891" alt="image" src="https://github.com/user-attachments/assets/40c7f242-3cda-43d7-962a-623ef613866f" />

<img width="1883" height="902" alt="image" src="https://github.com/user-attachments/assets/c7009823-682f-4faa-a283-6ba2891d0042" />

<img width="1874" height="889" alt="image" src="https://github.com/user-attachments/assets/6103a151-7d96-49d5-b5b8-e6facd9afb72" />

<img width="1847" height="878" alt="image" src="https://github.com/user-attachments/assets/2af823a2-082b-42a3-babd-c56b190ff500" />

<img width="1859" height="864" alt="image" src="https://github.com/user-attachments/assets/4d987805-5dbb-40ad-9951-4243b7f09831" />

<img width="1832" height="886" alt="image" src="https://github.com/user-attachments/assets/4f85496f-fa64-4653-98fc-0d83bb673004" />

<img width="1854" height="874" alt="image" src="https://github.com/user-attachments/assets/0ddf175f-6015-4ba3-adfc-d9056f88815e" />

-----------------------------------------------------------------------
# STP convergence
-----------------------------------------------------------------------
<img width="1889" height="935" alt="image" src="https://github.com/user-attachments/assets/474bba7a-686a-4b11-8d75-ca0da1a3408e" />

<img width="1887" height="907" alt="image" src="https://github.com/user-attachments/assets/a00e427f-0745-4355-a5e6-5e6101bb790d" />

<img width="1888" height="938" alt="image" src="https://github.com/user-attachments/assets/b2a991da-b190-490c-9de8-353c7c74dacc" />

<img width="1885" height="937" alt="image" src="https://github.com/user-attachments/assets/6d8c0320-7fd3-4a32-8e40-ff078066727f" />

<img width="1889" height="938" alt="image" src="https://github.com/user-attachments/assets/98d1811a-3bae-4a87-ba5e-64b234dbb18e" />

-----------------------------------------------------------------------
# STP Tuning
-----------------------------------------------------------------------
<img width="1853" height="875" alt="image" src="https://github.com/user-attachments/assets/6765de67-b481-4065-b4f8-50ef9e72fde0" />

<img width="1908" height="950" alt="image" src="https://github.com/user-attachments/assets/660d4dbe-fe37-477f-b195-c00681b6873c" />

-----------------------------------------------------------------------
# STP protect and loop prevent
-----------------------------------------------------------------------
<img width="1886" height="881" alt="image" src="https://github.com/user-attachments/assets/eb430e3f-24ca-41f6-9462-339d2219ef1c" />

<img width="1906" height="935" alt="image" src="https://github.com/user-attachments/assets/b22c3f68-e27b-4891-b720-f0fe58f1aa02" />

 - UDLD 는 보통 fiber link(광)에 사용
 - Normal : 단방향 발견시 에러만 띄움
 - Aggressive : 단방향 발견시 err-disable
 - UDLD 기본 hello time (udp) 는 15초

<img width="1898" height="947" alt="image" src="https://github.com/user-attachments/assets/3843bddb-c69d-428a-b725-56bd06c81601" />


------------------------------------------------------------------------
#  RSTP 
------------------------------------------------------------------------
<img width="1888" height="941" alt="image" src="https://github.com/user-attachments/assets/30ea1736-df78-4970-bbfa-586a4a202ce5" />

<img width="1858" height="902" alt="image" src="https://github.com/user-attachments/assets/95c99d2e-bbac-440a-b0be-85853b32ec95" />

------------------------------------------------------------------------
# MSTP
------------------------------------------------------------------------
<img width="1910" height="927" alt="image" src="https://github.com/user-attachments/assets/f09fb5cc-b447-4bbe-8e84-4e4f4d10543c" />

<img width="1558" height="892" alt="image" src="https://github.com/user-attachments/assets/4696b9af-d5bd-4701-a41d-3093ec69f099" />

<img width="1904" height="929" alt="image" src="https://github.com/user-attachments/assets/324b2254-d422-4b35-9c26-4d9886daf414" />

<img width="1910" height="929" alt="image" src="https://github.com/user-attachments/assets/bb1beb23-31af-4d3a-912f-32251bfa3830" />

<img width="1901" height="928" alt="image" src="https://github.com/user-attachments/assets/3d1ad355-7d8d-4897-96c1-1d164f7265b6" />

<img width="1889" height="908" alt="image" src="https://github.com/user-attachments/assets/5461c54e-8b7a-429b-8dc7-f424883f20cf" />

<img width="1249" height="143" alt="image" src="https://github.com/user-attachments/assets/6b2c4ab8-6c4d-4dcb-a469-c20a0681487b" />

------------------------------------------------------------------------
# DTP
------------------------------------------------------------------------
<img width="1895" height="914" alt="image" src="https://github.com/user-attachments/assets/a7cf19eb-ccd2-4269-988f-df2233297cd1" />

<img width="1896" height="912" alt="image" src="https://github.com/user-attachments/assets/b2cdeda5-a990-4fa3-8a6b-374726dd4bac" />

<img width="1894" height="911" alt="image" src="https://github.com/user-attachments/assets/50fbf7d1-7496-42c5-8153-5f13f52366ef" />

<img width="1898" height="915" alt="image" src="https://github.com/user-attachments/assets/24e5a0ee-d87b-4408-acad-47648b11d216" />

<img width="1900" height="914" alt="image" src="https://github.com/user-attachments/assets/c06a8470-088f-4e65-89f0-64cc59e509b0" />

<img width="1898" height="914" alt="image" src="https://github.com/user-attachments/assets/f05e9729-ce2e-488c-aa74-170c21383f29" />



















