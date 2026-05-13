---
title: 仅 Adobe Analytics 实施的先决条件
description: 了解将流媒体收藏集用于仅限Adobe Analytics的实施或Edge实施的先决条件
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: 7b042e45-e35a-43d6-b59e-282573c6a326
TQID: https://experienceleague.adobe.com/OqimGafihuirpnAaZ4AvrX2lrOmCtr0FLXk3QwoVTew
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 212
ht-degree: 16%

---

# Edge 实施的先决条件

本节中介绍的先决条件特定于通过Edge实施实施Adobe流媒体收集。

1. **完成常规先决条件**<br>
无论您是实施适用于仅Adobe Analytics实施的流媒体收藏集，还是适用于Edge实施的流媒体收藏集，请确保您满足[一般先决条件](/help/getting-started/prereqs.md)。

1. **确认您正在实施与Edge Network和流媒体收藏集兼容的Adobe解决方案**<br>
在使用Edge实施流媒体收集时，您还必须具有有效的Customer Journey Analytics、Adobe Analytics、Adobe Journey Optimizer或Real-Time Customer Data Platform实施。 有关更多信息，请参阅以下文档资源：
   * [Customer Journey Analytics指南](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-landing.html?lang=zh-Hans)
   * [实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)
   * [Adobe Journey Optimizer文档](https://experienceleague.adobe.com/docs/journey-optimizer.html?lang=zh-Hans)
   * [Real-Time Customer Data Platform文档](https://experienceleague.adobe.com/docs/real-time-customer-data-platform.html)

1. **获取媒体跟踪服务器URL**<br>
向您的Customer Journey Analytics代表询问媒体跟踪服务器URL。<!-- This is the `collection-api-server` URL for the Mobile SDK, the JavaScript SDK, and the non-collection-api tracking server for Roku. Domain names for API implementation is: `[your_namespace].hb-api.omtrdc.net`. -->

1. **使用Edge Network实施流媒体收集**<br>
按照[使用Edge Network实施流媒体收藏集](/help/implementation/edge/implementation-edge.md)中的步骤操作。
