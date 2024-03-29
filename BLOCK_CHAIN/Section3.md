# Section 3

## What we will learn in this section
- Transactions and UTXOs
- Where do transaction fees come from?
- How wallets work
- Signatures: Private & Public Keys
- Signatures: Keys Demo
- What is Segregated Witness? (SegWit)
- Public Key vs Bitcoin Address
- Hierarchically Deterministic (HD) Wallets

### Transactions and UTXOs
UTXO - Unspent Transaction Output, 아직 쓰지 않은 잔액이라는 의미
비트코인 네트워크에서는 잔액이라는 개념이 존재하지 않기 때문에, 트랜잭션에 의한 결과물들의 합을 잔액이라는 개념으로 사용하는데 이를 UTXO 데이터로 대체한다.
각 지갑의 UTXO들은 해당 지갑 주인에 대해 공개키 암호로 잠겨있다.
이러한 체계에서 거래를 하기 위해서는 UTXO를 선택하여 거래액 이상(수수료 포함)을 만들고 해당 트랙잭션을 input으로 하여 새로운 UTXO를 만들어 거래를 진행한고 해당 트랜잭션을 사용처리하여 잔액을 줄이는 형태이다. 만약 거래액을 정확히 맞출 수 없다면 초과분에 대하여 자신에게 보내는 형태로 UTXO를 새로 만들어낸다.

### Where do transaction fees come from?
UTXO를 처리하면서 수수료도 같이 처리함.

### How wallets work

코인이 지갑에 있는 것은 아님 그저 블록체인 네트워크 상의 내용을 보기 쉽게 만들어줄뿐
지갑은 블록체인 상의 UTXO를 확인하여 사용자에게 얼만큼의 UTXO가 있는지 보여준다.
* 입력값으로 사용된 Transaction의 체크는 어떻게 하는것인지? block의 내용을 변경해서 바꿀 수 있는 것도 아닌데?? output 쪽에 기록이 되는건지

### Signatures: Private & Public Keys
트랜잭션의 내용을 암호화하는 방법  
![private&pulbic](../assets/Screenshot%20from%202022-09-13%2019-59-16.png)

transaction을 개인키로 서명하고 공개키와 함께(?) 브로드캐스팅 -> 블록체인 검증 함수를 통해서 다른 노드들이 검증하는 듯?

### Signatures: Keys Demo
https://tools.superdatascience.com/blockchain/public-private-keys

### What is Segregated Witness? (SegWit)
블록사이즈: 1mb
거래 속도의 확장성
비트코인은 현재 기술력으로 1초에 7개의 거래를 성사시킴, 시중의 금융기관의 처리 속도에 비해 매우 느림(1초에 수백 만 건)
이런 거래 속도의 확정성 문제 때문에 나오게 된 것이 세그윗(Segregated Witness; Segwit)  

트랜잭션에서 서명을 분리하여 실제 블록에 담을 수 있는 트랜잭션 수를 늘린다(하드포크 없이 실질적 블록사이즈를 늘릴 수 있게 됨)
* 궁금한 점 그럼 서명은 어디에 저장이 되는 건가? 찾아보니 segwit주소라는 개념이 있는데 이게 어떻게 연결되는 걸까요, Witness라는 새로운 데이터 레이어를 넣고 블록과 동기화 한다는데 이게 뭐죠..


### Public Key vs Bitcoin Address

Private key --(타원함수)--> Public key --(해시함수)--> Address   
코인을 보낼 때 주소 뿐만 아니라 Public key의 주소로 바로 보내는 것도 가능함. 하지만 주소라는 값을 쓰는 이유는 타원함수의 혹시 모를 결함이 발견되었을 경우, 즉 역설계가 가능해지는 경우 public key가 완전 공개되어있다면 private key가 역설계되어 보안에 큰 문제가 생기게 되는데 이를 막기 위해 해싱을 통해 주소와 public key 사이에 암호화 계층을 하나 더 쌓아 최대한 피해를 늦추기 위한 것임

### Hierarchically Deterministic (HD) Wallets  

계층결정적 지갑이라는 단어가 너무 어렵다... 대충이라도 이해한 내용을 적어보자면 pirvate key 하나로 다수의 거래를 할 경우 거래의 종류에 따라 account의 대한 대략적인 정보를 알 수 있게 된다. 예를 들어 하나의 계정(address)로 집 근처의 피자를 계속 사먹었을 때, 적어도 계정의 주인이 해당 피자가게 근처에 살고 있다는 사실을 알 수 있게 된다. 이러한 점은 익명성이 철저하게 보장되어야 하는 블록체인에 있어서 큰 약점으로 다가 올 수 있게 됐고 , Bip를 통해 새로운 개선책을 제시함
사용자는 Master private key를 통해 언제든 새로운 private key를 생성하고 새로운 address를 통해 거래가 가능함
만약 기업의 경우, Master private key를 소유한 사람은 계층적으로 하위에 있는 private key를 통해 모든 계정에 접근할 수 있게 되며, 역방향은 성립하지 않는다.
Master public key는 public key를 생성할 수 있게 도와주며 검증에 사용된다. 정도로 정리 할 수 있을거 같다.