---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

timezone: Pacific/Honolulu # 夏威夷-阿留申标准时间 (UTC-10)

timezone: America/Anchorage # 阿拉斯加标准时间 (UTC-9)

timezone: America/Los_Angeles # 太平洋标准时间 (UTC-8)

timezone: America/Denver # 山地标准时间 (UTC-7)

timezone: America/Chicago # 中部标准时间 (UTC-6)

timezone: America/New_York # 东部标准时间 (UTC-5)

timezone: America/Halifax # 大西洋标准时间 (UTC-4)

timezone: America/St_Johns # 纽芬兰标准时间 (UTC-3:30)

timezone: America/Sao_Paulo # 巴西利亚时间 (UTC-3)

timezone: Atlantic/Azores # 亚速尔群岛时间 (UTC-1)

timezone: Europe/London # 格林威治标准时间 (UTC+0)

timezone: Europe/Berlin # 中欧标准时间 (UTC+1)

timezone: Europe/Helsinki # 东欧标准时间 (UTC+2)

timezone: Europe/Moscow # 莫斯科标准时间 (UTC+3)

timezone: Asia/Dubai # 海湾标准时间 (UTC+4)

timezone: Asia/Kolkata # 印度标准时间 (UTC+5:30)

timezone: Asia/Dhaka # 孟加拉国标准时间 (UTC+6)

timezone: Asia/Bangkok # 中南半岛时间 (UTC+7)

timezone: Asia/Shanghai # 中国标准时间 (UTC+8)

timezone: Asia/Tokyo # 日本标准时间 (UTC+9)

timezone: Australia/Sydney # 澳大利亚东部标准时间 (UTC+10)

timezone: Pacific/Auckland # 新西兰标准时间 (UTC+12)

---

# HeliosLz

1. 自我介绍：hi，大家好。我叫 Helios，希望可以深入了解 Optimism 方面的知识，加深自己对生态的理解程度。
2. 你认为你会完成本次残酷学习吗？Yes

## Notes

<!-- Content_START -->

### 2025.01.06

笔记内容

### 2025.01.07

**Optimism 简介**

Optimism 是以太坊的 Layer 2 扩容解决方案，基于 Optimistic Rollups 技术。它的目标是提高以太坊的可扩展性，同时保持其高度的安全性和去中心化特性。Optimism 通过在链下处理大量交易，减少网络拥堵，降低交易费用，从而增强 Ethereum 网络的性能。

工作原理

1.	Rollup 技术：
     * Optimism 使用 Rollup 技术，将交易数据批量提交到以太坊主链上进行验证。Rollup 本质上是将多个交易压缩成一个数据包，并将这个数据包发送到以太坊主链上。
     * 在 Optimistic Rollups 中，假设交易是有效的，只有在出现争议时才会进行检查。若没有问题，交易将在链上得到确认；如果有问题，其他用户可以提交挑战，智能合约会检查交易的有效性。

2.	Optimistic vs. ZK-Rollups：
    * Optimistic Rollups 和 ZK-Rollups 都是 Layer 2 解决方案，但它们的工作方式不同。ZK-Rollups 通过使用零知识证明（ZKPs）直接验证交易的正确性，而 Optimistic Rollups 假设交易是有效的，只有在质疑的情况下才需要进行验证，这种方式在性能上通常更高效。

3.	交易处理：
    * 在 Optimism 中，用户可以在 Layer 2 网络上进行低成本、快速的交易，所有交易的最终状态都会通过周期性的批量更新提交到以太坊主链。

4.	安全性：
    * 虽然大部分交易都在 Optimism 上处理，但所有的交易数据最终都提交到以太坊主链上，因此依然继承了以太坊的安全性。

如果有交易存在问题，可以通过“欺诈证明”机制发起挑战，确保数据的有效性。

**总结**

Optimism 是一种通过 Optimistic Rollups 技术扩展以太坊的 Layer 2 解决方案，能够大幅度提升交易吞吐量、降低交易成本，同时保持以太坊的安全性。它的设计使得现有的以太坊生态系统能够快速迁移到更加高效的环境中，满足更大规模的去中心化应用需求。


### 2025.01.08

**为什么会有 Mev 的产生，为什么 op 可以避免 Mev？**

MEV（最大化可提取价值，Maximum Extractable Value）产生的原因

MEV 指的是在区块链网络中，矿工（或验证者）可以通过重新排序、插入或删除交易，从中提取的额外价值。MEV 是一种通过控制区块中交易执行顺序的行为来获得的额外利润。其产生原因主要有以下几点：

1. 交易排序的可操控性：
* 在传统的区块链网络（如以太坊）中，矿工或验证者有权决定区块中交易的执行顺序。如果矿工或验证者能根据交易顺序进行优化（比如优先处理价格差异大的交易），就能从中获利。

2. 交易前的透明度：
* 以太坊和其他区块链的交易池（mempool）是公开的，矿工可以看到待处理的交易，并且可以预见到潜在的套利机会。例如，在去中心化交易所（DEX）上，可能存在由于订单簿顺序导致的价格滑点或闪电贷机会。

3.	套利机会和价格操控：
* MEV 的主要来源之一是 套利。例如，在不同的交易所之间，可能存在价格差异，矿工或验证者可以通过重新安排交易顺序或插入自有交易来利用这些差价，从中赚取差价利润。

4.	闪电贷攻击：
* 闪电贷可以使攻击者在没有任何初始资本的情况下借贷大量资金，然后利用这些资金进行价格操控或操纵市场，最后还款。通过操控交易顺序，攻击者可以从这些市场中提取价值。

**Optimism 如何避免 MEV**

Optimism 作为一个基于 Optimistic Rollups 的 Layer 2 扩容解决方案，它通过一些机制减少了 MEV 的问题。以下是 Optimism 如何减少 MEV 的几种方式：
	
1. 交易可预测性和透明性：
* Optimism 通过在 Layer 2 中处理大量的交易，并在最终提交至以太坊主链时进行批量确认，减少了交易池的操控空间。在 Optimism 中，交易的顺序和执行通常更加可预测，因为它们是批量提交和处理的，这减少了矿工通过操控交易顺序来提取 MEV 的机会。

2. 交易提交顺序和竞争降低：
* 在 Optimism 中，交易的排序和执行通常由 Rollup 的协议控制，而不是由单个矿工或验证者决定。这减少了矿工之间为了操控交易顺序而进行的竞争，也降低了 MEV 的产生空间。

3. 费用的分配机制：
* Optimism 采用了一种更加透明的费用分配模型，其中 gas费 和奖励等机制的调整可以减少对矿工优先排序交易的动力。通过减少矿工基于 MEV 动机的收益，降低了 MEV 的诱因。

4. 透明的验证和争议处理：
* Optimistic Rollups 的核心特性之一是争议解决机制。如果某个交易被质疑有效性，网络会进行验证并采取相应措施，这样的机制减少了通过恶意操作获得 MEV 的机会。

5.	在主链和子链的分离：
* Optimism 将交易和数据处理的负载转移到 Layer 2，并通过最终提交批量处理到以太坊主链上。这种分离的机制减少了 Layer 1 上的矿工可以控制和操纵的交易数据，从而减少了 MEV 产生的空间。

**总结**

MEV 是因为区块链中矿工或验证者可以操控交易顺序，从中提取额外的价值。它的主要原因是交易排序的可操控性、交易池的透明性和市场中的套利机会。而 Optimism 通过批量处理交易、减少交易顺序的可操控性、采用更加透明的费用机制和争议解决机制，来减少矿工或验证者通过操控交易获取 MEV 的机会。

### 2025.01.09

### 2025.01.10

### 2025.01.11

### 2025.01.12

### 2025.01.13

### 2025.01.14

### 2025.01.15

### 2025.01.16

### 2025.01.17

### 2025.01.18

### 2025.01.19

### 2025.01.20

### 2025.01.21

### 2025.01.22

### 2025.01.23

### 2025.01.24

### 2025.01.25

### 2025.01.26

<!-- Content_END -->
