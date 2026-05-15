---
title: 内容
description: 报告每个播放的唯一媒体，按内容ID键控。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 6%

---


# 内容

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容**&#x200B;报告维度。 有关如何收集此变量，请参阅[内容ID](/help/implementation/variables/core/content-id.md)。*

>[!ENDSHADEBOX]

**Content**&#x200B;维度报告每个播放的唯一媒体，并以在会话开始时设置的内容ID作为键值。 它是流媒体报表的主要细分，也是视频名称、视频长度、资产ID、首次播放日期和内容评级等分类维度的联接键。

## 如何填充此维度

内容由播放器在会话开始时设置为资产的稳定标识符。 会话的每个后续事件均会报告相同的内容ID。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.name`收集。 在访问期间持续存在。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.name`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `video`, `post_video` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!IMPORTANT]
>
>内容ID为必填项。 如果未设置或为空，则会话将从流媒体报表中删除，并且不会出现在任何媒体报表或[!UICONTROL 所有流媒体]区段中。

## 维度项目

每个项目都是一个在会话开始时报告的唯一内容ID。 使用稳定的标识符(例如，内部CMS ID、行业ID（例如EIDR或TMS/Gracenote）或永久概要)，以便同一资源的会话会随着时间的推移汇总到单个行项目。

## 推荐的区段

| 区段 | 规则 |
| --- | --- |
| [!UICONTROL 所有流媒体] | 存在内容(ID) |
