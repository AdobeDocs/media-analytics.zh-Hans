---
title: 内容渠道
description: 报告每个会话播放的分发站点、网络或属性。
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
source-wordcount: '163'
ht-degree: 8%
---

# 内容渠道

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容渠道**报告维度。 有关如何收集此变量，请参阅[内容渠道](/help/implementation/variables/core/content-channel.md)。*

>[!ENDSHADEBOX]

**内容渠道**&#x200B;维度报告每个会话播放的分发站点、网络或属性。 使用它可按网络或属性的一部分划分播放。

## 如何填充此维度

渠道由播放器在会话开始时设置，并在会话期间持续存在。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.channel`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>如果未设置渠道，则会为该会话取消填充维度。

## 维度项目

每一项都是会话开始时设置的文本字符串。 可接受任何字符串。 典型值是网络名称、站点路径的一部分或内部属性标识符。
