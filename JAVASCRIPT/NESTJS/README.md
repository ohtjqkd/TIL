# NestJS

Node.js에 기반을 둔 웹 API

- Express 또는 Fastify 프레임워크를 래핑하여 동작(default express)
- 데이터베이스, ORM, 설정, 유효성 검사 등 수많은 기능을 기본 제공
- Angular로부터 영향을 많이 받았으며, 모듈/컴포넌트 기반으로 프로그램을 작성하여 재사용성을 높임
- IoC, DI, AOP와 같은 객체지향 개념을 도입함
- 타입스크립트를 기본으로 채택하고 있어 타입 언어의 장점을 누릴 수 있음

## Node.js의 특징
__단일 쓰레드 | non-blocking I/O | 이벤트 기반 비동기 방식__

Node.js는 애플리케이션 단에서 하나의 쓰레드에서 작업을 처리한다. (백그라운드에서는 쓰레드 풀을 구성해 작업을 처리)
하나의 작업이 끝날때까지 기다리지 않고 비동기로 처리한다. 이를 푸드코드에 비유해 표현하자면 다음과 같다.
1. 주문을 한 곳에서 받는다. (node 애플리케이션)
2. 하나의 주문을 받으면 해당 주문 처리를 기다리지 않고 식당에게 맡긴다. (백그라운드에 위임)
3. 각각의 식당에서는 먼저 완성된 음식을 호출벨을 이용해 손님에게 전달한다. (이벤트 기반 비동기 처리)

### Node.js의 장단점
- __장점__
단일 쓰레드 이벤트 기반 비동기 방식은 부하가 적어, 대규모 네트워크 애플리케이션을 개발하기 적합하다.

- __단점__
1. 데드락의 위험이 적다(?)
2. 하나의 쓰레드를 사용하기 때문에, 해당 쓰레드에 문제가 생기게 되면 애플리케이션 전체에 오류를 일으킬 위험이 있다.
3. 컴파일러 언어의 처리속도에 비해 성능이 떨어진다.(V8 엔진의 성능도 향상되고 있기는 하다.)
4. 여러 이벤트를 동시에 처리하는 경우 콜백 지옥에 빠져 가독성이 떨어지게 되는 경우가 발생할 수 있다. (ES6에서 Promise가 도입되면서 간결해짐)


[https://wikidocs.net/158475]
[https://kyounghwan01.github.io/blog/etc/nest/validation-dto/#dto-%E1%84%85%E1%85%A1%E1%86%AB]
[https://progressivecoder.com/how-to-setup-a-nestjs-sequelize-postgresql-integration/]
[https://tech.kakao.com/2019/08/01/graphql-basic/]
[https://baeharam.netlify.app/posts/Node.js/Node.js-Sequelize-%EB%8B%A4%EB%A3%A8%EA%B8%B0]