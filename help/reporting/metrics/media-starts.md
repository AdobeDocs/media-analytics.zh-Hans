---
title: 媒体开始
description: 计算开始的每个媒体会话，包括以前置广告或缓冲结束的会话。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# 媒体开始

**媒体开始**&#x200B;量度将计入每个开始的媒体会话。 一旦后端收到`media.sessionStart`事件，即使查看者在前置式广告、缓冲或任何主内容播放之前退出，服务器端也会增加。 将其用作funnel排名最前的媒体报表量度；将其与[Content starts](content-starts.md)配对，以测量广告和缓冲流失。

## 如何计算此指标

在收到`media.sessionStart`事件时，媒体后端设置`mediaReporting.sessionDetails.isViewed = true`。 报告的指标是每个会话`1`。 “媒体开始”报告在开始调用上，而不是在结束调用上。 这是唯一一个不会等待会话关闭的阶段1量度。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.view`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
