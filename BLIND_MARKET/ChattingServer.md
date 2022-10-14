# HTTP, Socket, Websocket, STOMP

## HTTP 통신
HTTP 통신은 HTML 파일을 전송하려는 목적으로 만들어졌으나 __현재는 JSON, Image 파일 등을 전송__ 을 주로함

HTTP 통신은 클라이언트에서 서버로 요청을 보내고 서버가 응답하는 방식으로 이루어짐, 이로 인해 가지는 특성
- 클라이언트는 요청만 하고 서버는 이 요청이 있을 때만 응답 -> 단방향 통신

## Socket 통신
프로세스간 통신(IPC)를 다룰 때도 나온 socket통신 방식 client와 server를 일종의 프로세스라고 생각한다면 이해하기 쉽다.
socket은 양방향 통신이 가능하기 때문에 client <-> server의 데이터 교환이 가능해진다.

스트리밍 서비스나 채팅처럼 실시간으로 데이터를 주고 받아야하는 경우 connection을 빈번하게 맺고 끊는 http 통신보다는 socket 통신이 적합하다. 물론 polling 방식을 통해 socket 방식을 비슷하게 구현할 수 있긴 하지만, 매요청마다 발생하는 네트워크 비용과 짧은 시간에 무수히 많은 connection을 맺고 끊는 것보다는 부하가 덜 발생하는 듯함.

- [출처](https://kotlinworld.com/75)에 따르면 http 통신도 socket통신에 중 하나임(서버포트에 소켓을 열어두고 요청을 기다리니까?) 하지만 http를 따로 구분하는 이유는 요청에 대한 응답을 하는 웹통신의 특성상 http가 중요한 프로토콜로 구분됐기 때문이라고 함.

## Websocket
웹소켓과 TCP/IP 소켓은 차이가 있음
웹소켓은 http layer(Application layer)에서 작동.. 결국 socket이 어떤 layer에서 작동하는지만 다른거 같다.
http 프로토콜을 사용한다면 ws프로토콜, https를 사용한다면 wss라고 표시함
ws는 트래픽이 많고 지연이 낮은 접속환경에서 유리함

## STOMP
stomp는 http에서 모델링 되는 Frame([HTTP/2에서 사용하는 정보의 단위](https://brunch.co.kr/@sangjinkang/3)) 기반 프로토콜