---
title: 章节数
description: 报告在会话期间开始的章节数量。
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---


# 章节数

**章节计数**&#x200B;量度报告会话期间开始的章节数量。 使用它可比较不同内容中的章节使用情况。 对于按章节维度（章节名称、位置）透视的章节开始计数，请使用启用章节变量类别时可用的章节开始量度。

## 如何计算此指标

会话期间每收到`media.chapterStart`个事件，媒体后端就会递增`mediaReporting.sessionDetails.chapterCount`。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.chapterCount`映射到自定义事件的[处理规则](https://experienceleague.adobe.com/zh-hans/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （处理规则将`a.media.chapterCount`映射到的自定义事件；请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
