---
title: 平均分钟观众数
description: 报告内容运行时在任意给定分钟观看的平均查看者数量。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# 平均分钟观众数

**平均受众访问分钟数**&#x200B;量度报告内容运行时在任意给定分钟观看的平均观看人数。 这是标准的“AMA”衡量标准，用于比较不同长度内容之间的媒体覆盖范围。

## 如何计算此指标

媒体后端将每个会话的平均受众访问分钟数计算为`Content time spent / Content length`。 当跨会话合计时，总计表示内容每分钟的平均受众大小。 该量度在结束调用时报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.averageMinuteAudience`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `event_list`，`post_event_list` （请参阅[`event.tsv`](https://experienceleague.adobe.com/zh-hans/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)查找） |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>平均受众访问分钟数要求非零[内容长度](/help/reporting/dimensions/content-length.md)。 如果内容长度未设置或为零，则不会为会话生成此量度。
