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

# Neal Lee

1. 自我介绍
用挣钱激励自己学习，用学习激励自己赚钱。
2. 你认为你会完成本次残酷学习吗？
可以的。
## Notes

<!-- Content_START -->

### 2025.01.06
核心概念 - Optimistic Rollup 是 Optimism 的关键，借父链（以太坊）安全与共识机制运作。
块存储 - Bedrock里，L2块以特定方式存于以太坊，提交后不可改，用压缩格式写入L1降成本。
块生产 - “排序器”管理块生产，防MEV。块每2秒生成，交易通过直接或L1提交至排序器，L1提交具备抗审查能力，当前由Optimism Foundation运行块生产。
块执行 - 执行引擎（op-geth）通过对等网络同步、rollup节点（op-node）从L1派生两种方式接收块。
跨层转移 - 支持 L1 和 L2 间资产转移，OP Mainnet 用标准桥实现。从以太坊到 OP Mainnet为 “存款”，反向 “取款” 分三步（初始化、提交证明、最终完成）。
故障证明 - 状态承诺在L1有7天挑战期，无挑战即确认，受挑战可经故障证明处理，不回滚OP Mainnet。该流程现因EVM更新而重构。

### 2025.01.07
Layer 2扩容技术是为解决区块链主网（Layer 1）交易拥堵和高手续费等问题而发展起来的，通过将部分交易从主网转移到二层网络进行处理，实现了在不改变主网底层协议的基础上提升区块链的性能。常见的Layer 2扩容技术如下：

#### State Channels
- 原理：允许用户在链下建立通道进行多次交易，只在通道开启和关闭时将交易结果记录在主链上，期间的交易状态在链下维护。
- 优点：交易速度快，可实现即时确认；交易成本低，因为大量交易无需上链。
- 缺点：通道内的资金有一定的锁定时间；安全性依赖于参与者的信用和智能合约的安全性。
- 应用：主要应用于高频小额交易场景，如支付、微交易等。

#### Sidechains
- 原理：与主链平行的独立区块链，通过双向锚定技术实现与主链的资产转移和交互。侧链有自己的共识机制和交易处理能力，可独立处理交易。
- 优点：具有较高的灵活性，可根据需求定制侧链的功能和参数；能实现一定程度的扩容，缓解主链压力。
- 缺点：跨链交互的安全性和复杂性较高；侧链的安全性和主链存在一定的耦合性。
- 应用：可用于实现特定的业务逻辑或功能，如隐私交易、游戏等。

#### zk-Rollups
- 原理：将多个链下交易打包成一个批次，生成一个零知识证明，然后将证明和交易摘要提交到主链。主链只需验证零知识证明的有效性，即可确认整个批次交易的合法性。
- 优点：数据可用性和安全性高，主链可验证交易的有效性；隐私性好，零知识证明可隐藏交易细节。
- 缺点：技术实现复杂，对开发者要求高；证明生成和验证的计算成本较高。
- 应用：适用于对隐私和安全性要求较高的场景，如金融交易、身份认证等。

#### Optimistic Rollups
- 原理：假设所有提交到Layer 2的交易都是合法的，先将交易结果快速更新到Layer 2，并将交易数据压缩后提交到主链。在一定的挑战期内，如果有用户发现交易存在问题，可发起挑战，通过智能合约进行验证和处理。
- 优点：兼容性好，易于与现有以太坊生态系统集成；交易速度较快，可实现快速确认。
- 缺点：挑战期内存在一定的安全风险；交易最终确认时间较长。
- 应用：广泛应用于以太坊Layer 2解决方案，如Optimism、Arbitrum等。

### 2025.01.08

#### zk-rollup gas fee
- 链下部分（存储+证明者成本）：状态存储和 SNARK（零知识证明）生成的成本。
（这部分依赖于硬件资源的使用，因此是不变的。我们的基准估计每次转账约为 0.001 美元。）
- 链上部分（gas 成本）：对于每个zkSync 区块，验证者必须支付以太坊 gas 来验证 SNARK，另外每笔交易额外支付约 0.4k gas 来发布状态。
（链上部分是一个变量，取决于以太坊网络中当前的 gas 价格。但是，这部分比普通 ETH/ERC20 转账的成本要便宜几个数量级。）

1. 交易费最低价
依赖于主网 gas 的价格
**链上 gas fee = 每 wei 的价格 * 交易大小 * gas 的费用 * 代币的风险系数**
**链下部分 ： SNARK（零知识证明）生成的成本。这部分依赖于硬件资源的使用，因此是不变的。每次转账基准约为 0.001 美元。**

2. 影响最低价的因素
依赖于主网的 calldata 的费用
<!-- 主网的 gas 的相关处于草案阶段的 EIP 主要为 EIP4488，该方案将 calldata 非0字节数据由16gas 降低至 3 gas，对 layer2 TPS的影响较大，利好 layer2 的 Rollup，可以大大降低Rollup主网的交易成本，非0字节的数据可以降低为当前的 1/5 的成本不到，0 字节的也可以微微降低（ab，op，zk 等预计都可以下降至目前 1/5 的手续费）。 -->

3. 费用支付方式
zkSync 中的转账天然支持 “无 gas 交易”：用户在被转账的代币中支付交易费用。
<!-- 例如，如果您想交易 DAI 稳定币，您无需拥有 ETH 或任何其他代币。只需支付一小部分 DAI 的费用。 -->

#### Op Gas 机制
**两个成本来源：L2 执行费和 L1 数据/安全费。**

- L2 执行费
就像在以太坊上一样，Optimism 上的交易必须为他们使用的计算量和存储量支付gas 。每笔 L2 交易都会支付一定的执行费用，等于交易使用的 gas 数量乘以交易附带的 gas 价格。这也是以太坊的收费方式。

<!-- 这是（简单的）公式：
l2_execution_fee = transaction_gas_price * l2_gas_used
使用的 L2 气体量取决于您尝试发送的特定交易，交易在 Optimism 上使用的 gas 量通常与在 Ethereum 上的大致相同。 -->

- L1 数据费
Op 与以太坊不同，因为 Op 上的所有交易也都发布到以太坊。此步骤对于 Op 的安全属性至关重要，因为这意味着同步 Op 节点所需的所有数据始终在以太坊上公开可用。这就是使 Op 成为 L2 的原因。

Op 上的用户必须支付向以太坊提交交易的费用。称之为L1 数据费用 ，这是 Op（和其他 L2）与以太坊之间的主要差异。由于以太坊上的 gas 成本非常昂贵，因此 L1 数据费用通常会在 Op 上占据交易的总成本。该费用基于四个因素：
 1. 以太坊当前的gas价格。
 2. 将交易发布到以太坊的 gas 成本。这交易长度的大小（以字节为单位）成比例。
 3. 以gas计价的固定费用。当前设置为 2100。
 4. 一种动态的间接费用，按固定数字支付的 L1 费用。当前设置为 1.24。
公式：L1_data_fee = L1_gas_price * (tx_data_gas + fixed_overhead) * dynamic_overhead

### 2025.01.09

<!-- 尝试从 L1 入金到 L2，暂未成功，在找原因。 -->
借助官方桥，自己用 viem 入金 L2 成功。

### 2025.01.10

尝试erc20 入金 op，暂未成功，

### 2025.01.11

仔细看了文档，使用相对应的版本，approve 还没成功， 后续步骤无法成功。
报错 Unexpected error when checking bridge Error: could not detect network (event="noNetwork", code=NETWORK_ERROR, version=providers/5.7.2)
但是 chainId 是对的。

也看了 viem 的相关文档，有入金 eth 的例子，还未找到发送 ERC20 相关的例子。

### 2024.07.12

<!-- Content_END -->
