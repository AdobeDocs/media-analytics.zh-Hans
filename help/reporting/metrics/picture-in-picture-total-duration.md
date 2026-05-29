---
title: 画中画总时长
description: 报告查看者在会话期间画中画所花费的累积秒数。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---


# 画中画总时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**画中画总持续时间**&#x200B;报告量度。 有关如何收集此变量，请参阅[画中画](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**画中画总持续时间**&#x200B;量度报告查看者在会话期间画中画所花费的累计时间（以秒为单位）。 后端对画中画状态开始和匹配状态结束事件之间的每个间隔求和。

## 如何计算此指标

媒体后端计算会话期间所有画中画间隔的经过时间总和。 该量度在结束调用时报告。 Analysis Workspace将该值显示为`HH:MM:SS`；数据馈送、Data Warehouse和报表API以秒为单位显示该值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.pictureinpicture.time`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "pictureInPicture"`，字段`time` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
