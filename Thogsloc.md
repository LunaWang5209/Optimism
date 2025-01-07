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

# Thogsloc

1. 自我介绍
在web3呆过一阵子的社区新人，来和大家一起参与学习
2. 你认为你会完成本次残酷学习吗？
Waaaagh！
## Notes

<!-- Content_START -->

### 2025.01.06

Optimistic Rollup 依赖于“父链”的安全性，核心思想是利用父链的共识机制。

Bedrock 版本中，L2 区块被存储在以太坊区块链上，使用非合约地址来减少 L1 的交易费用。区块以压缩格式写入 L1。

Sequencer 负责：
提供交易确认和状态更新、
构建和执行 L2 区块、
将用户交易提交到 L1。

op-geth 组件通过两种机制接收区块：
通过点对点网络与其他执行引擎同步。
从L1派生L2区块。

OP Rollup 通过以上方法使得交易得到快速处理和保持低成本。

### 2024.07.12

<!-- Content_END -->
