---
title: 计算量度
description: Adobe Analytics和Customer Journey Analytics中流媒体报表的自定义计算量度。
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 计算量度

Adobe流媒体服务的计算量度是基于标准流媒体量度构建的自定义量度，可让您在不更改实施的情况下得出平均广告逗留时间或媒体完成率等比率。

要在Analysis Workspace中创建这些计算指标，请在[Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview)或[Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)中查看各自的计算指标概述。

| 计算量度 | 描述 | 公式 |
| --- | --- | --- |
| 平均 每个媒体流的广告 | 每[[!UICONTROL 个媒体开始的[[!UICONTROL 广告开始次数]](/help/reporting/metrics/ad-starts.md)]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| 平均 每个媒体流的章节数 | 每个[[!UICONTROL 媒体开始的[[!UICONTROL 章节开始次数]](/help/reporting/metrics/chapter-starts.md)]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| 平均 媒体逗留时间 | 每[[!UICONTROL 个媒体开始]](/help/reporting/metrics/media-starts.md)的[[!UICONTROL 媒体逗留时间]](/help/reporting/metrics/media-time-spent.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| 平均 内容逗留时间 | 每个[[!UICONTROL 内容开始时间[[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| 平均 广告逗留时间 | 每[[!UICONTROL 个广告开始的[[!UICONTROL 广告逗留时间]](/help/reporting/metrics/ad-time-spent.md)]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| 平均 章节逗留时间 | 每个[[!UICONTROL 章节开始的[[!UICONTROL 章节逗留时间]](/help/reporting/metrics/chapter-time-spent.md)]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| 媒体完成率 | [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md)与[[!UICONTROL 媒体开始]](/help/reporting/metrics/media-starts.md)的速率 | `[Content completes] / [Media starts]` |
| 内容完成率 | [[!UICONTROL 内容完成]](/help/reporting/metrics/content-completes.md)与[[!UICONTROL 内容开始]](/help/reporting/metrics/content-starts.md)的速率 | `[Content completes] / [Content starts]` |
| 广告完成率 | [[!UICONTROL 广告完成]](/help/reporting/metrics/ad-completes.md)与[[!UICONTROL 广告开始]](/help/reporting/metrics/ad-starts.md)的速率 | `[Ad completes] / [Ad starts]` |
| 章节完成率 | [[!UICONTROL 章节完成]](/help/reporting/metrics/chapter-completes.md)与[[!UICONTROL 章节开始]](/help/reporting/metrics/chapter-starts.md)的速率 | `[Chapter completes] / [Chapter starts]` |
| 开始前放弃的比率 | [[!UICONTROL 开始前丢帧]](/help/reporting/metrics/drops-before-start.md)与[[!UICONTROL 媒体开始次数]](/help/reporting/metrics/media-starts.md)的速率 | `[Drops before start] / [Media starts]` |
| 内容暂停持续时间率 | [[!UICONTROL 总暂停持续时间]](/help/reporting/metrics/total-pause-duration.md)与[[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)的速率 | `[Total pause duration] / [Content time spent]` |
| 内容缓冲时间率 | [[!UICONTROL 总缓冲持续时间]](/help/reporting/metrics/total-buffer-duration.md)与[[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)的速率 | `[Total buffer duration] / [Content time spent]` |
| 内容开始时间率 | [[!UICONTROL 开始时间]](/help/reporting/metrics/time-to-start.md)与[[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Time to start] / [Content time spent]` |
| 广告逗留时间率 | [[!UICONTROL 广告逗留时间]](/help/reporting/metrics/ad-time-spent.md)与[[!UICONTROL 内容逗留时间]](/help/reporting/metrics/content-time-spent.md)的比率 | `[Ad time spent] / [Content time spent]` |

