# {stualan}

1. 一个web3技术学习者
2. 你认为你会完成本次残酷学习吗？会，学习op中的设计思想和一些治理相关的内容

## Notes

<!-- Content_START -->

### 2025.01.06

- 阅读[OP Rollup设计](https://docs.optimism.io/stack/rollup/overview)理念文档
---

## **Optimism Rollup 概述**

Optimism Rollup 是一种 Layer 2 扩展解决方案，旨在提高以太坊的可扩展性，同时保持与以太坊主网的高度安全性和兼容性。它通过将交易批量处理并压缩后提交到以太坊主网，显著降低了交易成本并提高了吞吐量。

---

### **核心概念**

1. **Rollup 技术**  
   - Rollup 是一种 Layer 2 扩展技术，将大量交易数据压缩后提交到以太坊主网。
   - 交易执行在链下进行，但数据存储在链上，确保安全性和透明性。
   - Optimism 使用 **Optimistic Rollup**，默认假设所有交易有效，除非有人提交欺诈证明。

2. **Optimistic Rollup 的特点**  
   - **低成本**：通过批量处理交易，减少以太坊主网的 Gas 费用。
   - **高吞吐量**：链下执行交易，显著提高交易处理速度。
   - **安全性**：依赖以太坊主网的安全性，通过欺诈证明机制确保交易有效性。

3. **欺诈证明（Fraud Proof）**  
   - 如果有人提交无效交易，其他节点可以生成欺诈证明，挑战该交易。
   - 挑战成功后，无效交易会被回滚，恶意行为者会受到惩罚。

4. **EVM 等效性**  
   - Optimism Rollup 完全兼容以太坊虚拟机（EVM），开发者可以无缝迁移以太坊 DApp。
   - 支持所有以太坊工具和基础设施（如 MetaMask、Truffle 等）。

---

### **Optimism Rollup 的架构**

1. **Sequencer（排序器）**  
   - 负责接收用户交易，排序并批量提交到以太坊主网。
   - 提供即时交易确认，优化用户体验。

2. **Verifier（验证者）**  
   - 验证链下交易的有效性，确保与以太坊主网状态一致。
   - 在发现无效交易时生成欺诈证明。

3. **数据可用性**  
   - 所有交易数据都存储在以太坊主网上，确保透明性和可验证性。
   - 即使 Layer 2 节点离线，用户也可以从主网恢复数据。

4. **跨链通信**  
   - 通过 **L1 和 L2 之间的消息传递**，实现资产和数据的跨链转移。
   - 用户可以将资产从以太坊主网存入 Optimism Rollup，或从 Rollup 提现到主网。


### **Optimism Rollup 的优势**

1. **低成本**  
   - 通过批量处理和压缩交易，显著降低 Gas 费用。
   - 适合高频交易和小额支付场景。

2. **高兼容性**  
   - 完全兼容以太坊 EVM，开发者无需修改代码即可迁移 DApp。
   - 支持现有以太坊工具和基础设施。

3. **安全性**  
   - 依赖以太坊主网的安全性，通过欺诈证明机制确保交易有效性。
   - 数据存储在链上，确保透明性和可验证性。

4. **用户体验**  
   - 提供即时交易确认，减少用户等待时间。
   - 支持跨链资产转移，方便用户操作。
---

### **Optimism Rollup 的挑战**

1. **挑战期延迟**  
   - 提现到以太坊主网需要等待挑战期结束（通常 7 天）。
   - 可能影响用户体验。

2. **中心化风险**  
   - Sequencer 目前由 Optimism 团队运营，存在一定的中心化风险。
   - 未来计划引入去中心化 Sequencer。

3. **欺诈证明复杂性**  
   - 欺诈证明机制需要复杂的实现和验证。
   - 可能增加开发和维护成本。

### 2025.01.07
---
### **Optimism Rollup 的工作流程**

1. **交易提交**  
   - 用户将交易发送到 Optimism Rollup 的 Sequencer。
   - Sequencer 对交易进行排序并生成批次。

2. **批次提交**  
   - Sequencer 将交易批次压缩后提交到以太坊主网。
   - 主网存储交易数据，确保数据可用性。

3. **状态更新**  
   - 交易在链下执行，生成新的状态根。
   - 状态根提交到以太坊主网，更新 Layer 2 状态。

4. **欺诈证明挑战期**  
   - 提交的状态根进入挑战期（通常为 7 天）。
   - 在此期间，任何人都可以提交欺诈证明，挑战无效交易。

5. **最终确认**  
   - 如果挑战期内无人挑战，状态根被最终确认。
   - 如果有挑战，以太坊主网会仲裁并决定是否回滚交易。
---

### 2025.01.08
Layer-2 扩容方案旨在解决以太坊主网的拥堵和高 Gas 费问题。目前主要有四种 Layer-2 解决方案，它们在交易成本、安全性、速度等方面各有优劣。以下分别介绍这四种方案的交易成本：

**1. Optimistic Rollup **

*   **工作原理：** 乐观 Rollup 将大量交易在链下打包和执行，然后将交易数据（calldata）和状态根发布到以太坊主链。它“乐观地”假设交易是有效的，并通过欺诈证明机制来处理无效交易。
*   **交易成本：**
    *   **L2 Gas 费（链下）：** 非常低，因为交易主要在链下执行。
    *   **L1 Gas 费（链上）：** 主要成本是 calldata 的 Gas 费，用于将压缩后的交易数据发布到以太坊主链。因此，L1 Gas 费受以太坊主链 Gas Price 的影响较大。
    *   **总 Gas 费：** `总 Gas 费 = L2 Gas 费 + L1 Gas 费`。总费用通常比以太坊主网低很多，但仍然会受到以太坊主网 Gas Price 的波动影响。
*   **影响 L1 Gas 费的因素：**
    *   **Calldata 大小：** 交易数据越多，calldata 越大，L1 Gas 费越高。
    *   **以太坊主链 Gas Price：** 主网 Gas Price 越高，L1 Gas 费越高。
    *   **批量处理效率：** 将更多 L2 交易打包成一个 L1 交易可以分摊 L1 Gas 费。
*   **代表项目：** Arbitrum、Optimism。

**2. ZK Rollup（零知识Rollup）**

*   **工作原理：** ZK Rollup 在链下执行交易，并生成一个简洁的零知识证明（zk-SNARK 或 zk-STARK），证明这些交易的有效性。这个证明会被发布到以太坊主链，验证者无需重新执行所有交易即可验证其有效性。
*   **交易成本：**
    *   **L2 Gas 费（链下）：** 也很低。
    *   **L1 Gas 费（链上）：** 主要成本是发布零知识证明的 Gas 费。虽然证明本身比 calldata 小得多，但生成证明的计算成本较高。
    *   **总 Gas 费：** 通常比 Optimistic Rollup 更低，尤其是在交易量较大时。
*   **优势：** 安全性更高，因为不需要等待期和欺诈证明。
*   **劣势：** 开发难度较高，通用性不如 Optimistic Rollup。
*   **代表项目：** zkSync、StarkNet。

**3. Validium**

*   **工作原理：** Validium 与 ZK Rollup 类似，也使用零知识证明来验证链下交易的有效性。但不同之处在于，Validium 将交易数据存储在链下，而不是像 ZK Rollup 那样存储在链上。
*   **交易成本：**
    *   **L2 Gas 费（链下）：** 非常低。
    *   **L1 Gas 费（链上）：** 极低，因为只需在链上发布证明，而无需发布交易数据。
*   **优势：** 交易成本最低。
*   **劣势：** 数据可用性存在一定风险，因为数据存储在链下，如果数据提供者出现问题，可能会导致用户无法访问自己的资产。
*   **适用场景：** 适合对安全性要求不高，但对成本非常敏感的应用，例如游戏、支付等。
*   **代表项目：** StarkEx。

**4. Plasma**

*   **工作原理：** Plasma 使用一种“子链”结构，将交易放在独立的子链上执行，并通过默克尔树将子链的状态根锚定到以太坊主链。
*   **交易成本：**
    *   **L2 Gas 费（链下）：** 较低。
    *   **L1 Gas 费（链上）：** 用于将子链的状态根提交到主链，成本相对较低。
*   **劣势：** 提款需要较长的等待期（挑战期），并且在某些情况下可能需要用户进行数据可用性证明，这会增加复杂性。
*   **应用受限：** 由于其固有的局限性，Plasma 的应用范围相对有限，主要用于简单的支付和代币转移。
*   **目前使用较少**

**四种方案的交易成本对比（大致排序，具体数值会根据网络状况变化）：**

Validium < ZK Rollup < Optimistic Rollup < 以太坊主网

### 2025.01.09
通过阅读 [资料](https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe) 构想经过三个阶段
- Stage 0 — Full Training Wheels: At this stage, the rollup is effectively run by the operators. Still, there is an source-available software that allows for the reconstruction of the state from the data posted on L1, used to compare state roots with the proposed ones.
- Stage 1 — Limited Training Wheels: In this stage, the rollup transitions to being governed by smart contracts. However, a Security Council might remain in place to address potential bugs. This stage is characterized by the implementation of a fully functional proof system, decentralization of fraud proof submission, and provision for user exits without operator coordination. The Security Council, comprised of a diverse set of participants, provides a safety net, but its power also poses a potential risk.
- Stage 2 — No Training Wheels: This is the final stage where the rollup becomes fully managed by smart contracts. At this point, the fraud proof system is permissionless, and users are given ample time to exit in the event of unwanted upgrades. The Security Council’s role is strictly confined to addressing soundness errors that can be adjudicated on-chain, and users are protected from governance attacks.
### 2025.01.10
### 2025.01.11
### 2025.01.12
### 2025.01.13
### 2025.01.14
### 2025.01.15
### 2025.01.16
### 2025.01.17
### 2025.01.18
<!-- Content_END -->
