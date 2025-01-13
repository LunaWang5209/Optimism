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




### 2025.01.07
##### Bridge
Optimism 允许用户在 L2（如 OP Mainnet）和底层 L1（如 Ethereum mainnet）之间的智能合约发送任意消息，从而实现 ETH 或代币（包括 ERC20 代币）的转移。标准桥（Standard bridge）使用这一功能，允许用户从 Ethereum 存入代币到 OP Mainnet，并允许从 OP Mainnet 提取代币回 Ethereum。

- **从 Ethereum 到 OP Mainnet**: 称为存款(deposit)，通过使用 L1CrossDomainMessenger 或 L1StandardBridge 完成，成为对应 L1 区块的第一个 L2 区块的一部分。

- **从 OP Mainnet 到 Ethereum**: 称为提款(withdrawl)，分为三个阶段：初始化提款 L2 交易、等待下一个输出根提交到 L1 并提交提款证明、以及在故障挑战期结束后完成提款。


### 2025.01.08
#### Layer2的解决方案交易成本对比

- **为什么要L2？更快、更便宜**
   普通转账eth需要字节数112左右，ZK压缩为12个字节，op系压缩为78.4（不固定，假设压缩了30%的空间），假设swap转账需要字节数约180左右，ZK压缩为14个字节，op系压缩为126个字节。
- 目前主要有四种技术方案：**Optimistic Rollup、ZK Rollup、Plasma、Validium。**

##### Optimistic Rollup
**交易成本**
- L2 执行费：每笔 L2 交易都会支付一定的执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。
   - `l2_execution_fee = transaction_gas_price * l2_gas_used`
- L1 数据/安全费：Optimism 上的用户必须支付向以太坊提交交易的费用，称之为L1 数据费用
   - `L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead`

##### ZK Rollup
**交易成本**
在zkSync 中，每笔交易的成本有两个组成部分：
- 链下部分（存储 + 证明者成本）：状态存储和 SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。
- 链上部分（gas 成本）：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态。

**影响地板价的因素**
Rollup的交易地板价依赖于 ETH 主网 calldata 的费用。

**无气体转账**
用户可以直接用被转账的代币中支付交易费用（如DAI）而无需使用原生Token支付

### 2025.01.09
#### Layer2扩容方案对比

##### Rollup
**ZK Rollup**
zk-Rollups 是一种基于零知识证明的二层扩容方案。首先由 Rollup Operator 组件将多个链下交易聚合成一个批次，之后使用零知识证明（例如 zk-SNARKs 或 zk-STARKs）生成一个简洁的证明文件，这个证明可以验证整个批次的交易的有效性，而不需要逐一检查每笔交易；然后将证明及与该批次相关的数据提交到主链，主链通过验证证明的正确性，确保交易是有效的；主链验证通过后，链上合约会根据证明中的数据更新链上的状态。这意味着，尽管交易是在链下进行的，但链上状态仍然得到了更新，确保了数据的一致性。
- 零知识证明（Zero-Knowledge Proof，简称 ZKP）是一种密码学概念，它允许一个证明者向验证者证明某个陈述为真，而无需透露任何关于该陈述的其他信息。简而言之，零知识证明可以让一个人证明他拥有某种信息，而不需要透露这个信息本身。


**OP Rollup**
Optimistic Rollups 是一种基于乐观性验证的二层扩容方案，即默认提交的区块是正确的，除非有人提出质疑。它同样需要 Rollup Operator 将许多链下交易聚合成一个批次，之后计算批次交易产生的新状态（如余额、合约状态等）并生成一份链下状态更新；然后将链下状态更新、相关数据提交到主链，这个状态默认是正确的，不需要额外验证；但是在状态更新提交后，会有一个固定的挑战期，在此期间，任何人都可以通过提供欺诈证明来质疑提交的状态更新的有效性，与被质疑状态的相关的整个交易将通过 EVM 运行检验，如果证明状态更新是错误的，提交者会被惩罚（扣除押金），同时链上状态会回滚到正确的状态；如果在挑战期内没有人质疑状态更新，或者质疑被证明是错误的，那么链上状态会根据提交的状态更新进行更新。

###### ZK 与 OP 比较
||Optimistic Rollups（OP）|zk-Rollups（ZK）|
|----|----|----|
|交易验证方式|通过欺诈证明（fraud proofs）验证交易，默认交易有效，需链下用户和节点持续监测|通过零知识证明（如zk-SNARKs或zk-STARKs）验证交易，生成简洁证明确保交易有效性|
|安全性|因默认交易有效存在一定安全风险，需链下积极监测|基于零知识证明验证方式，安全性较高|
|吞吐量与性能|链下交易处理速度通常较快，但链上验证可能需更长时间（等待欺诈证明挑战周期）|生成零知识证明需计算资源，但链上验证速度较快|
|通用性|完全兼容EVM，适合通用智能合约执行和复杂计算，众多DAPP可直接迁移|在通用智能合约和复杂计算方面应用目前受一定限制|
|成本|通常链下交易成本较低|生成零知识证明需计算资源，可能链下交易成本较高|
|整体优势|更适合处理复杂智能合约场景，以太坊兼容性好|在安全性和隐私保护方面有优势| 

##### 参考文章
- [L2 扩容技术详解：Optimistic Rollups 与 zk-Rollups](https://web3caff.com/zh/archives/55667)
- [Optimistic Rollup vs. ZK Rollup 对比](https://learnblockchain.cn/article/738)
- [一文详解以太坊扩容方案：OP vs ZK Rollup](https://foresightnews.pro/article/detail/7248)

### 2025.01.10
#### 扩容方案
[L2 扩容技术详解：Optimistic Rollups 与 zk-Rollups](https://web3caff.com/zh/archives/55667)


##### 链上扩容
链上扩容（Layer 1），通过优化底层区块链协议本身来提高吞吐量。

- **分片**是将区块链网络分割成多个相互独立的子链，每个子链可以并行处理交易。这样，整个网络的吞吐量会随着子链数量的增加而线性增长，分片也是以太坊 2.0 路线图中关键的一步，分片之后 TPS 和 Gas 才能得到真正的优化。
- **共识算法的创新**很少见了，像之前提出的 POS、DPOS、DAG 等都是相对于 POW 的创新，相比于 POW，它们可以减少网络资源消耗，提高交易处理速度，同样，以太坊也选择了这条路。
- **对底层区块链协议进行优化**，例如调整区块大小、区块产生时间等，可以在一定程度上提高网络的吞吐量，比如比特币的隔离见证（SegWit）升级。

##### 链下扩容
链下扩容（Layer 2），通过在底层区块链之上构建新的协议层来实现扩容。

- **状态通道**：状态通道（State Channels）允许用户在链下进行交易，仅在通道开启和关闭时与主链进行交互，这极大地减少了链上交易数量，从而提高了吞吐量，像 Raiden Network 和 Lightning Network 就是分别针对以太坊和比特币的状态通道扩容产品。
- **Plasma**：Plasma 是一种子链（sidechain）方案，允许用户将资产从主链迁移到子链，并在子链上进行交易，子链周期性地将其状态更新提交给主链，以确保安全性，比如 OMG Network。
- **Rollups**：Rollups 是将多笔交易打包成单个证明（zk-SNARKs 或 Optimistic Rollup 的欺诈证明），并提交到主链。这样，主链仅需验证证明而无需处理每笔交易，从而提高了吞吐量。典例是 zkSync（基于 zkRollup）和 Optimism（基于 Optimistic Rollup），Arbitrum 同样也是基于 OP 的 产品。
Arbitrum 是一种基于 Optimistic Rollups 的二层扩容解决方案，它结合了 Optimistic Rollups 的优势，并对仲裁过程进行了创新和优化，在处理质疑和仲裁时采用了二分查找（Binary Search）技术，降低了仲裁过程的复杂性和成本。二分查找仲裁可以缩小错误范围，这个过程在链下执行，而链上只需要验证最后的争议部分，从而减少了链上的交易处理成本，但是这个过程也延长了处理时间，所以在发生仲裁的情况下 Arbitrum 比 Optimistic 更便宜，但也更慢。

### 2025.01.11
#### Stages：Rollup成熟度的三阶段评级框架
根据 rollup 对这些训练轮的依赖将 rollup 分为三个不同的阶段
##### Stage 0 — Full Training Wheels 第 0 阶段 — 全辅助
At this stage, the rollup is effectively run by the operators. Still, there is an source-available software that allows for the reconstruction of the state from the data posted on L1, used to compare state roots with the proposed ones.
在此阶段，rollup 由 Operator 有效地运行。尽管如此，仍然有一个源代码可用的软件，允许从 L1 上发布的数据中重建状态，用于将状态根与建议的根进行比较。
##### Stage 1 — Limited Training Wheels 第 1 阶段 — 有限的辅助轮
In this stage, the rollup transitions to being governed by smart contracts. However, a Security Council might remain in place to address potential bugs. This stage is characterized by the implementation of a fully functional proof system, decentralization of fraud proof submission, and provision for user exits without operator coordination. The Security Council, comprised of a diverse set of participants, provides a safety net, but its power also poses a potential risk.
在此阶段，rollup 过渡到由智能合约管理。但是，安全理事会可能会继续存在以解决潜在的错误。此阶段的特点是实施功能齐全的证明系统、分散欺诈证明提交以及在没有操作员协调的情况下提供用户出口。安理会由不同的参与者组成，提供了一个安全网，但其权力也带来了潜在风险。
##### Stage 2 — No Training Wheels 第 2 阶段 — 没有辅助轮
This is the final stage where the rollup becomes fully managed by smart contracts. At this point, the fraud proof system is permissionless, and users are given ample time to exit in the event of unwanted upgrades. The Security Council’s role is strictly confined to addressing soundness errors that can be adjudicated on-chain, and users are protected from governance attacks.
这是 rollup 完全由智能合约管理的最后阶段。此时，防作弊系统无需许可，用户有充足的时间退出，以防发生不必要的升级。安全理事会的作用严格限于解决可以在链上裁决的健全性错误，并保护用户免受治理攻击。

##### 框架
|项目|Stage 0 要求|Stage 1 要求|Stage 2 要求|
|----|----|----|----|
|自我标识|需自我标识为rollup| - | - |
|L2 状态根发布|在L1上发布L2状态根| - | - |
|数据可用性（DA）|在L1上提供数据可用性，要保证重建 L2 状态的数据在 L1 上可用| - | - |
|重建状态源软件|提供能从L1数据重建L2状态的rollup node软件| - | - |
|证明系统| - |使用适当的证明系统，如欺诈证明或zk rollups的证明系统，至少5个外部行为者可提交欺诈证明（可白名单）|欺诈证明系统应完全去中心化，无需许可，任何人可提交欺诈证明|
|用户退出机制| - |用户可在无操作员协调下退出，至少有7天时间退出（不包括安全理事会和治理相关升级）|用户至少有30天时间退出（包括DAO发起的升级，有链上错误检测系统时对检测到的错误除外）|
|安全理事会设置| - |由至少8个参与者组成的多重签名设置，50%共识阈值，至少一半参与者为外部人员，身份公开披露|安理会权力应高度受限，仅在链上检测到可裁决的健全性错误时能干预| 

### 2025.01.12
#### Optimism治理机制
今天先列一下框架，明天查一下资料对比：
- Token House V.S. Citizen House
- Mission Grants V.S. RetroPGF

**Token House**
- 基于token持有量分配vote权重
- 可以delegate token给其他代表 (delegates)
- 负责Mission Grants

**Citizen House**
- 基于声誉的，由链上投票选出
- 负责RetroPGF


<!-- Content_END -->
