### 1. 公钥导出地址
```
def public_to_address(puk)
   s = hashlib.new("sha256", pubkey).digest()
   r = hashlib.new("ripemd160", s).digest()
   bits = bech32.convertbits(r, 8, 5)
   return bech32.bech32_encode("cosmos", bits)
```

### 2. 地址的合法性校验
```
def validat_address(address):
  return re.match('^cosmos[A-Za-z0-9]{39}', address)
```

### 3. 手续费相关的
```
fees = gas * gas-prices
https://docs.cosmos.network/master/basics/gas-fees.html#gas-and-fees 
```

### 3. 获取账户信息和账户余额

```
def get_account_number_sequence_balance(self, address: str):
   url = 'https://api.cosmos.network/auth/accounts/' + address
   resp = requests.get(url, timeout=10)
   value = resp.json()['result']['value']
   return int(value['account_number']), int(value['sequence']), value['coins']    
```

### 4. 广播交易到区块链网络

```
def send_tx(tx:str):
    url = 'https://api.cosmos.network/txs'
    headers = {'content-type': "application/json"}
    resp = requests.post(url, tx, headers, timeout=10)
    r = resp.json()
    return r
```


### 5. 获取地址相关的交易
```
def get_tx_by_address(txid:str) -> Optional[Dict[str, Any]]:
   use explore api 
```


### 6. 根据txid查询相关的交易信息
```
def get_tx_by_hash(hash:str) -> Optional[Dict[str, Any]]:
   url = 'https://api.cosmos.network/txs/' + hash
   resp = requests.get(url, timeout=15)
   return resp.json()
```


      
