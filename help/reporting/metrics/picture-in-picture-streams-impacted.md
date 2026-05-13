---
title: 受画中画影响的流数量
description: 计算查看者至少一次输入画中画的会话数。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---


# 受画中画影响的流数量

>[!BEGINSHADEBOX]

*本页涵盖受画中画影响的&#x200B;**流**报表量度。 有关如何收集此变量，请参阅[画中画](/help/implementation/variables/player-state/picture-in-picture.md)。*

>[!ENDSHADEBOX]

受画中画影响的&#x200B;**流**&#x200B;量度计算查看器至少输入一次画中画播放的会话数。 量度是会话级别的布尔值 — 在同一会话中，多个画中画条目计为一个受影响的流。 对于画中画输入的总量，请使用[画中画计数](picture-in-picture-count.md)。

## 如何计算此指标

媒体后端在第一次收到`statesStart`中具有`pictureInPicture`的`media.statesUpdate`事件时，将`pictureInPicture`条目的`mediaReporting.states[]`中的`isSet`标志设置为`true`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 播放器状态跟踪]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.states.pictureinpicture.set`收集。 |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details)条目，其中`name = "pictureInPicture"`，字段`isSet` |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
