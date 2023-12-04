## DNS(Domain Name System)
DNS는 인터넷의 전화번호부와 같다. 
우리가 웹 브라우저에 도메인 이름(예: www.github.com )을 입력할 때, DNS는 이를 이해할 수 있는 IP 주소(예: 192.0.2.1)로 변환한다.

### 작동 원리
1. 도메인 이름 조회
사용자가 도메인 이름을 입력하면, 이 요청은 먼저 로컬 DNS 서버로 전송된다.

![](https://velog.velcdn.com/images/tme2685/post/e17b77d5-35d7-462e-af70-9344ddec1c66/image.png)

2. 계층적 조회
로컬 DNS 서버는 루트 DNS 서버에서 시작하여 계층적으로 내려가 하위에 있는 DNS서버까지 순차적으로 조회한다.

4. IP 주소 반환
DNS 서버는 DNS Query 메시지로 받은 도메인 네임에 대응하는 IP 주소를 DNS Response 메시지에 포함하여 클라이언트로 보낸다. 이 정보는 일정 시간 캐싱되어 빠른 액세스를 위해 저장된다.

![](https://velog.velcdn.com/images/tme2685/post/469315b4-ca92-44fb-84fe-dbb148d46bd1/image.png)


## ARP(Address Resolution Protocol)
ARP는 네트워크 상의 장치가 다른 장치의 IP 주소를 물리적인 MAC (Media Access Control) 주소로 변환하는 데 사용되는 프로토콜이다.

### 작동 원리
1. ARP 요청
장치는 목적지 IP 주소를 알고 있지만 해당 MAC 주소를 모를 때 ARP 요청을 네트워크에 브로드캐스트한다.

3. ARP 응답
해당 IP 주소를 가진 장치는 자신의 MAC 주소를 포함한 ARP 응답을 보낸다.

5. ARP 테이블
각 장치는 ARP 테이블에 IP 주소와 매핑된 MAC 주소를 저장하여 통신을 진행한다.

### DNS와 ARP의 상호작용
DNS와 ARP는 서로 다른 역할을 하지만, 인터넷 통신에서 상호 보완적이다. DNS가 도메인을 IP 주소로 변환하면, ARP는 이 IP 주소를 사용하여 로컬 네트워크 내의 해당 장치의 MAC 주소를 찾는다. 이 두 과정을 통해 원활한 인터넷 연결이 가능해진다.



