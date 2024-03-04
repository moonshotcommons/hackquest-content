# Content/ 引文

在开始学习 Solana 之前，让我们先来了解 Solana 的历史。

## **Solana 的历史**

2017年11月，Anatoly Yakovenko发表了一篇白皮书，介绍了“Proof of History”这一技术（我们会在后续章节详细介绍），用于在不信任彼此的计算机之间进行时间同步。Anatoly 有在高通、Mesosphere 和Dropbox 设计分布式系统的经验，他知道有了可靠的时钟，网络同步就会变得很简单，而简单的同步能让网络运行得非常快，只受网络带宽限制。

Anatoly 注意到像比特币和以太坊这样没有时钟的区块链系统只能达到每秒 15 次的交易速度，而如果希望搭建一个世界中心化支付系统（如Visa）则需要峰值65,000次每秒的交易速度。 没有时钟，很明显他们永远无法像 Visa 那样成为全球支付系统。当 Anatoly 解决了计算机之间时间不一致的问题时，他意识到这是将多年的分布式系统研究应用到区块链领域的关键。他的解决方案不仅提高了效率，而且速度提高了成千上万倍。

Anatoly 一开始是在自己的 Github 中使用 C 语言实现了 Solana 的原型。曾在高通与 Anatoly 一起合作的 Greg Fitzgerald 鼓励他以 Rust 语言重新编写这个项目。Anatoly 两周内就完成了迁移到 Rust 的工作，并把这个项目命名为 Loom。

2018年2月13日，Greg Fitzgerald 开始为 Anatoly 的白皮书创建开源实现的原型。2月28日，Greg 就发布了首个版本，这个版本在半秒内就可以验证和处理超过10,000个签名交易。不久之后，另一位之前在高通工作的同事 Stephen Akridge 展示了如何通过图形处理器来验证签名，大大提高了处理速度。Anatoly 邀请 Greg、Stephen 和其他三个人共同创办了一家名为 Loom 的公司。

同一个时候，一个基于以太坊的项目 Loom Network 出现了，很多人经常把两个项目搞混。Loom团队决定重新给这个项目取个名字。最后他们决定把这个项目叫做 Solana 以纪念他们在圣地亚哥北部小海滩 Solana Beach 工作和冲浪的三年。2018年3月28日，团队创建了Solana 的 GitHub，并把Greg Fitzgerald 创作的原型命名为Solana。