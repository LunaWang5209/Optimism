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

# {DongChoeyGit/董卓杰}

1. Working hard to be a Web3 builder、Eterpay Web3 department manager、Bankless DAO member、Bankless CNmember、LeapOnchain Channel builder、Lil Nounser

2. 是的，我会完成本次残酷共学

## Notes

<!-- Content_START -->

### 2025.01.06

Optimism 的核心是帮助来自世界各地的人在中心化经济背景下利用它的 Optimistic Rollup 技术以及 Optimism 的 Tokenomics 搭建社区的治理体系。它的 Rollup 机制跟随着以太坊的共识作为核心思想，这个选择由于跟随主链的共识避免产生新共识造成的分叉，在一定程度上为其提供了足够的安全性。

### 2025.01.07

在 Optimism 的迭代更新“Bedrock”后，使用了一种非合约地址保存到以太坊的方式来减少 L1 的 gas fee，具体是将数据以压缩格式打包储存，使用 EIP-4844 的 blobs 作为实现路径。该路径的设计可以做到保持数据不可修改性同时，保证了可用性与完整性，更重要的是区块以压缩的格式写入 L1 极大减少了交易成本。

### 2025.01.08

Optimism “块” 的生产机制：Optimism 基金会是目前 OP Mainnet 上唯一的区块生产者，根据 Optimism 的 “Bedrock” 升级的内容，区块的生产由 sequencer 单一负责，完成交易的确认、状态的更新、L2 区块的构建与执行以及将用户交易数据提交到 L1。在 sequencer 设置了私有的内存池，以此规避 MEV 带来的问题。sequencer 没两秒生成一个区块，不管区块中是否包含交易。在 Optimism 中交易有两种提交的方式：1.直接提交：该方式成本较低，但缺乏抗审查性。2.提交到相应的 L2 区块中，这种方式提供了抗审查性。sequencer 必须同时要处理 L1 中的合法交易，以保持数据的一致性。

### 2025.01.09

Optimism 的区块执行引擎通过 op-geth 的组建实现的，主要通过两种机制接收：1.点对点的网络更新方式。2.节点的 Rollup。
Optimism允许在L1和L2之间发送消息，实现ETH和ERC20代币的转移。标准桥功能支持从以太坊存入代币到OP Mainnet及提取回以太坊。
从以太坊到OP Mainnet的交易称为存款，使用L1CrossDomainMessenger或L1StandardBridge。从OP Mainnet到以太坊的提款分为三个阶段，包括初始化提款、提交证明和完成提款。

### 2025.01.10

Optimism 的故障证明机制
在 Optimism 中使用状态承诺发布到以太坊主链，但是一一种待定状态，没有直接的有效证明。这种待定状态称之为挑战窗口（7 天时间），在此时间内如果没有人对更新的状态有异议，则会被视为最终确认状态，一旦进入最终确认状态，以太坊智能合约将会执行接收。当挑战窗口期间有人有异议，可以对承诺发出挑战，通过“故障证明”将其无效化。如果挑战成功则会从状态承诺链中移除，并可能被另一个提议的承诺替换。需要注意的是，成功的挑战不会回滚OP主网本身，只会影响已发布的状态承诺。交易的顺序和OP主网的状态不会因故障证明挑战而改变。故障证明过程目前正在进行重大重构，这是由于2021年11月11日EVM等效性更新的副作用。
<!-- Content_END -->
