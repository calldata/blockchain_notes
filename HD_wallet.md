# HD wallet原理

bip32, bip39, bip44协议已经事实上成为了数字货币钱包的工业标准。bip32描述了HD钱包的各个层级密钥的产生过程。
bip39方便钱包的备份，bip44实现了钱包的多币种支持。

## bip39协议

bip39协议描述了如何从随机种子产生助记词的过程， 具体的算法步骤：

1. 创建一个128到256位的随机序列（熵）。
2. 提出SHA256哈希前几位（熵长/ 32），就可以创造一个随机序列的校验和。
3. 将校验和添加到随机序列的末尾。
4. 将序列划分为包含11位的不同部分。
5. 将每个包含11位部分的值与一个已经预先定义2048个单词的字典做对应。
6. 生成的有顺序的单词组就是助记码。

助记词产生过程的伪代码描述(以12个助记词的产生为例)：

```python
#word_list为bip39协议规定的2048个英文单词
def generate_mnemonic(word_list):
    random128bit = csprng()
    checksum = sha256(random128bit)[0:4]
    entropy = random128bit.append(checksum)
    word_indexes = split_every_11bit(entropy)
    
    mnemonic = []
    for idx in word_indexes:
        mnemonic.append(word_list[idx])

    return mnemonic
```

从助记词产生产生`root seed`的过程：

7. PBKDF2密钥延伸函数的第一个参数是从步骤6生成的助记符。
8. PBKDF2密钥延伸函数的第二个参数是盐。 由字符串常数“助记词”与可选的用户提供的密码字符串连接组成。
9. PBKDF2使用HMAC-SHA512算法，使用2048次哈希来延伸助记符和盐参数，产生一个512位的值作为其最终输出。 这个512位的值就是种子。

算法的伪代码描述：

```python
def generate_root_seed(mnemonic, salt):
    return PBKDF2(mnemonic, salt, iterations=2048)
```

在bip32协议中，将会使用这个`root seed`作为根种子生成主密钥，主链码等。

## bip32协议

bip32协议描述了HD钱包的标准，主密钥，链码，子密钥等的产生过程。

主密钥和主链码的生成过程伪代码描述：

```python
def generate_master_private_key_and_master_chain_code():
    mnemonic = generate_mnemonic(word_list)
    seed = generate_root_seed(mnemonic, salt)
    key = hmac-sha512(seed)
    master_private_key, master_chain_code = key[0:256], key[256:512]

    return master_private_key, master_chain_code

def child_key_derivation(parent_private_key, parent_chain_code, index):
    key = hmac-sha512(parent_private_key + parent_chain_code + index)
    child_key, child_chain_code = key[0:256], key[256, 512]

    return child_key, child_chain_code
```

## bip44协议

基于 BIP32 的系统，赋予树状结构中的各层特殊的意义。让同一个 seed 可以支援多币种、多帐户等。各层定义如下：
m / purpose' / coin_type' / account' / change / address_index
其中的 purporse' 固定是 44'，代表使用 BIP44。而 coin_type' 用来表示不同币种，例如 Bitcoin 就是 0'，Ethereum 是 60'。


#### 参考链接：

1. https://github.com/ethereum/EIPs/issues/84
2. http://ibloodline.com/assets/master-bitcoin/ch05.html