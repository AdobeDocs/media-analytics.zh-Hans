---
title: 艺人
description: 报告音频内容的表演艺术家。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# 艺人

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**Artist**&#x200B;报告维度。 请参阅[艺术家](/help/implementation/variables/standard-metadata/artist.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**艺人**&#x200B;维度报告音频内容的表演艺人（例如，`"Crested Larks"`）。 使用它可按表演者划分音乐或播客目录的参与度。

## 如何填充此维度

艺人由播放器在会话开始时为音频内容设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.artist`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudioartist` |

## 维度项目

每个项目都是会话开始时报告的文字艺术家姓名。 为每个艺术家使用稳定的规范名称，以便数据不会在不同格式变量之间分段。
