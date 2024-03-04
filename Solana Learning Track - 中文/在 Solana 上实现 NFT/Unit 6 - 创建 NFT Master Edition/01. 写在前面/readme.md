# Content/引文

前面的课程，我们提到介绍了 Metaplex 协议，以及其中的 **Token Metadata** 程序，作用是将附加数据添加到 NFT，是整个 Metaplex 合约生态的基础。

上一章，我们学习了使用 **metadata PDA** 来装饰自己的 NFT，有了***name***, ***symbol***, ***uri*** 等等，用户使用钱包连接上节课创建好的 ***metadata account*** ，就可以展示 NFT；

而这一章，我们就要创建一个 ***MasterEdition***，可以在我们第二章铸造好的 token 基础上，增加一个附加 decoration PDA，叫做 ***MasterEdition*（**主版本**）**。这个 PDA 表示我们可以在原有 NFT 的基础上，继续铸造更多的复制品。

准备好了吗？让我们继续前进，深入 Solana NFT 开发的精彩世界！