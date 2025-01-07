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

# {partypill}

1. 自我介绍
一个自学了一些python的老白。想努力学习获得更多收益。

2. 你认为你会完成本次残酷学习吗？
我愿意为此努力。

## Notes

<!-- Content_START -->

### 2025.01.06

笔记内容
1、今天第一天打卡，记录那些我不懂的东西并明天得出结论。
“默认假设所有交易都是有效的，只有在有人提出争议时才进行验证”：以太坊的验证机制是什么？怎么通过验证机制保持安全性？这点我不懂需要继续学习。
以太坊虚拟机（EVM）：不懂这个东西是啥，需要进一步回溯学习。
“挑战期”（Challenge Period）：不知道这个概念
复杂智能合约：不懂这个的机制，只知道因为它需要主网交互，导致需要高处理。
L2 和 L1 层：对概念掌握不清晰。
退出时间：这个也不清楚，需要搞明白挑战期。

欺诈证明（Fraud Proof）机制：不懂。
2、今天学到的东西
知道了op设计的初衷是为了降低eth的高gas，因为安全，去中心化和速度是不可能三角。eth保证了安全和去中心化，但速度没法保证。所以一开始设计了子链Plsma，除了少数必要的交易其他都在子链上处理，但这导致了子链的信息无法同步到eth主网，一个是不安全，另一个是挑战期退出慢。
然后op设计了打包交易上传，等于压缩了多次交易只需要一次上链，好处是同步速度快，坏处就是扩容性差。

3、阅读steps去了解必要的信息。

### 2025.01.07
1、回顾昨天的问题

1.1“默认假设所有交易都是有效的，只有在有人提出争议时才进行验证”：以太坊的验证机制是什么？怎么通过验证机制保持安全性？这点我不懂需要继续学习。

答案：Optimistic Rollup（乐观汇总）才假设所有交易有效，以太坊不会假设交易有效。以太坊使用 Merkle Patricia Trie（MPT） 存储账户状态，确保数据完整性和可验证性。验证的细节太复杂看不懂。需要继续学习。

1.1以太坊虚拟机（EVM）：不懂这个东西是啥，需要进一步回溯学习。

答案：以太坊虚拟机（Ethereum Virtual Machine, EVM） 是以太坊的核心组件，它是一个去中心化的计算环境，专门用于执行智能合约和处理交易。可以把 EVM 理解为一个“全球共享的计算机”，它负责运行智能合约，并确保所有节点对智能合约的执行结果达成一致。

这玩意用gas当计算限制，每次使用算力都消耗gas，避免无限支出，天才的设计。uni等很多都是在这个上面运行的。

1.3、“挑战期”（Challenge Period）：不知道这个概念

答案：Optimistic Rollup 默认认为所有交易都是有效的，但为了防止欺诈，系统引入了 挑战期（Challenge Period），通常为 7 天。

挑战期的作用：
让任何人都可以检查 Layer 2 的状态更新。
允许提交 欺诈证明（Fraud Proof），如果发现问题，则回滚错误状态并惩罚作恶者。
保障 Layer 2 交易的安全性，防止欺诈行为。
挑战期的主要缺点：
提现时间较长（通常需要 7 天）。
需要额外的保证金机制，以激励挑战者维护系统安全。

1.4、复杂智能合约：不懂这个的机制，只知道因为它需要主网交互，导致需要高处理。

答案：复杂智能合约指的是功能强大、逻辑复杂、需要与多个智能合约交互的合约。这类合约通常涉及多个状态更新、跨合约调用，并且在以太坊主网（Layer 1）执行时会消耗较高的 Gas 费用。

1.5、L2 和 L1 层：对概念掌握不清晰。
答案：L1 是 主链（Main Chain），它是 整个区块链网络的基础层，负责：安全性、共识机制、智能合约执行、数据存储

L1 直接在区块链上执行交易，并确保去中心化，但由于区块容量有限，它的交易处理能力较低，容易造成 网络拥堵和高 Gas 费。L2 是建立在 L1 之上的扩展解决方案，它在主链之外处理大部分交易，然后将结果提交到 L1，从而减少主链负担，提高交易速度，并降低 Gas 费用。

L2 不改变 L1 的共识机制，而是通过批量处理交易或链下计算来优化性能。op就是使用Rollups的L2

1.6、退出时间：这个也不清楚，需要搞明白挑战期。

答案：退出时间（Withdrawal Time） 指的是用户 从 Optimistic Rollup（OP Rollup）提取资金回到 Layer 1（L1） 所需的时间。
这个时间通常较长（通常 7 天），主要是由于 挑战期（Challenge Period） 机制的存在。

2、精读一下 Vitalik 2014 年的文章。
已经粗读，前置要求的信息太多，需要明天用第一性原理不断溯源。
### 2024.07.12

<!-- Content_END -->
