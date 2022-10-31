# DOT SavourHd 需要对接的接口

- 开放节点：https://rpc.polkadot.io
- go-sdk: https://github.com/savour-labs/go-substrate-rpc-client

### 1. 根据地址获取账户余额

- state_queryStorageAt
- state_queryStorage 

以上两个方法都可以


### 2. 获取 Account Nonce 

请求示范
```
{
   "jsonrpc":"2.0",
   "method":"account_nextIndex",
   "params": ["16ZL8yLyXv3V3L3z9ofR1ovFLziyXaN1DPq4yffMAZ9czzBD"],
   "id":1
}
```
或者
```
{
   "jsonrpc":"2.0",
   "method":"system_accountNextIndex",
   "params": ["16ZL8yLyXv3V3L3z9ofR1ovFLziyXaN1DPq4yffMAZ9czzBD"],
   "id":1
}
```

- params 里面传入的是对应的地址

返回示范

```
{
    "jsonrpc": "2.0",
    "result": 88,
    "id": 1
}
```

result: result 的值就是 Account Nonce


### 3. 获取最新 blockNumber 和 blockHash

请求示范

```
{
   "jsonrpc":"2.0",
   "method":"chain_getBlock",
   "id":1
}
```
返回示范

```
{
    "jsonrpc": "2.0",
    "result": {
        "block": {
            "header": {
                "parentHash": "0xcdaa562dd34ca954202ac5b7ab1225603cac1d672375b9958d5985704578843b",
                "number": "0xc07d6a",
                "stateRoot": "0x49776ff1f4d59b0f30c333a356b82e2dee5e94cd339856a6492c0c7ed38487a7",
                "extrinsicsRoot": "0x02ecb9e290b81f6c36ce35cf22ecdec67fadec1c940567418486464af3640606",
                "digest": {
                    "logs": [
                        "",
                        ""
                    ]
                }
            },
            "extrinsics": [
                "0x280403000b0ca851088401",
                ""
            ]
        },
        "justifications": null
    },
    "id": 1
}
```
- number: 最新区块高度
- stateRoot：最新区块Hash

### 4. 获取specName，specVersion， transactionVersion 等参数

请求示范

```
{
   "jsonrpc":"2.0",
   "method":"state_getRuntimeVersion",
   "id":1
}
```
返回示范

```
{
    "jsonrpc": "2.0",
    "result": {
        "specName": "polkadot",
        "implName": "parity-polkadot",
        "authoringVersion": 0,
        "specVersion": 9291,
        "implVersion": 0,
        "apis": [
            [
                "0xdf6acb689907609b",
                4
            ]
        ],
        "transactionVersion": 14,
        "stateVersion": 0
    },
    "id": 1
}
```
- specName: 链名称
- specVersion：版本
- transactionVersion：事物版本

### 5. 获取链名称 

请求示范

```
{
   "jsonrpc":"2.0",
   "method":"system_chain",
   "id":1
}
```
返回示范

```
{
    "jsonrpc": "2.0",
    "result": "Polkadot",
    "id": 1
}
```

### 6. 广播交易

请求示范

```
{
   "jsonrpc":"2.0",
   "method":"author_submitExtrinsic",
   "params": ["0x00000000"],
   "id":1
}
```

失败返回示范

```
{
    "jsonrpc": "2.0",
    "error": {
       .......
    },
    "id": 1
}
```
成功返回交易 Hash


### 7. 根据地址获取交易记录

- 自行调研第三方接口


   
   
sidecar api 链接：https://paritytech.github.io/substrate-api-sidecar/dist/




