---
title: 专辑
description: 报告音轨所属的相册。
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
source-wordcount: '136'
ht-degree: 10%
---

# 专辑

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**相册**&#x200B;报告维度。 请参阅[相册](/help/implementation/variables/standard-metadata/album.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**相册**&#x200B;维度报告该音轨所属的相册（例如，`"Pinegrove"`）。 使用它可以在同一专辑的曲目间汇总参与度。

## 如何填充此维度

相册由播放器在会话开始时为音频内容设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.album`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## 维度项目

每个项目都是会话开始时报告的文字相册标题。 来自不同艺术家的具有相同标题的两张专辑折叠为单个行项目。 与[艺人](artist.md)维度配对，以消除混淆。
