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

学习第三天：
今天学习Stage 的介绍：https://medium.com/l2beat/introducing-stages-a-framework-to-evaluate-rollups-maturity-d290bb22befe

1.stage的意思，事物发展的阶段，等级，在这里就是一个判断框架，目的就是来判断评估 Rollups 项目，处于那个阶段，以便让用户知道，它的去中心化程度。分为以下三个阶段：

第0️⃣阶段：由操作员运行，有一个开源可用软件。

第1️⃣阶段：由操作员运行，升级为智能合约运行，保留一个安全委员会，解决少部分问题，OP是用的故障证明。

第2️⃣阶段：完全由智能合约运行，安全委员会非必要不干涉，除了重大问题。

这三个阶段，从0️⃣到2️⃣，将人操作干涉，逐渐不断缩小，交给代码，体验到了，代码的力量。


2.在l2beat网站上，选取了前排名52个项目里，处于第0️⃣阶段的有42个，处于第1️⃣阶段的有2个，处于第2️⃣阶段有3个。


<img width="1191" alt="截屏2025-01-08 11 28 23" src="https://github.com/user-attachments/assets/85c0669c-8a3b-42d6-840a-f58bcd2e2e64" />


3.在OP系统里，有四个项目，用了故障证明，一个是base，OP主网，swell，lnk,其余的都没用，swll与lnk刚加入，就使用了，说明使用的难度不大，uni 也承诺上线就使用，可能其他项目不重视这个，在他们眼里，这不是什么紧急的事，不知道我的看法对不对？

### 2025.01.09


学习第四天，今天学习有关零知识证明的知识

1.ZK（或是ZKP）全称Zero-knowledge proof,即零知识证明，它是一种方法，目的呢是，通过该方法，证明者可以向另一方验证者证明一个事实，不需要透露该事实的具体信息。这个脑补了一下，感觉很有意思。相应的带来好处，是保护隐私，还有一个是解决验证难的问题。

2.ZK-SNARK全写Zero-Knowledge Succinct Non-Interactive Argument of Knowledge，其中succinct是简洁的意思，Non-Interactive，其中Non,是非，不的意思，而Interactive是交互的意思，合起来是非交互式的。Argument是论证的意思，总体合起来就是，零知识证明里的一种简洁非交互式的知识论证。注意它只是其中一种，零知识证明构造的方法。

3.ZK-SNAEKs到ZK-STARKs,这里的s代表可扩展的，ZK-STARKs是前面的升级版本，这里的字母T代表透明性，比起ZK-SNAEKs,效率更高，理论上强十倍，更加去中心化，还可以抗量子特性，但相应的有个缺点，就是技术相对来说新一点。实现难度比较大，做个简单类比，相当于欺诈证明，与有效证明的关系。ZK-SNAEKs是目前通用的证明算法，而ZK-STARKs目前技术不够成熟，是特用的证明算法，目前使用ZK-STARKs的项目有StarkWare ,POlygon Miden等。

4.zkEVM其实是运行在L2层的类EVM虚拟机器，因此更为精确的说法是Zero Knowledge virtual Machine,Virtual 是虚拟的意思，zkvm,只不过大家强调其兼容以太坊而称为zkEVM,现有项目也在考虑逐渐放弃了为特定应用程序而做优化，而升级支持运行通运合约即zkEVM Rollup.因此ZKEVM Rollup虽然作为ZK Rollup的下位概念，在大部分情况下，提起ZK Rollup时变指zkEVM rollup.

5.总结，好好理解吸收这些概念，才能知道这些项目方在干嘛。


### 2025.01.10

学习第五天，今天学习有关blob扩容与Flashblocks 。

1.今天早上回看 OP Labs 产品主管 Sam McIngvale 将与 Token Relations 的 Jacquelyn Melinek 一起深入讨论 Optimism 的 2025 年产品路线图，里面提到blob扩容，我就好奇查了一下。
blob 扩容是一种新的交易类型，这种交易类型，可以为以太坊提供一个额外的外挂数据库，这种交易是为rollup量身制定的，rollup的数据以Blob的形式上传至以太坊，额外的数据空间可以是rollup实现更高的tps和更低的成本，同时也将原本rollup占据的区块空间释放给更多的用户。由于Blob的数据是临时存储的，数量的暴增并不会对节点的储存性能造成越来约越重的负担。

2.在最新的以太升级计划中，将三个块升级为六个，那么他的TPS会翻倍，目前二层的tps如下图。


<img width="844" alt="截屏2025-01-10 16 52 24" src="https://github.com/user-attachments/assets/a07cedff-3933-4025-9666-38b8d5272d5b" />

那么最高的base也就会达到143.28，在这场高性能竞争中，缓解了不少。

3.Vitalik Buterin：确实需要在以太坊核心开发中更好地确定优先级，优先支持 blob 扩容。



  <img width="685" alt="截屏2025-01-10 17 16 16" src="https://github.com/user-attachments/assets/4001a436-331d-4a41-9d91-93987bd376b2" />






4.Flashblocks 该协议允许矿工和验证者透明地交易区块内的交易顺序，从而减少MEV导致的不公平性和乱象，250 毫秒的 Flashblocks：这一模块提供极快的确认时间，同时引入了原生的回退保护机制，防止由于交易失败引发的重复费用。同时，Flashblocks 还大幅提升了 Gas 吞吐量，使得用户在繁忙的网络环境中仍能以较低的成本完成交易；2）可验证的优先级排序：每个 Flashblock 内的交易将根据可验证的优先级进行排序。这不仅提供了更强的用户保障，还允许应用内部化 MEV，从而减少外部 MEV 提取对网络的冲击，进一步提升了整体的市场效率。若是uni链上线，将有十倍的升级体验。

5.总结，明显的感觉到，市场的竞争激烈，我在想技术，有没有护城河，若是没有的话，那么到底什么是项目方的护城河呢？

### 2025.01.11


学习第5天，今天想了解一下，二层 op arb zksync stark 创始人团队情况。


1. Optimism： 由一组以太坊开发人员创建，创始人包括 Jinglan Wang、Ben Jones 和 Karl Floersch。
   
Jinglan Wang 拥有计算机科学背景，曾在谷歌和 Uber 工作过。她是经验丰富的区块链布道者。在 MIT 时期加入了学校的比特币俱乐部，开启了自己的加密之旅，后来又到纳斯达克担任区块链产品经理，并创立了贸易融资公司 Eximchain。之后，她又和 Jeremy Gardner 共同创立了区块链教育网络 The Blockchain Education Network，帮助全球各地的学校组建区块链俱乐部。

Ben Jones 是一名软件工程师，拥有在以太坊上构建去中心化应用程序的经验。他在空闲时常以自己的艺名 Weird ETH Yankovic 制作一些基于以太坊的模仿歌曲，也是團隊中的艺术家。

Karl Floersch目前是CEO，研究员和开发人员，曾参与过多个以太坊项目，包括以太坊 2.0。 是以太坊基金会的 OG 开发者，他爱好冥想和即兴饶舌，从小受到印度教的熏陶，通过冥想来思考和感悟一些事情，用饶舌表达自己当下的感受我。

顺便在 youtube 找到了采访Jinglan Wang和 Karl Floersch 的视频，顺便截了个图。

<img width="1185" alt="截屏2025-01-11 12 35 03" src="https://github.com/user-attachments/assets/f4f7b613-2dac-4d45-944a-276c6c4fba49" />

2.Offchain Labs：
Ed Felten 是 Offchain Labs 的联合创始人兼首席科学家。除了在 Offchain Labs 担任职务之外，Ed 也是普林斯顿大学的教授，近 30 年来他一直在普林斯顿大学为学生提供计算机科学和公共事务方面的教育.

Steven Goldfeder 是 Offchain Labs 的联合创始人兼首席执行官，此前他在普林斯顿大学获得了博士学位后进入 Google 工作。

Harry Kalodner 是 Arbitrum / Offchain Labs 的联合创始人兼首席技术官。他在美国普林斯顿大学获得计算机科学博士学位。


<img width="800" alt="截屏2025-01-11 13 01 34" src="https://github.com/user-attachments/assets/a8374756-bf21-4a2f-a428-e438b374b457" />


3.zksync ：Alex Gluchowski 是 Matter Labs 的联合创始人兼首席执行官，他正在使用零知识证明扩展以太坊。 在此之前，他是香港 Entropy Labs 的研发总监，专注于以太坊研发，Alex 拥有柏林工业大学的计算机科学硕士学位。

Marcin Michalski目前是负责 ZKsync 首席协议架构师。在此之前，他在 NEAR Blockchain 负责协议开发。

Meghan Hughes 是 Matter Labs 首席营销官，此前是 Solana 基金会市场副总裁。她毕业于西蒙斯大学。


<img width="950" alt="截屏2025-01-11 16 27 38" src="https://github.com/user-attachments/assets/2e127e7e-47ad-45b0-ba75-775268f7ecf2" />


4.StarkWare ：
Eli Ben-Sasson：Co-Founder & 首席科学家，以色列理工学院计算机专业的教授。Zcash 的创始科学家，zkSNARKs 的发明者。

Alessandro Chiesa：Co-Founder & 首席科学家，加州大学伯克利分校计算机专业的教授。Zcash 的创始科学家，zk-SNARKs 的联合发明者，libsnark 的核心开发者。
Uri Kolodny：Co-Founder & CEO，Uri 是一个商业经验丰富、善于合作的连续创业者。

Michael Riabzev：Co-Founder & 首席架构师。以色利理工学院的博士，曾在 Intel、IBM 工作。

Oren Katz：工程副总裁。Hebrew 大学计算机专业毕业，Tel Aviv MBA，20 年经验的资深工程师。

<img width="966" alt="截屏2025-01-11 16 35 58" src="https://github.com/user-attachments/assets/684f32eb-e76c-4327-8a23-e891d7125e37" />

5.个人的感悟，他们都很优秀，目前的顶级大佬，都对加密改变这个世界着迷，为加密世界添砖加瓦，对于我个人，不太懂技术，我个人更偏向于年轻的创业者，觉着他们有更多充沛的精力，思想包袱少，带着羞涩的纯粹性，更能贴近这个时代。

### 2025.01.12

今天学习第六天，目的是要了解，bolb扩容，会给以太坊带来的问题，及相应的解决办法。

1.按照V神的路线规划，若是中期目标每槽是16MB，如果结合汇总数据压缩的改进，我们将获得约58000TPS。那么显然会带来以下问题？

a.节点负担过大，在数据存储上还是数据同步上，使得以太坊节点过大，而导致以太坊的中心化程度降低。

b.数据可用性问题，如果节点不去下载全部bolb数据，就会面临数据可用性的问题，因为数据不在链上开放且随时访问，如果对某个交易数据存疑，发起挑战，那么拿不到原始数据，就无法证明这个数据是有问题的。所以要解决数据的可用性问题，就必须得保证数据的随时开放且可以访问。

2.数据可用性采样：
引入数据可用采样性，目的是来降低节点负担过大，同时保证了数据的可用性。

数据可用采样性DAS，它的思想是将blob中的数据切割成数据碎片，并且让节点由下载bolb数据转变为随机抽查blob数据碎片，让blob的数据碎片分散在以太坊的每个节点中，但是完整的blob数据却保存在整个以太坊中，前提是节点需要足够多且去中心化。

3.为了实现数据可用性采样（DAS）采用了两个技术：纠删码（erasure Coidng )和KZG多项式承诺（KZG Commitment 这里的KZG是来自三密码学家名字的首字母，即 Katz, Zeldovich, 和 Gennaro，他们提出了这一概念)。

a.纠删码，是一种编码容错技术，使用纠删码切割数据可以使得所有以太坊上节点在拥有50%以上的数据碎片情况下，就可以还原出原始数据，这样大大的降低了数据缺失的概率。

b.KZG多项式承诺，是一种密码学技术，通常用于零知识证明和其他加密协议，目的是来证明这个数据碎片，来源于blob的原始数据，所以负责编码的角色还需要生成一个KZG多项式承诺，来证明这个纠删码的数据碎片确实是原始数据的一部分。

4.danksharding（这个英文单词的意思是，太坊研究员Dankrad Feis提出来的分片技术形式命名的），是初始分片方案sharding1.0方案的升级版本，使用了一套新的分片思路去解决以太坊的扩容问题，即围绕着Layer2的rollup进行扩容的分片方案，这套新的分片方案可以在不大量增加节点负担，且保证去中心化和安全性的同时，解决可扩展性问题，同时解决了MEV带来的负面影响。


### 2025.01.13



<!-- Content_END -->
