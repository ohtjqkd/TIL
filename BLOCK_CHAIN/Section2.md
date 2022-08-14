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
    비트코인은 4년마다 절반으로 줄어들었지만 정확히는 채굴된 블록이 210,000개에 달할 때마다 코인 보상을 절반으로 줄인다.
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