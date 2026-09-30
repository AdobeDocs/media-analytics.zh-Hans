---
title: 内容名称
description: 报告每个媒体会话的可读标题。
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 11%
---

# 内容名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容名称**报告维度。 有关如何收集此变量，请参阅[内容名称](/help/implementation/variables/core/content-name.md)。*

>[!ENDSHADEBOX]

**内容名称**&#x200B;维度报告每个媒体会话的可读标题。

## 如何填充此维度

友好名称由播放器在会话开始时设置。 报告的值与发送的内容相匹配。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.friendlyName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
