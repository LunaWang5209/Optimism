---
timezone: America/Chicago
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

# Alan Xin

1. Now: Web3 builder/investor Prev: CoinDesk Chinese, BanklessDAO

2. 你认为你会完成本次残酷学习吗？Yes.

## Notes

<!-- Content_START -->

### 2025.01.06

I've added some extended readings to this chapter.

## Layer2 扩容方案 的补充材料

### What is Bedrock?
Bedrock is a major upgrade and the codebase architecture for Optimism. Optimism uses Optimistic Rollup technology to improve transaction throughput and reduce costs while inheriting the security of Ethereum. The Bedrock upgrade represents a fundamental shift in how Optimism operates, aiming for improved performance, modularity, and Ethereum equivalence.

**I. Key Features of Bedrock**

1. Enhanced Modularity:
  - Bedrock introduces a modular design for the Optimism stack. This modularity allows the Optimism network to evolve rapidly and adapt to changing requirements while maintaining compatibility with Ethereum.
  - Each component in the stack can be upgraded independently, ensuring easier maintenance and innovation.

2. Ethereum Equivalence:
- Bedrock moves Optimism closer to Ethereum equivalence, meaning the L2 operates more like the Ethereum mainnet. This simplifies interactions with Ethereum-native tools, applications, and smart contracts.
- Developers can seamlessly deploy applications on Optimism using the same tools and code as they would on Ethereum.

3. Optimized Rollup Architecture:
- Bedrock improves the rollup mechanics, including batch submission and fraud proofing.
- Transaction batch processing is streamlined, reducing latency and ensuring faster finality for transactions.

4. Lower Costs:
- The new architecture optimizes data compression and storage, which significantly reduces the cost of transactions on Optimism.
- By leveraging Ethereum's calldata efficiency, Bedrock makes it cheaper to post transaction data on the Ethereum mainnet.

5. Improved Syncing and Performance:
- Syncing between Optimism and Ethereum is faster under Bedrock.
- Transaction throughput and node performance are enhanced to support a growing user base and developer ecosystem.

6. Multi-Proof System:
- Bedrock introduces support for multi-proof systems, paving the way for advanced fraud proofs and better security for the rollup.

**II. Why Is Bedrock Important?**
- Scalability: With reduced costs and improved performance, Bedrock strengthens Optimism's ability to handle a higher transaction volume, making Ethereum-based applications more accessible to users.
- Developer Friendly: The Ethereum equivalence ensures that developers do not need to learn a new framework to build or deploy on Optimism.
- Interoperability: Bedrock's modularity and Ethereum compatibility promote interoperability with other Layer 2 solutions and Ethereum-based applications.
- Ecosystem Growth: Lower transaction fees and improved performance make Optimism an attractive platform for decentralized applications (dApps), boosting user adoption and network activity.

**III. Bedrock and the OP Stack**
The OP Stack is a set of standardized, open-source components for building scalable blockchains. Bedrock is a flagship implementation of the OP Stack, showcasing its potential as a robust L2 solution. Other projects can use the OP Stack to create their own rollups, contributing to the broader modular blockchain ecosystem.
Bedrock signifies a leap forward for Optimism and demonstrates how Layer 2 solutions can evolve to provide scalable, cost-efficient, and user-friendly infrastructure while staying closely aligned with Ethereum's values.


### What is EIP-4844?
EIP-4844, also known as Proto-Danksharding, is a proposed Ethereum Improvement Proposal aimed at improving Ethereum's scalability, specifically for Layer 2 (L2) solutions such as rollups. It introduces blob-carrying transactions, a mechanism for handling large amounts of data more efficiently and at lower costs without permanently increasing the Ethereum blockchain's state size.

This proposal is a significant step toward full Danksharding, Ethereum's long-term vision for scalability through data sharding. EIP-4844 focuses on temporary data storage to support rollups and other scaling technologies, making transactions faster and cheaper for users.

**I. Key Features of EIP-4844**

1. Blob-Carrying Transactions:
  - EIP-4844 introduces a new type of transaction that carries blobs of data.
  - Blobs are large chunks of binary data designed to store rollup-related information.
  - These blobs are not stored permanently on the Ethereum blockchain but are instead available for a short period (e.g., a few weeks) to be processed by rollups.

2. Off-Chain Blob Storage:
- Blobs are stored off-chain, reducing the burden on the Ethereum blockchain's state.
- Validators and clients only need to verify the availability of these blobs for a limited time, ensuring data integrity while minimizing long-term storage requirements.

3. Lower Data Costs:
- The cost of including blob data in a transaction is significantly lower than the cost of storing data on-chain.
- This reduction in costs is a major benefit for L2 rollups, which rely on storing transaction data as calldata on Ethereum.

4. Improved Scalability for Rollups:
- Rollups (Optimistic Rollups and ZK Rollups) benefit from EIP-4844 because it provides a cost-effective way to publish their data to Ethereum.
- This enhances their throughput and reduces fees for end users.

5. Transition Toward Danksharding:
- EIP-4844 lays the groundwork for Danksharding, Ethereum’s full sharding design, which will implement multiple shard chains and significantly increase Ethereum’s data availability and scalability.
- Proto-Danksharding is a simpler, intermediate step to achieve some of the benefits of Danksharding without requiring the full sharding infrastructure immediately.

**II. Benefits of EIP-4844**

1. Lower Transaction Costs:
- By reducing the cost of storing rollup data, EIP-4844 helps bring down fees for rollup transactions, making Ethereum more affordable for users.
2. Better Scalability:
- The ability to handle large blobs of data without permanently increasing the blockchain size ensures Ethereum can support higher transaction volumes.
3. Rollup-Centric Ethereum (The "Rollup-Centric Roadmap"):
- Ethereum's scalability strategy focuses on rollups as the primary method for scaling. EIP-4844 directly enhances rollup efficiency, aligning with Ethereum's roadmap.
4. Minimal Impact on Ethereum Clients:
- The introduction of blobs is designed to minimize disruption to existing Ethereum clients while adding scalability improvements.

**III. Technical Overview of Blob Mechanics**

- Blob Size: Each blob is around 125 kB in size, optimized for storing rollup data.
- Data Availability Sampling (DAS): Validators ensure that blobs are available for the required period using data availability sampling techniques.
- Gas Cost: A new gas market for blob data is introduced, separate from Ethereum's normal gas mechanics, to ensure costs are predictable and fair.

**IV. Current Status of EIP-4844**

As of now:
- EIP-4844 is in development and under discussion in the Ethereum developer community.
- It is expected to be implemented in a future Ethereum upgrade (possibly in 2024–2025), following Ethereum's transition to Proof of Stake (PoS) and related upgrades.

**In Summary**

EIP-4844 is a critical milestone in Ethereum's scaling journey. By introducing blob-carrying transactions and enabling cheaper data availability, it strengthens the foundation for rollup-centric scalability and moves Ethereum closer to its long-term vision of being a highly scalable, efficient, and user-friendly blockchain.


### NOTES

### Block production

Have a mempool
- Tx submitted to sequencer are not censorship resistant because mempool is private.
- Tx can be submitted either directly to the sequencer or on L1's L2 block(in the second case, Tx is called deposits).

**Q:** 
Suppose the sequencer always follows the rules and doesn't commit any fraud, and the verifier keeps working to detect fraud but gets no incentives because no fraud is found. Would the verifier lose motivation to keep doing the verification work?

**A:** 
Yes, in the scenario where the sequencer always follows the rules and no fraud occurs, verifiers might lose motivation over time if they are not rewarded for their continuous efforts to monitor and validate transactions. This presents a potential challenge in systems like Optimistic Rollups, where fraud detection is a rare event. Verifiers still incur costs (e.g., computational resources, infrastructure) to monitor the sequencer, and without ongoing incentives, their participation could dwindle.

### Block execution
  
- Execution engine update using p2p network with other execution engines
- Rollup node derives L2 blocks from L1. (slower than the first one but censorship resistant)

### Bridging ETH or tokens between layers

- Moving from OP mainnet to Ethereum
- Withdrawal is finalized after the fault challenge period(a week on mainnet) ends.

**Q:** 
According to OP docs, the withdrawal from OP mainnet to Ethereum is finalized after the fault challenge period ends (a week on mainnet). Isn't one week too long for transactions to be finalized compared with traditional non-blockchain transactions?

**A:** 
Yes, the one-week challenge period for withdrawals from Optimism (OP) to Ethereum Layer 1 (L1) can feel long compared to traditional non-blockchain transactions, which are typically finalized almost instantly. This delay is a fundamental aspect of the Optimistic Rollup design, ensuring security through a fraud-proof mechanism. 

### Stage 的介绍

Framework to guid the progreassion of rollups from Stage 0 to Stage 2.

**Stage 0**
  - Call itself a rollup.
  - L2 state roots are posted on L1
  - Provide data availability on L1
  - Capable of reconstructing the rollup's state source

**Stage 1**
  - Use a proper proof system
  - at least  external actors that can submit a fraud proof. (Why 5?)
  - Users can exit without the operator's coordination
  - Users have at least 7days to exit in case of unwanted upgrades
  - Security council is properly set up

**Stage 2**
  - Fraud proof system is permissionless
  - Users have at least 30 days to exit in case of unwanted upgrades.
  - Security Council is restricted to act only due to errors detected on chain.
    
### 2024.07.12

<!-- Content_END -->
