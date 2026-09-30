---
title: 电台/电视台
description: 报告音频广播内容的电台名称或ID。
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
source-wordcount: '138'
ht-degree: 10%
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
| Adobe Analytics | 启用[[!UICONTROL 音频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.station`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.station`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoaudiostation` |
| Audience Manager | `c_contextdata.a.media.station` |

## 维度项目

每个项目都是会话开始时报告的字面工作站名称或ID。 每个工作站使用一个规范标识符，以便参与不会因调用符号变量而分段。
