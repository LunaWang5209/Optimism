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

# 小飞轮

1. 自我介绍
 我是一个加密爱好者，由于不会代码，每次看到共学会退避三尺，这次鼓起勇气来了。
3. 你认为你会完成本次残酷学习吗？
   会

## Notes

<!-- Content_START -->

### 2025.01.06
学习Layer2 扩容方案: https://docs.optimism.io/stack/rollup/overview

1.传统的“多链”架构方法存在两个基本问题：

每条链都会引入一种新的安全模型，随着新链被引入生态系统，系统性风险也会随之增加。（相关链接）
新链的启动成本很高，因为它们需要新的验证器集和区块生产者。
注：降低风险，降低成本。

2.想到一个问题，如果超级op框架下自定义gas,手续费与sol链上的手续费相比？
假设arb系统上的链，与op上的链相当，选取ape链上交易一笔，则手续费是0.006283U，而sol链上是0.03732U，可以得出一个简单结论，在便宜这块，sol的竞争优势将消失。

3.在Blockspace 和 Standard Rollup 章程里，自定义 gas 代币链是标准的吗？不是，标准链必须使用以太坊作为其 gas 代币，那么问题来了，这样做的目的是什么，有什么好处，现阶段这样，还是以后都是？

4.将交易发布到超级链是不可扩展的，因为交易数据必须提交到容量有限的 L1.建议的解决方案:目前，L1 数据可用性(DA)的扩展程度还不足以支持互联网级别的扩展。但是，可以使用 Plasma 协议来扩展 0P 链可访问的数据可用性。
问题:若是Plasma 与零知识证明，结合扩展会有什么效果?得到一下答案

<img width="616" alt="截屏2025-01-06 11 11 12" src="https://github.com/user-attachments/assets/4439dcdf-0c41-44a7-89ae-366708079cd1" />

5.在设计理念原则，有几句很喜欢的话，简单性、实用性、可持续性，Optimism 倾向于尽可能使用现有的经过实战检验的以太坊代码和基础设施，尽管 Optimism 充满了理想主义，但其背后的设计过程最终还是由实用主义驱动。核心 Optimism 团队有现实世界的限制，基于 Optimism 构建的项目有现实世界的需求，使用 Optimism 的用户有现实世界的问题。Optimism 的设计理念优先考虑用户和开发人员的需求，而不是理论上的完美。有时最好的解决方案并不是最漂亮的解决方案。
注：有时候，有效远比正确更重要。


### 2025.01.07
学习第二天
今天学习Optimism 与其他 Layer 2 的比较：https://learnblockchain.cn/article/3703

1.二层继承了以太坊的安全性，那么只专注扩展性，和去中心化，这样就破解了区块链三角困境，一个很好的思路。

2.看到一个图如下
<img width="711" alt="截屏2025-01-07 10 50 24" src="https://github.com/user-attachments/assets/0c8e44b7-bf42-4dc7-a75e-576ff0135f6b" />

然后用了chantGPT帮我理解概念
Validity Proofs，英文单词的意思，Validity有效性，指某些事物合法的，正确，符合逻辑，Proofs，证明，指用来证明事物的真实性，有效性，合起来叫有效性证明。通过数学来证明，这里的数学是ZK——Proofs零知识证明。

Fault Proofs 英文单词Fault是错误过失的意思，合起来是错误了，怎么证明，称为欺诈证明。
有效证明，跟欺诈证明的目的是什么，解决纷争，追求交易的正确性。

在有效性证明里，交易数据可以放在链上，也可以放在链下，链上叫ZK—rollup,链下validium,有效的链下数据存储，前者交易数据完全在链上，后者交易数据在链下，而状态根在链上。
Volition 英文的意思，是主观的，自由选择，在这里是用户自由选择，将数据存储到链上，或者链下。

Plasma 欺诈证明里的一种方式，将交易数据状态根，提交到以太主网，而optimistic,将整个交易数据提交到以太主网，那么这里面有个问题，plasma在7天窗口挑战期，交易数据能否调出来验证，是一个问题，而V神最近提出，这个交易数据，可以用零知识证明来解决。很有意思的事，期待后面的走向。

Plasma若是加上，零知识证明，会解决什么问题，零知识证明（ZK Proofs）解决了 Plasma 的关键问题之一：数据可用性问题 和 状态更新的正确性验证问题。

3.今天的学习很愉快，chantGPT帮我梳理了很多问题。







### 2025.01.08

<!-- Content_END -->
