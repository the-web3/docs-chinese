## MPC 钱包技术方案文档

### 一. 概述
 
MPC 是使用多方计算的方式各个节点产生密钥分片，各节点自行托管密钥分片，由于完整的密钥没有在整个网络中出现过，只要确保阀值节点的密钥分片不泄漏，钱包就是安全的。

MPC 私钥管理是目前比较流行私钥管理方案，该方至少需要三方参与才能完成，两方计算没有意义；参与的节点多一些相对比较安全一些，该方案的优势就是弱化私钥的概念，用户体验好，安全度高，缺点是参与方少的话安全度会低一些。


### 二. 架构设计

整个项目设计架构图如下：

![mpc-arc.png](https://github.com/savour-labs/savour-docs-chinese/blob/main/images/mpc-arc.png)

- APP 端发起 KeyGen 请求，并把自己的公钥给到 hailstone, hailstone 广播 PulicKey 给各节点，节点收到公钥之后 keygen
- keygen 完成之后，将公钥和私钥分片绑定，以供后面签名交易的时候验证签名
- APP 发起交易，hailstone 调度各节点签名，签名前先验签，验签通过之后，开始签名
- 节点签完名之后给到 hailstone，hailstone 将交易发送到区块链网络，并返回交易 Hash 给 APP 端

### 三. 实现细节

#### 1. keygen 流程图

![mpc-keygen.png](https://github.com/savour-labs/savour-docs-chinese/blob/main/images/mpc-keygen.png)


#### 2. sign 流程图

![mpc-sign.png](https://github.com/savour-labs/savour-docs-chinese/blob/main/images/mpc-sign.png)
