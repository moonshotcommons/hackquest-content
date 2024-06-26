# Content/内容

### 目标

本节的目标是学习一种 Layer 2 的实现方式，叫做状态通道。

### 问题

因为 Alice 的公司在与其他公司做跨境交易，每一笔订单交易的金额其实不是很大，平均数在 100 美元。

Alice 和客户是在 Bitcoin 一层网络做交易结算的，随着时间流逝她发现有如下问题：

1. 为了防止货物发出去了但是没有收到款项，Alice 和别的公司交易都是一笔订单结算完成才进行下一笔（一般为 100 美元），毕竟只有一笔被违约的话还是可以承受的，两笔交易都被对方违约的风险就无法承受了。由于每一笔交易在 Bitcoin 一层网络结算完成一般都要等待 10 分钟，每一天的交易量就不能很多，Alice 本可以赚更多钱的。
2. 由于 Bitcoin 一层网络的交易手续费太贵了，所以 Alice 这边每一笔交易其实都少赚了一些钱，所以她更希望订单的价值大一些，这样更容易摊平这些手续费损失。

### 解决方案

因为这些问题的存在，Alice 就去找 Bob 请教，Bob 告诉了她一种方法叫做状态通道。具体的方案如下：

- 每天上午 9 点上班的时候，Alice 和客户一起创建一个多签名钱包（多个私钥控制），将一定数量的资金锁定在这个钱包中，并将该交易记录在区块链上。这个交易作为开启通道的证据。
- 通道建立之后，Alice 和客户就可以在通道内进行频繁的交易了，这些交易并不会立即被提交到 Bitcoin 一层网络上，而仅仅是双方都将交易的状态变化记录在本地，并相互交换更新后的状态。
- 每一天下午 6 点下班前，Alice 和客户希望关闭通道时，他们可以将最终的状态提交到 Bitcoin 一层网络上，并由 Bitcoin 一层网络验证和执行这个状态更新，最终状态包含了通道运行期间内的所有交易信息。

如此一来，

- Alice 和客户每天的交易就可以无限多了，因为在通道内完成交易是非常快的，可能每秒钟都可以完成 10 笔交易了，完全够用了。
- 另外 Alice 每天只要下班前统一付一次 Bitcoin 一层网络的手续费就行了，省下了很多钱。

但是由于 Alice 和客户都在各自的本地记录交易状态变化，难免有时候会出现不一致的时候，她们需要制定出争议解决的方案，方案如下：

- 如果 Alice 和客户之间发生争议，例如一方欺诈或拒绝合作，她们可以选择将争议提交到 Bitcoin 一层网络上进行解决，在争议解决阶段，Bitcoin 一层网络将验证这个争议，以确定最终的状态。
- 其中一种常用的验证机制是简化支付验证（Simplified Payment Verification，SPV）
- SPV 验证过程中的关键步骤是验证交易在区块链中的位置和有效性。参与者可以使用 Merkle 树结构来验证交易是否包含在特定的区块中。Merkle 树是一种二叉树结构，其中每个叶子节点代表一个交易，而每个非叶子节点的值是其子节点值的哈希。通过比较交易的哈希与 Merkle 树的根哈希，参与者就可以确认该交易是否包含在区块中了。
- 一层网络验证之后，争议解决了，双方的钱款就会按照正确的值返回到各自的钱包里了。

如此一来，Alice 的问题解决了，她非常开心，打算明天就试试这个方案。

### **小结**

这一小节我们学习了状态通道这种方案，它的技术原理如下：

1. 打开通道：参与者质押一定链上资产在多签合约中以打开状态通道；
2. 使用通道：参与者在通道中自由进行交易，本地更新状态，不提交到链上；
3. 关闭通道：在所有参与者一致同意后，提交最终状态到链上进行最终清算，一定时间内无人质疑即完成交易。

它解决了交易结算不及时，手续费比较高的两个问题。

### 下一节

刚才提到状态通道解决了交易结算不及时，手续费比较高的两个问题。

但是状态通道是否有什么缺点呢？同学们可以思考一下。

下一小节我们会讨论状态通道的缺点，然后再学习一种新的 Layer2 的实现方式。

# Learn More

状态通道是最早由 Lighting Network 在 2015 年提出的链下扩容技术，它通过链下交易链上清算来提高交易吞吐量。参与者可以安全地进行链下交易，将最终结果发布到区块链，最大限度地减少与主网的交互。

代表项目：

- [Connext](https://connext.network/)
- [Kchannels](https://www.kchannels.io/)
- [Perun](https://perun.network/)
- [Raiden](https://raiden.network/)
- [Statechannels.org](https://statechannels.org/)