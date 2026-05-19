---
title: 专辑
description: 报告音轨所属的相册。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
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
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.album`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.album`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudioalbum` |
| Audience Manager | `c_contextdata.a.media.album` |

## 维度项目

每个项目都是会话开始时报告的文字相册标题。 来自不同艺术家的具有相同标题的两张专辑折叠为单个行项目。 与[艺人](artist.md)维度配对，以消除混淆。
