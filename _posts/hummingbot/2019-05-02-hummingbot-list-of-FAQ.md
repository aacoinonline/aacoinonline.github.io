---
layout: post
title: intro
order: 4
category: hummingbot
tags: [hummingbot]
keywords: hummingbot
description: hummingbot 中文翻译
---


## FAQ

下面是一些对于Hummingbot经常会问到的问题，如果你有额外的问题或者需要帮助，请加入官方的[Hummingbot Discord server ](https://discord.hummingbot.io/) 或者通过邮件contact@hummingbot.io 联系我们。

### 一般问题

#### Hummingbot是什么？

Hummingbot是一个开源的交易软件，由 CoinAlpha, Inc. 开发，它允许用户通过一个本地的客服端实现加密货币的市场交易策略。

更详细的信息，请阅读[Hummingbot白皮书](https://www.hummingbot.io/whitepaper.pdf) 

#### 怎么样才能获取Hummingbot最新动态？

注册并加入到邮件列表或者加入官方的[Discord](https://discord.hummingbot.io/) 

#### 为什么要让大众使用Hummingbot，而不是仅仅在公司内部运行？

-  使命：

我们创建了CoinAlpha公司，因为我们相信区块链技术使个人能够在一个公平的竞争环境中与大型金融机构竞争，将Hummingbot作为开放源码软件发布给公众，进一步推进了这一任务。Decentralized market making

- 去中心化市场做市：

有数百家分散的数字资产交易所需要流动性，但专注于做市商的专业人士相对较少，无法满足这些交易所的需求。与此同时，做市需要在每个服务的市场上都有专门的库存（货币），考虑到市场近乎无限的组合，一个做市商不可能服务于整个市场。分散的、社区驱动的方法允许每个做市商服务于他们具有比较优势的市场。这是解决加密行业[流动性问题](https://www.hummingbot.io/blog/2019-01-thin-crust-of-liquidity/) 的一个更为理想的长期解决方案。

- 监管限制：

对加密货币的监管仍在演变和不明确，这给机构/公司交易带来了特别的挑战。作为一家技术公司，我们希望专注于构建技术，而不是把时间花在追寻和监控不断变化的法规上。


#### 为什么让Hummingbot开源?

- 透明度

为了使用Hummingbot，用户必须提供自己的私钥和API密钥,与钱包软件类似，我们希望用户了解这些敏感信息是如何被使用的，并在使用Hummingbot时给他们带来舒适;

- 社区

去中心化、区块链技术和加密货币都是由热情的技术人员基于社区的理念构建的。我们欢迎开发人员研究代码，提出改进建议，添加一些很酷的新特性，或者帮助识别bug或任何其他问题。

#### Hummingbot使用什么开源授权?

Hummingbot是在Apache 2.0下授权的。

#### 需要多少加密货币才能开始？

虽然使用Hummingbot没有最小资产数量，但用户应该注意交易所设定的最小订单大小，在[交易所链接](https://docs.hummingbot.io/connectors)文档中，包含了交易所最小订单的链接。

我们建议您先从较小的资产开始,慢慢的熟悉Hummingbot。

#### 我的private keys 和API keys 安全吗？

由于Hummingbot是一个本地客户端，所以您的私钥和API密钥与运行它们的计算机一样安全。密钥用于在本地机器上本地创建授权指令，只有已经签名或授权的指令才从客户机发出。

始终保持谨慎，确保运行Hummingbot的计算机是安全的，没有未经授权的访问。

#### 是否需要一个Ethereum节点来运行Hummingbot？

可以使用Hummingbot在中心化交易所、去中心化交易所(DEX)或两者兼而有之上创建交易的机器人。对于基于Ethereum的去中心化交易所，需要访问Ethereum节点。

我们描述了访问节点的[几种方法](https://docs.hummingbot.io/installation/node)。

#### 运行Hummingbot需要花费什么？

Hummingbot是一个免费软件，所以你可以免费下载、安装和运行它。

Hummingbot的交易是在交易所进行的正常交易;因此，使用Hummingbot时，你需要支付每个交易所的费用(例如maker、taker和提现费)，就像你在那个交易所正常交易一样(比如没有使用Hummingbot)。

- maker，taker【挂单交易的费用和主动交易的费用，一般主动买卖的费用高于挂单的费用】

### 数据收集？
#### 当使用Hummingbot的时候，你们会收集什么数据？

用户可以完全控制向我们发送多少数据。根据用户的选择，这可能包括:

**以太钱包地址**
- 汇总、匿名交易和订单量
- 在客户端接口中输入的命令
- 错误、通知和交易事件的日志条目


 ⚠️

私有密钥和API密钥存储在本地，仅用于Hummingbot客户机的操作。在任何情况下，私有密钥或API密钥都不会与CoinAlpha共享，也不会以授权Hummingbot操作所需的事务之外的任何方式使用。

#### 为什么要向您发送我的使用数据？

- 获得更好的支持：

授予对您的日志和客户机命令的访问权使我们能够更快地诊断您的问题并提供更好的支持。

- 参与伙伴激励计划：
 
**我们的一些交易所合作伙伴将根据总成交量对我们进行补偿。我们计划与参与其中的用户共享这一点。**


- 帮助我们提高产品：

我们致力于使Hummingbot成为加密算法交易的最佳开源软件。了解用户如何使用该产品将帮助我们更快地改进它。


我们仅将用户数据用于上面列出的用途。CoinAlpha和我们的员工被严格禁止将任何用户数据用于交易相关目的。

#### 可以选择不分享我的使用数据吗?

当然-日志配置文件是完全可编辑的。此外，用户可以覆盖默认设置的模板。

