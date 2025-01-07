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

# wuyanhui

1. 自我介绍
   一名web2资深，刚入行web3半年

3. 你认为你会完成本次残酷学习吗？
   非常期待这一次的学习，保证完成任务！

## Notes

<!-- Content_START -->

### 2025.01.06

1. 学习 Optimism 的基本概念，为什么会出现 Optimism
什么是 Optimism？
Optimism 是一种基于以太坊的 Layer 2 解决方案，旨在提高以太坊的交易速度并降低交易费用，同时保持以太坊主网的安全性和去中心化特性。它通过 Optimistic Rollups 技术将大部分计算和数据存储从以太坊主网移到 Layer 2，从而缓解主网的拥堵问题。
为什么会出现 Optimism？
Optimism 主要是为了解决以太坊主网在大规模使用时遇到的以下问题：
1. 高昂的交易费用（Gas费）
以太坊主网的交易费用随着网络负载的增加而急剧上升，尤其在 DeFi 和 NFT 活跃时，普通用户难以负担高额费用。
2. 低交易吞吐量（TPS, Transactions Per Second）
以太坊主网的 TPS 约为 15-30，这在面对大规模用户时显得不够用，导致交易延迟和用户体验下降。
3. 网络拥堵
当网络交易量激增时，主网变得极为拥堵，用户需要支付更高的 Gas 费以加速交易确认。
Optimism 的目标
● 降低交易费用
通过将大量的计算和数据移至 Layer 2，用户可以享受显著降低的交易费用。
● 提高交易速度
在 Layer 2 上，交易的处理速度比主网快得多，适合对延迟敏感的应用（如 DeFi、NFT 市场等）。
● 增强以太坊的可扩展性
帮助以太坊应对更多用户和应用场景，为 Web3 生态提供更好的基础设施。


2. Layer 2 扩容方案有哪些，解决了哪些问题
Layer 2 是指构建在以太坊主网（Layer 1）之上的扩展解决方案，旨在提高以太坊网络的性能，主要包括以下方案：
1. Rollups
Rollups 是目前最广泛应用的 Layer 2 扩容方案，它们将大量交易汇总（Rollup）到一个批次中，并将交易数据提交到以太坊主网。
● Optimistic Rollups（如 Optimism、Arbitrum）
  ○ 工作原理：假设所有交易都是有效的，只有在发现欺诈时才进行验证。
  ○ 解决的问题：提高 TPS，降低 Gas 费。
  ○ 缺点：存在欺诈挑战期（通常为 1 周）。
● ZK-Rollups（如 zkSync、StarkNet）
  ○ 工作原理：通过生成零知识证明，直接证明交易的有效性。
  ○ 解决的问题：更快的结算时间和更低的 Gas 费。
  ○ 缺点：实现复杂度较高。
2. State Channels
State Channels 允许用户在链下直接进行交易，最终将结果提交到链上。
● 解决的问题：减少链上交互次数，提高交易速度并降低费用。
● 缺点：需要用户保持在线，适用于特定场景（如支付渠道）。
3. Plasma
Plasma 使用子链（Child Chain）处理大量交易，定期将摘要提交到主网。
● 解决的问题：通过将大量交易从主网移到子链来提高吞吐量。
● 缺点：退出过程较慢，适用于简单的转账场景。
4. Validium
Validium 类似于 ZK-Rollups，但将数据存储在链下。
● 解决的问题：提供高吞吐量和低费用，同时保护用户隐私。
● 缺点：需要信任外部数据存储。


3. Optimistic Rollups 是什么，解决了哪些问题
Optimistic Rollups 的定义
Optimistic Rollups 是一种基于“乐观假设”的扩容技术。在 Optimistic Rollups 中，所有提交的交易默认被认为是有效的，除非有用户提出欺诈证明（Fraud Proof），以此来减少交易验证的计算量。
工作原理
1. 批量处理交易：Optimistic Rollups 将数千笔交易打包成一个批次，并将其压缩后的数据提交到以太坊主网。
2. 乐观假设：假设所有交易都是正确的，因此无需逐笔验证。
3. 欺诈挑战期：在一定时间内（如 7 天），任何人都可以提交欺诈证明。如果证明成功，Rollup 批次将被回滚，恶意验证者会被罚款。
Optimistic Rollups 解决了哪些问题？
1. 降低交易费用
Rollups 的批量处理显著降低了用户需要支付的 Gas 费。
2. 提高交易吞吐量
每秒可处理数千笔交易，相比以太坊主网的 15-30 TPS，有了巨大的提升。
3. 减轻主网负担
通过将大部分计算和存储移至 Layer 2，减少了主网的拥堵。
4. 增强去中心化
相比其他扩容方案（如侧链），Optimistic Rollups 保留了以太坊主网的安全性和去中心化特性。
### 2024.07.12

<!-- Content_END -->
