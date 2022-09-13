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