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

# {古忆}

1. 自我介绍
币圈老韭菜

2. 你认为你会完成本次残酷学习吗？
会

## Notes

<!-- Content_START -->

### 2025.01.06

1. 核心概念
Optimistic Rollup是一种扩展以太坊的 L2 技术，利用以太坊（L1）的安全性，而无需独立的共识机制。通过在 L1 上发布压缩数据，提供高效且经济的交易处理能力。在 L1 上提交状态的同时，不立即验证其有效性，而是提供一个挑战窗口，如果无人质疑则状态最终确定。
Optimism是基于 Optimistic Rollup 的 L2 网络。它通过与以太坊的深度集成，提供快速、低成本的交易解决方案，同时保留了以太坊的安全性。

2. 主要机制

2.1 区块存储
在 Optimism 的 Bedrock 架构中，L2 区块以压缩格式写入以太坊，以减少写入成本。使用 EIP-4844 blob 技术，确保数据一旦提交到 L1，就无法被篡改或审查。

2.2 区块生成:
排序器：负责提供交易确认和状态更新，构建并执行 L2 区块，将用户交易提交到 L1。区块生产速度：每两秒生成一个区块。
交易提交方式：直接提交到排序器：成本低，但缺乏抗审查性。通过 L1 提交：确保抗审查性，通过 "epoch" 与 L1 关联。
当前由 Optimism Foundation 运行唯一的排序器。

2.3 区块执行
执行引擎通过点对点网络或从 L1 同步区块更新状态。
Rollup 节点：从 L1 中派生 L2 区块，确保抗审查性。

### 2025.01.07

什么是 Derivation Pipeline？
Derivation Pipeline 是 OP Stack 协议的核心部分，负责处理和验证交易。它通过对 Sequencer 提交的交易和批次推导出一致的状态，确保区块链的安全和完整。

主要功能
批次提交与排序：将交易整理成批次，并提交到 Layer 1（L1）进行确认和最终记录。
安全头与非安全区块：安全头——已在 L1 确认的最新状态。非安全区块——已排序但未在 L1 确认的交易。
重组与恢复：如果排序窗口（如 12 小时）过期仍未确认批次，会回滚未确认的区块，并用默认空区块继续处理新交易。

排序窗口：
定义交易从提交到确认的最大时间。超过窗口时间会触发回滚机制，清除未确认的交易。
示例：12 小时窗口：过期后回滚未确认交易，用默认区块推进网络。24 小时窗口：延长时间，但可能增加资源消耗和处理难度。

<!-- Content_END -->
