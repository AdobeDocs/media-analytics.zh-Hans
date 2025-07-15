---
title: 仅 Adobe Analytics 实施的先决条件
description: 了解将流媒体收藏集用于仅限Adobe Analytics实施的先决条件
feature: Streaming Media, Workspace Basics
role: User, Admin, Data Engineer
exl-id: f94a5339-f777-44ec-ba79-0a1986c52225
source-git-commit: 0b0b4a373b15191dcb37dc436413f68cdc70768e
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 44%

---

# 仅 Adobe Analytics 实施的先决条件

此部分中描述的先决条件特定于使用仅Adobe-Analytics实施实施流媒体收集(不使用Edge时)。

1. **完成常规先决条件**<br>
无论您是实施适用于仅Adobe Analytics实施的流媒体收藏集，还是适用于Edge实施的流媒体收藏集，请确保您满足[一般先决条件](/help/getting-started/prereqs.md)。

1. **确认您具有Adobe Analytics实施**<br>
使用仅限Analytics的实施实施流媒体收集时，还需要Adobe Analytics基本实施。 有关更多信息，请参阅[实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans)。

1. **获取媒体跟踪服务器 URL**<br>
请向您的 Adobe Analytics 代表询问媒体跟踪服务器 URL。这是Mobile SDK的`collection-api-server` URL、JavaScript SDK和Roku的非收藏集API跟踪服务器。 API 实施的域名是：`[your_namespace].hb-api.omtrdc.net`。

1. **下载当前的 Media SDK 或实施所需的扩展**<br>
根据实施路径的不同，为 Web、移动或过顶平台[下载当前 SDK](/help/getting-started/download-sdks.md)。必须实施所需的扩展才能启用流媒体收集扩展路径。

1. **启用 Adobe Analytics 报告**<br>
要在 Analytics 中启用报告，并查看所收集的内容和广告数据，您必须在 Analytics 中启用报告。请参阅[媒体报告启用](/help/reporting/media-reports-enable.md)。
