---
title: 广告开始
description: 计入会话期间开始播放的每一个广告。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 10%

---


# 广告开始

**广告开始**&#x200B;指标计算会话期间开始播放的每一个广告。 请将其与[广告完成](ad-completes.md)配对，以计算广告完成率，并将其与等效会话级汇总的[广告计数](/help/reporting/metrics/ad-count.md)配对。

## 如何计算此指标

在收到`media.adStart`事件时，媒体后端设置`mediaReporting.advertisingDetails.isStarted = true`。 该量度将在广告开始调用中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.view`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
