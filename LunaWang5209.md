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

### 2025.01.08

Sequencer 是 OP Stack 链的“交易调度员”，负责接收、排序并将 L2 的交易发布到 L1。如果它出问题，交易处理可能受影响，但用户仍然有办法解决。
Sequencer 故障主要分两种：
  完全停机：Sequencer 无法接收或处理交易，网络看起来“卡住”了。比如软件漏洞或云服务故障会导致这种情况。用户可以绕过它，直接向 L1 上的 OptimismPortal 合约提交交易，保证交易被处理。
  交提交故障：Sequencer 能接收和处理交易，但无法将交易发布到 L1。短时间内用户感受不明显，但如果问题持续，可能导致链状态回滚或重组。解决方法同样是通过 OptimismPortal 合约提交交易。
OptimismPortal 合约是关键：这是 L1 上的一个智能合约，允许用户直接提交 L2 交易，绕过 Sequencer。它支持所有类型的交易，并且这些交易在 L2 上看起来与 Sequencer 提交的交易完全一样。

### 2025.01.09
L2 扩容解决方案及成本分析

一、背景 
• 以太坊网络发展迅速（DeFi、NFT），但因低TPS和高Gas费用导致网络拥堵。 
• ETH 2.0扩容需时间，L2解决方案是中短期内解决以太坊低效率问题的关键。 

二、L2 优势： 
• 更高的速度和更低的费用； 
• 可能获得激励和空投； 
• 保持以太坊的安全性和完整性。      

三、L2 的主要技术方案 
1.Optimistic Rollup 
2.ZK Rollup 
3.Plasma 
4. Validium    

四、交易费用对比：
1.ZK Rollup 
• 链下成本：基于硬件（如生成零知识证明），每笔交易约0.001美元。 
• 链上成本：用于验证和状态更新，依赖以太坊Gas费用，但比直接在以太坊上交易便宜很多。 
• 总成本： 普通转账：0.07美元 ； 接收新地址：0.213美元 ；Swap交易：0.167美元   
ZK Rollup特点：
• 压缩效率极高，普通ETH转账TPS可提升100倍以上，复杂交易（如Uniswap）可提升400倍以上。 
• 随着EIP-4488等改进提案，成本可能下降至当前的1/5。  

2.zkPorter 
• 与ZK Rollup不同，数据可用性链下处理，大幅降低成本。 
• 交易成本约为1-3美分，适合高频、低成本的应用场景。  

3.Optimistic Rollup 
• 成本构成： L2执行费：基于交易使用的Gas量和L2 Gas价格； L1数据费：用于向以太坊提交数据，约占总费用的大部分。  
 • 特点：成本较ZK Rollup稍高，适合某些特定用例。  

4.Arbitrum 
• 成本依赖于具体交互方式，Gas机制和Optimism类似。 



### 2025.01.10
L2 是以太坊扩展的关键： 
• 提供更高的吞吐量； 
• 降低交易成本，改善用户体验； 
• 保留以太坊的安全性。   

方案优劣势： 
• ZK Rollup：交易成本低、安全性高、压缩效率优，适合大多数场景。 
• zkPorter：成本更低，适合高频低值交易。 
• Optimistic Rollup/Arbitrum：成本适中，但性能略逊于ZK Rollup。    未来更多应用将迁移到L2，推动区块链的大规模应用！

### 2025.01.11

评估Rollup成熟度的Stages框架
背景
Rollup是一种信任最小化的以太坊扩展方案，但初期通常依赖“训练轮”来进行系统更新和修复。
随着Rollup的发展，需逐步移除“训练轮”以实现完全去中心化。
L2BEAT基于Vitalik Buterin的提案，提出了一个三阶段框架，用于评估Rollup的成熟度。

Stages框架
Stage 0：完全训练轮
定义：Rollup由运营方完全控制。
要求：
1.项目自称为Rollup。
2.L2状态根在L1上发布。
3.数据在L1上提供可用性。
4.提供开源软件以从L1数据重建L2状态。

Stage 1：有限训练轮
定义：治理由智能合约主导，但仍有“安全委员会”应对潜在问题。
要求：
1.实施有效的证明系统（如欺诈证明或零知识证明）。
2.至少5名外部参与者可提交欺诈证明。
3.用户无需运营者协调即可退出。
4.用户在升级前至少有7天退出时间（排除安全委员会干预）。
5.安全委员会由至少8名成员组成，50%需为外部人员。

Stage 2：无训练轮
定义：完全由智能合约控制，去中心化且无需信任。
要求：
1.欺诈证明系统完全开放。
2.用户在升级前至少有30天退出时间。
3.安全委员会仅限于处理链上检测到的严重错误。

### 2025.01.12
请假


### 2025.01.13


### 2025.01.14


### 2025.01.15


### 2025.01.16


### 2025.01.17


### 2025.01.18


<!-- Content_END -->
