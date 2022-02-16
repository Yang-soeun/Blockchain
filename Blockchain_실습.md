# ⭐ Blockchain_실습

<details>
  
<summary> ✏ Testing Blockchain </summary>
<div markdown="1">
 
## Implementing Blockchain Using Python
- [Source_code](blockchain.py)
  
### Compotents:
- Timestamp : the time that the block was added to the blockchain
- Index : a running number starting from() indicating the block number.
- Hash of the previous block : the hash result of the previous block.
- Nonce : the number used once.
- Transaction(s) : each block will hold a variable number of transactions.
  
### Installing Flask
✔ 관리자 권한으로 실행
  
` $ pip install flask `
` $ pip install request `
  
 > Flask is a web framework that makes building web applications easy and rapid
  
## Running_terminal1
` $ python blockchain.py 5000 `
- 결과
  
![terminal1](https://user-images.githubusercontent.com/87464750/154253242-a9868d35-d29c-4b27-9d45-97cf4a6a15c2.png)

✔ 첫 번째 노드에서 실행되는 첫 번째 블록체인이 현재 실행 중인것을 볼 수 있다.

## terminal2
  
### 📑 first block
` $ curl http://localhost:5000/blockchain `
- 결과

![genesis_block](https://user-images.githubusercontent.com/87464750/154254418-83e11ca4-e3c8-435d-b885-d3f61fd16b23.png)
  
```
{
  "chain" : [{
    "hash_of_previous_block: "181cfa3e85f3c2a7aa9fb74f992d
    0d061d3e4a6d7461792413aab3f97bd3da95",
    "index" : 0,
    "nonce" : 61093,
    "timestamp" : 1644946853.955589,
    "transactions" : []
  }],
  "length" : 1
}
```
✔ 첫 번째 블록(인덱스 0)인 제니시스 블록이다.
  
### 📑 Try Mining
- Try mining a block to see how it will affect the blockchain Type the following
  
` $ curl http://localhost:5000/mine `
- 결과
  
✔ The block that is mined will now be returned:
  
![mine1](https://user-images.githubusercontent.com/87464750/154255602-91fb686f-4056-4ad9-a62e-5d0c16017955.png)

```
{
  "hash_of_previous_block": "d7a7c6ee011820a5d156c5158cb27ea48943d4817a48218829aa865bf4a21fbc",
  "index" : 1,
  "message" : "New Block Mined",
  "nonce" : 13807, 
  "transactions" : [{
    "amount" : 1,
    "recipient: "4d9de024d88d4eb7b16f4f353e5b9ddf",
    "sender" : "0"
  }]
}
```
✔  블록에 단일 트랜잭션이 포함되어 있으며 이는 채굴자에게 제공되는 보상이다.

### 📑 Obtain the blockchain from node
` $ curl http://localhost:5000/blockchain`
 
- 결과
  
✔ 이제 새로 채굴된 블록이 블록체인에 있는 것을 볼 수 있다:
  
![obtain](https://user-images.githubusercontent.com/87464750/154257790-70bc949c-cba8-49a3-8e41-f7cd1458ddc0.png)
  
```
{
  "chain" : [{
  "hash_of_previous_block: "181cfa3e85f3c2a7aa9fb74f992d
  0d061d3e4a6d7461792413aab3f97bd3da95",
  "index" : 0,
  "nonce" : 61093,
  "timestamp" : 1644946853.955589,
  "transactions" : []
}, {
  "hash_of_previous_block": "d7a7c6ee011820a5d156c5158cb27ea48943d4817a48218829aa865bf4a21fbc",
  "index" : 1,
  "message" : "New Block Mined",
  "nonce" : 13807, 
  "transactions" : [{
    "amount" : 1,
    "recipient: "4d9de024d88d4eb7b16f4f353e5b9ddf",
    "sender" : "0"
    }]
  }]
  "lenght" : 2
}
```
  
</br>
  
> Remember that the default difficulty target is set to four zero. you can change it to five zero and retest the blockchain. </br> you will realize that it now takes a longer time to mine block. since it is more difficult to find a nonce thath results in a hash beginning with five zeros.

</br>

### 📑 Add a transaction
- Let's add a transaction to a block by issuing the following command in Terminal.
  
```
$ curl -X POST -H "Content-Type: application/json" -d "{\"sender\": \"04d0988bfa799f7d7ef9ab3de97ef481\", \"recipient\": \"cd0f75d2367ad456607647edde665d6f\",\"amount\": 5}" "http://localhost:5000/transactions/new"
```
  
- 결과
  
![add](https://user-images.githubusercontent.com/87464750/154260518-56e9a9af-eb3a-474a-a71d-f42937177987.png)

✔ 성공적으로 블록이 추가되었다.
  
✔ 이제 블록을 mine 할 수 있다.
  
### 📑 Mine the block
` $ curl http://localhost:5000/mine `
- 결과

![mine2](https://user-images.githubusercontent.com/87464750/154261674-d98b2e9e-177d-4de5-814d-b13f1dbfa8be.png)
  
```
{
  "hash_of_previous_block": "7beffae74017f36dfd91d1e3a71bab570d6f10e8d97dfdae37d17d66ae7b4c32",
  "index" : 2,
  "message" : "New Block Mined",
  "nonce" : 98128, 
  "transactions" : [{
    "amount" : 5,
    "recipient: "cd0f75d2367ad456607647edde665d6f",
    "sender" : "04d0988bfa799f7d7ef9ab3de97ef481"
}, {
    "amount" : 1,
    "recipient: "4d9de024d88d4eb7b16f4f353e5b9ddf",
    "sender" : "0"
  }]
}
```
  
✔ 블록 2가 채굴되었으며 여기에는 두 개의 트랜잭션이 포함되어 있다. 하나는 수동으로 추가한 것이고 miner에 대한 보상이 있다.
 
### 📑 Add Block
- Examine the content of the blockchain by issuing this command.
  
- 결과

![last](https://user-images.githubusercontent.com/87464750/154263518-08b1befb-51d5-45d7-9cb4-8c4c42878a4a.png)

```
{
  "chain" : [{
    "hash_of_previous_block: "181cfa3e85f3c2a7aa9fb74f992d
     0d061d3e4a6d7461792413aab3f97bd3da95",
    "index" : 0,
    "nonce" : 61093,
    "timestamp" : 1644946853.955589,
    "transactions" : []
}, {
    "hash_of_previous_block": "d7a7c6ee011820a5d156c5158cb27ea48943d4817a48218829aa865bf4a21fbc",
    "index" : 1,
    "message" : "New Block Mined",
    "nonce" : 13807, 
    "transactions" : [{
      "amount" : 1,
      "recipient: "4d9de024d88d4eb7b16f4f353e5b9ddf",
      "sender" : "0"
  }]
}, {
    "hash_of_previous_block": "7beffae74017f36dfd91d1e3a71bab570d6f10e8d97dfdae37d17d66ae7b4c32",
    "index" : 2,
    "message" : "New Block Mined",
    "nonce" : 98128, 
    "transactions" : [{
      "amount" : 5,
      "recipient: "cd0f75d2367ad456607647edde665d6f",
      "sender" : "04d0988bfa799f7d7ef9ab3de97ef481"
}, {
      "amount" : 1,
      "recipient: "4d9de024d88d4eb7b16f4f353e5b9ddf",
      "sender" : "0"
    }]
  }]
  "lenght" : 3
}
```

✔ 이제 두 트랜잭션이 포함된 새로 추가된 블록이 표시된다.

 </details>
 </div>
 
<details>
  
<summary> ✏ Connecting to the Ethereum Blockchain </summary>
<div markdown="1">
  
 </details>
 </div>
 
 
