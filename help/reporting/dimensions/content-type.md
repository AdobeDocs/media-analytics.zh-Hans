---
title: 内容类型
description: 报告流的格式（VOD、Live、Linear、Podcast、song等）。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

---


# 内容类型

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**内容类型**报告维度。 有关如何收集此变量，请参阅[内容类型](/help/implementation/variables/core/content-type.md)。*

>[!ENDSHADEBOX]

**内容类型**&#x200B;维度报告流的格式（例如，视频为VOD、直播或线性，音频为歌曲、播客或有声书）。

## 如何填充此维度

内容类型由播放器在会话开始时设置，并在每个事件中执行。 它不是派生的；报告的值与收集期间发送的值匹配。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.contentType`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>如果未设置内容类型或内容类型为空，则维度将报告会话的`missing_content_type`。 使用此值可查找需要修复的实施。

## 维度项目

Adobe定义的值会填充内置区段和报表。 接受自定义字符串，但不会匹配内置区段。

| 流类型 | 推荐值 |
| --- | --- |
| 视频 | `vod`, `live`, `linear`, `ugc`, `dvod` |
| 音频 | `song`, `podcast`, `audiobook`, `radio` |

## 推荐的区段

| 区段 | 规则 |
| --- | --- |
| [!UICONTROL VOD内容] | 内容类型= `vod` |
| [!UICONTROL 实时内容] | 内容类型= `live` |
| [!UICONTROL 线性内容] | 内容类型= `linear` |
