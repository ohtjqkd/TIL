# 로드밸런싱(Load Balancing)

과거의 네트워크 트래픽은 서버 1대만으로 감당이 가능한 수준이었다. 하지만 최근에 와서는 이런 트래픽들이 급격하게 늘어나면서 하나의 서버로는 감당하기 어려운 상황이 됐다.

## 해결을 위한 방안
![scale-up & out](https://blog.kakaocdn.net/dn/bVnDmo/btq6AN1h8ZI/Si4OYxQK9J9aLKzo4YnpUk/img.png)
- SCALE-UP(Vertical Scalling)
    서버의 연산 능력을 높이기 위해 서버의 하드웨어의 성능을 높이는 방법
    - 장점
        - 추가적인 네트워크 연결 없이 용량을 증강할 수 있고, 추가되는 용량이나 업그레이드 비용만 부가되기에 비용적인 증강이 스케일아웃에 비해 낮고 설계가 쉽다.
        - 무엇보다 비교적 업그레이드가 쉽고, 필요 장비와 전력 소모를 어느 정도 아낄 수 있다.
        - 인프라 비용이 추가로 발생하지 않는다.
        - 서버를 추가하는 방법이 아니기 때문에 여러대의 서버를 두는 것보다 데이터 정합성 이슈(데이터가 일관되지 않는 문제)에서 자유롭다.
    - 단점
        - 다만 스케일업을 할수록 기존 하드웨어의 냉각, 공간, 전력공급 등의 문제가 발생할 수 있고, 하드웨어 허용 범위 내에서만 확장이 가능하기 때문에 그 이상으로 업그레이드를 하고자 한다면 한계가 있다. 새로운 장비로 교체하는 방법밖에 없음
        - 스케일 업의 일정 수준을 넘어가는 순간, 성능 증가 폭이 미미해진다. cpu 의 예를 들자면, i3 에서 i5로 스케일업하는 경우, 1.5배 이상의 성능 변화가 있는 반면, i5 에서 i7로 스케일업하는 경우, 1.2 배의 성능 변화밖에 없다
        - 서버 한 대에 모든 부하가 집중되므로 장애 시 서버가 복구될 때까지 서비스를 중단해야 하는 상황이 발생한다. 내가 사용하려던 서비스가 중단된다면, 그에 안좋은 기억이 생기고 타 서비스로 이용을 바꾸거나, 서비스를 사용하지 않을 수 있는데, 이것은 엄청난 비즈니스 손실이 생길 수 있다.
    - 사용하기 적합한 경우
        - 한 대의 서버에서 모든 데이터를 처리하므로 데이터 갱신이 빈번하게 일어나는 ‘데이터베이스 서버’에 적합한 방식이다.

- SCALE-OUT
    비슷한 성능의 서버를 추가하여 트래픽을 분산시켜주는 방법
    - 장점
        - 서버 한 대가 장애로 다운되더라도 다른 서버로 서비스 제공이 가능하다는 장점이 있다.
        - 용량, 성능 확장에 한계가 없다. 하드웨어를 변경하는 것이 아닌 비슷한 성능의 서버를 여러 대 두는 방법이기 때문에, 확장이 무제한 가능하다. 즉, 단일 서버에 작업이 쌓여서 멈춰있는 병목현상을 줄일 수 있다.
    - 단점
        - 여러 대의 서버로 돌아가기 때문에  데이터 정합성 이슈(데이터가 일관되지 않는 문제)가 생길 수 있다. 그에따라 모든 서버에서 데이터 일관성을 유지해야하기 때문에 설계 및 관리가 복잡하다.
        - 세션, 웹 이미지 등 서버에 저장되는 데이터를 어떤식으로 공유해야할지에 대한 기술적인 한계가 있다.
        - 병렬 컴퓨팅 환경을 구성하고, 유지하려면, 로드 밸런싱에 대한 높은 이해도가 요구된다.
    - 사용하기 적합한 경우: 
        - 높은 병렬성을 실천하기 쉬운 경우
        - 정합성을 유지하기 쉬운 경우
        - 웹서버

출처: https://junghyungil.tistory.com/151

## 그래서 로드밸런싱이 필요한 이유가?
Scalling을 할 때는 위의 장단점을 고려하여 scalling 방법을 선택한다. 이때 만약 scale-out을 선택하게 된다면 필수인 것이 로드 밸런싱이다.
로드 밸런싱은 서버의 부하(Load)를 여러대의 서버로 분산시켜주는 것을 말한다.
<img style="width: 50%; display: block;" src = "https://post-phinf.pstatic.net/MjAxOTEyMTBfMjE3/MDAxNTc1OTU0ODk1ODQ3.-GJxkoK7Apn4l0K5L1OXN4NFGsseRoaNhW2r0KIQJdog.0BchcWEI-WS-uEb3iRRrD0JyO_6eZoIWh7xf4f4J2fMg.JPEG/%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%84%9C_%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98.jpg?type=w1200"/>
로드밸런서(일종의 proxy)를 서버와 클라이언트 사이에 두고 몇가지 규칙을 통해 각각의 서버에 넘겨주게 된다.  

### 로드밸런싱 알고리즘
- 라운드로빈 방식(Round Robin Method)  
    서버에 들어온 요청을 순서대로 돌아가며 배정하는 방식입니다. 클라이언트의 요청을 순서대로 분배하기 때문에 여러 대의 서버가 동일한 스펙을 갖고 있고, 서버와의 연결(세션)이 오래 지속되지 않는 경우에 활용하기 적합합니다.

- 가중 라운드로빈 방식(Weighted Round Robin Method)  
    각각의 서버마다 가중치를 매기고 가중치가 높은 서버에 클라이언트 요청을 우선적으로 배분합니다. 주로 서버의 트래픽 처리 능력이 상이한 경우 사용되는 부하 분산 방식입니다. 예를 들어 A라는 서버가 5라는 가중치를 갖고 B라는 서버가 2라는 가중치를 갖는다면, 로드밸런서는 라운드로빈 방식으로 A 서버에 5개 B 서버에 2개의 요청을 전달합니다.

- IP 해시 방식(IP Hash Method)  
    클라이언트의 IP 주소를 특정 서버로 매핑하여 요청을 처리하는 방식입니다. 사용자의 IP를 해싱해(Hashing, 임의의 길이를 지닌 데이터를 고정된 길이의 데이터로 매핑하는 것, 또는 그러한 함수) 로드를 분배하기 때문에 사용자가 항상 동일한 서버로 연결되는 것을 보장합니다. 

- 최소 연결 방식(Least Connection Method)  
    요청이 들어온 시점에 가장 적은 연결상태를 보이는 서버에 우선적으로 트래픽을 배분합니다. 자주 세션이 길어지거나, 서버에 분배된 트래픽들이 일정하지 않은 경우에 적합한 방식입니다.

- 최소 리스폰타임(Least Response Time Method)  
    서버의 현재 연결 상태와 응답시간(Response Time, 서버에 요청을 보내고 최초 응답을 받을 때까지 소요되는 시간)을 모두 고려하여 트래픽을 배분합니다. 가장 적은 연결 상태와 가장 짧은 응답시간을 보이는 서버에 우선적으로 로드를 배분하는 방식입니다.
    
## L4 & L7 로드밸런서

L4, L7로드밸런서가 가장 많이 사용됨
L4부터 포트정보를 기반으로 트래픽 분산이 가능하기 때문
<img width="45%" src="https://post-phinf.pstatic.net/MjAxOTEyMTBfNCAg/MDAxNTc1OTU1MzY3OTM2.nG91HOEOh6Sc1AuUgbN3O4pcnEI-rh24UKSrrrjkrcsg.VcG18MidW4az7Oh0RQfRPLDBHNRyGayE1BsQxDImL3Ig.JPEG/L4-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200" />
<img width="45%" src="https://post-phinf.pstatic.net/MjAxOTEyMTBfMjA1/MDAxNTc1OTU1MzgxODY5.odnG4CRES0e5bH7sOKyWRP1c8uO_XC4VX9A3HPeI1JQg.lNL2eJYbMz6NX1e5YFzfHDMQHn4YrdOJR2VYHmq5e1Ig.JPEG/L7-%EB%A1%9C%EB%93%9C%EB%B0%B8%EB%9F%B0%EC%8B%B1.jpg?type=w1200" />

- 비교
    - L4
    L4 로드밸런서는 네트워크 계층(IP, IPX)이나 트랜스포트 계층(TCP, UDP)의 정보를 바탕으로 로드를 분산합니다. IP주소나 포트번호, MAC주소, 전송 프로토콜에 따라 트래픽을 나누는 것이 가능
    - L7
    반면 L7 로드밸런서의 경우 애플리케이션 계층(HTTP, FTP, SMTP)에서 로드를 분산하기 때문에 HTTP 헤더, 쿠키 등과 같은 사용자의 요청을 기준으로 특정 서버에 트래픽을 분산하는 것이 가능합니다. 쉽게 말해 패킷의 내용을 확인하고 그 내용에 따라 로드를 특정 서버에 분배하는 것이 가능한 것입니다. 위 그림과 같이 URL에 따라 부하를 분산시키거나, HTTP 헤더의 쿠키값에 따라 부하를 분산하는 등 클라이언트의 요청을 보다 세분화해 서버에 전달할 수 있습니다. 또한 **L7 로드밸런서의 경우 특정한 패턴을 지닌 바이러스를 감지해 네트워크를 보호할 수 있으며, DoS/DDoS와 같은 비정상적인 트래픽을 필터링할 수 있어 네트워크 보안 분야**에서도 활용되고 있습니다.
![L4&L7](https://post-phinf.pstatic.net/MjAxOTEyMTBfMTUx/MDAxNTc1OTU2NzEwMzMy.SekjHws4oCgNmCkjYoiZg_pfAlBu2yC66wPkLq0JHbsg.Zn9aLJYZX7rbdEL-X4HRkVO4PCgDNanhQntuR-iGBwkg.PNG/%EC%9B%B9_1920_%E2%80%93_1.png?type=w1200)

출처: https://m.post.naver.com/viewer/postView.naver?volumeNo=27046347&memberNo=2521903