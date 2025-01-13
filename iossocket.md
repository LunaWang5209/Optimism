---
timezone: Asia/Shanghai
---

# iossocket

1. 自我介绍： web3 爱好者，熟悉前端开发
2. 你认为你会完成本次残酷学习吗？会

## Notes

<!-- Content_START -->

### 2025.01.06

#### Overview of Optimism Layer 2 Scaling Solution

Optimism is a Layer 2 scaling solution for Ethereum that aims to increase the transaction throughput of the Ethereum network while reducing transaction fees, thereby enhancing the user experience. Below is a detailed explanation of the Optimism Layer 2 scaling approach:

1. Background and Purpose

   While Ethereum is a powerful network, it often faces congestion and high transaction fees during peak times. Layer 2 solutions like Optimism emerged to alleviate the burden on the main chain by processing a portion of transactions off-chain.

2. How It Works

   Optimism is based on a technology called "Optimistic Rollups." Here’s how it operates:

- Optimistic Assumption: Optimism assumes that most transactions are valid, therefore it does not immediately verify every transaction. This approach reduces the computational demands for validating transactions on-chain.

- Batch Processing of Transactions: Users’ transactions are batch processed and submitted to the Ethereum main chain in a rollup format. This means that multiple transactions are combined into a single transaction, saving space and reducing costs.

- Fraud Proof Mechanism: If someone questions the validity of a transaction, they can submit a fraud proof that triggers a verification process for that specific transaction. This ensures that even with the optimistic assumption, the security of the network is maintained.

3. Advantages

- Increased Throughput: Optimism significantly increases the transaction processing ability of the network, supporting thousands of transactions per second.

- Reduced Transaction Fees: By alleviating the load on the main chain, users can enjoy lower transaction fees when trading on the Optimism chain.

- Compatibility: Optimism supports existing Ethereum tools and decentralized applications (DApps), allowing developers to easily migrate their applications to Optimism.

4. Limitations and Challenges

- Latency Issues: Due to the optimistic assumption, the confirmation time for transactions may be slightly slower than on the main chain, especially when fraud proofs are required.

- Security Considerations: Although optimistic rollups are theoretically secure, they rely on adequate economic incentives and the honesty of network participants. Therefore, the security of the network partially depends on user behavior.

5. Conclusion

   By moving transaction processing off-chain, Optimism provides an effective way to scale Ethereum's capabilities. As a Layer 2 solution, it offers higher transaction speeds and lower fees while maintaining compatibility with the main chain. As the Ethereum ecosystem continues to grow, Optimism and similar scaling solutions will play a critical role in enhancing blockchain performance.

### 2025.01.07

#### Bridging Tokens Between L1 and L2

Purpose of Design: Optimism is designed to allow users to send arbitrary messages between smart contracts on Layer 2 (such as OP Mainnet and OP Sepolia) and the underlying Layer 1 (Ethereum mainnet and Sepolia). This capability enables the transfer of ETH or tokens (including ERC20 tokens) between the two networks. The specific mechanisms of communication differ depending on the direction in which messages are sent.

#### Functionality of the Standard Bridge

On the OP Mainnet, users can utilize the Standard Bridge functionality to perform the following actions:

1. Deposit tokens from Ethereum (L1) to OP Mainnet (L2).
2. Withdraw the same tokens from OP Mainnet (L2) back to Ethereum (L1).

#### Moving from OP Mainnet to Ethereum

The process of withdrawing from OP Mainnet (L2) to Ethereum consists of three stages:

1. Initialize Withdrawal: This is done by initiating a withdrawal operation through an L2 transaction.

2. Wait for Output Root Submission: Users must wait for the next output root to be submitted to L1. This process can be monitored using the SDK. Users are required to submit a withdrawal proof using proveWithdrawalTransaction. This new step allows for off-chain monitoring of withdrawals, making it easier to identify incorrect withdrawals or output roots, thereby protecting users on OP Mainnet from various potential bridge vulnerabilities.

3. Finalize Withdrawal: After the fault challenge period ends (one week on the mainnet, a shorter time on the test network), the withdrawal operation will be finalized.

#### Summary

In summary, Optimism provides a mechanism through the Standard Bridge that allows users to effectively transfer ETH and tokens between the Ethereum mainnet (L1) and OP Mainnet (L2). The deposit and withdrawal mechanisms enable users to flexibly convert assets while ensuring security.

### 2025.01.08

#### Fraud Proofs and the Challenge Window in Optimism Rollup

The **challenge window** for fraud proofs occurs on **L1 (Ethereum Mainnet)**. This is a key design feature of Optimism Rollup (and other similar optimistic rollup solutions), aimed at ensuring the correctness of L2 state transitions.

#### Why Does the Challenge Window Happen on L1?

1. **Security**:

   - L1 (Ethereum Mainnet) offers higher security and decentralization. Handling fraud proofs on L1 ensures that the challenge process is not affected by potential centralization or malicious behavior on L2.

2. **Data Availability**:

   - L2 transaction data and state roots are periodically submitted to L1. Verifiers can access this data on L1 to check whether the state transitions submitted by the Sequencer are correct.

3. **Finality**:
   - L1 serves as the ultimate arbitration layer. If the Sequencer submits an incorrect state transition, verifiers can initiate a challenge on L1 and execute the fraud proof logic there, ensuring that the incorrect state is corrected.

#### How the Challenge Window Works

1. **State Submission**:

   - The Sequencer submits batches of L2 transactions and state roots to L1.

2. **Challenge Period Begins**:

   - After submission, a fixed challenge window (typically 7 days) opens. During this period, anyone can verify whether the state transitions submitted by the Sequencer are correct.

3. **Fraud Proof**:

   - If a verifier detects that the Sequencer has submitted an incorrect state root, they can initiate a challenge on L1 and provide a fraud proof.
   - A fraud proof typically includes:
     - The problematic batch of transactions.
     - Evidence that the Sequencer executed certain transactions incorrectly.

4. **Arbitration**:

   - Smart contracts on L1 will verify the fraud proof. If the proof is valid, the state root submitted by the Sequencer will be rejected, and the incorrect state transition will be rolled back.

5. **Penalization**:
   - If the Sequencer is proven to have submitted an incorrect state transition, they may be penalized (e.g., their staked collateral may be slashed).

#### Summary

The **challenge window** for fraud proofs occurs on L1 (Ethereum Mainnet) to leverage L1's security and decentralization, ensuring the correctness of L2 state transitions. The existence of a challenge window is a core mechanism of optimistic rollups, using economic incentives and cryptographic proofs to ensure that the Sequencer cannot act maliciously or submit incorrect state transitions.

### 2025.01.09

#### Comparison of Optimism, StarkNet, and Scroll

Optimism, StarkNet, and Scroll are all Layer 2 solutions for Ethereum, each offering distinct approaches to enhancing scalability, security, and developer experience. Here's a concise comparison of these platforms:

#### Optimism

- **Technology**: Uses Optimistic Rollups, which batch transactions off-chain and post them on-chain. Transactions are assumed valid unless challenged.
- **EVM Compatibility**: Fully compatible with Ethereum's Virtual Machine (EVM), allowing seamless deployment of existing smart contracts.
- **Governance**: Features a token-based governance model with the OP token, allowing holders to vote on proposals.
- **Ecosystem**: Has a well-established ecosystem with a variety of decentralized applications (dapps) already integrated.
- **Transaction Finality**: Offers cheaper fees than Ethereum but has a slower finality due to the challenge period.

#### StarkNet

- **Technology**: Employs ZK-Rollups (StarkRollups) using STARKs, providing faster transaction finality and enhanced privacy through zero-knowledge proofs.
- **EVM Compatibility**: Not fully EVM compatible, requiring developers to adapt to a new environment and potentially different programming languages.
- **Governance**: Utilizes its own token, STRK, though specific governance details may vary.
- **Ecosystem**: Still growing, with a focus on high-performance and privacy-centric applications.
- **Transaction Finality**: Offers quicker finality compared to Optimism due to the absence of a challenge period.

#### Scroll

- **Technology**: Also uses ZK-Rollups, aiming for EVM equivalence to ensure full compatibility with Ethereum's Virtual Machine.
- **EVM Compatibility**: Fully compatible with EVM, allowing developers to migrate existing contracts without changes.
- **Governance**: Details on governance are less clear, but it may follow a similar token-based model.
- **Ecosystem**: Relatively new, with an emerging ecosystem focused on ease of migration for Ethereum dapps.
- **Transaction Finality**: Promises fast finality with the benefits of ZK-Rollups, though still in developmental phases.

#### Summary

- **Optimism** is ideal for developers seeking EVM compatibility and an established ecosystem, despite slower finality.
- **StarkNet** offers faster, more private transactions but requires adaptation to a new development environment.
- **Scroll** aims to provide the best of both worlds with EVM equivalence and ZK-Rollup efficiency, though it is still evolving.

Each solution has its strengths and trade-offs, and the choice depends on the specific needs of developers and users, such as transaction speed, privacy, and ease of deployment.

### 2025.01.10

#### Rollup Maturity Framework: A Three-Stage Approach

In the rapidly evolving blockchain landscape, **Rollups** have emerged as a key solution for scaling Ethereum while maintaining trust minimization. However, the development of Rollups often involves an initial phase of centralized control, referred to as "training wheels," which allows for system updates and bug fixes in a controlled environment. To guide the transition from centralized control to full decentralization, a **three-stage framework** has been introduced to evaluate the maturity of Rollups.

#### **Background**

- **Rollups** are Layer 2 scaling solutions that bundle transactions off-chain and post proofs on Ethereum to enhance scalability.
- Early-stage Rollups rely on centralized components (training wheels) for flexibility and security, but these must eventually be removed to achieve full decentralization and inherit Ethereum's security properties.
- The framework aims to provide a clear roadmap for Rollups to progress toward trust minimization and decentralization.

#### **The Three Stages of Rollup Maturity**

#### **Stage 0 — Full Training Wheels**

- **Characteristics**: The Rollup is operated by centralized entities, but open-source software allows state reconstruction from Layer 1 (L1) data.
- **Requirements**:
  1. The project self-identifies as a Rollup.
  2. L2 state roots are posted on L1.
  3. Data Availability (DA) is ensured on L1.
  4. Open-source software is available to reconstruct the L2 state from L1 data.

#### **Stage 1 — Limited Training Wheels**

- **Characteristics**: The Rollup transitions to smart contract governance, but a **Security Council** remains to address potential bugs.
- **Requirements**:
  1. A proper proof system (e.g., fraud proofs or validity proofs) is implemented.
  2. At least 5 external actors can submit fraud proofs.
  3. Users can exit without operator coordination.
  4. Users have at least 7 days to exit in case of unwanted upgrades.
  5. A Security Council is properly set up (e.g., multisig with 8+ members, 50% consensus threshold, and at least half external participants).

#### **Stage 2 — No Training Wheels**

- **Characteristics**: The Rollup is fully governed by smart contracts, with no centralized control.
- **Requirements**:
  1. The fraud proof system is permissionless (open to all participants).
  2. Users have at least 30 days to exit in case of unwanted upgrades.
  3. The Security Council can only act on adjudicable on-chain errors (e.g., soundness bugs).

#### **Key Components of the Framework**

- **Data Availability (DA)**: Ensures all necessary data for state reconstruction is available on L1.
- **Fraud Proofs**: Mechanisms to dispute invalid state transitions (for Optimistic Rollups) or verify validity proofs (for ZK-Rollups).
- **Security Council**: A multisig-based safeguard to address critical bugs, with power diminishing as the Rollup matures.
- **Exit Mechanisms**: Guarantees that users can withdraw their assets independently, even in adverse scenarios.

#### **Significance of the Framework**

- **Clear Roadmap**: Provides Rollup projects with a structured path to achieve decentralization and trust minimization.
- **Risk Assessment**: Helps users and developers evaluate the security and maturity of Rollups.
- **Community Engagement**: Encourages discussions around Rollup development and incentivizes projects to prioritize security and decentralization.

#### **Future Directions**

- The framework will evolve based on community feedback and new technical developments.
- It aims to serve as a reference point for Rollup projects to align their roadmaps with the goal of being "secured by Ethereum."

#### **Conclusion**

The three-stage framework offers a comprehensive approach to evaluating Rollup maturity, from centralized control (Stage 0) to full decentralization (Stage 2). By defining clear requirements for each stage, it guides Rollup projects toward achieving Ethereum-level security and trust minimization, while fostering informed discussions within the community.

### 2025.01.11

#### Optimism Tokenomics

Optimism's Tokenomics primarily revolves around its governance token, OP. Below are the key points:

#### 1. **Token Distribution**

The OP token distribution plan is as follows:

- **Ecosystem Fund**: 25% allocated to support ecosystem development.
- **Core Contributors**: 19% allocated to the core development team.
- **Investors**: 17% allocated to early investors.
- **Airdrops**: 19% distributed to community members via airdrops.
- **RetroPGF**: 20% allocated for Retroactive Public Goods Funding.

#### 2. **Governance**

OP tokens are used for governing the Optimism network. Holders can participate in proposals, voting, and other decision-making processes.

#### 3. **Airdrops**

Optimism rewards early users and community members through airdrops. The first airdrop distributed 5% of the total supply, with more airdrops planned in the future.

#### 4. **RetroPGF**

RetroPGF (Retroactive Public Goods Funding) aims to reward projects that contribute to the ecosystem. 20% of the tokens are allocated for this program.

#### 5. **Inflation Mechanism**

OP tokens have an inflation mechanism, though the specifics are not fully disclosed. It is expected that the inflation rate will gradually decrease over time.

#### 6. **Use Cases**

OP tokens are primarily used for:

- **Governance**: Participating in network decision-making.
- **Incentives**: Rewarding users and developers.
- **Fee Payment**: Potentially used for transaction fees in the future.

#### 7. **Total Supply**

The total supply of OP tokens is 4.29 billion, with an initial circulating supply of approximately 274 million tokens.

#### Summary

Optimism's Tokenomics is designed to drive ecosystem growth and incentivize community participation through mechanisms such as token distribution, governance, airdrops, and RetroPGF.

### 2025.01.12

#### Layer 2 Scaling Solutions

Layer 2 scaling solutions are designed to address the scalability issues of blockchain networks like Ethereum. Below are some mature Layer 2 scaling solutions:

#### 1. **Rollups**

Rollups are currently the most popular Layer 2 scaling solutions, divided into two types:

- **Optimistic Rollups**

  - **Principle**: Assume all transactions are valid by default but allow validators to challenge and submit fraud proofs during a dispute period.
  - **Advantages**: High compatibility, supports general-purpose smart contracts.
  - **Representative Projects**: Optimism, Arbitrum.

- **ZK-Rollups (Zero-Knowledge Rollups)**
  - **Principle**: Use zero-knowledge proofs (ZK Proofs) to verify transaction validity, with compressed data submitted to the main chain.
  - **Advantages**: High security, no waiting period for withdrawals.
  - **Representative Projects**: zkSync, StarkNet, Loopring.

#### 2. **State Channels**

- **Principle**: Users conduct multiple transactions off-chain and submit the final result to the main chain.
- **Advantages**: Ideal for high-frequency, low-value transactions with minimal latency.
- **Disadvantages**: Not suitable for complex smart contract scenarios.
- **Representative Projects**: Lightning Network (Bitcoin), Raiden Network (Ethereum).

#### 3. **Plasma**

- **Principle**: Create child chains to handle transactions, with periodic state commitments to the main chain.
- **Advantages**: Suitable for specific use cases (e.g., payments).
- **Disadvantages**: Data availability issues and complex exit mechanisms.
- **Representative Projects**: OMG Network.

#### 4. **Validium**

- **Principle**: Similar to ZK-Rollups but stores data off-chain.
- **Advantages**: Higher throughput and lower costs.
- **Disadvantages**: Relies on data availability, slightly lower security than ZK-Rollups.
- **Representative Projects**: Immutable X.

#### 5. **Sidechains**

- **Principle**: Independent blockchains connected to the main chain via two-way bridges.
- **Advantages**: High flexibility and customizability.
- **Disadvantages**: Security depends on the sidechain's consensus mechanism.
- **Representative Projects**: Polygon PoS (formerly Matic Network), Skale.

#### 6. **Hybrid Solutions**

Some projects combine multiple Layer 2 technologies to optimize performance:

- **Polygon**: Supports various scaling solutions, including Polygon PoS, Polygon Hermez (ZK-Rollup), and Polygon Miden (STARK-based).
- **Arbitrum Nitro**: Combines Optimistic Rollup with WASM technology to enhance performance.

#### 7. **Optimistic Chains**

- **Principle**: Similar to Optimistic Rollups but uses an independent consensus mechanism.
- **Representative Projects**: Boba Network.

#### Summary

The most mature Layer 2 scaling solutions are **Rollups**, particularly **Optimistic Rollups** and **ZK-Rollups**. Other solutions like state channels, Plasma, and sidechains also play a role in specific scenarios. As technology evolves, more hybrid solutions and innovative approaches are expected to emerge.

<!-- Content_END -->
