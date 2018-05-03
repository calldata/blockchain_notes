## HD wallet原理

bip32协议

bip39协议
将 seed 用方便记忆和书写的单字表示。一般由 12 个单字组成，称为 mnemonic code(phrase)，中文称为助记词或助记码。

bip44协议
基于 BIP32 的系统，赋予树状结构中的各层特殊的意义。让同一个 seed 可以支援多币种、多帐户等。各层定义如下：
m / purpose' / coin_type' / account' / change / address_index
其中的 purporse' 固定是 44'，代表使用 BIP44。而 coin_type' 用来表示不同币种，例如 Bitcoin 就是 0'，Ethereum 是 60'。


#### 参考链接：
1. https://github.com/ethereum/EIPs/issues/84