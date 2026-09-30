---
title: 内容播放器名称
description: 报告每个媒体会话由哪个播放器呈现。
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
source-wordcount: '196'
ht-degree: 7%
---

# 内容播放器名称

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容播放器名称**报告维度。 有关如何收集此变量，请参阅[内容播放器名称](/help/implementation/variables/core/content-player-name.md)。*

>[!ENDSHADEBOX]

**内容播放器名称**&#x200B;维度报告哪个播放器呈现了每个媒体会话（例如，`HTML5 Player`、`Brightcove`或`Roku Player`）。 使用它来比较同一资产中不同参与者的参与度、完成度和质量。

## 如何填充此维度

播放器名称由播放器在会话开始时设置，并在会话期间持续存在。 该值会在每个事件中发送并在Adobe Analytics和Customer Journey Analytics中报告。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.playerName`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>如果未设置播放器名称，则会为该会话取消填充维度。 在报表中，无法按播放器划分没有播放器名称的会话。

## 维度项目

每一项都是会话开始时设置的文本字符串。 对每个播放器使用稳定、不同的名称，以便不同播放器的数据不会折叠到单个行项目中。
