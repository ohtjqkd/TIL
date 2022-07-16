# Section 1

## What we will learn in this section
- What is a Blockchain?
- Understanding SHA256 Hash
- Immutable Ledger
- Distributed P2P Network
- How Mining Works (Part 1: The Nonce)
- How Mining Works (Part 2: The cryptographic puzzle)
- Byzantine Fault Tolerance
- Consesus Protocol (Part 1: Defense against attackeres)
- Consesus Protocol (Part 2: Competing chains)
- Blockchain Demo

## What is a Blockchain?
Blockchain은 관리 대상 데이터를 '블록'이라고 하는 소규모 데이터들이 P2P 방식을 기반으로 생성된 체인 형태의 연결고리 기반 분산 데이터 저장 환경에 저장하여 누구라도 임의로 수정할 수 없고 누구나 변경의 결과를 열람할 수 있는 분산 컴퓨팅 기술 기반의 원장 관리 기술이다
-출처: wikipedia

- Block의 구조
    Data: 블록이 담고 있는 데이터, transaction에 대한 정보가 담겨있을 것
    Prev.Hash: 이전 블록의 Hash값, 블록은 이전 블록의 Hash값을 가지고 연결한다.
    Hash: Block의 fingerprint와 같은 것

블록체인은 각 블록을 hash값으로 연결하여 데이터를 저장한다.


## Understanding SHA256 Hash
Hash란 임의의 크기를 가진 데이터를 고정된 크기의 데이터로 변환하는 것을 말한다.
Hash는 각 블록을 식별하게 해주는 식별자로 이용된다.
- Hash 알고리즘 특징
    - 단방향: 데이터를 통해 Hash값을 알 수 있지만 Hash값을 통해서는 데이터를 도출할 수 없음
    - 결정론적이어야함: 어떤 데이터를 넣던 정해진 크기의 데이터로 변환되어야함
    - 연산이 빨라야함: 말그대로임
    - 쇄도 효과(Avalanche Effect): 미세한 데이터의 변경으로도 극명하게 다른 Hash값이 나와야함
    - 충돌저항성: 다른 데이터로 같은 해쉬값이 나올 수 있는 확률은 물론 존재하지만 이를, 임의로 만들어 낼 수 있을 정도가 되면 안된다는 뜻인거 같음


## Immutable Ledger
기존의 원장의 경우 (ex. 종이장부, 스프레드시트 등) 어떠한 이유로 손상되거나 변경될 수 있다. 예를 들면 자연재해로 인해 장부가 손실되거나, 누군가 종이장부의 내용을 바꾼다거나, 스프레드시트의 경우 해커들에 의해 간단하게 변경될 수 있다.
블록체인의 경우, 해커가 장부의 내용(블록의 데이터)을 변경하려고 할 경우 블록의 Hash값이 변경되면서 뒤에 연결되어 있는 블록들이 유효하지 않게 된다.
이처럼 손으로 쓰는 원장에서 한 항목을 쉽게 변경할 수 있는 것과 달리 블록체인에서는 이어지는 전체 항목을 변경해햐 한다.
이것이 바로 Immutable하다고 하는 이유이다.


## Distributed P2P Network
만약 이런 블록체인을 한 명만 가지고 있다면 시간이 많이 걸리기는 하겠지만 해커들에 의해 이어진 모든 블럭의 정보를 변경하는 것도 가능하긴 할 것이다.
하지만 이런 블록체인을 네트워크 참여자들이 모두 가지고 있다면?
주변의 노드들이 주기적으로 서로 유효성을 검사하게 되며 현재 가지고 있는 블록체인과 달라진 점이 포착되면 (블록체인이 오염됐다면) 주변의 노드의 블록체인을 통해 복구할 수 있게된다.
이처럼 하나의 노드만을 해킹해서는 블록체인 네트워크를 해킹할 수 없고, 네트워크의 51%를 동시에 모두 해킹해야 네트워크를 망가뜨릴 수 있다.
이는 네트워크 참여자가 늘어나면 늘어날 수록 해킹이 어렵고 51%의 참여 노드를 공격하는 비용이 얻을 수 있는 이득보다 적어 사실상 무의미해진다. 또한 어떻게 해서 해킹을 성공했다 하더라도 해킹이 그 블록체인의 가치를 떨어뜨리기 때문에 해킹을 하더라도 의미가 없다..


## How Mining Works (Part 1: The Nonce)
여러 transaction을 어떻게 하나의 블록에 담을 수 있냐
불변원장에서 바꿀 수 있는 값은 Nonce 밖에 없음 이를 통해 현재 블록의 Hash값을 변경할 수 있음 (그런데 Why?)

## How Mining Works (Part 2: The cryptographic puzzle)
채굴자들은 block에 담을 transaction 데이터들과 Block number 이전 해쉬를 고정시킨 상태에서 Nonce만을 변경해가며 target 해쉬가 나올때까지 무차별 대입을 통해 Hashing을 한다. 역설계가 불가능하기 때문에 해당 값이 나올 때까지 무차별 대입을 해볼 수 밖에 없다.
만약 target hash 보다 낮은 hash값을 찾아낸다면 그때 문제를 풀었다고 체인에 알리고 블록을 추가하는 듯

## Byzantine Fault Tolerance
비잔틴 내결함성
다수의 의사결정자들이 합의를 도출해야 할 때 생길 수 있는 문제

1982년 래슬리 램포트 연구 논문에서 사용한 표현

가정된 상황
- 각 장군들이 합동하여 과반수 이상이 출병해야만 승리할 수 있음
- 각 장군들은 전령을 통해서 연락을 주고 받음
- 각 장군들은 근처의 장군에게 연락함
- 장군들 중 배신자가 존재할 수도 있고, 배신자는 실제 전파받은 공격계획과 다른 내용을 전파할 수 있음. 메시지지도 중간에 훼손할 수 있다.

분산화된 시스템에서 합의를 달성할 수 있는 방법은 최소 2/3 이상이 신뢰할 수 있는 자여야한다.
만약 1/3 이상이 악의적인 의도를 가지고 있다면 시스템이 실패할 수 있다는 것을 의미함

이런 비잔틴 내결함성 문제는 다양한 산업에서 풀어야할 사항이다. (항공, 우주, 원자력) - 일부의 결함이 발생하더라도 시스템 기능을 유지하기 위해서

블록체인에서는 이런 내결함성에 대해 어떻게 저항성을 높이는지 알아보자

## Consesus Protocol (Part 1: Defense against attackeres)
## Consesus Protocol (Part 2: Competing chains)
## Blockchain Demo