# DNS 동작 과정

## DNS란

DNS(Domain Name System)은 **호스트 이름을 IP 주소로 변환해주는 디렉터리 서비스**이다.

1. DNS 서버들의 계층구조로 구현된 분산 데이터베이스
-> 원하는 IP 주소는 가까운 DNS 서버에 캐싱되어 있다.
평균 DNS 지연, DNS 네트워크 트래픽 감소
2. 호스트가 분산 데이터베이스로 질의하도록 허락하는 애플리케이션 계층 프로토콜

➕ **DNS의 주요 서비스**

- **host aliasing**: 복잡한 호스트 이름을 가진 호스트는 하나 이상의 별칭을 가질 수 있다.
- **mail server aliasing**
- **부하 분산**: 중복 웹 서버들은 여러 IP 주소가 하나의 정식 호스트 이름과 매핑된다.

### DNS 계층구조


![image](https://github.com/user-attachments/assets/8749576a-8569-4c00-8e9c-3cb9e1121f6f)



[DNS 계층 구조](https://www.cloudflare.com/ko-kr/learning/dns/glossary/dns-root-server/)

- **Root DNS server**: 가장 상위 DNS 서버로서 국제 인터넷 주소 관리 기구(ICANN)에 의해 전체 도메인 네임 공간을 관리, TLD DNS server ip 주소를 갖는다
- **TLD DNS server**: 도메인 등록 기관이 관리, 책임 DNS server의 ip 주소를 갖는다
- **Authoritative DNS server**: 실제 도메인과 ip 주소 관계가 기록, 저장, 변경되는 서버
- **Local DNS server**: 사용자들이 제일 먼저 접근하는 DNS server, 대표적으로 캐싱역할

## DNS 동작 원리 개요

1. 사용자가 웹 브라우저에 [www.example.com](http://www.example.com/) 을 입력한다.
2. [www.example.com](http://www.example.com/) 에 대한 요청은 일반적으로 ISP가 관리하는 Local DNS Server로 라우팅된다.
3. DNS 해석기는 [www.example.com](http://www.example.com/) 에 대한 요청을 DNS root name server에 전달
4. Local DNS Server는 [www.example.com](http://www.example.com/) 에 대한 요청을 .com 을 관리하는 TLD DNS Server에 전달한다.
5. TLD DNS Server는 Authoritative DNS Server로 요청을 보내고 IP 주소를 받아온다.
6. Authoritiative DNS Server는 해당 IP 주소를 Local DNS Server에 반환한다.
7. 확보한 IP 주소를 웹 브라우저로 반환한다.
8. Local DNS Server는 다음에 누군가가 example.com을 탐색할 때 좀 더 빠르게 응답할 수 있도록 사용자가 지정한 일정 기간 example.com의 IP 주소를 캐싱한다.
9. 웹 브라우저는 Local DNS Server로부터 얻은 IP 주소로 www.example.com에 대한 요청을 전송한다.
10. 웹 서버 또는 그 밖의 리소스는 www.example.com의 웹 페이지를 웹 브라우저로 반환하고 웹 브라우저는 이 페이지를 표시한다.

![image](https://github.com/user-attachments/assets/5722b58c-1829-4c00-8ba1-7266bc400369)


### 재귀적 쿼리, 반복적 쿼리

- **재귀적 쿼리(Recursive Query)**: 요청 호스트가 Local DNS Server에게 요청하는 쿼리
-> DNS Server가 대신 찾아주는 방식
- **반복적 쿼리(Iterative Query)**: Local DNS Server가 상위 DNS 서버에게 요청하는 쿼리
-> 클라이언트가 직접 물어봄

### DNS에서의 TTL(Time To Live)

: Local DNS Server에서 특정 DNS 레코드가 DNS cache에 얼마나 오래 유지될 수 있는지 나타내는 값

linux - dig 명령

![image](https://github.com/user-attachments/assets/12e30c84-ec4e-421f-990a-7acb8bb7911a)



TTL이 0이 된다면 -> DNS 서버는 해당 도메인에 대한 질의 요청을 사용자에게 해주지만 캐싱하지 않고 바로 버린다.
