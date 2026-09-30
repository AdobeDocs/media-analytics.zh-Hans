---
title: 丢帧（维度）
description: 报告每个会话的累计丢帧计数。
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
source-wordcount: '183'
ht-degree: 7%
---

# 丢帧（维度）

>[!BEGINSHADEBOX]

*此页涵盖&#x200B;**丢帧**&#x200B;维度。 Adobe Analytics从同一`a.media.qoe.droppedFrameCount`上下文数据变量自动填充配对的[丢帧（指标）](/help/reporting/metrics/dropped-frames.md)。 Customer Journey Analytics公开单个`xdm.mediaReporting.qoeDataDetails.droppedFrames`字段，您可以将其用作维度或指标。 有关如何收集此变量，请参阅[丢帧](/help/implementation/variables/quality/dropped-frames.md)。*

>[!ENDSHADEBOX]

**丢帧**&#x200B;维度报告会话期间丢帧的总数。 使用维度可按准确放置计数划分参与度。

## 如何填充此维度

播放器在累积丢弃时更新QoE对象的`droppedFrames`值。 后端报告关闭调用中的最新值。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体质量]](/help/reporting/setup/analytics-reporting.md)后，自动从上下文数据`a.media.qoe.droppedFrameCount`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| 数据馈送 | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## 维度项目

每个项目都是关闭调用中报告的文字跌落值。 对于会话级别的布尔报表（是否有任何丢帧），请使用[受丢帧影响的流](/help/reporting/metrics/dropped-frame-impacted-streams.md)。
