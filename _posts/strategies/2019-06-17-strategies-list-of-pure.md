---
layout: post
order: 1
title: 单交易所做市
category: strategies
tags: [strategies]
keywords: strategies
description: hummingbot 中文翻译
---


## 单纯的做市策略(单一交易所的买卖)

### 如何操作？

在纯粹的市场决策策略中，用户不断在市场上发布限价和限价报价，并期望其他用户完成他们的订单。你可以控制你的出价和要求离中间价有多远，订单数量是多少，以及你想要取消和替换它们的频率。

**警告**

请在执行此策略时保持谨慎，并设定适当的止损限额。此策略的当前版本旨在成为用户可以测试和自定义的基本模板。在不进行额外修改的情况下，以大量资本运行该策略可能会赔钱。

### 示意图

下图说明了做市是如何进行的。Hummingbot通过在一个交易所下买卖订单，指定价格和大小来建立市场。


![image](https://docs.hummingbot.io/assets/img/pure-mm.png)


### 先决条件:库存

1。您将需要在交易所持有报价和基本货币的库存。
2。您还将需要一些以太支付DEX的交易费用(如果适用)。

### 配置预排

以下是第一次运行config时的所有步骤。

**提示:配置期间自动完成输入**

在执行命令行配置过程时，在提示符处按<TAB>将显示有效的可用输入。

    
    提示                                      描述
    
    What is your market making strategy >>>:  输入 pure_market_making
                                              目前可用的选项:cross_exchange_market_making或arbitrage(区分大小写)
    
    Import previous configs or                第一次运行机器人时，输入create。
    create a new config file?                 如果您之前已经初始化，输入import，它将要求您指定配置文件的位置。
    (import/create) >>>:  
                                              
    
    Enter your maker exchange name >>>:       在纯做市策略中，交易所是bot发出报价和发出订单的交易所。
                                              当前可用的选项:binance或coinbase_pro或radar_relay或ddex(区分大小写)
                                              
    Enter the token symbol you would like     输入交易所的令牌符号。示例输入:ZRX-WETH
    to trade on [maker exchange name] >>>:    注意:确保该对是用于交易的有效对，例如，使用WETH而不是ETH。
                                              
                                              
    What is your preferred quantity per order 这将设置order_amount(参见[定义](https://docs.hummingbot.io/strategies/pure-market-making/#configuration-parameters))。 --- 订单的数量
    (denominated in the base asset, 
    default is 1)? >>>:   
                                              
    How far away from the mid price           这将设置bid_place_threshold(参见[定义](https://docs.hummingbot.io/strategies/pure-market-making/#configuration-parameters))。
    do you want to place the next bid         : 距离中间距离的报价，按百分比计算;买入的价格
    (Enter 0.01 to indicate 1%)? >>>:
    
     
    How far away from the mid price           将设置ask_place_threshold(参见[定义](https://docs.hummingbot.io/strategies/pure-market-making/#configuration-parameters))。
    do you want to place the next ask         : 距离中间距离的报价，按百分比计算;卖出的价格
    (Enter 0.01 to indicate 1%)? >>>:
    
    
    How often do you want to cancel           这将设置cancel_order_wait_time(参见[定义](https://docs.hummingbot.io/strategies/pure-market-making/#configuration-parameters))。
    and replace bids and asks                 ：取消设定的时间（按秒计算）
    (in seconds)? >>>:
    
    
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

以下参数是Hummingbot配置文件中的字段(位于/conf文件夹中，例如conf/con_pure_market_making_strategy _[#].yml)。

       
    术语                                          定义
    order_amount                                 限价买卖订单的数量
                                                 确保你有足够的金额，对于买卖订单设定的数量
                                                 如果你没有足够金额来平衡买卖双方，策略将不会下订单。
                                                 
    
    bid_place_threshold                          以小数表示的量(即输入0.01对应1%)
                                                 如果该策略设置为0.01，则将购买(投标)订单从中间价格的1%处触发
                                                 例子:假设如下，
                                                 最高出价（买价）:99，最高要价（卖价）:101;中间价:100((99+ 101)/2)。
                                                 如果您将bid_place_threshold设置为0.1，即10%，它将以低于100的中间价格10%的价格(即90)，下您的买入订单。
                                                 
    
    ask_place_threshold                          以小数表示的量(即输入0.01对应1%)
                                                 如果该策略设置为0.01，则卖出(卖出)订单的价格将比中间价格低1%
                                                 例子:假设如下，
                                                 最高出价:99，最高要价:101;中间价:100((99+ 101)/2)。
                                                 如果您将ask_place_threshold设置为0.1，即10%，它将以高于100的中间价格10%的价格(即110)下您的销售订单(ask)。
                                                 
    cancel_order_wait_time                       以秒为单位的金额，这是下限价订单的持续时间。默认值:60秒。
                                                 限价投标和询价单被取消，新的投标和询价单根据当前的中间价格和设置在此期间进行。
                                                 
                                                 
                                             
**友情提示，请先用少量资金进行测试之后再进行大量资金的操作，并保证理解的内容和实际的操作一致**


