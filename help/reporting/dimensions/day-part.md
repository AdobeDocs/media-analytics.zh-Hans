---
title: 时段
description: 报告内容广播或播放的时段时间（上午、下午、黄金时段、深夜）。
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
source-wordcount: '151'
ht-degree: 9%
---

# 时段

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**时段**&#x200B;报告维度。 请参阅[日期部分](/help/implementation/variables/standard-metadata/day-part.md)以了解如何收集此变量。*

>[!ENDSHADEBOX]

**时段**&#x200B;维度报告广播或播放内容时的时段。 通用值为`"Morning"`、`"Afternoon"`、`"Primetime"`和`"Late Night"`。 使用它可独立于查看者的本地时区来比较不同白天的参与情况。

## 如何填充此维度

播出时段由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/setup/analytics-reporting.md)时，自动从上下文数据`a.media.dayPart`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.dayPart`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videodaypart`, `post_videodaypart` |
| Audience Manager | `c_contextdata.a.media.dayPart` |

## 维度项目

每个项目都是会话开始时报告的文本时段label。 在实施中使用一组固定的值以保持行项目的一致性。
