---
title: 计算量度
description: Adobe Analytics和Customer Journey Analytics中流媒体报表的自定义计算量度。
feature: Metrics
role: User, Admin
source-git-commit: 1251b66173158b8fea92516197b3b9f444bfaaf7
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---

# 计算量度

Adobe流媒体服务的计算量度是基于标准流媒体量度构建的自定义量度，可让您在不更改实施的情况下得出平均广告逗留时间或媒体完成率等比率。

要在Analysis Workspace中创建这些计算指标，请在[Adobe Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics/components/calculated-metrics/cm-overview)或[Customer Journey Analytics](https://experienceleague.adobe.com/zh-hans/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview)中查看各自的计算指标概述。

| 计算量度 | 描述 | 公式 |
| --- | --- | --- |
| 平均 每个媒体流的广告 | 每次媒体开始的广告开始次数 | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 每个媒体流的章节数 | 每次媒体开始的章节开始次数 | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 媒体逗留时间 | 每次媒体开始的总逗留时间(`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 平均 内容逗留时间 | 每次内容开始的内容逗留时间(`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 平均 广告逗留时间 | 每次广告开始的广告逗留时间(`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 平均 章节逗留时间 | 每次章节开始的章节逗留时间(`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 媒体完成率 | 内容完成次数与媒体启动次数的比率 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 内容完成率 | 内容完成次数与内容开始次数的比率 | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| 广告完成率 | 广告完成次数与广告开始次数的比率 | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| 章节完成率 | 章节结束次数与章节开始次数的比率 | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| 开始前放弃的比率 | 开始前丢帧次数与媒体开始次数的比率 | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| 内容暂停持续时间率 | 总暂停时间与内容逗留时间的比率 | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 内容缓冲时间率 | 缓冲总时间与内容逗留时间的比率 | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 内容开始时间率 | 开始时间与内容逗留时间的比率 | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| 广告逗留时间率 | 广告逗留时间与内容逗留时间的比率 | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |

