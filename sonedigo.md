---
timezone: Asia/Shanghai
---

> 请在上边的 timezone 添加你的当地时区，这会有助于你的打卡状态的自动化更新，如果没有添加，默认为北京时间 UTC+8 时区
> 时区请参考以下列表，请移除 # 以后的内容


timezone: Asia/Shanghai


---

# {Harris Lee}

1. 自我介绍

大家好，我是Harris Lee，一位对OP Layer 2的发展感兴趣的教师，希望可以学习并传播ETH&OP 生态
2. 你认为你会完成本次残酷学习吗？

我为什么要认为不会呢？肯定是会的，希望最后能学下来并传播推广

## Notes

<!-- Content_START -->

### 2025.01.01

笔记内容

测试一下PR
### 2024.01.02

### 2024.01.06

笔记内容：
今天学习的内容是Optimism的overview
Firstly, Optimism is a Layer 2 scaling solution for Ethereum. The idea of Optimism rollups is to create a new type of blockchain that allows for faster transactions and lower fees than traditional Ethereum, which is using EIP-4844 blobs.

Secondly, Optimism block production is managed by the sequencer. The sequencer will provide the following services:
1. Providing transaction confirmations and state updates
2. Constructing and executing L2 blocks
3. Submitting user transcations to L1

The sequencer does have a mempool, similar to Ethereum.

Transactions get to the sequencer in two ways: 
1. Transactions submitted directly to the sequencer. But these transactions cannot be made censorship-resistant since only the sequencer knows them
2. Transcations deposit to L1, which are included in the chain in the apporpriate L2 block. It provides OP mainnet with L1 Ethereum-level censorship resistance. For the moment, The Optimism Foundation runs the only block producer on OP mainnet.

Block execution receives blocks using two mechanisms:

1.The execution engine can update itself using peer to peer network with other execution engines.
2.rollup node derives the L2 blocks from L1.

OP also could be thinking as bridging ETH or tokens between layers

OP is designed for users sending arbitrary messages between smart contracts on L2 and the underlying L1

Moving from Ethereum to OP mainnet called "deposit", meanwhile, moving from OP mainnet to Ethereum called "withdrawal"

Fault proofs:

When a state commitment is challenged, the commitment can  be invalidated through a "fault-proof" process. This process wil replace the invalidated state commitment with a new one. A successful challenge does not roll back OP Mainnet itself, only the published commitments about the state of the chain. The order of transactions and the state of Op mainnet is unchanged by a fault-proof challenge.

<!-- Content_END -->
