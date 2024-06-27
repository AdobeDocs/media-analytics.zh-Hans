---
title: 仅 Adobe Analytics 实施的先决条件
description: 了解将流媒体收集加载项用于仅限Adobe Analytics的实施或Edge实施的先决条件
feature: Media Analytics, System Requirements
role: User, Admin, Data Engineer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
source-git-commit: 4ed604cb1969212421fecd40996d7b25af50a2b2
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 10%

---

# Edge 实施的先决条件

本节中介绍的先决条件特定于通过Edge实施实施Adobe流媒体收集加载项。

1. **完成常规先决条件**<br>
无论您是实施适用于仅Adobe Analytics实施还是Edge实施的流媒体收集加载项，请确保您满足以下条件 [常规先决条件](/help/getting-started/prereqs.md).

1. **确认您正在实施与Edge Network和流媒体收集加载项兼容的Adobe解决方案**<br>
在使用Edge实施流媒体收集加载项时，您还必须具有有效的Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer或Real-time Customer Data Platform实施。 有关更多信息，请参阅以下文档资源：
   * [Customer Journey Analytics 指南](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hans)
   * [实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans)
   * [Adobe Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans)
   * [Real-time Customer Data Platform文档](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **获取媒体跟踪服务器URL**<br>
请向您的Customer Journey Analytics代表询问媒体跟踪服务器URL。 <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **使用Edge Network实施流媒体收集加载项**<br>
请按照中的步骤操作 [使用Edge Network实施流媒体收集加载项](/help/implementation/edge/implementation-edge.md).
