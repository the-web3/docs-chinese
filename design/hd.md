# SavourDao HD 钱包模块设计文档

## 一. HD 钱包模块会涉及到以下这些功能

- 助记词生成
- 验证助记词
- 导出助记词
- 导出私钥
- 导入助记词
- 导入私钥，
- ETH系列导出导入 Keystore
- Eos 系列账户激活
- 获取账户余额
- 离线签名转账
- 查看交易记录

### 1. **生成助记词和验证助记词**

![1.svg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2e12bf1d-7b44-44c0-be2c-a88e52523614/1.svg)

### 2**. 导出助记词和私钥**

![2.svg](https://github.com/SavourDao/docs/blob/main/images/1.svg)

### **3. 导入助记词和私钥**

![3.svg](https://github.com/SavourDao/docs/blob/main/images/2.svg)

### 4.**转账背后的秘密**

![4.svg](https://github.com/SavourDao/docs/blob/main/images/3.svg)

### 5.**查看余额和交易记录**

![5.svg](https://github.com/SavourDao/docs/blob/main/images/4.svg)

## 二. **行情模块**

行情模块一般是一个行情聚合器，会有主流的中心化交易所和主流的去中心化化交易的行情

![11.svg](https://github.com/SavourDao/docs/blob/main/images/5.svg)

### 1.行情模块业务流程图

![22.svg](https://github.com/SavourDao/docs/blob/main/images/6.svg)

## 三. 新闻资讯模块

     这个比较简单，这里不再做叙述，主要是为了丰富钱包的功能，提供一些行业新闻和行业动态的文章或者快讯。

## 四. **Dapp 浏览器**

![33.svg](https://github.com/SavourDao/docs/blob/main/images/7.svg)

以上是我们 Q3 要实现的功能，币种接入 BTC，ETH，BSC，Polygon， EOS 和 Solanan。
