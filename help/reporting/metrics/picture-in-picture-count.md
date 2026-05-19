---
title: 画中画计数
description: 报告查看者在会话期间输入画中画的次数。
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# 画中画计数

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**画中画计数**报告量度。 有关如何收集此变量，请参阅[画中画](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

**画中画计数**&#x200B;量度报告查看者在会话期间进入画中画播放的次数。 每个画中画状态开始事件都会增加计数。 与受画中画影响的流配对[（对于会话级别的布尔汇总）](picture-in-picture-streams-impacted.md)，与受画中画影响的流配对（对于总状态时间）[画中画总持续时间](picture-in-picture-total-duration.md)。

## 如何计算此指标

媒体后端会递增每个画中画状态开始事件的此计数。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.pictureinpicture.count`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "pictureInPicture"`，字段`count` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
