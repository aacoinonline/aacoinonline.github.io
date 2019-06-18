---
layout: post
order: 1
title: 策略概述 
category: strategies
tags: [strategies]
keywords: strategies
description: hummingbot 中文翻译
---

## 策略

### 目前发布的Hummingbot有两种策略。单击策略名称了解更多信息。

    策略                               描述
    
    Arbitrage                         旨在捕捉两个不同交易所之间的价差(一个低买，另一个高卖)。
    
    Cross exchange market making      也称为流动性镜像或交易所再营销。
                                      在这一策略中，Hummingbot在较小或流动性较差的交易所建立市场(创建买卖订单)，在流动性较好的交易所进行相反的背对背交易。
    
                                      与其他做市策略相比，该策略的风险和复杂度相对较低，我们认为这将是一个很好的初始用户起点。
                                      
                                      
    Pure market making                在一个交易所发布一种工具的买卖报价，在积极管理库存的同时自动调整价格。
                                      与其他策略相比，他的策略具有较高的风险和复杂性，我们要求用户在运行之前保持谨慎并完全理解它。
                                      
                                      
Hummingbot[白皮书](https://www.hummingbot.io/whitepaper.pdf)提供了更多关于这些策略的细节，以及我们正在为未来版本的Hummingbot研究的额外策略。                                   

**注意**

这些策略应该是基本的模板。我们鼓励用户根据自己的目的扩展这些模板，如果他们愿意，可以与社区共享它们。

