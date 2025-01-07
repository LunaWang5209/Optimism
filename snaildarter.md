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


### 2024.07.12

<!-- Content_END -->
