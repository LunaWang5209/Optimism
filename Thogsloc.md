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

### 2025.01.07

OP Stack 是支持 OP Rollup 的基础架构和协议栈，为 OP Rollup 提供了必要的组件和功能，包含：

桥接（Bridges）
允许不同区块链之间的交互。
信使（Messengers）：用于在链之间传递消息。
存款（Deposits）：用户将资产转移到Optimism链的过程。
取款（Withdrawals）：用户从Optimism链提取资产的过程。
担保的 gas 费市场（Guaranteed Gas Market）：确保交易费用的透明和可预测性。
提案（Proposals）：用户可以提交改进建议。

执行引擎（Execution Engine）
负责处理和执行交易的核心组件。

汇总节点（Rollup Node）
用于聚合和验证交易的节点。
P2P 通信：节点之间的点对点通信。
派生（Derivation）：如何从 L1 链派生出 L2 链的状态。

故障证明（Fault Proof）
确保交易安全性和有效性。
Cannon Fault Proof VM：用于验证交易的虚拟机。

预编译（Precompiles）、预部署（Predeploys）、预安装（Preinstalls）
涉及到在 Optimism 链上预先配置的合约和功能。

超级链配置（Superchain Configuration）
允许用户根据需求调整协议参数。

治理代币（Governance Token）
描述 Optimism 的治理机制，用户如何参与决策。

### 2025.01.08

Optimism OP Stack 的 L2 链衍生规范

L2 链衍生是指从 L1 链(以太坊主网)推导 L2 链的过程。核心思想是:
每个 L1 区块都映射到一个"sequencing epoch"(序列化纪元)
每个 L2 区块都属于且仅属于一个 epoch
L2 链的每个状态和交易都可以从 L1 链的数据中确定性地推导出来

关键术语
Sequencing Epoch: 序列化纪元,一个 L1 区块对应的 L2 区块集合
L1 Origin: L2 区块对应的 L1 源区块
Batcher Transaction: 批处理交易,用于在 L1 上提交 L2 链的数据
Channel: 多个批次的压缩集合
Frame: Channel 的数据分片

设计目标
确保 L2 链的数据完全由 L1 链推导
保证链的确定性和可验证性
支持高效的跨链数据传输

例子:
假设以太坊主网(L1)每 12 秒出一个区块,而 Optimism L2 链每 2 秒出一个区块。那么一个 L1 区块通常会对应 6 个 L2 区块。
这些 L2 区块将包含:
L1 属性交易
用户存款交易
常规sequencer交易

L2 链衍生管道架构
Optimism 设计了一个八阶段的流水线架构来实现 L2 链的衍生:

L1 遍历 (L1 Traversal)
读取下一个 L1 区块头
更新系统配置
为后续阶段准备数据

L1 检索 (L1 Retrieval)
从 L1 区块中提取 Batcher 交易
验证 Batcher 交易的合法性
将交易数据传递给下一阶段

帧队列 (Frame Queue)
缓存并解码单个数据交易
将解码后的通道帧传递给下一阶段

通道银行 (Channel Bank)
管理和缓存通道数据
读取已准备好的通道
解压缩通道数据

通道阅读器 (Channel Reader)
从解压缩的数据中解析批次
准备批次数据用于后续处理

批次队列 (Batch Queue)
对批次进行时间戳重排序
处理批次间的时间间隙
生成必要的空批次

Payload 属性衍生 (Payload Attributes Derivation)
将批次转换为 Payload 属性
更新系统配置
准备区块构建所需的详细信息

引擎队列 (Engine Queue)
将 Payload 属性发送到执行引擎
管理 L2 链的安全头、最终头
处理区块的实际构建和确认

关键设计原则

数据流向
数据从流水线外部流向内部
处理顺序是反向的,从最内层开始

状态管理
每个阶段维护自己的内部状态
跟踪已处理的 L1 区块引用

灵活性
支持正常同步和历史重放
能处理 L1 链的重组事件

批次处理的关键特征
支持多通道、多帧交错
帧不需要按顺序传输
单个 Batcher 交易可以携带多个通道的帧

安全机制
区块安全级别:
Unsafe L2 块: 尚未从 L1 衍生
Safe L2 块: 可从当前规范 L1 链衍生
Finalized L2 块: 可从最终确定的 L1 部分衍生

网络升级自动化
通过特殊的自动化交易实现网络升级
在特定区块插入必要的合约变更交易

### 2025.01.09

交易列表推导
对于每个 L2 区块的创建，都遵循严格的交易列表构建规则：

交易类型及顺序
交易必须按照以下顺序包含：

存款交易 (Deposited Transactions)
L1 属性存款交易：从 L1 区块头读取
用户存款交易：从 L1 区块的收据中读取（仅在 epoch 的第一个 L2 区块）

网络升级自动化交易
在特定区块插入特殊交易
用于自动执行网络升级

排序交易 (Sequenced Transactions)
常规的 L2 用户签名交易
来自 sequencer 批次
网络升级自动化交易示例

以 Ecotone 升级为例：
Ecotone 升级交易详细信息
目标地址：0x420000000000000000000000000000000000000F（Gas Price Oracle 代理）
Mint 金额：0
交易值：0
Gas 限制：50,000
特殊数据：包含升级合约地址的调用

关键设计原则
确定性
交易列表完全由 L1 数据确定性推导
保证 L2 链的一致性和可验证性

严格顺序
交易必须按照预定义顺序排列
确保网络升级和状态转换的可预测性

灵活性
支持动态网络升级
允许在不修改执行层的情况下进行协议升级

网络升级机制
Optimism 设计了一个灵活的网络升级框架：
通过特殊交易自动执行升级
最小化对现有系统的侵入
支持渐进式协议演进

升级流程
识别升级时机
准备自动化交易
在特定区块插入升级交易
执行合约代理更新或部署

### 2025.01.09

OP Stack 的安全机制基于多层防御策略。

1. 信任最小化 (Trust Minimization)
通过 L1 锚定实现最小化信任
所有 L2 状态都可以在 L1 上验证
用户资产始终可以通过 L1 提取

2. 欺诈证明机制 (Fraud Proof Mechanism)
允许任何人挑战不正确的 L2 状态根
提供经济激励来维护系统诚实性
欺诈证明窗口通常为 7 天

关键安全组件 (Key Security Components)

挑战窗口 (Challenge Window)
7 天时间让任何人验证和挑战状态
经济博弈理论确保诚实行为

保证金机制 (Deposit Mechanism)
挑战者和防御者都需要质押保证金
错误的挑战将导致保证金被没收

多重签名管理 (Multi-Signature Management)
关键系统合约使用多签治理
降低单点失败风险

安全威胁防御 (Security Threat Defense)

L1 锚定防御 (L1 Anchoring Defense)
所有 L2 状态根发布到 L1
确保状态可追溯和可验证
任何不一致都可被快速发现和纠正

排序器安全 (Sequencer Security)
去中心化排序器集合
轮换机制防止单点攻击
经济激励确保诚实行为

风险缓解策略 (Risk Mitigation Strategies)

紧急暂停机制 (Emergency Pause Mechanism)
发现严重漏洞可立即暂停系统
管理员多签可触发

渐进式升级 (Incremental Upgrade)
分阶段部署新功能
每个阶段都有充分的安全审计

经济博弈 (Economic Game)
攻击成本高于收益
通过保证金和激励机制确保系统安全

技术防御细节 (Technical Defense Details)

状态根验证 (State Root Verification)
每个区块状态根都需要严格验证
不匹配将触发挑战流程

交易重放保护 (Transaction Replay Protection)
防止重放攻击
使用唯一随机数和签名验证

合约升级安全 (Contract Upgrade Security)
代理合约模式
升级需要多重签名批准

### 2025.01.11

OP Stack 标准桥接
核心功能概述 (Core Function Overview)
标准桥接是 OP Stack 中实现跨域资产转移的关键组件。

主要职责 (Primary Responsibilities)
允许 ETH 和 ERC20 代币在不同域间转移
提供统一的跨域资产桥接标准接口
支持 L1 原生和 L2 原生代币转移

关键合约地址 (Key Contract Addresses)
L2 标准桥接合约地址：0x4200000000000000000000000000000000000010

接口定义 (Interface Definition)

关键事件 (Key Events)
solidity

// ERC20 桥接完成事件 (ERC20 Bridge Finalization Event)  
event ERC20BridgeFinalized(  
    address indexed localToken,     // 本地代币地址 (Local Token Address)  
    address indexed remoteToken,    // 远程代币地址 (Remote Token Address)  
    address indexed from,            // 发送地址 (Sender Address)  
    address to,                      // 接收地址 (Recipient Address)  
    uint256 amount,                  // 转移金额 (Transfer Amount)  
    bytes extraData                  // 额外数据 (Extra Data)  
);  

// ETH 桥接发起事件 (ETH Bridge Initiation Event)  
event ETHBridgeInitiated(  
    address indexed from,            // 发送地址 (Sender Address)  
    address indexed to,              // 接收地址 (Recipient Address)  
    uint256 amount,                  // 转移金额 (Transfer Amount)  
    bytes extraData                  // 额外数据 (Extra Data)  
);  

核心方法 (Core Methods)
solidity

// ERC20 代币桥接方法 (ERC20 Token Bridge Method)  
function bridgeERC20(  
    address _localToken,     // 本地代币地址 (Local Token Address)  
    address _remoteToken,    // 远程代币地址 (Remote Token Address)  
    uint256 _amount,         // 转移金额 (Transfer Amount)  
    uint32 _minGasLimit,     // 最小 Gas 限制 (Minimum Gas Limit)  
    bytes memory _extraData  // 额外数据 (Extra Data)  
) external;  

// ETH 桥接方法 (ETH Bridge Method)  
function bridgeETH(  
    uint32 _minGasLimit,     // 最小 Gas 限制 (Minimum Gas Limit)  
    bytes memory _extraData  // 额外数据 (Extra Data)  
) payable external;  

跨域转移流程 (Cross-Domain Transfer Process)

ERC20 代币转移步骤 (ERC20 Token Transfer Steps)
确保目标域存在对应的可铸造代币合约
调用 bridgeERC20 方法
触发跨域资产转移事件
目标域合约完成资产铸造

ETH 转移流程 (ETH Transfer Process)
调用 bridgeETH 方法
锁定源域资产
在目标域解锁或铸造等量资产

升级能力 (Upgrade Capabilities)
L1 和 L2 标准桥接合约支持代理升级
使用可升级代理模式
确保协议可平滑演进

安全性考虑 (Security Considerations)
使用标准化接口减少安全风险
支持最小 Gas 限制，防止 DoS 攻击
额外数据提供灵活性
事件日志提供完整转移追踪

兼容性 (Compatibility)
保留向后兼容的 Legacy API
确保现有应用无缝迁移
支持多种代币标准

关键限制 (Key Limitations)
需要目标域存在对应的可铸造代币合约
转移受 Gas 限制和桥接合约规则约束

### 2025.01.12

跨域消息传递（Cross Domain Messengers）
跨域消息传递是 OP Stack 中实现不同域（L1 和 L2）间通信的关键机制。

核心合约 (Core Contracts)
L1CrossDomainMessenger
L2CrossDomainMessenger
预部署地址：0x4200000000000000000000000000000000000007

消息传递流程 (Message Passing Process)
发送消息 (Sending Messages)
solidity
function sendMessage(  
    address _target,     // 目标地址 (Target Address)  
    bytes memory _message, // 消息内容 (Message Content)  
    uint32 _minGasLimit   // 最小 Gas 限制 (Minimum Gas Limit)  
) external payable;  
中继消息 (Relaying Messages)
solidity
function relayMessage(  
    uint256 _nonce,        // 消息随机数 (Message Nonce)  
    address _sender,       // 发送者地址 (Sender Address)  
    address _target,       // 目标地址 (Target Address)  
    uint256 _value,        // 转账金额 (Transfer Value)  
    uint256 _minGasLimit,  // 最小 Gas 限制 (Minimum Gas Limit)  
    bytes memory _message  // 消息内容 (Message Content)  
) external payable;  

消息版本管理 (Message Version Management)
版本 0
编码方式：abi.encodeWithSignature("relayMessage(address,address,bytes,uint256)")
包含：目标地址、发送者、消息、随机数
版本 1
编码方式：abi.encodeWithSignature("relayMessage(uint256,address,address,uint256,uint256,bytes)")
包含：随机数、发送者、目标地址、转账值、Gas限制、消息数据

关键事件 (Key Events)
solidity
event SentMessage(  
    address indexed target,    // 目标地址 (Target Address)  
    address sender,            // 发送者 (Sender)  
    bytes message,             // 消息内容 (Message Content)  
    uint256 messageNonce,      // 消息随机数 (Message Nonce)  
    uint256 gasLimit           // Gas 限制 (Gas Limit)  
);  

event RelayedMessage(  
    bytes32 indexed msgHash    // 消息哈希 (Message Hash)  
);  

安全与升级 (Security and Upgradability)
升级机制 (Upgrade Mechanism)
使用可升级代理合约
支持消息版本动态更新

安全特性 (Security Features)
成功/失败消息哈希追踪
消息重放保护
最小 Gas 开销计算

跨域通信流程 (Cross-Domain Communication Process)

L1 到 L2
    
用户在 L1 发送消息
自动中继到 L2
用户在 L1 支付 Gas

L2 到 L1

用户在 L2 发起提现
证明提现
等待最终确认窗口
在 OptimismPortal 上完成提现

最佳实践 (Best Practices)
始终指定足够的 Gas 限制
验证消息发送和中继状态
处理可能的失败场景
遵循版本兼容性

### 2025.07.12

<!-- Content_END -->
