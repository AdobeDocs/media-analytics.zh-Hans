---
title: 隐藏式字幕计数
description: 报告查看者在会话期间启用字幕的次数。
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%
---

# 隐藏式字幕计数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**隐藏式字幕计数**&#x200B;报表量度。 有关如何收集此变量，请参阅[隐藏式字幕](/help/implementation/variables/player-state/closed-captioning.md)。*

>[!ENDSHADEBOX]

**隐藏式字幕计数**&#x200B;量度报告查看器在会话期间启用字幕的次数。 每个启用字幕的状态开始事件都会增加计数。 与受隐藏式字幕[&#128279;](closed-captioning-streams-impacted.md)影响的流配对，用于会话级别的布尔汇总，与受隐藏式字幕影响的[隐藏式字幕总持续时间](closed-captioning-total-duration.md)配对，用于总状态时间。

## 如何计算此指标

媒体后端会在每个启用字幕的状态开始事件上增加此计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.states.closedcaptioning.count`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "closedCaptioning"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
