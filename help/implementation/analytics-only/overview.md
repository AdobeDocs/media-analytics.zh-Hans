---
title: 仅限Analytics的实施概述
description: 适用于流媒体的Adobe Analytics加载项的先决条件和实施方法，用于仅限Analytics的实施。
feature: Streaming Media
role: User, Admin, Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 5%
---
# 仅限Analytics的实施概述

仅限Analytics的实施使用Adobe Analytics for Streaming Media加载项将数据直接发送到Adobe Analytics，而不使用Edge Network。 仍完全支持这些方法。 对于新实施，Adobe建议改用[Edge实施](/help/implementation/edge/overview.md)，因为它除Adobe Analytics之外，还允许数据对Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP可用。

## 先决条件

1. **完成常规先决条件。** 请参阅[常规先决条件](/help/getting-started/prereqs.md)。

1. **确认Adobe Analytics实施。** 仅限于Analytics的流媒体实施需要基本的Adobe Analytics实施。 请参阅[实施Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)。

1. **获取媒体跟踪服务器URL。** 向您的Adobe Analytics代表询问媒体跟踪服务器URL (`collection-api-server` URL)。 域通常遵循模式`[your_namespace].hb-api.omtrdc.net`。

1. **下载SDK或安装扩展。** 根据您的平台，[下载当前的SDK](/help/getting-started/download-sdks.md)或安装所需的标记扩展。

## 选择实施方法

每个页面都涵盖特定于流媒体的设置。 每个事件和每个变量的代码位于[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)中。

| 代码库 | In-code | 使用标记 |
|---|---|---|
| Web (JavaScript) | [JavaScript](javascript.md) | [Media Analytics标记扩展](javascript-tags.md) |
| Chromecast | [Chromecast](chromecast.md) | — |
| Roku | [Roku 2.x](roku-2x.md) | — |
| API | [媒体收集API](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/implementation) | — |

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [实施概述](/help/implementation/overview.md)
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
