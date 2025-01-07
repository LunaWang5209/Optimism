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

# Louis

1. 自我介绍
My name is louis and I am a blockchain development engineer

2. 你认为你会完成本次残酷学习吗？
I believe that I can complete the study task

## Notes

<!-- Content_START -->

### 2025.01.06

Optimism 是一种“乐观型 Rollup”，即以太坊的 Layer 2 扩展解决方案，通过利用以太坊的安全性来提高交易吞吐量并降低费用。 与传统区块链不同，乐观型 Rollup 默认假设交易是有效的，只有在出现挑战时才执行计算，从而显著提高效率。

**乐观型 Rollup 的关键组成部分：**

- **区块存储：**在 Bedrock 版本中，Optimism 使用非合约地址（0xff00...0010）在以太坊上存储 Layer 2（L2）区块，以最小化 gas 费用。 这些区块作为交易提交，使用 EIP-4844 blobs，一旦包含在具有足够验证的区块中，即可确保数据的可用性和完整性。 这种设计使 Optimism 继承了以太坊的安全保证。

- **区块生产：**一个称为“排序者”的实体负责区块生产。 排序者提供交易确认，构建和执行 L2 区块，并将用户交易提交到 Layer 1（L1）。 在 Bedrock 中，排序者拥有一个私有内存池，以防止矿工可提取价值（MEV）机会。 无论交易量如何，每两秒生成一个区块。

- **区块执行：**交易在 L2 链上执行，结果定期发布到以太坊。 这种方法减少了以太坊的计算负担，同时保持安全性。

- **资产桥接：**用户可以使用桥接将 ETH 和代币在以太坊和 Optimism 之间转移。 从以太坊移动资产到 Optimism 涉及在以太坊的合约中锁定代币，并在 Optimism 上铸造相应的代币。 相反的过程涉及在 Optimism 上销毁代币，并在以太坊上解锁它们。

- **故障证明：**Optimism 采用一种挑战机制，默认假设交易是有效的，除非被证明无效。 如果有人发现无效交易，可以提交故障证明进行挑战。 该系统在无需对每笔交易进行链上计算的情况下确保正确性。

通过利用这些机制，Optimism 在保持以太坊的安全性和去中心化的同时，实现了更高的可扩展性和更低的费用。 

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

### 2025.01.09

<!-- Content_END -->
