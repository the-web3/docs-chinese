## MPC 钱包技术方案文档

### 一. 概述
 
MPC 是使用多方计算的方式各个节点产生密钥分片，各节点自行托管密钥分片，由于完整的密钥没有在整个网络中出现过，只要确保阀值节点的密钥分片不泄漏，钱包就是安全的。

### 二. 架构设计

整个项目设计架构图如下：

![mpc-arc.png](https://github.com/savour-labs/savour-docs-chinese/blob/main/images/mpc-arc.png)

### 三. 实现细节
