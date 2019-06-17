---
layout: post
order: 1
title: Cross exchange market making
category: strategies
tags: [strategies]
keywords: strategies
description: hummingbot 中文翻译
---


## 跨交易所交易策略

### 如何工作的？

交叉交易市场的建立在[策略](https://docs.hummingbot.io/strategies/)中进行了描述，并在Hummingbot[白皮书](https://hummingbot.io/whitepaper.pdf)中进行了进一步的讨论。

### 示意图

下面的图表说明了跨交易所市场是如何运作的。交易包括两个交易所，一个买入交易所和一个卖出交易所。Hummingbot使用take exchange上可用的市场水平在maker exchange上创建买卖订单(充当做市商)(图1)。

![image](https://docs.hummingbot.io/assets/img/xemm-1.png)


买入指令:Hummingbot可以在taker exchange上以99美元的价格出售资产(这是可获得的最高出价);因此，它在创客交易所(maker exchange)以较低的98美元买入。

卖出指令:Hummingbot可以以101美元的价格在接受者交易所(taker exchange)购买资产(可获得的最佳要价)，因此在创客交易所(maker exchange)以102美元的高价卖出指令。

![image](https://docs.hummingbot.io/assets/img/xemm-2.png)

如果买家(买家D)填充Hummingbot卖出订单在maker交易所(图2❶),

在taker交易所Hummingbot立即购买资产(图2❷)。

最终的结果:Hummingbot出售相同的资产为102美元(❶)和购买101美元(❷),1美元的利润。

** 我的理解： 在Maker交易所中以102$的价格卖出了，然后会触发在Taker交易所中的101$的买入，存在102-101的差价，盈利1$**
** 同理，如果在maker中以98$的价格买入了，也会触发在taker交易所中以99$的价格卖出，存在99-98 =1 的差价，盈利1$**


### 先决条件:库存

1.为了进行跨交易所交易，你需要在两个交易所持有存货，一个机器人将建立市场的地方(maker交易所)，在另一个地方，机器人将提供流动性，并对冲任何已完成的订单(taker交易所)。
2.您还将需要一些以太支付在去中心化交易所交易中的gas费用。

首先，我们假设maker交易所是一个基于以太的去中心化交易所，而接taker交易所是Binance。

**我的理解：流动性强的做taker，流动性差的做maker，，，具体的情况请尝试来确定是否成立**


### 配置预排

以下是第一次运行config时的所有步骤。

**提示:配置期间自动完成输入**

在执行命令行配置过程时，在提示符处按<TAB>将显示有效的可用输入。


提示                                      描述

What is your market making strategy >>>:  输入 cross_exchange_market_making
                                          目前可用的选项:arbitrage或pure_market_making(区分大小写)

Import previous configs or                第一次运行机器人时，输入create。
create a new config file?                 如果您之前已经初始化，输入import，它将要求您指定配置文件的位置。
(import/create) >>>:  
                                          

Enter your maker exchange name >>>:       在跨交易所的市场决策策略中，Maker交易所是bot下Maker订单的交易所。
                                          当前可用的选项:radar_relay或ddex(区分大小写)
                                          
Enter your taker exchange name >>>:       在跨交易所的市场决策策略中，Taker交易所是机器人下达Take指令的交易所。
                                          当前可用选项:binance(区分大小写)
                                          
                                          
Enter the token symbol you would like to   输入Maker交易所交易的令牌符号。示例输入:ZRX-WETH
trade on [maker exchange name] >>>:        确保该对是交换的有效对，例如，使用“WETH”而不是“ETH”。
                                         

Enter the token symbol you would like to   输入Taker交易所交易的令牌符号。示例输入:ZRX-ETH
trade on [taker exchange name] >>>:        确保(1)该对与为maker exchange输入的令牌符号相对应，
                                           且(2)是该exchange的有效对。注意，在这个例子中，使用ETH而不是WETH。

What is the minimum profitability for     设置min_profitability(参见[定义](https://docs.hummingbot.io/strategies/arbitrage/#configuration-parameters))。
your to make a trade?                     : 交易的最小盈利的设定
 (Enter 0.01 to indicate 1%) >>>:
 
Do you want to actively adjust/cancel     设置active_order_canceling(参见定义)。
orders (Default True) >>>:                ：你想主动调整/取消订单吗

 
What is the minimum profitability to      设置cancel_order_threshold(参见定义)
actively cancel orders? (Default to 0.0,  ：取消订单的最低盈利能力是多少?
only specify when active_order_cancelling 
is disabled, value can be negative) >>>:


What is the minimum limit order expiration  设置limit_order_min_expiration(参见定义)
in seconds? (Default to 130 seconds) >>>:   ：订单的最小时限(以秒为单位)是多少?

 
Enter your Binance API key >>>:           您必须创建一个启用交易的Binance API key key(选择“启用交易”)。

Enter your Binance API secret >>>:



Would you like to import an existing wallet    导入或创建一个Ethereum钱包，用于在DDEX上进行交易。
or create a new wallet? (import / create) >>>: 输入一个有效的输入:
                                               
                                               import:从输入私钥导入钱包。
                                                   如果您选择导入，您将被要求输入您的私钥以及一个密码来锁定/解锁用于Hummingbot的钱包
                                                - 您的钱包私钥>>>
                                                - 一个密码，以保护您的钱包密钥>>>
                                                
                                               create: 创建一个带有新私钥的新钱包。 
                                               - 如果您选择create，您将只需要输入一个密码来保护您新创建的钱包
                                               - 一个密码，以保护您的钱包密钥>>>
                                               
                                               **提示**
                                               使用Metamask中提供的钱包(即从Metamask导入钱包)，您可以查看Hummingbot在去中心化交易所网站上创建的订单和完成的交易。
                                               
Which Ethereum node would you like             输入一个Ethereum节点URL，以便Hummingbot在基于Ethereum的去中心化交易所进行交易时使用。
your client to connect to? >>>:                有关更多信息，请参见安装:[设置Ethereum节点](https://docs.hummingbot.io/installation/node)。
                                               
                                               **提示**
                                               如果您正在使用Infura端点，请确保在URL之前添加https://。
                                               
 
### 配置参数

以下参数是Hummingbot配置文件中的字段(位于/conf文件夹中，例如conf/conf_arbitrage_strategy_ _[#].yml)。

   
术语                                          定义
min_profitability                            以小数表示的量(即输入0.01对应1%)。
                                             Hummingbot在交易所下订单的最低盈利能力。
                                                
                                             例如:假设最低盈利能力阈值为0.01，并且在take exchange (binance)上有一个投标价格为100的令牌符号，
                                             Hummingbot将向制造商交易所(ddex)发出99美元(或更低)的竞价指令，以确保1%(或更高)的利润;
                                             Hummingbot只有在交易所出价最高的情况下才会下这个订单。
                                             

active_order_canceling                       True or False
                                             如果启用(参数设置为True)， Hummingbot将根据min_profit阈值取消该设置。
                                             如果设置为False, Hummingbot将允许任何未完成的订单过期，除非cancel_order_threshold达到。


cancel_order_threshold                       以小数表示的量(即输入0.01对应1%)，可以是0，也可以是负数。
                                             当活动订单取消设置为False时，如果订单的盈利能力低于此阈值，Hummingbot将取消现有订单，并在可能的情况下，下一个新订单。
                                             这允许机器人取消订单时，支付gas取消(如果适用)比潜在的贸易损失更好。
                                             

limit_order_min_expiration                   以秒为单位数量，这是任何限价订单的最小持续时间。默认值:130秒。

top_depth_tolerance                          在Hummingbot修改其订单之前，以报价货币表示的最高总订单量，其价格高于Hummingbot的订单。
                                             例子:假设最高深度宽容100和20 Hummingbot投标价格,
                                                 如果存在一个订单总金额超过100的价格(高)比Hummingbot的出价,
                                                 Hummingbot将取消其订单在20和重新评估下一个新的出价的机会。
                                             **这个实在翻译不出来汗，，，汗，，，汗，，，**
                                             
trade_size_override                          以最大允许订单大小的报价货币表示的金额。
                                             **这个实在翻译不出来汗，，，汗，，，汗，，，**
                                             
                                             示例:假设交易大小超过为100，并且令牌符号为ETH/DAI，那么允许的最大订单大小是值为100 DAI的订单大小。
                                             
                                             
