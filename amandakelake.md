---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Asia/Shanghai

---

# amandakelake

1. 自我介绍

大家好，我是LGC，对OP比较感兴趣，希望通过这次共学，理解和认识 Optimism 的生态和相关信息知识，加深对 layer2 的理解

2. 你认为你会完成本次残酷学习吗？

会的！

## Notes

<!-- Content_START -->

### 2025.01.06

#### Layer2

##### layer2基础概念
[What is layer 2?](https://ethereum.org/zh/layer-2/learn/)
区块链有三个理想属性：decentralized、secure、scalable （三元悖论）

==The main goal of scalability is to increase transaction speed (faster finality), and transaction throughput (high transactions per second), without sacrificing decentralization or security==

以太坊当前面临的问题：低吞吐量（每秒15~30笔交易）、高gas费用、用户体验差。Layer2 的目标是通过将交易从主链转移到 Layer2 网络来解决这些问题

[What is layer 2?](https://ethereum.org/zh/layer-2/learn/)
https://vitalik.eth.limo/general/2021/01/05/rollup.html Vitalik 详细解释了 Rollup 技术，包括 Optimistic Rollup 和 ZK-Rollup 的区别

##### L2技术类型

* rollup
    * Optimistic rollups：乐观汇总，使用欺诈证明
    * ZK rollups：使用有效性证明
* state channels （状态通道）
* plasma

#### **OP Stack Overview**

[Vision - Optimism Official Blog](https://optimism.io/vision)
[Getting started with the OP Stack](https://docs.optimism.io/stack/getting-started)

The OP Stack is development stack thats powers Optimism，as Optimism evolves，so will the OP Stack.

Optimism Bedrock is the current iteration of the OP Stack.

The OP Stack of today was built to support [the Optimism Superchain](https://docs.optimism.io/superchain/superchain-explainer) (a proposed network of L2s)

##### OP Rollup
[OP Rollup 扩容方案](https://docs.optimism.io/stack/rollup/overview)

* 区块存储：L2 区块保存到以太坊区块链中的一个非合约地址中`0xff00000000000000000000000000000000000010`，借此来降低L1 gas费用
    * 区块是EIP-4844 blob 提交，无法修改或审查，这就是 OP Mainnet 继承以太坊的可用性和完整性保证的方式
* 区块生产：由`sequencer`单一管理
* **Fault proofs** （故障证明）：challenge window持续7天

### 2025.01.07

#### Layer2 解决方案对比

由于以太坊网络拥堵导致 gas fee 大幅上涨（每秒 15～30 笔交易），Layer2 的解决方案目前主要聚焦在解决网络面临的低效率问题，同时仍能保持以太坊区块链的完整性

目前主要有四种技术方案：Optimistic Rollup、ZK Rollup、Plasma、Validium

* ZK Rollup 和 Optimistic Rollup 都是将交易数据压缩后存储在主链上，通过主链验证交易的有效性，从而实现扩容
* Plasma 和 Validium 则是将交易数据存储在链下，通过主链验证交易的有效性，从而实现扩容

普通转账 ETH 需要字节数 112 左右，ZK 压缩为 12个字节，OP 系压缩为 78.4 左右

#### Gas 费用

* ZK Sync 每笔交易的成本由 2 个部分组成
    * 链下部分（存储+证明者成本）：状态存储和 SNARK（零知识证明）生成的成本（这部分依赖于硬件资源的使用，因此是不变的。我们的基准估计每次转账约为 0.001 美元。）
    * 链上部分（GAS 成本）：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态（链上部分是一个变量，取决于以太坊网络中当前的 gas 价格。但是，这部分比普通 ETH/ERC20 转账的成本要便宜几个数量级。）

* Optimistic Rollup 每笔交易的成本由L2 执行费和L1 数据费组成
    * L2 执行费：每笔 L2 交易都会支付一定的 执行费用 （等同于以太坊的收费方式）
    * L1 数据费：Optimism 上的所有交易也都发布到以太坊，此步骤对于 Optimism 的安全属性至关重要，因为这意味着同步 Optimism 节点所需的所有数据始终在以太坊上公开可用（受以太坊当前的gas价格影响）

[一文了解Layer2的四大解决方案交易成本对比](https://learnblockchain.cn/article/3703#4、optimism%20Gas%20机制)

<!-- Content_END -->
