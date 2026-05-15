---
title: 全屏计数
description: 报告查看器在会话期间进入全屏的次数。
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 8%

---


# 全屏计数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**全屏计数**&#x200B;报告量度。 有关如何收集此变量，请参阅[全屏](/help/implementation/variables/player-state/full-screen.md)。*

>[!ENDSHADEBOX]

**全屏计数**&#x200B;量度报告查看器在会话期间进入全屏的次数。 每个全屏状态开始事件都会增加计数。 与受全屏[&#128279;](full-screen-streams-impacted.md)影响的[个流配对，以生成会话级别的布尔汇总；与全屏总持续时间](full-screen-total-duration.md)配对，以生成状态总时间。

## 如何计算此指标

媒体后端在每个state-start全屏事件中递增`mediaReporting.states[]`的`fullscreen`条目中的`count`字段。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.fullscreen.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "fullscreen"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
