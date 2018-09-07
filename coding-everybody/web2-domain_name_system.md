# Web2. Domain Name System

## IP 주소와 hosts

- host
  - 인터넷에 연결된 컴퓨터(장치)
- Internet Protocol Address
  - 인터넷 상에서 host의 주소
- Domain Name
  - IP 주소는 어려움
  - 기억하기 쉬운 형식으로. 이름이 있었으면.... Ex. Example.com
- hosts
  - IP주소와 Domain Name을 맵핑해놓은 문서 파일
  - 일종의 전화번호부
  - Client에서 Domain Name으로 접속 시도 시, hosts 파일이 해당하는 IP 주소를 반환해줌

## 도메인 이름과 보안

- hosts파일을 해킹하면 특정 IP로 접속되도록 수정할 수 있음
- 대안은 https!

## DNS의 태동

- DNS 이전
  - SRI(Stanford Research Institute)가 전세계에 있는 hosts파일을 관리함
  - 원하는 Domain Name을 IP와 함께 SRI에 등록 요청
  - 모든 Clinet가 SRI에서 hosts 파일을 다운로드받아서 사용
  - 각 Client가 직접 관리하는 것이 아니라 SRI라는 신뢰할 수 있는 기관에서 관리
- 한계
  - SRI에서 다운로드 받기 전까지는 추가된 호스트의 이름을 사용할 수 없음
  - SRI에서는 수작업으로 파일을 갱신 : 많은 비용
  - 하나의 host 파일에 인터넷에 있는 모든 도메인 네임이 담긴다? -> 한계
- 해결
  - 1983년 SRI의 hosts파일을 관리하던  Jon Postel & Paul Mockapetris는 DNS를 고안

## DNS (Domain Name System)

- DNS Server
  - (IP주소, Domain Name)을 등록 요청받고 저장
- 장점
  - 수작업으로 저장하던 것을 자동화
  - Server를 통해서 host의 이름을 서비스함. 변경된 내용 바로 반영
- 과정
  - Client에서 Domain Name을 접속 시,
    1. Hosts 파일에서 Domain Name에 해당하는 IP 찾기
    2. 없으면, DNS Server에 요청 후, IP를 반환받기

## Public DNS

- Client에서 인터넷 접속 시, ISP에서 DNS Server의 IP를 세팅해 줌
- 사용할 DNS Server 변경 가능
  - 성능이 느리다거나, Privacy Issue
- Public DNS
  - 무료로 사용할 수 있는 DNS Server
- Google에서도 DNS Server를 제공함!
  - 8.8.8.8 & 8.8.4.4 : 두 개인 이유. 하나가 문제 생기면 다른 것 사용
- 1.1.1.1
  - 빠른 Public DNS

## DNS Internal

- DNS Server의 역할
  1. Domain Name의 IP 저장
  2. 요청 시, Domain Name의 IP 반환
- DNS Server는 전 세계에 여러개가 있음
- Domain Name의 구조
  - ex) blog.example.com**.**    (뒤에는 점(.)이 생략되어 있음)
    1. Root Domain : **.**
    2. Top-level Domain : **com**
    3. Second-level Domain : **example**
    4. Sub Domain Domain : **blog**
  - 각각의 부분들을 담당하는 DNS Server가 있음 (!)
    - 상위는 하위를 알고 있어야함
      - Root Domain을 담당하는 Server들은 Top-level Domain을 담당하는 Server들을 알고있어야함
    - Sub Domain을 담당하는 Server가 IP 주소를 가지고 있음
- 과정
  - 인터넷 접속 시,  (blog.example.com)
    1. Root Domain Server에게 요청
        - "모르겠지만" Top-level Domain이 com이네? com을 담당하는 DN Server의 IP를 알려줄게
    2. Top-level Name Server에게 요청
    3. Second-level Name Server에게 요청
    4. Second-level Name Server에게 요청 -> IP를 받음

## DNS register

- 기관/Role
  - ICANN
    - 비영리단체
    - 전세계의 IP 주소를 관리
    - Root name server의 관리자
      - a.root-servers.net ~ m.root-servers.net
    - 사실상 인터넷의 관리자
  - Registry (등록소)
    - Top-level Domain 관리
      - ex) .com을 관리하는 a.gtld-server.net
  - Registrar (등록대행자)
    - 대신 등록해주는 자
  - Registrant (등록자)
    - 등록을 원하는 서버
- Second-Level Domain의 네임서버 (authoritative name server)
  - 보통 등록대행자가 제공
  - 무료도 있음
- 등록 과정 예시 (example.com)
  1. 도메인 신청 : 등록자 -> 등록대행자
      - "example.com 등록해줘"
      - 등록대행자의 네임서버는 a.xxx.net이라고 가정
  2. Top-level Domain Name Server에 등록 : 등록대행자 -> 등록소
      - .com. 을 관리하는 Top-level Domain Name Server가 example.com의 NS가 a.xxx.net이라는 것을 기록하게 함
      - 저장할 Record :  example.com NS a.xxx.net
  3. IP 연결
      - 등록자가 example.com의 IP는 123.123.123.123이라는 것을 Second-Level Domain의 네임서버에 등록 (보통 등록대행자 Site 통해 등록)
      - 저장할 Record : example.com A 123.123.123.123
        - A는 address
- 접속 과정 예시 (example.com 접속)
  1. Client -> Default DNS Server 에 요청
  2. Default DNS Server -> Root Name Server 에 요청
      - .com을 관리하는 Top-level Domain Name Server의 IP 반환
  3. Default DNS Server  -> Top-level Domain Name Server (.com.)에 요청
      - example.com.을 관리하는 Second-level Domain Name Server의 IP 반환
  4. Default DNS Server  -> Second-level Domain Name Server (example.com.)
      - example.com.의 IP 반환!
  5. Default DNS Server -> Client
      - example.com.의 IP 반환!
  6. Client -> example.com.의 IP로 접속

## nslookup

- Domain Name의 정보를 확인하는 Command
- 사용법 : nslookup example.com
- 기본 type = a 임. type=ns로 명령 시 nameserver의 정보를 얻을 수 있음

## DNS record & CNAME

- DNS Record : DNS Server에 저장하는 Domain Name에 대한 정보 1건
  - ex) example.com. A 123.123.123.123
- [Record Type](https://en.wikipedia.org/wiki/List_of_DNS_record_types)
  - A : Address. IPv4 주소를 반환함
    - ex) example.com. A 123.123.123.123
  - CNAME : Canonical Name Record. Alias 개념.
    - ex) www.example.com. A example.com.
