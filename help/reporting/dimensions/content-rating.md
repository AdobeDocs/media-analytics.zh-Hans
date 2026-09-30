---
title: 内容评级
description: 报告由电视节目家长指南或区域评级系统定义的受众评级。
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
source-wordcount: '400'
ht-degree: 2%
---

# 内容评级

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容评级**&#x200B;报告维度。 有关如何收集此变量，请参阅[内容评级](/help/implementation/variables/standard-metadata/content-rating.md)。*

>[!ENDSHADEBOX]

**内容评级**&#x200B;维度报告每个会话的受众评级。 使用它来比较各评级层的参与度和广告负载。

## 如何填充此维度

内容评级由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics（处理规则） | 创建将`a.media.rating`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Adobe Analytics（分类） | [内容(ID)](content.md)维度的分类。 为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;后，Adobe会自动创建此分类。 您负责填充和维护分类值。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送（处理规则） | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.rating`映射到的eVar） |
| 数据馈送（分类） | 不适用 — 数据馈送不支持分类。 |
| Audience Manager | `c_contextdata.a.media.rating` |

## 分类方法

为报表包启用&#x200B;**[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)**&#x200B;后，Adobe会自动创建内容评级分类结构。 您负责使用[分类集](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html)填充和维护分类。

此方法在每个内容ID及其评级之间保证存在1:1的关系。 分类更新会以追溯方式应用于该ID的所有历史数据。

>[!IMPORTANT]
>
>请勿更改内容评级分类名称。 重命名它可导致Adobe重新创建原始分类，从而产生重复项。

## 处理规则方法

创建将`a.media.rating`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 这种方法捕获内容评级为每次点击值，而无需分类维护。

取舍是您丢失了内容评级与父[内容(ID)](content.md)维度之间保证的1:1关系。 如果实施在不同事件间为同一内容ID发送的值不一致，则同一内容下可能会显示多个评级。 更新值仅适用于以后的数据。

## 维度项目

每个项目都是会话开始时报告的文字评分值（例如，`"TVY"`、`"TVG"`、`"TVPG"`、`"TVMA"`）。 每个评级系统应遵循一组固定的值，以避免行项目出现碎片情况。
