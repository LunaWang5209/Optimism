---
timezone: Asia/Shanghai
---


# Ye

1. 自我介绍
     - 清华-南加大 Communication Data Science 25'硕士在读，链上数据分析2年经验，Dune [@wyeeeh](https://dune.com/wyeeeh)，X [@wyeeeeh](https://x.com/wyeeeh)，Optimism NumbaNERDs 分析师，入选Optimism RetroPGF Round 3 & Round 6 头部贡献者。

2. 你认为你会完成本次残酷学习吗？
   - 有激励就有野心，之前完成过Sixdegree Lab和BuidlerDAO发起的Dune Analytics共学计划，以及DeFiHackLabs发起的Solidity残酷共学计划。

## Notes

<!-- Content_START -->

### 2025.01.06
#### Layer2 扩容方案
在 Bedrock 中，Layer2区块通过非合约地址以压缩格式写入L1区块链 (Ethereum)上，以减少Layer1的 gas 费用。这
种方式确保了 OP Mainnet 继承了 Ethereum 的可用性和完整性保证。
##### Optimistic Rollups
- Optimistic Rollups 使用它们的父链（如 Ethereum）的共识机制（如PoS），而不是自己提供共识机制。
- 在 Optimistic Rollup 中，状态承诺被发布到 L1（在 OP Mainnet 的情况下是 Ethereum）而不提供直接的有效性证明。这些承诺在“挑战窗口”期间被视为待定状态。如果在挑战窗口期间无人挑战状态承诺，则视为最终确定。当状态承诺被挑战时，可以通过“故障证明”过程使其无效。成功的挑战不会回滚 OP Mainnet 本身，只会移除有关链状态的发布承诺。

##### 区块
Optimism 的区块生产主要由单一的“排序器 (sequencer)”管理，负责提供交易确认、状态更新、构建和执行 L2 区块以及将用户交易提交到 L1。为了避免 MEV，Bedrock 中的排序器拥有一个私有的 mempool。OP Mainnet 每两秒产生一个区块，无论区块是否包含交易。

执行引擎（op-geth 组件）通过两种机制接收区块：
- **通过Layer 2 内部的P2P网络同步状态。** 执行引擎（op-geth 组件）通过点对点（P2P）网络与其他在同一 Layer 2 网络上的执行引擎进行通信和数据同步。
- **通过rollup 节点（op-node 组件）实现，从 L1 派生 L2 区块。** 这种方法相比于直接的 P2P 网络同步会慢一些，因为它需要等待 L1 区块的确认，并且处理从 L1 到 L2 的映射逻辑。然而，这种方法能抗审查。由于 L2 区块的生成是基于已经公开且被广泛认可的 L1 数据，这就使得任何试图对 L2 数据进行审查或篡改的行为都会被发现并受到阻止。可以把这种机制比喻为通过官方渠道获取信息，虽然可能不是最快的，但却是最可靠和最不容易被篡改的。

##### Bridge
Optimism 允许用户在 L2（如 OP Mainnet）和底层 L1（如 Ethereum mainnet）之间的智能合约发送任意消息，从而实现 ETH 或代币（包括 ERC20 代币）的转移。标准桥（Standard bridge）使用这一功能，允许用户从 Ethereum 存入代币到 OP Mainnet，并允许从 OP Mainnet 提取代币回 Ethereum。

- **从 Ethereum 到 OP Mainnet**: 称为存款(deposit)，通过使用 L1CrossDomainMessenger 或 L1StandardBridge 完成，成为对应 L1 区块的第一个 L2 区块的一部分。

- **从 OP Mainnet 到 Ethereum**: 称为提款(withdrawl)，分为三个阶段：初始化提款 L2 交易、等待下一个输出根提交到 L1 并提交提款证明、以及在故障挑战期结束后完成提款。


### 2025.01.07

<!-- Content_END -->
