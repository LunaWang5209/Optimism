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

# {183Aaros}

1.  About me: Hey, I'm 183Aaros, a member of OPCN and one of the tutors of the OP co-learning this time. I'm delighted to learn the fundamentals of OP together with everyone here. Here's my personal web if you're interested in know more about me :) -> 183aaros.notion.site
2. About Notes: trying to use md grammar after 2-3 days 
3. Yes

## Notes

<!-- Content_START -->

### 2025.01.06

Optimism Co-learning Notes, day1: 

#### OP and OP Rollup

Dedication:
scaling Ethereum's tech
expanding its ability
coordinape ppl world-wide to build decentralised economies+governance systems

Principle:
impact=profit

OP Collective:
Builds open-source software

OP Stack:
decentralised software stack
backbone of blockchains i.e. OP Mainnet& base

OP Rollups:
Leverage the consensus mechanism of L1

#### Block

Block storage:
using non-contract address(for min gas) on ETH
write in compressed format
transaction anti-censorship via EIP-4844 blobs
inherits ETH availability& integrity

Biobiography:
https://specs.optimism.io/

### 2025.01.07

Key takeaway:

#### OP Mainnet Transaction fee
Transaction fee [Execution Gas Fee(Base fee, Priority fee), L1 Data Fee]

#### L1 Data Fee，Ecotone:
(1)tx_compressed_size = [(count_zero_bytes(tx_data)*4 + count_non_zero_bytes(tx_data)*16)] / 16

(2)
weighted_gas_price = 16*base_fee_scalar*base_fee + blob_base_fee_scalar*blob_base_fee

L1 Data Fee, Ecotone = (1) * (2)

#### L1 Data Fee，Fjord
L1 Data Fee，Fjord(FastLZ-compressed size, base fee/ blob base fee):

(1) estimatedSizeScaled = max(minTransactionSize * 1e6, intercept + fastlzCoef*fastlzSize)

(2)l1FeeScaled = baseFeeScalar*l1BaseFee*16 + blobFeeScalar*l1BlobBaseFee

where both scalars are scaled by 1e6,

thus,

L1cost = (1)*(2)/1e12

#### Biobiography:
https://docs.optimism.io/stack/transactions/fees

### 2025.01.08

Key takeaway:

Stage 0 - Full training wheels, still an source available software allows reconstruction of the state.

 - rollup
 - state roots
 - provide DA (data availability) on L1
 - reconstructiion of state source available

Stage 1 - Limited ~, governed by smart contract, council implementation for security.

- proper proof system
- fraud proof
- user may exit without oper's coordination
- 7 days exit window
- 50% of the security council participants from external

Stage 2 - No ~, final stage, no council.

- permissionless
- 30 days exit window
- Security Council restricted to errors detected

### 2025.01.09
The learning material today I choose from, has head back to VB's original articles on scaling, which inspring the design of Optimism.

Key takeaway: (mainly focus the aspect of VB's analytical framework)

Some prior background - Blockchain scaling/decentralised/safety triangle dillema etc.

Identify the problem 
- the consensus architectures rely on every node processing every transaction

When it comes to soluions, one particular thing that really stand out is, 
VB has assessed many factors even potential growth model and how would these model choices could end up with.
i.e. Batching vs. other solutions, in a sense of the comparison of a linea growth model solution vs. exponential growth model, but with a trade-off (i.e. ETH 2.0, a trade-off of the dev cycle).

At the very last part of the article, VB has mentioned shadow chain, we can see the idea that inspired Optimism Rollups. From the analytical thinking side, he identified the trade-offs, and can also see how his analytical framework constructs the original version of L2 solution that temporarily compromises, but better for solving the trilemma in the long run.

#### Biobiography:
Buterin, V. (2014) 'Scalability, Part 1: Building on Top', Vitalik Buterin's Blog, 17 September 2014.
https://blog.ethereum.org/2014/09/17/scalability-part-1-building-top

### 2025.01.10
休息

### 2025.01.11

#### Optimism Collective
- a collective of companies + communities + citizens working together
       - to reward publicgood
       - build a sustainable future for Ethereum

#### Vision
- standardization
- Supechain scales
- governance protect security
- governance creates flywheel of sustainable growth and dev

#### Mission
- to create an internet that benefits all and is owned by none

#### Governance
- digital democratic governance consists of 2 houses
- Token house: submitting, deliberating, voting on various types of governance proposals.
    - vote directly
    - delegate
- Citizen house: 1 person = 1 vote, also responsible for RPGF (Retro Funding);
    - reduce concentration of power
    - safeguard against capture of Token House (whales etc.)
    - Allocate resources for long-term benefit

#### Biobiography:
Citizens House section: https://community.optimism.io/citizens-house/citizen-house-overview

#### What's next?
Understand how Token house and citizen house works in a more in-depth aspect.

Sources:
1. The Collective’s Operating Manual
https://github.com/ethereum-optimism/OPerating-manual/blob/main/manual.md#valid-proposal-types

2. The Collective’s Working Constitution
https://gov.optimism.io/t/working-constitution-of-the-optimism-collective/55

3. Identity and Reputation: Foundation within the Collective
https://community.optimism.io/identity/identity-and-rep

4. Decentralization Milestone
https://docs.google.com/spreadsheets/d/1IpL0oTd3AgNBu_eWdjP9EjbQfZjq-_Nd3yU1H2ke3vY/edit?gid=0#gid=0

5. Decision Diagram Working Model
https://www.figma.com/board/iXqyKmLJeBeplKpJBHDI7G/PUBLIC%3A-Optimism-Decision-Diagram-Working-Model?node-id=0-1&node-type=canvas&t=QLiz1uM1DepwYyHy-0

<!-- Content_END -->
