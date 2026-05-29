---
title: 发布者
description: 报告音频内容发布者。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# 发布者

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**发布者**&#x200B;报告维度。 有关如何收集此变量，请参阅[发布者](/help/implementation/variables/standard-metadata/publisher.md)。*

>[!ENDSHADEBOX]

**发布者**&#x200B;维度报告音频内容发布者（例如，播客网络或有声读物发布者）。 使用它可以在策划的音频目录中比较发布者之间的参与情况。

## 如何填充此维度

Publisher由播放器在会话开始时为音频内容设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.publisher`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## 维度项目

每一项都是会话开始时报告的文字发布者名称。
