---
title: 标签
description: 报告发布音频内容的录制标签。
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
source-wordcount: '134'
ht-degree: 10%
---

# 标签

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**标签**&#x200B;报告维度。 有关如何收集此变量，请参阅[标签](/help/implementation/variables/standard-metadata/label.md)。*

>[!ENDSHADEBOX]

**标签**&#x200B;维度报告释放音频内容的录制标签（例如，`"Capitol Records"`）。 使用它来比较音乐或播客目录中不同标签之间的参与度。

## 如何填充此维度

播放器在会话开始时为音频内容设置标签。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.label`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## 维度项目

每一项都是会话开始时报告的文字标签名称。 为每个标签使用稳定的规范名称，以便参与不会因拼写或压印变体而碎裂。
