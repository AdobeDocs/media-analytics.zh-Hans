---
title: 受全屏影响的流数量
description: 计算查看者至少进入全屏一次的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# 受全屏影响的流数量

>[!BEGINSHADEBOX]

*本页涵盖受全屏影响的&#x200B;**流**&#x200B;报表量度。 有关如何收集此变量，请参阅[全屏](/help/implementation/variables/player-state/full-screen.md)。*

>[!ENDSHADEBOX]

受全屏影响的&#x200B;**流**&#x200B;量度计算查看器至少进入全屏一次的会话数。 量度是会话级别的布尔值 — 同一会话中的多个全屏条目计为一个受影响的流。 若要获得全屏输入总数量，请使用[全屏计数](full-screen-count.md)。

## 如何计算此指标

媒体后端在第一次收到`statesStart`中具有`fullscreen`的`media.statesUpdate`事件时，将`fullscreen`条目的`mediaReporting.states[]`中的`isSet`标志设置为`true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.fullscreen.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "fullscreen"`，字段`isSet` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
