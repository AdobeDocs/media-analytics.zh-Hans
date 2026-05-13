---
title: 流类型
description: 捕获每个媒体会话是音频还是视频内容。
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 5%

---


# 流类型

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**流类型**&#x200B;报告维度。 有关如何收集此变量，请参阅[流类型](/help/implementation/variables/core/stream-type.md)。*

>[!ENDSHADEBOX]

**流类型**&#x200B;维度捕获每个媒体会话是音频还是视频内容。 为报表包启用[媒体核心](/help/reporting/media-reports-enable.md)后，它将在Adobe Analytics中可用，并且可用于任何包含流媒体数据的数据集。

## 如何填充此维度

流类型由播放器在会话开始时设置，并持续到会话关闭调用。 它不是计算或派生的。 报告的值与收集期间发送的值完全匹配。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 媒体核心]](/help/reporting/media-reports-enable.md)后，自动从上下文数据`a.media.streamType`收集。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.streamType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videostreamtype` |

>[!IMPORTANT]
>
>如果未设置流类型，则会为该会话取消填充维度。 这些会话将从仅音频和仅视频内置区段中排除，如果与流类型划分结合使用，则所有流媒体区段会少计。

## 维度项目

| 值 | 描述 |
| --- | --- |
| `video` | 该会话包含视频内容。 |
| `audio` | 该会议是播客、有声读物或音乐流等音频内容。 |

从技术上讲，收集API接受自定义值，但不建议这样做。 它们将与下面描述的内置区段不匹配，并且可能会导致实施之间的报表不一致。

## 推荐的区段

流类型是Adobe Analytics的内置[!UICONTROL 媒体流类型]区段的基础。 使用这些区段将任何流媒体报表的范围限定为特定内容类型：

| 区段 | 规则 |
| --- | --- |
| [!UICONTROL 所有流媒体] | 存在内容(ID) |
| [!UICONTROL 仅限音频] | 存在内容(ID)且流类型= `audio` |
| [!UICONTROL 仅限视频] | 内容(ID)存在且流类型!=`audio` |

>[!TIP]
>
>[!UICONTROL 仅视频]区段使用`!=`规则而不是`= video`正确捕获流类型可能设置为非`audio`的自定义值的会话。
