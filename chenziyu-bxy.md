---
timezone: Asia/Shanghai
---
---

# {陈子谕}

1. 自我介绍
  我是陈子谕，我想要成为一名web3开发人员，我会为此持续付出努力，直到完成目标

2. 你认为你会完成本次残酷学习吗？
  会，这是我第一次进行残酷学习，我相信这会是一次很不错的体验，加油

## Notes

<!-- Content_START -->

### 2025.01.06
Rollup协议概述
Optimism的核心思想是Optimistic Rollup（乐观汇总）。它是一种利用另一个区块链的安全性来进行扩容的协议。

Optimistic Rollups 简要概述（TL;DR）
Optimism是一个“Optimistic Rollup”，这实际上是描述一个利用另一个“父链”区块链的安全性的区块链。具体而言，Optimistic Rollups使用父链的共识机制（如工作量证明PoW或权益证明PoS）来保障安全，而不需要自己提供一个共识机制。在OP Mainnet的情况下，这个父链是以太坊。

区块存储
在Bedrock架构下，L2区块被存储到以太坊区块链中，使用非合约地址（例如0xff00..0010）来减少L1的gas费用。这些区块以EIP-4844 Blob的形式作为交易提交，因此，一旦这些区块被包含到区块中并获得足够的验证，就无法再被修改或审查。这样，OP Mainnet继承了以太坊的可用性和完整性保证。

这些区块被以压缩格式写入L1，以减少成本，因为写入L1是OP Mainnet交易的主要成本。

区块生产
Optimism的区块生产由一个名为“sequencer”（顺序器）的单一方主要管理，提供以下服务：

提供交易确认和状态更新。
构建并执行L2区块。
将用户交易提交到L1。
在Bedrock中，sequencer有一个类似L1以太坊的内存池，但该内存池是私有的，以避免开启MEV（最大化提取价值）的机会。在OP Mainnet中，区块每两秒生成一次，不论是空区块（没有交易），填充满交易，还是其他情况。

交易有两种方式到达sequencer：

直接提交给sequencer的交易：这种交易提交成本较低，因为不需要单独的L1交易费用，但无法实现审查抵抗，因为只有sequencer知道这些交易。
在L1提交的交易（称为存款）：这些交易会包含在相应的L2区块中。每个L2区块由“epoch”（对应的L1区块）和在该epoch内的序列号标识。epoch的第一个区块包括了所有在对应L1区块发生的存款。
如果sequencer试图忽略一个合法的L1交易，它会导致状态与验证者不一致，这与尝试伪造状态的情况一样。这确保了OP Mainnet具备与以太坊L1相同的审查抵抗能力。

目前，Optimism基金会是OP Mainnet唯一的区块生产者。

区块执行
执行引擎（通过op-geth实现）接收区块有两种机制：

通过P2P网络与其他执行引擎同步：这种方式与L1的执行客户端同步状态类似。
通过Rollup节点（op-node）从L1衍生L2区块：这种机制较慢，但具有审查抵抗能力。
跨层桥接ETH或代币
Optimism的设计使得用户可以在L2（如OP Mainnet、OP Sepolia等）与底层L1（如以太坊主网、Sepolia等）之间发送任意消息。这使得在两个网络之间传输ETH或代币（包括ERC20代币）成为可能。具体的消息传递机制根据消息发送的方向不同而有所区别。

OP Mainnet使用这一功能，通过标准桥接（Standard Bridge）使得用户可以将代币从以太坊存入OP Mainnet，同时也可以从OP Mainnet提取相同的代币。有关标准桥接的详细信息，请参考开发者文档和示例。

从以太坊到OP Mainnet
在Optimism术语中，交易从以太坊（L1）到OP Mainnet（L2）被称为存款（Deposits）。

用户可以通过L1CrossDomainMessenger或L1StandardBridge进行存款。
存款交易会成为“epoch”对应的第一个L2区块的一部分。这个L2区块通常会在相应的L1区块几分钟后创建。
从OP Mainnet到以太坊
从OP Mainnet到以太坊的操作被称为提款（Withdrawals），包括以下三个步骤：

初始化提款：通过L2交易启动提款。
等待输出根提交到L1：然后通过proveWithdrawalTransaction提交提款证明。这个新步骤允许通过链外监控提款过程，从而使得识别不正确的提款或输出根变得更容易，保护OP Mainnet用户免受潜在的桥接漏洞。
等待挑战期结束：提款的挑战期为一周（主网），或者更短（测试网络）。挑战期结束后，提款最终确定。

故障证明
在Optimistic Rollup中，状态承诺会被发布到L1（在OP Mainnet中是以太坊），但这些承诺没有直接的有效性证明。相反，这些承诺会在一段时间内（称为“挑战窗口”）被视为待定状态。如果在挑战窗口期间（目前为7天）没有人对该状态承诺提出挑战，那么它就被视为最终确认。

当状态承诺被挑战时，可以通过“故障证明”（Fault Proof）过程将其作废。如果挑战成功，该承诺会从状态承诺链（StateCommitmentChain）中移除，并最终被新的承诺替代。需要注意的是，成功的挑战不会回滚OP Mainnet本身，只会替换有关链状态的已发布承诺。OP Mainnet的交易顺序和状态不会因为故障证明的挑战而改变。

当前，故障证明过程正在进行重大重构，这是由于2021年11月11日的EVM等价性更新带来的副作用。


### 2025.01.07
Layer 2值得关注的原因如下：

Layer 2网络将会更快、更便宜，能够让更多用户得以进入以太坊生态；
提前参与Layer 2网络的激励，能够获得奖励；
在Layer 2 发展的预期下，用户可将资产迁移至二层网络上，将会有很大概率获得空投；
因此，Layer 2 也是今年最重要的看点之一。对于用户来说，除了体验舒适之外，最关心的还是交易成本。本文从对比Layer 2各种解决方案的交易成本出发，方便各位读者能够更加清晰的了解到每个解决方案的优劣势。

1. 背景：以太坊的扩容需求
随着以太坊生态的蓬勃发展，去中心化金融（DeFi）和非同质化代币（NFT）等应用的增长促进了对更高交易吞吐量和更低交易费用的需求。然而，以太坊每秒处理的交易数（TPS）受到其网络设计的限制，且由于网络拥堵，gas费用高涨。因此，提升以太坊网络的吞吐量和降低交易费用成为了当前发展的关键目标。
2. Layer 2的作用
Layer 2（L2）解决方案是提升以太坊吞吐量和降低交易成本的关键技术。Layer 2网络通过在主链（Layer 1）之上构建第二层协议，允许更多交易处理而不直接占用主链的资源。这样，Layer 2能够为用户提供更快、更便宜的交易体验。
3. Layer 2的扩容技术方案
目前，Layer 2有四种主要的扩容技术方案：

1.Optimistic Rollup
2.ZK Rollup
3.Plasma
4.Validium

这些技术方案的核心思想是通过不同方式压缩数据、减少对主链的依赖，提高处理效率。
4. Layer 2的Gas费用
根据文章中的分析，比较了这几种方案的gas费用。计算方法基于当前以太坊的Gas费用（如Gas价格为30 Gwei）及出块时间等参数。以ETH价格为2500美元、每个区块Gas限额为3000万等条件，进行计算得出不同技术方案的交易处理能力和费用。
5. ZK Rollup的优势
通过ZK Rollup方案，数据压缩效果最为显著。文章指出，ZK Rollup可以将以太坊主链上的每个ETH交易的字节数压缩到12个字节，这使得其在处理交易时的可扩展性大幅提高。例如，ZK Rollup可以支持每秒大约11,818笔交易，而以太坊主网则只能支持约101笔交易。这意味着，ZK Rollup能大幅提升以太坊的吞吐量，尤其是对于ERC-20代币和去中心化交易所（如Uniswap）上的交易，ZK Rollup的扩展性优势更加明显。
6. Optimistic Rollup的扩展性
Optimistic Rollup也能提供可观的扩展性，虽然与ZK Rollup相比，压缩效果略逊一筹，但它依然能够显著降低交易成本并提升TPS。
7. 未来展望
随着EIP-4488和EIP-4844等提案的实施，Layer 2方案的成本有望进一步降低。这些改进将有助于优化rollup的表现，使以太坊网络的扩展能力更加可行，为更广泛的应用奠定基础。

### 2025.01.08
ZK Rollup的交易费用概述
ZK Rollup 是一种扩展解决方案，将计算和数据存储转移到链下，同时通过零知识证明（SNARK）确保数据的正确性和一致性。zkSync 是其中一种实现，它的交易费用由链下和链上两个部分组成。

1. 交易费用的组成
链下部分（存储 + SNARK 生成成本）

这部分费用由存储和零知识证明（SNARK）生成的计算成本构成，主要取决于硬件资源的使用，因此该费用是固定的，不随网络拥堵或ETH的Gas价格波动。

基准估计： 每次转账的链下费用约为 0.001 美元。
链上部分（Gas 成本）

每个 zkSync 区块都需要支付以太坊的Gas费用来验证 SNARK 证明。此外，每笔交易还需要额外支付一定的Gas费用来发布状态更新（状态∆）。

可变性： 这部分费用受到以太坊主网Gas价格的影响，因此会随着Gas价格的波动而变化。然而，相比传统的ETH/ERC20转账，zkSync的链上费用通常要便宜几个数量级。
2. 交易费用的地板价
地板价 是由以太坊的Gas费用和交易类型决定的。ZK Rollup的交易地板价依赖于ETH主网的Gas费用，并且会受到以下因素的影响：

ETH主网的Gas费用： 链上费用直接受以太坊Gas价格的影响。ZK Rollup需要在每笔交易中支付一定量的Gas来验证和提交状态更新。
交易大小： 交易的大小也影响Gas费用，尤其是在计算验证证明时。
代币风险系数： 代币的风险系数也可能影响费用，尤其是在价格波动较大的情况下。
计算公式如下：

（1）交易费用地板价
ZK rollup的交易地板价依赖于eth主网 gas的费用。

链上 gas fee = 每 wei 的价格 * 交易大小 * gas 的费用 * 代币的风险系数
链上费用=每 wei 的价格×交易大小×Gas费用×代币风险系数

链上部分（gas 成本） ：对于每个 zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态 。链上部分是一个变量，取决于以太坊网络中当前的 gas 价格。但是，这部分比普通 ETH / ERC20 转账的成本要便宜几个数量级。

实际大小= 每 wei 的价格 * 交易大小 * gas的费用 * 当前gas价格 * 代币
的风险系数
= wei_price_usdgas_tx_amountscale_gas_price*token_usd_risk
假设 ETH 价格为2500u，当前 gas 价格为30Gwei

普通交易的链上 gas 成本 = 2500/10^18*(0+300+2002)(3010^9)1.31 = 0.068u
交易接收者为新地址的链上 gas 成本 = 2500/10^18(0+940+2006) (30*10^9)1.31 = 0.20865u
假设eth价格为2500u,当前gas价格为30Gwei

普通交易的链上 gas 成本 = 2500/10^18*(0+300+2002) (3010^9)1.31 = 0.068u
交易接收者为新地址的链上 gas 成本 = 2500/10^18(0+940+2006) (30*10^9)1.31 = 0.20865u

3. 影响地板价的因素
EIP 4488的提案：

EIP 4488提案计划将ETH主网Calldata的Gas费用降低，从当前的16Gas减少至3Gas。这对Layer 2解决方案，如ZK Rollup，带来了巨大的好处。降低Calldata的费用将直接减少交易的链上费用，预计这将大大降低Rollup的交易成本，特别是对于非0字节数据（如ABIs、操作码等）。如果EIP 4488得以实施，Rollup的手续费将大幅下降，预计费用将降至目前的1/5。

4. 费用支付方式
无气体交易：

在zkSync中，用户可以进行“无气体交易”，即无需持有ETH或其他代币来支付交易费用。用户可以使用转账中的代币来支付交易费用。例如，如果您进行DAI的转账，可以直接使用DAI代币支付交易费用，而不需要额外持有ETH。这对于用户来说是非常方便的，尤其是在跨链交易时，免去持有ETH的麻烦。


### 2025.01.09
zkPorter的交易费用
zkPorter 是 zkSync 2.0 中的一项新功能，旨在提供具有链下数据可用性的解决方案。与 zkRollup（具有链上数据可用性）相比，zkPorter 在数据可用性上做了优化，从而大大降低了交易费用。

1. zkPorter的交易费用特点
zkPorter 不需要每笔交易都将数据存储在链上，因此相较于传统的 zkRollup，其交易成本显著降低。根据官方文档，zkPorter的交易费用预计在 1到3美分 之间，并且费用是相对恒定的，不受链上数据存储的影响。

链下成本： zkPorter的交易费用主要由链下计算和存储成本组成。由于不需要链上数据可用性保障，交易的费用低于 zkRollup。
固定费用： zkPorter 的费用相比 zkRollup 减少了大约100倍。
2. zkPorter的工作原理
在 zkSync 2.0 中，L2 状态分为两种类型：

ZK Rollup： 具有链上数据可用性，保证了每笔交易的数据能够随时被验证。
zkPorter： 具有链下数据可用性，通过“监护人”机制保障数据的安全性和可用性。
zkPorter 账户的主要优势在于交易费用大幅降低。例如，Uniswap 部署在 zkRollup 端的智能合约上时，zkPorter 账户可以以低于 0.03 美元 的费用进行 Swap 操作，并且所有交易只需要更新一次状态到以太坊，而不是每次都提交数据。

3. zkPorter的安全性和数据可用性
监护人机制： zkPorter 的数据可用性由 zkSync 代币持有者（称为监护人）保障。监护人通过参与权益证明（PoS）来保护数据的完整性，任何数据可用性问题都将导致监护人的权益被削减。
PoS机制： zkSync 的 PoS 比其他侧链系统更加安全，监护人只能冻结 zkPorter 状态，无法窃取资金。用户可以根据自己的安全需求自由选择是否使用 zkRollup 或 zkPorter。
4. 应用场景
假设一个应用场景，Uniswap 在 zkRollup 端部署其智能合约，zkPorter 账户用户可以以低成本进行交易，如：swap 操作。尽管进行多次交易，但所有这些交易的更新只需要提交一次到以太坊。这使得 zkPorter 成为低成本高效的选择，尤其适合频繁交易的应用场景。

5. zkPorter与zkRollup的对比
特性	zkRollup	zkPorter
数据可用性	完全在链上	通过监护人机制保障链下数据
交易费用	相对较高	1到3美分，低成本
安全性	通过链上数据验证提供安全性	通过权益证明机制保障数据可用性
适用场景	高安全性要求的应用	高频交易、低费用的应用
6. zkSync 2.0主网上线时间
根据官方文档，zkSync 2.0计划于2022年下半年上线主网，zkPorter 也将随着 zkSync 2.0一同推出。预计 zkPorter 将带来更高的交易吞吐量和更低的交易费用，进一步促进以太坊生态系统的发展。

总结
zkPorter 的主要优势在于其链下数据可用性和低交易费用。由于不需要将每笔交易的数据存储在链上，zkPorter 相比 zkRollup 在交易费用上有了显著降低。zkPorter 账户可以以低于 0.03 美元 的费用进行大规模的交易，同时借助监护人机制保障数据的可用性和安全性。这使得 zkPorter 成为高频交易、低成本场景的理想选择。

随着 zkSync 2.0 的推出，zkPorter 预计将在去中心化金融（DeFi）、NFT 和其他区块链应用中发挥重要作用，帮助以太坊扩展性提升，并为用户提供更好的体验。

### 2025.01.12
在区块链技术的快速发展中，Rollup 是一种关键的扩展解决方案，它旨在通过最小化信任依赖来提升以太坊的扩展能力。Rollup 的发展通常经历一个过渡阶段，通常称为“训练轮”，允许在受控环境下进行系统更新和错误修复。随着技术的成熟，最终目标是移除这些集中控制的部分，确保 Rollup 完全继承基础链（L1）的安全性，进一步向去中心化、无需许可的扩展目标迈进。

为了帮助指导这一转变，Vitalik Buterin 提出了一个分阶段的框架，将 Rollup 发展分为三个主要阶段：

第0阶段：全面训练
在这一阶段，Rollup 由运营商有效控制，主要目的是测试和优化系统。此阶段的关键特点包括：

状态重建功能：需要有软件能基于 L1 数据重建 L2 状态，以便验证提议的状态根。
L2 状态根发布：Rollup 必须将其状态根发布到 L1，这对于保障透明度和撤资等操作至关重要。
数据可用性：确保 L1 上的数据是可访问的，这对 Rollup 的安全性至关重要。
第1阶段：有限的训练轮
这一阶段标志着 Rollup 过渡到更多依赖智能合约的管理，但仍保留一定的中心化控制来处理系统问题。主要要求包括：

证明系统的应用：需要有功能齐全的证明系统，用于验证状态根的有效性。
外部参与者的欺诈证明：至少有5名外部参与者能够提交欺诈证明来确保系统的正确性。
用户退出机制：用户应当能够在没有运营商干预的情况下进行资产撤回。
升级的退出窗口：如出现不希望的升级，用户至少应有7天的时间来退出。
安全委员会的设立：一个由多方参与的安全委员会存在，以确保系统的安全性并解决潜在问题。
第2阶段：无需训练
此阶段标志着 Rollup 完全去中心化，由智能合约自主管理，防止任何单一实体对系统产生过多影响。主要特征包括：

完全去中心化的欺诈证明系统：任何人都应能提交欺诈证明，确保系统完全去中心化。
更长的退出时间：如果出现不必要的升级，用户应至少有30天的时间来退出系统。
安理会的角色限制：安理会仅在发生链上错误时介入，确保系统不被过度干预。
这一框架帮助解决了当前 Rollup 发展中的一些挑战，包括如何确保不同阶段的透明度和信任度，并提供了一个明确的评估标准。
这为 Rollup 从集中化到完全去中心化的过渡提供了技术指南，同时为社区提供了一个更加清晰的理解框架。
### 2024.07.12
<!-- Content_END -->
