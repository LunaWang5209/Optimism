---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容

---

# ATON

1. 自我介绍--web3新人 我要找web3工作！！！！！！！！！

2. 你认为你会完成本次残酷学习吗？--absolutly

## Notes

<!-- Content_START -->

### 2025.01.06

======================================

**Optimism是什么？**

https://www.youtube.com/watch?v=fHkgFu3NLmY&ab_channel=Exodus

基于ETH网络的（Layer2）为降低gas提高效率产品

rollup 将多比交易一起处理为单笔eth交易。

ai大致了解一下

> ### Layer 2 扩容方案
>
> - **定义**：Layer 2 是指在以太坊主链（Layer 1）之上构建的第二层协议，用于处理交易和智能合约的执行，从而减轻 Layer 1 的负担。
> - **目的**：通过在 Layer 2 上进行大部分计算和存储，减少 Layer 1 的交易数量和复杂性，从而实现更高的吞吐量和更低的费用。
>
> ### Optimistic Rollups
>
> - **基本原理**：Optimistic Rollups 是一种 Layer 2 扩容技术，它假设交易是有效的，除非有人提出异议。交易数据和执行结果会被压缩并提交到 Layer 1，而具体的执行过程则在 Layer 2 上进行。
> - 优点
>   - **高吞吐量**：可以在 Layer 2 上处理大量交易，然后将结果批量提交到 Layer 1。
>   - **低交易费用**：由于大部分计算和存储在 Layer 2 上完成，Layer 1 的费用显著降低。
>   - **兼容性**：与以太坊的 EVM 兼容，允许现有的以太坊应用和智能合约在 Layer 2 上运行。
>
> ### Tokenomics
>
> - **OP 代币**：Optimism 的原生代币是 OP，用于激励网络参与者，如验证者和开发者。
> - **用途**：OP 代币可用于治理投票、参与网络的维护和奖励贡献者等。
>
> ### 阶段（Stages）
>
> - **介绍**：Optimism 的发展分为多个阶段，每个阶段代表了技术进步和生态系统的成熟度。
> - **目的**：通过分阶段的迭代，逐步完善 Optimistic Rollups 技术和生态系统，确保安全性和可靠性。

optimism是基于layer1的他是怎样的存在形式 一个智能合约吗？

> Optimism 不是一个单独的智能合约，而是由一组智能合约以及与以太坊主网交互的外部系统组成的。 
>
> 什么外部系统？
>
> 就是指类似于eth的链结构，及其代码中的组件：sequencer verifier state_sync bridgeInfrastructure client
>
> 可以直接和l1上的op相关合约交互来实现op链上的交互

rollup就是指op把他链上的交易做一个打包 然后糅合成一笔交易发送并保存在eth啊网络上吗？

> 是的，**Rollup**（尤其是 **Optimistic Rollup**，如 Optimism）就是指将 **Layer 2**（例如 Optimism）上的交易批量打包，合并成一笔交易，然后将这个交易或状态根提交到 **Layer 1（以太坊）** 网络上进行记录和验证。简而言之，Rollup 通过将多个交易“打包”来提高吞吐量，减少费用，同时仍然保持以太坊主网的安全性。

**主网怎么验证op数据包的正确性的**

> op发送状态根给主网上的智能合约，**这个状态根是 hash[旧状态根+新状态(合约/账户)]** 计算得到的。主网上合约可以验证op状态根的正确性，然后等待挑战期。过后主网上合约就会保存这个有效的状态根，从而保障op的数据可用性DA。主网账户不会保存op链上的具体账户数据。

**怎么发起挑战**

> 如果某个节点或用户认为状态根是错误的（例如通过不合法的交易或状态更新），他们可以在挑战期内 **发起挑战**。挑战需要提供 **欺诈证明**（Fraud Proof），这通常是一个证明，展示如何从当前的状态根回溯到一个不合法的状态或交易。
>
> 这个 **欺诈证明** 可能包括：
>
> - **Merkle Proof**：证明特定交易或账户状态变更是非法的。
> - **交易链**：通过一系列合法的或非法的交易链来展示如何从原状态根到新的状态根之间存在不一致。
>
> **挑战成功的奖励**：如果你成功挑战了不合法的状态根，通常会获得奖励。这可能包括 **ETH** 或其他原生代币，奖励的分配是为了激励节点或用户参与网络的安全验证。
>
> **恶意行为的惩罚**：如果一个节点被证明提交了非法的状态根，可能会受到 **经济惩罚**，例如，损失部分押金或被暂时或永久禁止参与网络操作。

### 2025.01.07

任务：

1. **Stage**
2. Tokenomic
3. **EIP4844**

#### stage

stage简单看来就是对于Rollup系统的一个评估体系。

那三阶段分别是什么？

> 第0阶段：作者自娱自乐级。我开发了一个rollup链，我要开源一个“挖矿软件”让别人也能共同维护链上（状态根）。
>
> 第1阶段：我把软件的功能转移到智能合约上，就比如说状态根的验证这个环节，不再是在各个节点本地验证了，转而用智能合约。同时保留了安全委员会维护bug。注意需要有完整的验证,欺诈证明,退出机制且不受安全委员会干扰。
>
> 第2阶段：rollup完全由合约控制，充足的推出时间（对于不想升级软件的节点），安全委员会仅解决链上裁决的正确性错误，用户免受治理攻击。

那op属于哪一个？

> stage1 https://www.tradingview.com/news/cointelegraph:124d04da9094b:0-optimism-reaches-stage-1-decentralization-implementing-fault-proofs/

#### tokenomic

**1. OP 代币的主要用途**

OP 代币在 Optimism 网络中的主要用途包括：

- **治理**：OP 代币持有者可以参与 Optimism 网络的治理。通过投票，社区成员可以决定关于网络升级、协议改进、资金分配等重要事项。
- **激励**：为了激励网络中的参与者，OP 代币会用于奖励验证节点、开发者和用户。
- **费用支付**：OP 代币用于支付网络中的交易费用。

**2. OP 代币的分配**

OP 代币的初始分配计划如下：

- **空投（Airdrop）**：OP 代币通过空投的方式分发给早期用户，旨在激励社区参与，并帮助更广泛的用户了解和使用 Optimism。
- **社区奖励**：一部分 OP 代币会分配给社区成员作为激励措施，激励他们参与 Optimism 的治理和网络安全等活动。
- **团队和合作伙伴**：一部分 OP 代币会分配给 Optimism 的创始团队、投资者和合作伙伴。
- **DAO资金池**：Opitmism 将建立一个去中心化自治组织（DAO），其资金池用于资助网络的持续发展和其他生态系统的支持。

**3. 治理机制**

Optimism 的治理机制是基于 **Optimism Collective**，这是一个由代币持有者和项目参与者共同治理的机制。具体治理过程如下：

- **OP 代币持有者**：通过持有 OP 代币，用户可以对提案进行投票，决策包括协议升级、资金分配、奖励机制等。

- 治理的两阶段流程

  ：

  - **意向阶段（Idea Phase）**：社区成员提出改进提案，并进行讨论。
  - **决策阶段（Decision Phase）**：最终的治理提案将在 DAO 里进行投票，所有 OP 持有者都有参与权。

**4. 经济激励**

OP 代币的经济激励设计包括：

- **L2 网络安全**：为了确保 Optimism 的安全，验证者和节点运营商需要提供质押的 OP 代币作为担保。任何恶意行为或欺诈行为将导致质押的 OP 代币被扣除。
- **奖励机制**：参与 Optimism 网络的开发者、社区成员、以及其他网络提供者将根据他们的贡献（如代码贡献、开发 dApp、参与治理等）获得 OP 代币奖励。

**5. 代币的通胀机制**

- 激励分配

  ：OP 代币的分配并非一次性完成，而是采取 

  逐步释放

   的方式，以确保代币的供应能根据网络的需求逐渐增加。激励措施包括：

  - 每年一定数量的 OP 代币会释放给参与网络治理、开发和维护的社区成员。
  - 部分 OP 代币将作为奖励发放给网络节点和安全参与者，确保网络的持续运作和安全。

**6. 长期目标和去中心化进程**

Optimism 希望通过以下措施逐步实现全面去中心化：

- **更多参与**：OP 代币的治理机制将逐步增强社区的参与度，确保更多的用户、开发者和节点有机会对网络进行治理。
- **去中心化开发**：随着网络的发展，更多的开发者和第三方应用将能够在 Optimism 上进行部署，进一步推动其生态系统的发展。
- **逐步减少中心化控制**：通过 DAO 机制，Optimism 将逐步减少对中心化控制的依赖，确保协议的完全去中心化。

**7. 持续发展与生态建设**

Optimism 还通过 **OP基金会** 和其他生态系统项目来推动生态建设。代币的激励和治理机制将鼓励更多的开发者参与到 **Optimism Rollup** 上，带来更多的应用场景和用户。



#### EIP4844

**blob不参与以太坊状态计算！ 用状态根代替**

简单说来就是引入Blob存储并降低其gas

**提高 Layer 2 扩展性**：减少通过以太坊主链传递数据的成本，尤其是 **Optimistic Rollups** 和 **ZK-Rollups**。

**降低交易费用**：通过引入新的交易格式，减少 Rollup 相关的交易费用，这将极大地影响到网络上交易的成本，特别是 Rollup 中的数据传输。

**为分片（Sharding）铺路**：为未来的以太坊 **分片机制**（即以太坊 2.0）做好准备，进一步提升网络的扩展性。



### 2025.01.08

任务：

1. GAS相关表述https://learnblockchain.cn/article/3703

EIP-4488: Transaction calldata gas cost reduction with total calldata limit

> - 用户的交易通过第二层（Layer 2）的“分组”进行汇总，并通过“calldata”发布到主网。该改进将使发布 calldata 到主网的成本降低，从而显著减少最终用户的气费。
> - ZK-rollup 比以太坊基础层便宜 40 到 100 倍，由于在多笔交易中分摊气费，交易费用已经降低了 3 到 8 倍。根据 Buterin 的说法，扩大数据区域将使“rollup 成本降低 5 倍”。

Gas

> zkSync = **链下部分（存储 + 证明者成本 验证snark）**+**链上部分（gas 成本 验证snark）**
>
> Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。 --EIP4488
>
> zkPorter = 链下成本
>
> ![image-20250108215836301](./.William-02-02.assets/image-20250108215836301.png)
>
> Arbitrum= ![26.png](./.William-02-02.assets/50.png)
>
> optimism= L2 执行费和 L1 数据/安全费。
>
> 
>
> L2s 是目前以太坊扩展的最佳解决方案，在提供高吞吐量和更便宜的费用的同时，可以很好的利用 L1s 的安全性。但由于Layer 2的扩容解决方案也在不断的更新和调整，每种方案都有其各自的优劣势，总体来说，zk rollup的交易费用更低、极限/部分TPS更快、最大拓展性也大大的得到提高以及在安全性上也有保证，zkporter次之；其他解决方案的交易费用也有所降低，但是同zk rollup相比略逊色。





### 2025.01.09

休息

1. 分片sharding withEIP4844

### 2025.01.10

![image-20250110221523916](./.William-02-02.assets/image-20250110221523916.png)

零知识证明的方案是怎样的

在不给对方展示A的情况下 证明自己有A

> 首先包含两个角色
>
> 1. 验证者 Verifier 接受证明并验证其正确性，而不需要知道证明的详细内容。
> 2. 证明者 Prover 持有秘密信息并生成证明。
>
> 目前存在的方案 **zk-SNARKs** 和 **zk-STARKs**
>
> zk-SNARKs 是一种非交互式的零知识证明，它允许证明者在没有与验证者交互的情况下生成证明。它的“简洁性”意味着证明的大小和验证的时间非常短。
>
> zk-STARKs 是 zk-SNARKs 的一种改进版本，它同样是零知识证明，但不依赖于可信设置，因此更加去中心化和安全。STARKs 证明相对于 SNARKs 来说更为 **可扩展** 和 **透明**。

分片和EIP4844

> **EIP-4844**（Proto-Danksharding）是以太坊在实现分片之前的过渡方案，它通过引入新的数据存储形式（Blob）来增加以太坊的吞吐量并降低交易费用。
>
> 区块链的分片相关的实现
>
> ![image-20250110224052958](./.William-02-02.assets/image-20250110224052958.png)

### 2025.01.12

zk整体架构: 见assets/https://www.aicoin.com/zh-Hant/article/279743

简单来说：L2提交零知识证明至L1对应contract

![image-20250112183357908](./.William-02-02.assets/image-20250112183357908.png)、

![image-20250112183546766](./.William-02-02.assets/image-20250112183546766.png)

​	zkSync zkPorter

1. **合约实现的详解** 



### 2025.01.13



<!-- Content_END -->
