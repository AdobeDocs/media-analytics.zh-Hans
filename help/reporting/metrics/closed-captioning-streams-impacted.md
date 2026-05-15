---
title: 受隐藏式字幕影响的流数量
description: 计算查看器至少启用一次字幕的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# 受隐藏式字幕影响的流数量

>[!BEGINSHADEBOX]

*本页涵盖受隐藏式字幕影响的&#x200B;**流**报表量度。 有关如何收集此变量，请参阅[隐藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)。*

>[!ENDSHADEBOX]

受隐藏式字幕影响的&#x200B;**流**&#x200B;量度计算查看器至少启用一次字幕的会话数。 量度是会话级别的布尔值 — 在一个受影响的流中，同一会话计数内切换多个字幕。 对于总启用字幕的音量，请使用[隐藏式字幕计数](closed-captioning-count.md)。

## 如何计算此指标

媒体后端在第一次收到`statesStart`中具有`closedCaptioning`的`media.statesUpdate`事件时，将`closedCaptioning`条目的`mediaReporting.states[]`中的`isSet`标志设置为`true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.closedcaptioning.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "closedCaptioning"`，字段`isSet` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
