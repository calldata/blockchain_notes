# 收款提示

钱包收到其他地址发送来的交易如何得到通知？

* etherscan 实现了[websocket api](https://etherscan.io/apis#websocket), 可以订阅某个地址接收到新交易时的通知.

* 自己实现

从某个块开始，获取`transactions`字段每个交易哈希，根据交易哈希获取交易的详情，找到`from`, `to` 和 `value`字段，就可以知道谁给这个地址转账多少ether.

```javascript
let blk = getBlock(5000000)
let txHashes = blk.transactions;

txHashes.forEach((txHash) => {
    tx = getTransaction(txHash)
    return tx.to, tx.from, tx.value
})
```

