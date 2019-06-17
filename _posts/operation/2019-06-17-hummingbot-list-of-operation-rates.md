---
layout: post
title: 汇率
order: 1
category: operation
tags: [hummingbot]
keywords: hummingbot
description: hummingbot 中文翻译
---

## 汇率(交易的费率)

当您在多个交易所上运行策略时，可能会出现需要利用汇率在资产之间进行转换的情况。

特别是，当您在跨市场交易和套利等多腿策略中使用不同的稳定资产时，可能需要将一个稳定资产的价值转换为另一个稳定资产的价值。

例如，如果您在去中心化交易所上做一个WETH/DAI对的市场，您可能希望使用Coinbase上的ETH/USD对或Binance上的ETH/USDT对对冲已满的订单。使用USDT和DAI对美元的汇率可以让Hummingbot考虑到稳定剂之间的价格差异。


### 汇率类

为了实现这些转换，Hummingbot在con_global.yml中包含一个汇率类。在/conf目录中。在这里，您可以设置固定的汇率，也可以告诉Hummingbot使用price feed API实时动态地设置汇率。


### 例子:默认配置

在conf/conf_global.yml文件中:

    exchange_rate_conversion:
    - - DAI
      - 1.0
      - COINCAP_API
    - - USDT
      - 1.0
      - COINCAP_API
    - - USDC
      - 1.0
      - COINCAP_API
    - - TUSD
      - 1.0
      - COINCAP_API


默认情况下，Hummingbot使用CoinCap API来为上面的稳定币设定美元汇率。

当您使用DAI和/或USDT运行Hummingbot时，汇率显示在status命令中:

![image](https://docs.hummingbot.io/assets/img/exchange-rate-default.png)

### 例子:自定义配置

在conf/conf_global.yml文件中:

    exchange_rate_conversion:
    - - DAI
      - 0.97
      - OVERRIDE
    - - USDT
      - 1.0
      - OVERRIDE
    - - USDC
      - 1.0
      - COINCAP_API
    - - TUSD
      - 1.0
      - COINCAP_API
    - - PAX
      - 1.0
      - COINCAP_API


要设置固定汇率，请使用OVERRIDE替换COINCAP_API并设置固定汇率。在上面的例子中，1 DAI假设等于0.97美元，1 USDT假设等于1.00美元。

您还可以添加新的加密资产。在上面的例子中，添加PAX允许Hummingbot使用CoinCap提供的PAX/USD汇率。

您可以在status命令中看到这些自定义汇率:

![image](https://docs.hummingbot.io/assets/img/exchange-rate-custom.png)


Can you provide a sample about how the exchange effect about the exchange ???


