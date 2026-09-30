---
title: 流格式
description: 报告每个会话的质量层（通常为HD或SD）。
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
source-wordcount: '168'
ht-degree: 7%
---

# 流格式

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**流格式**&#x200B;报告维度。 有关如何收集此变量，请参阅[流格式](/help/implementation/variables/standard-metadata/stream-format.md)。*

>[!ENDSHADEBOX]

**流格式**&#x200B;维度报告每个会话的质量层（通常为`"HD"`或`"SD"`，但可接受任何字符串）。 使用它来比较不同交付质量层的参与度、完成度和质量。

## 如何填充此维度

流格式由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.format`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.streamFormat`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.format`映射到的eVar） |
| Audience Manager | `c_contextdata.a.media.format` |

## 维度项目

每一项都是会话开始时报告的文字格式值。 使用稳定的值集(`HD`、`SD`、`4K`、`UHD`)，以使行项目不会跨拼写变量进行分段。
