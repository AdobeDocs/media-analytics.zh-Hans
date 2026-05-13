---
title: 广告完成
description: 计入每个播放到结束的广告。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# 广告完成

**广告完成**&#x200B;量度计算每个播放到结束的广告。 将其与[广告开始](ad-starts.md)配对，以计算广告完成率。

## 如何计算此指标

在收到`media.adComplete`事件时，媒体后端设置`mediaReporting.advertisingDetails.isCompleted = true`。 该量度将在广告关闭调用中报告。 跳过或放弃的广告不计为已完成。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体广告]](/help/reporting/media-reports-enable.md)时，从上下文数据`a.media.ad.complete`自动收集。 |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
