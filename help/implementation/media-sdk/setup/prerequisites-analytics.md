---
title: 仅 Adobe Analytics 实施的先决条件
description: 了解为仅Adobe Analytics实施使用Adobe Analytics for Streaming Media加载项的先决条件
feature: Streaming Media, Workspace Basics
role: User, Admin, Developer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
TQID: https://experienceleague.adobe.com/falbDtUtqAMtmtQs2jLpEvUKmwvATotVu8njuTNZ09k
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: c77ba355-6681-41fe-b719-563d3f507fdb
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 243
ht-degree: 14%

---

# 仅 Adobe Analytics 实施的先决条件

此部分中描述的先决条件特定于为仅Adobe Analytics实施实施的Adobe Analytics for Streaming Media加载项（不使用Edge时）。

1. **完成常规先决条件**<br>
无论您是实施适用于仅Adobe Analytics实施还是Edge实施的流媒体服务，请确保您满足[一般先决条件](/help/getting-started/prereqs.md)。

1. **确认您实施了Adobe Analytics**<br>
为仅Analytics实施实施Adobe Analytics for Streaming Media插件时，还需要Adobe Analytics基本实施。 有关更多信息，请参阅[实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html)。

1. **获取媒体跟踪服务器URL**<br>
请向您的Adobe Analytics代表询问媒体跟踪服务器URL。 这是Mobile SDK的`collection-api-server` URL、JavaScript SDK和Roku的非收藏集API跟踪服务器。 API 实施的域名是：`[your_namespace].hb-api.omtrdc.net`。

1. **下载当前的Media SDK或实施所需的扩展**<br>
根据实施路径，[为Web、移动或过顶平台](/help/getting-started/download-sdks.md)下载当前SDK。 必须实施所需的扩展才能启用适用于流媒体的Adobe Analytics加载项。

1. **启用Adobe Analytics报表**<br>
要在Analytics中启用报表并查看所收集的内容和广告数据，您必须在Analytics中启用报表。 请参阅[媒体报告启用](/help/reporting/media-reports-enable.md)。
