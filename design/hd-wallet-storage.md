# HD 钱包的接入的整体数据存储设计

### 1.数据库

- 选用 sqlite3
- rn(nodejs 操作数据库)

### 2.表结构设计

#### 2.1 链表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
|   id    | bigInt |  ID   |
|   name  | varchar| 链名称 |
|   logo  | varchar| 链Logo |
|  is_del |  int   | 状态 0正常 1删除|


#### 2.2 资产表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
| id      | bigInt|   ID   |
| chain_id| bigInt|   链ID  |
| logo    | varchar| 币Logo |
| name    |varchar|  资产名称|
| contract|varchar|  合约地址|
| unit    | int   |  精度   |
| is_del  |  int  | 状态 0正常 1删除|


#### 2.3 助记词表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
| id      | bigInt|   ID    |
| coin_id | bigInt|   资产ID |
| encode  |varchar|  加密的助记词编码   |
| is_del  |  int  | 状态 0正常 1删除|


#### 2.4 账户表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
| id      | bigInt|   ID    |
| coin_id | bigInt|   资产ID |
| word_id | bigInt|   助记词ID |
| index   |  int  |  Bip地址索引 |
| address |varchar|   地址   |
| balance |varchar|   账户余额   |
| pub_key |varchar|   公钥    |
| priv_key|varchar|  加密的私钥    |
| is_del  |  int  | 状态 0正常 1删除|


#### 2.5 交易记录表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
| id      | bigInt|   ID    |
| coin_id | bigInt|   资产ID |
| from    |varchar|   转出地址 |
| to      |varchar|   转入地址 |
| tx_hash |varchar|  交易 Hash |
| rwa     |varchar|  签名的交易 |
| fee     |varchar|  交易手续费 |
| block   |bigInt |  所在区块 |
| direction|int |  方向：0 转入，1 转出 |
| status  |  int  | 状态  0成功  1失败|
| is_del  |  int  | 状态 0正常 1删除|


### 3. 加密算法

采用对称加密算法 AES，加密的 Key 为设备 ID + 用户输入的密码，具体参考 snow 代码库的 example 部门的代码


### 4. 操作方法


#### 4.1.APP 启动时

APP 启动时做一次初始化，把默认值支持的链和币种初始化到表

#### 4.2. 生成账户

生成助记词->验证助记词->验证通过->助记词编码存储到助记词表
助记词生成 seed-> Masterkey -> bip44 协议-> child privateKey -> publicKey->Address, 将地址对应的 Bip 协议的索引(默认 0)，私钥加密和公钥存储到账户表里面，并请求一次余额更新到表里。检测手机是否连网，如果连网，不断请求余额更新。

#### 4.3. 导出助记词和私钥

导出助记词->查询助记词表->得到助记词编码之后解密返回给界面
导出私钥->查询账户表->得到私钥后解密返回给界面

#### 4.4. 导入助记词和私钥

导入助记词->验证助记词->验证通过->助记词编码存储到助记词表

助记词 seed-> Masterkey -> bip44 协议-> child privateKey -> publicKey->Address, 将地址对应的 Bip 协议的索引(默认 0)，私钥加密和公钥存储到账户表里面，并请求一次余额更新到表里。检测手机是否连网，如果连网，不断请求余额更新。

导入私钥-> privateKey -> publicKey->Address, 将地址对应的 Bip 协议的索引(默认 0)，私钥加密和公钥存储到账户表里面，并请求一次余额更新到表里。检测手机是否连网，如果连网，不断请求余额更新。

#### 4.6. 获取余额

检测手机是否连网，如果连网，不断请求余额更新。

#### 4.7. 转账

发起转账-> 组织交易数据-> 从账户表里拿到 privateKey->交易签名->更新交易到交易表->广播交易->检测交易状态更新到交易记录表

#### 4.8. 获取交易记录

检测手机是否连网，如果连网，不断请求交易记录更新。




