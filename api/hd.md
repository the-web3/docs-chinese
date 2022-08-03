
###  钱包部分接口文档

**1.获取余额接口**

接口名称：api/v1/wallet/get_balance
请求方式：post
请求示范

```
    {
       "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
    	"address": "0x00000000000000000000000",
    	"contract_address": "0x00000000000000000"
    }
```

传入参数

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   address：要查询余额的地址，必传
*   contract\_address： 合约地址，没有合约的地址的直接传入空值，必传

返回示范
```
    {
      "status": true,
      "code": 2000,
      "message": "get account balance success",
      "data": {
    		"balance": "100000",
    	}
    }
```

返回值解释

*   balance: 余额

**2. 获取地址账户信息接口**

接口名称：api/v1/wallet/get_account_info

请求方式：post

请求示范
```
    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
      "address": "0x0000000000000000000000"
    }
```    

参数解释

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   address：要查询余额的地址，必传

返回示范
```
    {
    	"status": true,
    	"code": 2000,
      "message": "get account info success",
      "data": {
    		"nonce": "1",
    	  "account_number": 1000098
    	}
    }
```

返回值解释

*   nonce：eth 的 noce, 或者其他币种的类似 sequence 的东西
*   account\_number： 账户号

**3. 获取手续费接口**

接口名称：api/v1/wallet/get_fee

请求方式：post

请求示范
```
    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
      "message": "0x0000000000000000000000"
    }
```

参数解释

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   message：消息，非必传

返回示范
```
    {
    	 "status": true,
       "code": 2000,
       "message": "get transaction fee success",
       "data": {
    	   "low":{
    				"fee": 100000,
    	      "base_fee": 110000
    			  "gas_limit": 21000,
    			  "gas_price": 800000000000
    			},
    		 "meddium":{
    				"fee": 105000,
    			  "base_fee": 110000
    			  "gas_limit": 21000,
    			  "gas_price": 800000000000
    			}
    			"high":{
    				"fee": 110000,
    	      "base_fee": 110000
    			  "gas_limit": 210000,
    				"gas_price": 1800000000000
    			}
       }
    }
```

返回值解释

*   low 最慢档
*   meddium 中间挡
*   最快档
    *   fee： 使用 fee
    *   gas\_limit: gas\_limit
    *   gas\_price: gas\_price

**4. 广播交易接口**

接口名称：api/v1/send\_transaction

请求方式：post

请求示范
```
    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
    	"rawtx": "0x0000000000000000000000000000000000000000000000000000000000"
    }
```

参数解释

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   rawtx：要广播的交易

返回示范
```
    {
    	"status": true,
       "code": 2000,
       "message": "send transaction success"
       "data": {
    		  "hash": "0x0000000000000000000000000000000000000000000000000000000000"
    	}
    }
```

参数解释

*   hash: 交易 Hash

**5. 获取未花费的输入输出(此接口针对 utxo 系列)**

接口名称：api/v1/get\_unspend\_list

请求方式：post

请求示范
```
    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
      "address": "0x0000000000000000000000"
    }
``` 

参数解释

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   address：地址，必传

返回示范

    {
    	 "status": true,
       "code": 2000,
       "message": "get utxo success"
       "data": [
    			"txid": "0x00000000000",
    			"vout": 1000000,
    			"index": 0,
    			"script": "",
    		  "amount": 100000
       ]
    }
    

参数解释

*   txid: 交易ID
*   vout：输出
*   index：索引
*   script：锁定脚本
*   amount： 金额

**6.获取交易记录接口**

接口名称：api/v1/get\_address\_transaction

请求方式：post

请求示范

    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
      "address": "0x00000000000000000000000000"
      "contract_address": "0x00000000000000000000000000",
      "page": 1,
      "page_size": 10,
      "order": "time"
    }
    

参数解释

*   network: 网络，可传入参数为 mainnet 和 testnet， 必传
*   chain: 链名称，必传
*   symbol：币种名称，必传
*   address: 地址 必传
*   contract\_address：合约地址
*   page：页码
*   page\_size：没页显示的数量

返回示范

    {
       "status": true,
    	 "code": 2000,
       "message": "get transaction success"
       "data": [
    			 {
               "hash": "0x0000000000000000",
    					 "from": "0x0000000000000000",
    					 "to": "0x0000000000000000",
    					 "value": 0.001,
    					 "fee": 0.000001,
    	         "block": 1233221,
               "status": 0,
    	         "direction": "out"
    			 }
    	  ]
    }
    

参数解释

*   hash: 交易 Hash
*   from: 转出地址
*   to：转入地址
*   value：转入金额
*   fee：手续费
*   block：所在区块
*   status： 状态
*   direction: 方向，转入转出

**7.获取交易详情接口**

接口名称：api/v1/get\_hash\_transaction

请求方式：post

请求示范

    {
      "network": "mainnet",
    	"chain": "eth",
    	"symbol":"eth",
      "hash": "0x00000000000000000000000000"
    }
    

参数解释

返回示范

    {
       "status": true,
    	 "code": 2000,
       "message": "get transaction success"
       "data": {
             "hash": "0x0000000000000000",
    				 "from": [
    						"0x0000000000000000",
    						"0x0000000000000000"
    				  ]
    				 "to": [
    						"0x0000000000000000",
    						"0x0000000000000000"
    					]
    				 "value": [
    						0.001,
    						0.001
    					]
    				 "fee": 0.000001,
             "block": 1233221,
             "status": 0,
             "direction": "out"
    		 }
    }
    

参数解释

*   hash: 交易 Hash
*   from: 转出地址
*   to：转入地址
*   value：转入金额
*   fee：手续费
*   block：所在区块
*   status： 状态
*   direction: 方向，转入转出

**8.提交钱包接口**

接口名称 api/v1/submit\_wallet\_info

请求方式：POST

请求示例

    {
        "device_id": "111",
        "wallet_uuid": "txlist",
        "chain": "eth",
        "symbol": "eth"
        "wallet_name": "aaa",
        "address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
        "contract_addr": "",
    }
    
    

参数解释

*   device\_id：设备ID
*   wallet\_uuid：钱包ID
*   chain：链名称
*   symbol：资产名称
*   wallet\_name：钱包名称
*   address：地址
*   contract\_addr：合约地址

返回示例

    {
        "status": true,
        "code": 2000,
        "message": "wallet success",
        "data": null
    }

**9. 批量提交地址接口 ：** 

api 名称:`api/v1/wallet/batch_submit_wallet `
请求方式: POST 
请求示例
 ``` 
{
    "batch_wallet": [
        {
            "device_id": "guosjtest001",
            "wallet_uuid": "guosjtest01",
			 "chain": "eth",
            "symbol": "eth",
            "wallet_name": "aaa",
            "address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
            "contract_addr": "guosjtest",
        },{
             "device_id": "guosjtest001",
            "wallet_uuid": "guosjtest01",
			 "chain": "eth",
            "symbol": "eth",
            "wallet_name": "aaa",
            "address": "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48",
            "contract_addr": "guosjtest",
        }
    ]
}
```
返回示例
``` 
{
    "status": true,
    "code": 2000,
    "msg": "wallet success",
    "data": null
}
```

**10. 获取钱包资产：** 

api 名称：`api/v1/wallet/get_wallet_asset`
请求方式: POST 
请求示例
 
```
{
    "device_id": "111"
}
```

 **返回示例**

``` 
{
    "status": true,
    "code": 2000,
    "msg": "wallet success",
    "data": {
        "coin_asset": [
            {
                "wallet_name": "aaa",
                "wallet_balance": [
                    {
                        "id": 1,
                        "balance": 2.4689,
                        "icon": "1",
                        "name": "ETH",
                        "usdt_price": 7563.302327,
                        "cny_price": 49019.26883
                    }
                ]
            }
        ],
        "total_asset": 7563.302327
    }
}
```
 **返回参数说明** 


**11. 搜索配置代币：** 

api 名称：`v1/token/sourch_add_token`
请求方式：POST 
请求示例
 
```
{
    "toke_name": "U"
}
```
 
**参数：** 

 **返回示例**

``` 
{
    "status": true,
    "code": 2000,
    "msg": "wallet success",
    "data": [
        {
            "id": 1,
            "asset_id": 1,
            "token_name": "USDT",
            "icon": "1",
            "token_symbol": "USDT",
            "contract_addr": "sourch_add_token",
            "decimal": 18
        }
    ]
}
```

 **返回参数说明** 


**12. 删除钱包接口 ：** 

接口名称:`api/v1/wallet/delete_wallet`
请求方式：POST 
请求示例
 ``` 
{
   "device_id": "919679BF-C185-4A7B-BB9A-AEF3A3167892",
   "wallet_uuid": "9xuw9gb8pi"
}
```

 **返回示例**

``` 
{
    "status": true,
    "code": 2000,
    "msg": "wallet success",
    "data": null
}
```
 **返回参数说明**



