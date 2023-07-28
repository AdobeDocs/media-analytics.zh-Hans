---
title: 仅限Adobe Analytics实施的先决条件
description: 了解将流媒体用于仅限Adobe Analytics实施的先决条件
feature: "Media Analytics, System Requirements"
role: User, Admin, Data Engineer
source-git-commit: c4d058ee82f4995f42bfe21c0442004f1f7ea4af
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 58%

---

# 仅限Adobe Analytics实施的先决条件

本节中描述的先决条件特定于使用仅AdobeAnalytics实施（不使用Edge时）实施流媒体。

1. **完成常规先决条件**<br>
无论是为仅Adobe Analytics实施还是为Edge实施实施流媒体，都应确保您满足 [常规先决条件](/help/getting-started/prereqs.md).

1. **确认您实施了Adobe Analytics**<br>
使用仅限Analytics的实施来实施流媒体时，还需要使用Adobe Analytics基本实施。 有关更多信息，请参阅[实施 Adobe Analytics](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=zh-Hans)。

1. **获取媒体跟踪服务器 URL**<br>
请向您的 Adobe Analytics 代表询问媒体跟踪服务器 URL。这是移动 SDK、JavaScript SDK 和 Roku 的非收藏集 API 跟踪服务器的 `collection-api-server` URL。API 实施的域名是：`[your_namespace].hb-api.omtrdc.net`。

1. **下载当前的 Media SDK 或实施所需的扩展**<br>
根据实施路径的不同，为 Web、移动或过顶平台[下载当前 SDK](/help/getting-started/download-sdks.md)。必须实施所需的扩展才能启用适用于流媒体的 Adobe Analytics 扩展路径。

1. **启用 Adobe Analytics 报告**<br>
要在 Analytics 中启用报告，并查看所收集的内容和广告数据，您必须在 Analytics 中启用报告。请参阅[媒体报告启用](/help/reporting/media-reports-enable.md)。
