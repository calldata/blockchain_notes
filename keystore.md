# keystore

keystore使用用户的提供的密码加密存储账号的私钥，一般导出为一个json文件。

```json
{
  "version": 3,
  "id": "859100bf-cb10-401b-badd-01611e1d55b5",
  "address": "5cc29b545720c01927f1f631af5e43ac37fad287",
  "Crypto": {
    "ciphertext": "d73a6f7fbc566205e771bb3d03ca15ae4fca06acafef89ef39b1f6191857d7cb",
    "cipherparams": {
      "iv": "ce2b4c74cd0711fb8afd47e65e9ea351"
    },
    "cipher": "aes-128-ctr",
    "kdf": "scrypt",
    "kdfparams": {
      "dklen": 32,
      "salt": "92fd04e14f1f9d1f9fc0af5004c2001e32219f8372a5fcd6dd91ab00c357023b",
      "n": 8192,
      "r": 8,
      "p": 1
    },
    "mac": "a547e0798618b7f3699a216fee61a0ee57afe368c6f1870422bf9e749bb19f36"
  }
}
```

* version 版本号
* id 唯一标识
* address 以太坊账号地址
* Crypto 使用到的密码学组件
* ciphertext 对私钥加密后的密文
* cipherparams 密码学算法参数
* iv aes-128-ctr加密用到的iv值
* cipher 使用的哪种加密算法
* kdf 全称key derivation function, 使用用户输入的密码派生出给aes-128-ctr算法使用的加密密钥， scrypt算法是常用的从用户密码派生加密密钥的算法
* dklen, salt, n, r, p 为scrypt算法的输入参数
* mac 由派生的私钥的最后16字节和对密钥加密后的密文计算sha3哈希值

keystore就是对以太坊账号私钥进行加密保护的措施，以myetherwallet产生的keystore文件为例描述它的产生过程：

1. 用户提供密码
2. myetherwallet.com网站后台产生用户的私钥
3. 根据用户的提供的密码对私钥进行加密
4. 以keystore文件的标准输出一个json文件

当用户要恢复该账号时，只需要利用钱包软件导入这个keystore文件并输入对应的密码就可以解密私钥。


#### 参考链接

* https://www.myetherwallet.com/
* https://github.com/ethereum/wiki/wiki/Web3-Secret-Storage-Definition