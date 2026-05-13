---
title: 电台/电视台
description: 报告音频广播内容的电台名称或ID。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

---


# 电台/电视台

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**工作站**&#x200B;报告维度。 请参阅[工作站](/help/implementation/variables/standard-metadata/station.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**电台**&#x200B;维度报告广播音频内容的广播电台名称或ID（例如，`"NPR"`或`"WXYZ-FM"`）。 使用它来比较联合网络中不同站点的参与情况。

## 如何填充此维度

Station由播放器在会话开始时为音频内容设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.station`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudiostation` |

## 维度项目

每个项目都是会话开始时报告的字面工作站名称或ID。 每个工作站使用一个规范标识符，以便参与不会因调用符号变量而分段。
