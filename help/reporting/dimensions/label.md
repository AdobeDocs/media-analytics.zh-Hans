---
title: 标签
description: 报告发布音频内容的录制标签。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
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
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.label`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.label`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudiolabel` |
| Audience Manager | `c_contextdata.a.media.label` |

## 维度项目

每一项都是会话开始时报告的文字标签名称。 为每个标签使用稳定的规范名称，以便参与不会因拼写或压印变体而碎裂。
