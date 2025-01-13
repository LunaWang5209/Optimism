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

# {田喜碧}

1. 我于今年开始接触 Web3，期间参与过 NFT 相关工作。我一直从事视觉设计工作，若社区有物料更新需求，我很乐意提供帮助。我期望能在边学边做中深入熟悉这个领域，进而为 LXDAO 贡献自己的力量。我还参加过在曼谷举办的 Devcon 以及 LXDAO Coordination Day 活动

2. 会认真学习并完成这次的残酷共学，补足自己在web3领域缺失的板块，希望通过这次学习能为组织的未来发展做出贡献。

## Notes

<!-- Content_START -->

### 2025.01.06

关于Optimistic Rollup 
1.理解 Optimistic Rollup 是如何依赖于以太坊等“父”区块链的安全性来运行的。
2.了解 Optimism 作为 Optimistic Rollup 的具体实现及其设计目标。
3.Optimism 是一种“Optimistic Rollup”，利用以太坊的共识机制，而不提供自己的机制

### 2025.01.07
“纪元”和序列号标识，首个块包含对应L1块中的存款，以防排序器忽略合法交易
非合约池可和EIP-4844的blob格式在以太坊上存储L2区块，以降低交易成本。交易可以在直接提交或L1上提交的存款两种方式到达排序器，通过L2“纪元”和序列号标识，首个块包含对应L1块中的存款，以防排序器忽略合法交易。乐观基金是在OP Mainnet对区块生产的控制。

### 2025.01.08
块执行：通过与其他执行引擎的对等网络同步状态，能够有效地处理块，同时利用以太坊的安全性。
层间桥接：设计允许用户在 L2 和 L1 之间发送任意消息，实现 ETH 或代币的转移。在 OP Mainnet 中使用，允许代币从以太坊存入 OP Mainnet ，并从 OP Mainnet 提取回以太坊，相互切换。
以太坊迁移至 OP 主网：从以太坊 L1 到 OP 主网 L2 的交易，在交易中形成规范区块链的一部分。
OP 主网迁移至以太坊：提款过程确保了用户在 OP 主网和以太坊之间安全地转移资产，通过链下监控和故障挑战机制，增强了提款的安全性和可靠性。

### 2025.01.09
在 Optimistic Rollup 中，状态承诺发布到 L1（如以太坊），无需有效性证明。承诺在 7 天的“挑战窗口”内待定，若无质疑则视为最终承诺，最终承诺后，以太坊智能合约可安全接受提款证明。
若承诺被质疑，可通过“过错证明”使其无效，成功挑战后将被替换，挑战不会回滚 OP Mainnet，仅影响状态承诺，交易顺序和状态不变，因 EVM 等效性，故障验证流程正在重大更新。

### 2025.01.10
了解了以太坊当前的价格、区块gas上限、gas费用和平均出块时间，这些因素影响交易的效率和成本。认识到ZK Rollup在ETH转账和ERC20代币转账中的显著扩展性优势，尤其是在高并发交易时的表现。认识到ZK Rollup和Optimistic Rollup在以太坊生态系统中的重要性及其对提高交易效率和降低成本的影响，这些知识对理解去中心化金融（DeFi）和NFT等领域的应用非常有帮助。

### 2025.01.11
1.验证者需支付以太坊 gas 来验证 SNARK。每笔交易额外支付约 0.4k gas 来发布状态 ，这部分成本是变量，取决于以太坊网络当前的 gas 价格，相较于普通 ETH/ERC20 转账，链上部分的成本便宜几个数量级。
2.ZK Rollup 的交易地板价依赖于以太坊主网的 gas 费用。使用 ZK Rollup 的频率越高，费用越低，用户的状态数更新越多，ZK 支付给 Layer 1 的 gas 费用相对变少，但并未平摊至用户。
交易地板价与ETH主网的calldata费用密切相关，Calldata费用是指在以太坊网络中，用户在执行交易或调用智能合约时，所需支付的费用，特别是与数据传输相关的费用，直接影响智能合约的调用和Layer 2解决方案的经济性。通过降低这些费用，可以提高以太坊网络的可扩展性和用户体验，对Layer 2的TPS（每秒交易量）影响显著，有利于Layer 2的Rollup。
3.zkSync支持用户交易DAI稳定币时，用户无需持有ETH或其他代币，只需支付一小部分DAI作为费用。
<!-- Content_END -->
