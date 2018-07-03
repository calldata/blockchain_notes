# USDT 工作原理

USDT是发行在Omni layer上的一种资产，资产编号为31. Omni layer类似于ERC20代币平台，用户可以在上面发行自己的资产. Omni layer本身利用比特 OP_RETURN指令，将要发送的资产详细信息编码进20字节的数据中，发送和接收地址都是比特币地址.


#### 参考资料

* [omniexplorer](https://www.omniexplorer.info/)
* [使用omnicore-cli发送raw transaction](https://www.codetd.com/article/1692420)
* [omnicore rpc api 文档](https://github.com/OmniLayer/omnicore/blob/omnicore-0.0.10/src/omnicore/doc/rpc-api.md)
* [Omni Core Integration Guide (0.0.10) for Exchanges](https://docs.google.com/document/d/1vhL4QQL5nNstFfnxDvA-sHB8u5b797FQn550hkURWLM/edit)
* [发送一个 raw transaction的实例](https://gist.github.com/dexX7/352670c990ebf9ea31d6346a1519eb52)
* [如何得到TestOmni](https://github.com/OmniLayer/omnicore/issues/621)
* [regtest mode how to create Property](https://github.com/OmniLayer/omnicore/issues/620)
* [usdt raw transaction](https://steemit.com/usdt/@chaimyu/omni-usdt-raw-transaction)
* [SETTING UP OMNI CORE ON A SERVER](https://blog.omni.foundation/2016/12/12/setting-up-omnicore-on-a-server/)
* [Optimizing the payloads of Omni Layer transactions](https://medium.com/omnilayer/optimizing-the-payloads-of-omni-layer-transactions-ccb0a867da5d)
* [tether faucet on omni testnet](https://github.com/OmniLayer/omnicore/issues/529)
