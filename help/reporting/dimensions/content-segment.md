---
title: 内容区段
description: 报告在会话期间查看的播放头范围（以分钟为单位）。
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
source-wordcount: '202'
ht-degree: 6%
---

# 内容区段

**内容区段**&#x200B;维度报告在会话期间查看的播放头范围，以分钟为单位（例如，`[0-5]`表示分钟0到5）。 后端根据播放期间报告的最小和最大播放头值计算区段。 将其与[内容区段视图](/help/reporting/metrics/content-segment-views.md)量度一起使用，以分析长格式内容查看器实际使用的部分。

## 如何填充此维度

内容区段由媒体后端根据会话事件中报告的播放头值计算。 客户端未设置此参数。 报告的值派生自播放期间看到的播放头值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.segment`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>如果会话期间未正确报告播放头，则计算区段可能不准确。 对于实时流，根据会话期间看到的相对播放头值计算区段。

## 维度项目

每个项目都是一个字符串范围，它涵盖了会话期间所看到的播放头值（例如，`[0-5]`、`[5-10]`、`[10-15]`）。 粒度固定为5分钟。
