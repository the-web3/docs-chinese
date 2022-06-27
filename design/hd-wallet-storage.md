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
|  is_del |  int   | 状态 0正常 1删除|


#### 2.2 资产表
| 字段名称  |  类型  |   解释 |
|:-------:|:-----:|:--------|
| id      | bigInt|   ID   |
| chain_id| bigInt|   链ID  |
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

采用对称加密算法 AES，加密的 Key 为设备 ID + 用户输入的密码


### 4. 操作方法


#### 4.1.APP 启动时

APP 启动时做一次初始化，把默认值支持的链和币种初始化到表

#### 4.2. 各个表的增加，删除，修改和查询

生成和导入助记词的时候，把助记词编码之后存储到 助记词表 表，导出的时候其实就是对 助记词表 查询组织数据返回到界面，私钥的导入导出也是类似的操作。









