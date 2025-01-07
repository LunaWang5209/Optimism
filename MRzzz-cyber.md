---
timezone: Asia/Shanghai
---


# MRzzz-cyber

1. 自我介绍
我是 Marcus，LXDAO，OP 中文力量成员，我想通过这场学习，更系统的了解 Optimism 以及 Layer2 生态


2. 你认为你会完成本次残酷学习吗？
会完成，通过学习更深入的了解 Optimism

## Notes

<!-- Content_START -->

### 2025.01.06

### 什么是 Optimism？

基本介绍:Optimism 是一个利用 optimistic rollup 技术的的以太坊 L2 解决方案，目的是解决以太坊吞吐量不高，交易成本过高的问题，同时又保证了安全性和去中心化

区块链不可能三角：在区块链不可能三角中，去中心化，安全性和高 TPS，是不可能三角，以太坊足够安全，也具有去中心化，但是牺牲了吞吐量，而 Optimism 牺牲了哪方面，从而解决了以太坊的问题呢，在我看来是牺牲了一部分的去中心化，以为 Optimism 的共识层是基于以太坊的，其实是略微牺牲了一部分去中心化，但是保证了足够高的吞吐量

大规模应用：同时，Layer2 被认为是以太坊大规模应用的重要一步，没有人会因为一次交互而负担超过 10 刀甚至 100 刀以上的 Gas 费，在通过 EIP 4844 之后，Optimism 上交互一次的成本已经达到了小于 0.01 美金，在未来，大规模应用应该会逐渐爆发

Optimism 采取了 Optimistic rollup 的机制

Rollup 概念：将大量交易数据“打包”并压缩后提交到以太坊主网（Layer 1）(以太坊计算是一笔交易都多节点一起同步，Rollup 类似是把一笔交易里面打包多笔交易，提交给以太坊主网)
“Optimistic”设计：默认假设所有交易都是有效的，只有在有人提出争议时才进行验证。这种设计减少了计算量，提升了效率。（7 天验证有效期这个其实我目前还有一些问题，如何保证一些最基础的诚实节点，或者说如何从利益设计上解决这些问题，我看到了故障证明的设计，明天学习故障证明）

以太坊兼容性

EVM 等效性：Optimism 100% 兼容以太坊虚拟机（EVM），支持以太坊上的所有智能合约和工具。
开发者友好：开发者可以将现有的以太坊应用无缝迁移到 Optimism，无需重新编写代码。

安全性

所有数据都存储在以太坊主网，确保数据的完整性和可用性。
使用欺诈证明（Fraud Proof）机制检测并惩罚恶意行为。

经济性

大幅降低交易费用，通常比以太坊主网便宜 10-100 倍（通过 EIP 4844 之后，这个应该是便宜 1000 倍了）
通过高效的 Rollup 压缩技术，优化了存储和 gas 使用。




### Optimistic rollups 的演变历史
Layer2 的存在是是为了解决以太坊吞吐量不大的问题，以太坊目前的处理速度限制在每秒约 15-20 笔交易，这降低了短期内扩展以处理更多用户的可能性。这个问题存在的主要原因是以太坊的共识机制需要许多对等节点来验证区块链状态的每次更新
而这是很难满足大规模应用的，在之前，
在 Optimistic rollups 之前，有一个 Plsma 的扩容方案，Plsma 的扩容方案在 Optimistic rollups 推出之前，一直都是以太坊的重要扩容方案，Polygon 之前也是沿用 plsma 的设计

Plasma 是一种链下扩展方案，利用子链（或称 Plasma 链）处理大部分交易，同时仅将必要的信息提交到以太坊主网。

工作原理
子链结构：Plasma 链是独立的区块链，定期将“状态摘要”提交到以太坊主网。
安全性依赖主网：通过以太坊主网的共识机制和数据可用性，确保 Plasma 子链的安全性。
交易处理：用户在 Plasma 子链上进行交易，只有在需要结算或争议时才回到主网。
退出机制：用户通过“挑战期”（Challenge Period）来确保资金安全，避免恶意行为。

优点
高吞吐量：交易大部分在子链完成，主网压力小。
成本低：相比主网，子链上的交易费用更低。

缺点
数据可用性问题：如果子链运营者恶意，可能导致数据丢失。
通用性低：Plasma 更适合简单支付和转账，不擅长复杂智能合约。
用户体验不佳：退出主网时需要等待挑战期，可能长达数天。


![image](https://github.com/user-attachments/assets/e86821bd-6509-464a-8df9-9cf48604ddcf)

Plasma 上并不能跑 Uniswap，为了解决这个问题，Plasma Group 推出了 Optimistic rollups

由于 Plasma 子链 (Child Chain) 架构的一大缺点，就是在 L2 和 L1 层之间转移资金的耗时很长，有时用户甚至需要等上 1 周之久。这也使得像 Uniswap 这样的通用型智能合约无法运用在 Plasma 上。尽管 Ben 带领技术团队做了很多尝试，但「跑 Uniswap」的问题始终没有被解决。

就这样，Plasma Group 被自己亲手培养出的独角兽给难住了，Plasma 这个曾经被视为以太坊扩容「EndGame」的方案，也似乎走进了技术死胡同。现在，Plasma Group 的三位「扩容性先驱」必须找出新的解决方案。

Optimistic rollups 的论文来源是 Vitalik 2014 年发布的一篇论文，里面提到了 Shadow chain 的概念（有点类似于比特币的闪电网络），从而推出了 Optimistic Rollup

Optimistic Rollup 借鉴了 Plasma 的设计，但牺牲了其几乎无限的扩容性，以运行被叫做 OVM (Optimistic Virtual Machine) 的 EVM 兼容虚拟机，这也使 Optimistic Rollup 能够运行以太坊上能够运行的所有应用。

这一次，团队总算解决了 Plasma 面对的终极问题——OR 可以跑 Uniswap 了！


工作原理

Rollup 机制：Optimism Rollups 将交易数据和状态变化压缩后提交到以太坊主网，同时借助欺诈证明（Fraud Proof）来确保状态的正确性。
数据可用性：所有交易数据都会发布到以太坊主网，确保完整的数据可用性。
兼容性：与以太坊的 EVM（以太坊虚拟机）完全兼容，因此支持所有以太坊智能合约和工具。

优点

高通用性：可以运行复杂的智能合约。
安全性强：所有数据都存储在以太坊主网，保证数据可用性。
用户体验较好：相比 Plasma，退出时间短（通常几分钟到几小时）。

缺点

成本较高：由于 Rollup 仍需要将所有数据提交到主网，成本比 Plasma 高。
欺诈证明延迟：在极端情况下，欺诈证明可能需要一定时间。


### Next Step
1. 研究一下故障证明
2. 研究一下 Plasma 的实现原理，以及和 Optimistic rollups 的更进一步的区别
3. 精读一下 Vitalik 2014 年的文章：https://blog.ethereum.org/2014/09/17/scalability-part-1-building-top


### Reference
https://blog.ethereum.org/2014/09/17/scalability-part-1-building-top (Vitalik: Shadow Chain)

https://foresightnews.pro/article/detail/5893 (Optimisic rollup 成长史)

https://ethereum.org/en/developers/docs/scaling/plasma/

https://ethereum.org/en/developers/docs/scaling/optimistic-rollups/


### 2025.01.07

<!-- Content_END -->
