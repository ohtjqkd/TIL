# Section 2

## What we will learn in this section
- What is BitCoin?
- Bitcoin's Monetary Policy
- Understanding Minig Difficulty
- Virtual tour of a Bitcoin Mine
- Mining Pools
- Nonce Range
- How Miners Pick Transactions (Part 1)
- How Miners Pick Transactions (Part 2)
- CPUs vs GPUs vs ASICs
- How do Mempools works?
- Orphaned blocks
- The 51% Attack
- Extra: Bits To Target conversion

## What is BitCoin?
### 암호화폐의 3계층
- Technology layer
    Blockchain 기술 자체를 의미하는 계층
- Protocol & Coin layer
    Blockchain 기술을 사용하여 네트워크 참여자들간 어떻게 상호작용을 하고 합의할지 정해 놓은 규약 계층
    Bitcoin, Ethereum, Ripple, Neo, Waves 등 다양한 Protocol이 있으며 각각의 Protocol은 하나의 코인을 가지고 있다.
    ex) Bitcoin: bitcoin, Ethereum: ether, Ripple: ripple ...
    코인은 블록 채굴과 블록 추가에 대한 보상으로 참여자들의 상호 작용을 용이하게 하는 장점이다.
- Token layer
    ICO라는 용어는 Coin 상장을 의미하지 않는다. Token을 의미함
    Token과 Coin은 다른 개념이다.
    Token은 다양한 프로토콜로 구축되는 스마트 계약에 의존함. (ABI 해쉬를 얘기하는 건가?)
    Coin에 투자 = 프로토콜에 투자
    Token에 투자 = 구축하고 있는 것 이면의 아이디어에 투자

### The Bitcoin Ecosystem
- Nodes
    네트워크에서 채굴을 하지 않는 참여자가 사용하는 장치 (거래 목적)
- Miners
    블록에 트랜잭션을 추가하고 블록을 채굴하여 블록체인이 성장하도록 돕는 참여자들
- Large Mines
    대규모 채굴 설비를 가진 채굴자들(?)
- Mining Pools
    채굴자들이 함께 모여 채굴 작업을 하는 것

## Bitcoin's Monetary Policy

### The Havling(반감기)  

출시되는(보상으로 주어지는(?)) 코인의 수가 절반으로 줄어드는 주기
비트코인은 4년마다 절반으로 줄어들었지만 정확히는 채굴된 블록이 210,000개에 달할 때마다 __코인보상을 절반__ 으로 줄인다. 난이도를 조정하는 것은 블록 빈도 파트에서
이러한 반감기는 소프트웨어에 이미 구현되어 있으며 임의로 변경할 수 없다.
블록의 채굴은 언젠가 끝이 날 수 밖에 없지만 이러한 한계성 때문에 트랜잭션을 블록에 추가하려는 참여자는 더 높은 수수료를 지불하게 되고 이를 통해 코인 보상이 줄어들어도 전반적으로 비슷한 경제성을 가지게 된다고 한다.
* 인플레이션 관련 내용은 잘 이해가 안됨
### Block Frequency(블록 빈도)
블록이 나타나는 빈도를 이야기 함, 시스템 설계에 따라 다름
| Cryptocurrency | Average Blocktime |
| --- | --- |
| Bitcoin | 10 min |
| ethereum | 15 sec |
| ripple | 3.5 sec |
| litecoin | 2.5 min |

### Understanding Minig Difficulty
Today we will answer these questions
- What is the Current Target and how does that _feel_?
    선행제로 x: 16 ^ 64
    선행제로 1: 16 ^ 63 -> 1 / 16 := 6 / 10 ^ 2
    선행제로 2: 16 ^ 62 -> 1 / 16 ^ 2 := 4 / 10 ^ 3
    ...
    선행제로 18: 16 ^ 46 -> 1 / 16 ^ 18 := 2 / 10 ^ 22
    
    선행제로가 늘어날 때마다 기하급수적으로 난이도가 높아짐

- How is "Mining Difficulty" calculated?
Difficulty = current target / max target
처음에 비해 얼마나 어려워졌냐를 계산하는 식
난이도 조정 또한 이미 소프트웨어에 구현되어 있다. (선행제로를 늘려서)

### Virtual tour of a Bitcoin Mine
[채굴설비를 보여주는 기사](https://qz.com/1055126/photos-china-has-one-of-worlds-largest-bitcoin-mines/)

### Mining Pools

대규모 채굴장비를 가진 채굴자들이 생기면서 해싱파워가 낮은 노드들을 위해 도입된 기술
블록을 채굴할 때, 하나의 Minig Pool에 속한 노드들에게 Nonce의 범위를 나누어 할당하고, 채굴에 성공했을 때는 각 노드들이 제공한 연산력에 따라 보상을 분배한다.

* ASIC
[Application Specific Integrated Circuit, 주문형 반도체]

특정 응용 분야 및 기기의 특수한 기능 하나하나에 맞춰 만들어진 집적회로

반도체를 간단하게 분류하면 표준형 반도체(Standard)와 주문형 반도체(ASIC)로 나눌 수 있는데, 표준형 반도체는 규격이 정해져 있어 일정 요건만 갖추면 어떤 전자제품에도 쓸 수 있는 제품이다. 반면 주문형 반도체는 특정한 제품을 위해 사용되는 제품으로 반도체 생산 업체가 특정 주문에 맞춰 생산하는 제품이다.

즉 주문형 반도체는 특정 기기를 위해 필요한 기능만 수행하도록 설계 및 제작되는데, 이는 가전, 휴대폰, 자동차 등 각 분야별로 필요한 기능이 다르고 그에 따라 다른 칩이 필요하기 때문이다.

주문형 반도체는 크게 설계방식에 따라 사용자의 요구에 맞춰 처음부터 회로를 설계 및 제조하는 완전 주문형 IC(Full custom IC)과 표준화된 설계를 일부 사용하여 회로를 설계 및 제조하는 반 주문형 IC(semicustom IC)으로 나뉜다.

주문형 반도체는 다품종 소량생산 방식의 상품으로 요구되는 주문 사항을 만족 시키기 위해서 뛰어난 반도체 설계 능력이 요구된다.
출처: (https://semiconductor.samsung.com/kr/support/tools-resources/dictionary/semiconductor-glossary-application-specific-integrated-circuit-asic/)

### Nonce Range

Nonce의 범위 2 ^ 32 := 4 * 10 ^10
Hash의 범위 2 ^ 256 := 10 ^ 77

하나의 Nonce만으로는 문제의 답을 찾을 가능성이 매우 낮다. 따라서 타임스탬프와 조합하여 해시값을 찾을 수 있다. (timestamp는 1초마다 바뀌기 때문에 Nonce와의 조합으로 무한대의 조합이 가능함)
하지만 Mining Pool이나 1초 이내에 모든 Nonce를 확인 할 수 있다면 시간의 낭비를 가져온다. 이를 해결하는 방법은 다음에..

### How Miners Pick Transactions (Part 1)

블록은 주기를 가지고 하나씩 생성되지만, 트랜잭션은 이보다 빠르게 계속 발생한다.
이런 트랜잭션들은 블록에 쓰여지기 전에 대기하는 장소인 멤풀에 입력되고 채굴자들은 이 멤풀에서 트랜잭션을 선택하여 블록에 기록하게 된다.
멤풀에는 트랜잭션 아이디와 수수료 정보 등이 기록되어 있는데 채굴자는 보통 수수료가 높은 트랜잭션을 선택하여 블록에 기록하게 될 것이다.
이렇게 블록의 제한에 맞춰 트랜잭션을 1차적으로 선택하고 Nonce를 탐색하여 채굴을 시작한다.
이전 Nonce range에서 살펴본대로 해싱파워가 매우 높은 채굴풀이나 노드들은 timestamp가 바뀌기 전 이미 Nonce를 전부 탐색할 수 있기 때문에 유휴생산력이 생기고 이를 효율적으로 사용하기 위한 방법이 바로 트랜잭션을 교체하는 것이다.
가장 수수료가 낮은 트랜잭션을 멤풀에 있는 것들 중 가장 수수료가 큰 트랜잭션과 교체하면 블록의 내용이 변경되기 때문에 같은 Nonce라도 다른 해시값을 가지게 된다.

### How Miners Pick Transactions (Part 2)