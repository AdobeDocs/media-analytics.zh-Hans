---
title: 内容时长
description: 报告在会话开始时设置的每个媒体会话的总持续时间（以秒为单位）。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 6%

---


# 内容时长

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容长度**&#x200B;报告维度。 有关如何收集此变量，请参阅[内容长度](/help/implementation/variables/core/content-length.md)。*

>[!ENDSHADEBOX]

**内容长度**&#x200B;维度报告在会话开始时设置的每个媒体会话的总持续时间（以秒为单位）。 它支持后端量度，包括[进度标记](/help/reporting/metrics/progress-markers.md)和[平均受众访问分钟数](/help/reporting/metrics/average-minute-audience.md)。

## 如何填充此维度

内容长度由播放器在会话开始时设置。 报告的值是资产的完整持续时间（以秒为单位），而不是播放头经过的时间。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.length`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videolength, post_videolength` |

>[!NOTE]
>
>在Adobe Analytics中，此值还对应于[Content](content.md)维度上的&#x200B;**视频长度**&#x200B;分类。 您负责单独填充和维护该分类。 Customer Journey Analytics直接使用此维度。 如果需要，您可以使用[值分段](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/component-settings/value-bucketing)。

>[!IMPORTANT]
>
>如果未设置内容时长，或者内容时长不大于零，则不会为该会话生成进度标记和平均受众访问分钟数。 对于持续时间未知的实时流，请设置`86400`。

## 维度项目

每个项目都是在会话开始时报告的文字长度值（以秒为单位）。
