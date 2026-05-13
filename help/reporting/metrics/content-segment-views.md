---
title: 内容区段视图
description: 计算发生活动主内容播放的区段。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# 内容区段视图

**内容区段视图**&#x200B;量度计算发生活动主内容播放的五分钟内容区段。 该量度用于确认查看者是否在该区段中播放了内容，而不仅仅是加载或缓冲。 将其与[内容区段](/help/reporting/dimensions/content-segment.md)维度配对，以划分长格式内容查看者实际使用的部分。

## 如何计算此指标

媒体后端为任何涵盖区段的结束调用设置`mediaReporting.sessionDetails.hasSegmentView = true`，在该区段中至少接收到了主内容的一个`media.play`事件。 该量度在结束调用时报告。 在Media Edge API路径上，区段视图是在与内容启动相同的条件下触发的。 两者都需要主内容上的`media.play`。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.segmentView`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
