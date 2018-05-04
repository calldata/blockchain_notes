# 以太坊的一笔交易的完成过程

使用web3发送一笔交易为例子来说明这个过程

```javascript
var Tx = require('ethereumjs-tx');
var privateKey = new Buffer('e331b6d69882b4cb4ea581d88e0b604039a3de5967688d3dcffdd2270c0fd109', 'hex')

var rawTx = {
  nonce: '0x00',
  gasPrice: '0x09184e72a000', 
  gasLimit: '0x2710',
  to: '0x0000000000000000000000000000000000000000', 
  value: '0x00', 
  data: '0x7f7465737432000000000000000000000000000000000000000000000000000000600057'
}

var tx = new Tx(rawTx);
tx.sign(privateKey);

var serializedTx = tx.serialize();

//console.log(serializedTx.toString('hex'));
//f889808609184e72a00082271094000000000000000000000000000000000000000080a47f74657374320000000000000000000000000000000000000000000000000000006000571ca08a8bbf888cfa37bbf0bb965423625641fc956967b81d12e23709cead01446075a01ce999b56a8a88504be365442ea61239198e23d1fce7d00fcfc5cd3b44b7215f

web3.eth.sendRawTransaction('0x' + serializedTx.toString('hex'), function(err, hash) {
  if (!err)
    console.log(hash); // "0x7f9fade1c0d57a7af66ab4ead79fade1c0d57a7af66ab4ead7c2c2eb7b11a91385"
});
```

首先构造一个rawTx结构，包括几个主要字段：

* nonce 从该账号发出的交易次数，为了防止重放攻击
* gasPrice 以太坊的操作会消耗一定数量的gas，每单位gas用ether来计价
* gasLimit 最多希望消耗的gas数量
* to 交易接收者
* value 转出的ether数量
* data 如果这笔交易为转账交易data字段可以为空，如果为合约创建或者调用合约该字段不空

接下来将rawTx构造为一个标准的以太坊交易结构，用私钥对交易进行签名，序列化该交易结构方便网络传输，
最后调用web3的`sendRawTransaction`接口将交易广播至矿工节点，当矿工挖到这笔交易说明交易成功。

#### 参考链接

* https://github.com/ethereum/wiki/wiki/JavaScript-API#web3ethsendrawtransaction