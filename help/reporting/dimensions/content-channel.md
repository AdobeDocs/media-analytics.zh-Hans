---
title: 内容渠道
description: 报告每个会话播放的分发站点、网络或属性。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 7%

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
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.channel`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>如果未设置渠道，则会为该会话取消填充维度。

## 维度项目

每一项都是会话开始时设置的文本字符串。 可接受任何字符串。 典型值是网络名称、站点路径的一部分或内部属性标识符。
