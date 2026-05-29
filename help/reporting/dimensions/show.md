---
title: 节目
description: 报告属于某个系列的视频内容的节目或系列名称。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

---


# 节目

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**节目**&#x200B;报告维度。 有关如何收集此变量，请参阅[节目](/help/implementation/variables/standard-metadata/show.md)。*

>[!ENDSHADEBOX]

**显示**&#x200B;维度报告项目或系列名称。 多季的剧集将汇总为相同的节目行项目，因此使用它来比较整个系列生命周期的参与度。

## 如何填充此维度

当内容属于某个系列时，播放器在会话开始时会设置节目。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.show`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## 维度项目

每个项目都是会话开始时报告的文字节目名称（例如，`"Blinding Light"`）。 每次显示使用稳定、不同的名称，以便数据不会在共享单词的非相关程序之间折叠。
