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

### 2024.07.12

<!-- Content_END -->
