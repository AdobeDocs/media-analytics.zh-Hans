---
title: 仅限Adobe Analytics实施的先决条件
description: 了解将流媒体用于仅限Adobe Analytics实施的先决条件
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: 8a0f2c0b367b48ee5ac94e7fc6bcd0eadafbc5d8
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 13%

---

# Edge实施的先决条件

本节中介绍的先决条件特定于使用Edge实施实施流媒体。

1. **完成常规先决条件**<br>
无论是为仅Adobe Analytics实施还是为Edge实施实施流媒体，都应确保您满足 [常规先决条件](/help/getting-started/prereqs.md).

1. **确认您正在实施与Edge和流媒体兼容的Adobe解决方案**<br>
使用Edge实施流媒体时，您还必须具有有效的Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer或Real-time Customer Data Platform实施。 有关更多信息，请参阅以下文档资源：
   * [Customer Journey Analytics 指南](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hans)
   * [实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans)
   * [Adobe Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans)
   * [Real-time Customer Data Platform文档](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **获取媒体跟踪服务器URL**<br>
请向您的Customer Journey Analytics代表询问媒体跟踪服务器URL。 <!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **安装Media Analytics和Edge**<br>
请按照中的步骤操作 [安装Media Analytics和Experience Platform边缘](/help/implementation/edge/implementation-edge.md).