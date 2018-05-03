##Keyring的工作原理

keyring是metamask钱包用户账户的管理工具类，可以完成账户创建，交易签名，加密持久化存储等功能。
Keyring是对一系列接口的描述，主要完成以下功能：

- serialize()  将该kerying对象进行系列化使用用户提供的密码进行加密存储
- deserialize() 将加密存储的keyring对象反序列化
- addAccount(n=1) 新建账户，将账户相关信息通知keying以便能持久化存储
- getAccounts() 获取这个keyring管理的账户
- signTransaction(address, transaction) 用对应地址的私钥签名交易
- signMessage(address, data) 用对应地址的私钥签名数据
- exportAccount(address) 导出对应地址的私钥

keyring只是metamask钱包管理用户用户密钥的抽象接口，

####参考链接：
1.https://github.com/MetaMask/KeyringController/blob/master/docs/keyring.md
2.https://github.com/MetaMask/eth-hd-keyring
3.https://github.com/MetaMask/eth-simple-keyring