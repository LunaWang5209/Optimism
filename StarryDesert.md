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

# StarryDesert

1. 自我介绍

   大家好啊，我是参加过上次Arbitrum的共学的StarryDesert，我想继续我的以太坊知识学习之路

2. 你认为你会完成本次残酷学习吗？

   如果没有意外的话，上次我完成了，这次我也会完成，我会加油的

## Notes

<!-- Content_START -->

### 2025.01.06

笔记内容

#### Optimistic Rollup的本质

- Optimistic Rollup是一种依赖于"父链"安全性的区块链解决方案
- 它不需要自己的共识机制，而是利用父链(在这里是以太坊)的共识机制
- 这种设计可以大幅降低成本同时保持安全性

##### 区块存储机制

- 使用非合约地址(0xff00..0010)在以太坊上存储L2区块
- 采用 **EIP-4844** blobs提交交易
- 使用压缩格式写入以降低成本
- 继承了以太坊的可用性和完整性保证

##### 区块生产特点

- 由单一实体"排序者"(**sequencer**)管理
- 每2秒产生一个区块
- 具有私有交易池(**mempool**)以避免MEV
- 交易提交有两种方式：
  * 直接提交给排序者(成本低但可能被审查)
  * 通过L1提交(称为存款，具有抗审查性)

##### 跨层资产桥接

- 支持L1和L2之间的ETH和代币转移
- 从以太坊到OP Mainnet称为"存款"
- 从OP Mainnet到以太坊称为"提款"，需要经过三个阶段：
  * 初始化提款
  * 提交提款证明
  * 等待质疑期后完成提款

##### 错误证明机制

- 状态承诺在没有直接证明的情况下发布到L1
- 状态提交后有7天的质疑窗口期
- 在质疑期内可以通过"错误证明"(**fault proof**)流程挑战
- 成功的质疑只会影响已发布的状态承诺，不会回滚链本身

#### Optimistic Rollup的创新点和优势：

1. 扩展性优势
- 通过将大部分计算和存储转移到L2，显著提升吞吐量
- 保持与以太坊主网的安全性连接，实现可扩展性和安全性的平衡

2. 成本效益
- 通过数据压缩和批处理降低交易成本
- 继承以太坊的安全性而无需额外的共识成本

3. 兼容性
- 与以太坊完全兼容，支持智能合约
- 开发者可以轻松将以太坊应用迁移到Optimism

4. 安全设计
- 采用乐观验证机制，假设大多数交易都是诚实的
- 通过质疑期和错误证明机制确保安全性
- 继承以太坊的安全属性

5. 创新的跨链桥接
- 设计了安全的跨链通信机制
- 引入了多步骤验证流程增强安全性

**Optimistic Rollup** 的设计充分考虑了扩容性、安全性和去中心化这三个区块链的核心特性，是一个相对平衡的解决方案。虽然存在7天提款期这样的限制，但这是为了确保系统安全性的必要妥协。随着技术的发展，这些限制可能会在未来得到优化。



<!-- Content_END -->
