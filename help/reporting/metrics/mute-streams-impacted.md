---
title: 受静音影响的流数量
description: 计算查看器至少将音频静音一次的会话。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 8%

---


# 受静音影响的流数量

>[!BEGINSHADEBOX]

*本页涵盖受静音影响的&#x200B;**流**&#x200B;报表量度。 有关如何收集此变量，请参阅[静音](/help/implementation/variables/player-state/mute.md)。*

>[!ENDSHADEBOX]

受静音影响的&#x200B;**流**&#x200B;量度计算查看器至少静音一次的会话。 量度是会话级别的布尔值 — 在一个受影响的流中，在同一会话计数内进行多次静音切换。 对于静音音量总计，请使用[静音计数](mute-count.md)。

## 如何计算此指标

媒体后端在会话期间首次收到静音状态开始事件时设置此标志。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.mute.set`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "mute"`，字段`isSet` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
