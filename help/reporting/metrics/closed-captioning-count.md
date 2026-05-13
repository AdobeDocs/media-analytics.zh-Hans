---
title: 隐藏式字幕计数
description: 报告查看者在会话期间启用字幕的次数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 7%

---


# 隐藏式字幕计数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**隐藏式字幕计数**&#x200B;报表量度。 有关如何收集此变量，请参阅[隐藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)。*

>[!ENDSHADEBOX]

**隐藏式字幕计数**&#x200B;量度报告查看器在会话期间启用字幕的次数。 每个启用字幕的状态开始事件都会增加计数。 与受隐藏式字幕[&#128279;](closed-captioning-streams-impacted.md)影响的流配对，用于会话级别的布尔汇总，与受隐藏式字幕影响的[隐藏式字幕总持续时间](closed-captioning-total-duration.md)配对，用于总状态时间。

## 如何计算此指标

媒体后端在每个caption-enable state-start事件中递增`mediaReporting.states[]`的`closedCaptioning`条目中的`count`字段。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.closedcaptioning.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "closedCaptioning"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
