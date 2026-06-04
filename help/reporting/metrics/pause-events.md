---
title: 暂停事件
description: 计算会话期间发生的每次不同暂停次数。
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# 暂停事件

**暂停事件**&#x200B;量度计算会话期间收到的每个不同的[暂停开始](/help/implementation/events/playback/pause-start.md)事件，包括同一会话中的多次暂停。 请将其与[总暂停持续时间](total-pause-duration.md)配对，以获取平均暂停长度，并将其与[受暂停影响的流](paused-impacted-streams.md)配对，以计算至少暂停一次的会话。

## 如何计算此指标

媒体后端在每[个暂停开始](/help/implementation/events/playback/pause-start.md)事件时增加此计数。 单个连续暂停会生成一个增量，而不管其持续时间如何。 在播放器保持暂停状态时发送的心率[ping](/help/implementation/events/playback/ping.md)属于相同的暂停时段，并且不会再次递增计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.pauseCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | 不适用 |
