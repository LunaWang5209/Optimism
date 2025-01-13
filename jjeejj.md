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

# {你的名字}

1. 奕 iyi: 一名 后端 Golang、Node.js、Rust 开发者; 合约 ETH、Arb、Solana 开发者。进入 web3 行业 2 年
2. 你认为你会完成本次残酷学习吗？会

## Notes

<!-- Content_START -->

### 2024.07.11

笔记内容

### 2025.01.06

1. 初步了解了 Optimism layer2。存款、取款 是通过 bridge 来完成的，存款很快就可以完成，取款需要 challenge period 给出时间挑战时间来验证交易是否有效
2. 目前还不知道 和 Arb 的 区别, 待后续进一步学习

### 2025.01.07

1. 对比了 Optimism 和 Arbitrum 区别
   1. 都是使用了 Optimistic Rollup 来实现：假设某事为有效，直至其被证伪
   2. 解决争议的方式不一样：
      1. Optimism 会在 EVM 运行每笔交易，不能处理超过 EVM gas limit 的交易
      2. Arbitrum 会经过多伦协商，将最后单步的断言发给 EVM 进行验证， 消耗更少的 gas
      3. Optimism 解决争议的方式 更加简单，更加快速

### 2025.01.08

1. 学习了 文章 https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe 引入了 Stage 的概念 来判断 rollup 的 成熟程度
   1. Stage 0 还在中心化管理
   2. Stage 1 过度到智能合约管理，但是安理会可以独自解决潜在的错误
   3. Stage 2 完全由智能合约管理

### 2025.01.09

1. 阅读外部文章：Op 完全兼容 EVM ,严格执行 以太坊黄皮书，任何基于 Geth 编写的代码 都可以无需修改运行再 OP 上
2. 当运行验证节点，验证器在发现欺诈时会自动提交欺诈证明

### 2025.01.10

1. 阅读 https://community.optimism.io/welcome/welcome-overview 治理理念
   1. 由 company 、communities、citizens 组成 的 collective
   2. Superchain 标准化，推进了链的发展
   3. 治理模型有 2 部分组成：Token house and Citizens’ House, 2 院治理体系

### 2025.01.11

1. 今天 看了下 Token house 和 Citizens’ House 2 院治理体 有什么区别， 分别刻意投票什么，没有特明白，希望可以解答一下

### 2025.01.12

1. 阅读 Superchain 基本介绍：https://docs.optimism.io/stack/explainer
   1. Superchain 本质上是一个由多个采用 Optimism 的 OP Stack 构建的第二层（L2）区块链网络组成的集合
   2. 把 OP 主网 和 其他链 合并到一个 统一的 OP 链中 (chains within the Superchain)
   3. 相互之间是可以通信，标准的通信协议，共享的通信基础设置
   4. 去中心化的需要，目前还不能完全满足，但是是可以实现的
   5. Superchain 可以水平扩展多个链

<!-- Content_END -->
