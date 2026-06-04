---
title: 内容名称
description: 报告每个媒体会话的可读标题。
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 10%

---


# 内容名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容名称**&#x200B;报告维度。 有关如何收集此变量，请参阅[内容名称](/help/implementation/variables/core/content-name.md)。*

>[!ENDSHADEBOX]

**内容名称**&#x200B;维度报告每个媒体会话的可读标题。

## 如何填充此维度

友好名称由播放器在会话开始时设置。 报告的值与发送的内容相匹配。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.friendlyName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>在Adobe Analytics中，此值还对应于[Content](content.md)维度上的&#x200B;**视频名称**&#x200B;分类。 您负责单独填充和维护该分类。 Customer Journey Analytics直接使用此维度。

>[!IMPORTANT]
>
>如果未设置内容名称，则将为该会话取消填充维度。

## 维度项目

每个项目都是会话开始时报告的字面标题（例如，`"Blinding Light"`）。
