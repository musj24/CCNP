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
<img width="878" height="454" alt="image" src="https://github.com/user-attachments/assets/0f425e56-635b-48d2-b3b0-4c08fcf6c323" />

------------------------------------------------------------------
- L3
- 

