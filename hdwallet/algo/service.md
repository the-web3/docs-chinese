## algo 文档

go-sdk: https://github.com/algorand/go-algorand-sdk
开放节点1：https://mainnet-api.algonode.cloud， 节点提供商：https://algonode.io/api/#free-as-in--algorand-api-access
开放节点选择文档: https://developer.algorand.org/docs/get-started/devenv/ 
浏览器：https://algoexplorer.io/
接口文档：https://developer.algorand.org/docs/rest-apis/algod/v2/

### 1. 获取账户余额

```
curl https://mainnet-api.algonode.cloud/v2/accounts/ZW3ISEHZUHPO7OZGMKLKIIMKVICOUDRCERI454I3DB2BH52HGLSO67W754/

def get_account(address):
    path = "/v2/accounts/%s"% address
    info = await self.request_rest(path, method='GET')
    return info['balance']
```


### 2. 获取交易签名参数

```
curl https://mainnet-api.algonode.cloud/v2/transactions/params
def get_transaction_params():
    path = '/v1/transactions/params'
    return await self.request_rest(path, method='GET')
```

### 3.广播交易

请查看文档 /v2/transactions 看详情
```
def send_transaction(tx):
    path = '/v1/transactions'
    return await self.request_rest(path, method='POST', rawtxn=bytes.fromhex(tx))
```


### 4.根据地址获取交易列表

自行研究浏览器 api 获取




  

