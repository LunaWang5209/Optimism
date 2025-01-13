---
timezone: Asia/Shanghai
---


---

# {Marcus-Chen}

1. 我是一个汽车行业的研究员，之前做过一段时间的投资研究工作，现在转到汽车行业做战略咨询，一直想了解web3的试解

2. 我希望每天下班后花1-2个小时，完成这次学习，也让自己养成学习知识的习惯，希望能完成

## Notes

<!-- Content_START -->

### 2025.01.06
**OP是什么**
首先OP rullup是一种乐观汇总，是以太坊的 Layer 2 扩展解决方案，旨在提高交易吞吐量并降低费用。其核心思想是将大量交易在链下执行，然后将交易数据打包提交到以太坊主链。
默认情况下，这些交易被视为有效，只有在有人提出质疑时，才会通过欺诈证明机制进行验证，挑战期（通常为 7天），成功的挑战不会回滚 OP 主网本身，只会回滚已发布的关于链状态的承诺。 交易顺序和 OP 主网的状态因防故障质询而保持不变。
（当然还有一种验证方式是Zero-Knowledge Proof，会将多笔交易打包在一起，并发布到 Layer 1 区块链上，同时还会发布一个验证计算有效性的证明）
**单轮交互**
OP是单轮交互的，发布数据的一方只在遭遇质疑会和挑战者进行一次证明交互，减少了大量交互带来的成本，而**Arbitrum**是*多轮交互*的，通过反复交互验证缩小争议范围能够更好地支持复杂的智能合约，并提高系统的安全性

### 2025.01.07
OP网络的核心参与者：

Users（用户）：
指普通的用户或应用开发者，他们与 Layer 2 (L2) 网络交互。
用户可以：
提交交易到 Sequencers（排序者）。
通过 Layer 1 (Ethereum L1) 进行存款或取款操作。

Sequencers（排序者）：
负责接收用户提交的交易并对交易进行排序。
他们的职责包括：
接收交易并生成 L2 区块。
提交交易批次到 Ethereum L1 以获得最终性。
实时向网络广播交易的更新。

Verifiers（验证者）：
主要作用是验证 Sequencers 提交的输出结果。
他们会：
从 Ethereum L1 获取交易批次或存款数据。
验证输出提案是否正确，并在必要时发起挑战

**不同Layer2扩容方案运行环境与技术对比：**
- Ethereum (Layer 1)：作为基准环境，不使用任何扩容技术。
- ZK Rollup：采用零知识证明技术，交易验证快速，但计算成本较高。
- ZK Porter：结合 ZK Rollup 和 Validium 技术，将部分数据存储在链下，提高扩展性。
- Optimism：采用 Optimistic Rollup 技术，假设交易有效，仅在必要时进行欺诈证明。
- Arbitrum：同样基于 Optimistic Rollup，但使用多轮欺诈证明，适合复杂智能合约。
- AnyTrust：基于 Plasma 和 zkport 技术，更适合对数据隐私有更高需求的场景。

### 2025.01.08
**OP Stack** 是一组标准化的组件和工具，开发者可以用它来搭建自己的区块链或扩容方案
OP Stack 的结构可以分为多个模块，以下是一些核心组件：

Execution Layer（执行层）：
负责运行智能合约和处理交易。
类似以太坊的 EVM（以太坊虚拟机），OP Stack 支持与 EVM 完全兼容的操作。

Consensus Layer（共识层）：
确定交易的顺序和确认。
在 Optimism 中，Sequencer 是负责排序交易的核心角色。→Sequencer（*时间顺序、GAS费用优先、批次优化*）定期将已排序和打包的交易批次提交到以太坊（Layer 1），确认交易（提交内容为（*1交易批次数据*、*2状态根*））

Settlement Layer（结算层）：
管理与 Layer 1 的交互，例如提交批次交易和欺诈证明。
提供了跨 Layer 2 和 Layer 1 的安全保障。

Data Availability Layer（数据可用性层）：
记录交易数据并确保所有验证者都能访问。
OP Stack 目前依赖以太坊的 Layer 1 提供数据可用性

**L1 Smart Contract**

1、L1StandardBridge：
- 提供标准的资产桥接功能（ERC20、ETH 等），负责管理资产的存款和提款。
- 支持发送和接收跨层消息。

2、L1ERC721Bridge：
- 类似于 L1StandardBridge，但专门用于 NFT 的桥接。
- 允许用户将 NFT 存入或提取到 Layer 1 或 Layer 2。

3、L1CrossDomainMessenger：
- 负责 Layer 1 和 Layer 2 之间的消息传递。
- 确保不同层之间的信息是同步的，例如交易完成或存款成功。

4、OptimismPortal：
- 是系统的入口和核心交互点。
- 提供了状态查询、提案验证等功能，同时支持暂停/恢复系统操作。

5、DisputeGameFactory：
- 用于生成和管理争议游戏（Dispute Game）。
- 挑战者可以通过此模块验证 Layer 2 的状态根是否正确。

6、FaultDisputeGame：
- 管理具体的争议实例，用于防止 Layer 2 的欺诈状态被提交。

7、SuperchainConfig 和 SystemConfig：
- 配置整个系统的参数，例如区块时间、Gas 费用等。

8、AnchorStateRegistry：
- 用于存储和更新锚定状态（Anchor States），确保 Layer 1 和 Layer 2 的状态一致。

9、DelayedWETH：
- 管理延迟提款的 WETH，可能是为了增加额外的安全性或优化流程。

10、BatchInbox Address：
- 存储已提交的交易批次，用于 Layer 1 的验证和管理

**举例：从用户交互到争议解决的全流程--以ERC20代币为例**

*Step 1: 用户发起存款*

- 用户通过钱包向 Layer 1 的 L1StandardBridge 发起存款请求。
- 资产锁定：ERC20 代币在 L1 被锁定，并通过 L1StandardBridge 通知 Layer 2。

*Step 2: L1 向 Layer 2 通知*

- L1CrossDomainMessenger 接收存款事件，将消息传递给 Layer 2。
- Layer 2 的 Sequencer（排序器）根据存款事件更新 Layer 2 的状态，为用户创建等量的 Layer 2 代币。

*Step 3: 用户在 Layer 2 中发起交易*

- 用户使用 Layer 2 的资产进行交易。
- Layer 2 的 Sequencer 收集这些交易，并生成一个批次。

*Step 4: Batcher 打包交易*

- Batcher 将 Layer 2 的交易批次发送到 Layer 1，通过 Batch Inbox Address 存储。
- 作用：这些批次被作为 Layer 2 状态的证据存储在 Layer 1。

*Step 5: 验证或争议*
- 如果验证者认为提交的交易批次或状态根有错误，他们可以通过 DisputeGameFactory 发起争议。

*争议解决：*
- FaultDisputeGame 启动验证流程。
- 如果确认错误，系统将回滚状态并惩罚提交错误状态的角色。

*Step 6: 系统安全管理*
- 如果出现重大异常，Guardian 可以通过 OptimismPortal 暂停系统操作，防止进一步损害。

**资产操作（存款/提现）** 通过 **L1 Bridge**模块完成。

**交易批次管理** 通过 **Batcher 和 Batch Inbox Address**实现。

**跨层通信** 依靠 **L1CrossDomainMessenger**。

**争议解决** 由 **FaultDisputeGame** 保障系统安全性。

**系统安全** 由 **Guardian** 提供紧急保护

### 2025.01.09

**Stage 0: Minimal Trust Assumptions（最小信任假设）**

- Rollup 的安全性主要依赖 Layer 1（例如以太坊）的保障，但仍需要信任某些中心化的角色。
- Sequencer（排序者）是中心化的，通常由单个实体控制。
- 数据可用性完全依赖于 Layer 1。

**Stage 1: Permissionless Validators（无许可验证者）**

- 任何人都可以成为验证者，验证 Rollup 的交易和状态。
- 通过引入争议解决机制（Fault Proof 或 Validity Proof）来确保数据的正确性。*验证者的加入无须许可，任何人都可以运行验证节点*
- 数据验证和存储依然依赖 Layer 1。
- 
**Stage 2: Full Decentralization（完全去中心化）**

- Rollup 实现完全去中心化，Sequencer、验证者、数据存储都无需信任中心化实体。
- Layer 2 生态具备独立性，最大化保障用户和开发者的权益。
- *Sequencer 去中心化：允许多个 Sequencer 并行运行，解决单点故障问题。多个 Sequencer 通过共识机制协作排序交易。*

**Optimism 当前所处阶段：Stage 0，Optimism 正在开发去中心化 Sequencer 和无许可验证机制，目标是逐步向 Stage 1 和 Stage 2 过渡。**
**zkSync 已逐步接近 Stage 1，其 Validity Proof 系统允许无许可验证**
**目前没有任何 Rollup 达到 Stage 2**

**Rollup 如何依赖 Layer 1：**
- Rollup 使用 Layer 1 作为最终的裁判。所有状态更新（如余额变化）都必须通过 Layer 1 的验证机制来确认。·
- 如果 Rollup 层有任何问题（如 Sequencer 恶意操作），用户可以通过 Layer 1 上的数据恢复状态·

**当前大多数 Rollup（如 Optimism 和 Arbitrum）使用单个中心化的 Sequencer。通常由一个公司或组织运行（例如 Optimism 的 Sequencer 是由 Optimism Foundation 控制的）。**

**stage 0存在问题**
- 验证交易和状态的机制（如Fault Proof）是由中心化团队维护，普通用户无法直接参与验证
- Rollup 的治理（如升级智能合约或修改 Sequencer 配置）可能需要中心化团队进行人工操作，*但仍需要信任团队不会滥用权限。*

### 2025.01.10

**治理理念旨在创建一个由社区、公司和公民共同参与的数字民主治理模式，称为 Optimism Collective**，**核心理念是Impact = Profit**

**Optimism 采用双院制治理体系（Token House + Citizens' House）**
- Token House：负责提交、讨论和投票各类治理提案。代币持有者可以直接投票，或将投票权委托给他人。
- Citizens' House：基于声誉的“一人一票”治理实验。 负责追溯性公共产品资金（Retroactive Public Goods Funding，简称 Retro Funding）。该机制旨在奖励那些对集体和超级链（Superchain）产生积极影响的贡献者。


### 2025.01.11

### 2025.01.12

**根据不同的提案类型确定不同的投票机制和否决机制**

### 2025.02.07

笔记内容

### 2024.07.12

<!-- Content_END -->
