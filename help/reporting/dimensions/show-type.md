---
title: 节目类型
description: 报告内容格式（全集、预览、剪辑或其他）。
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# 节目类型

>[!BEGINSHADEBOX]

*此页面涵盖&#x200B;**显示类型**&#x200B;报告维度。 有关如何收集此变量，请参阅[显示类型](/help/implementation/variables/standard-metadata/show-type.md)。*

>[!ENDSHADEBOX]

**显示类型**&#x200B;维度使用字符串整数代码报告内容格式。 在衡量参与度时，使用它可将完整节目观看与短格式内容（如预告片和剪辑）分开。

## 如何填充此维度

节目类型由播放器在会话开始时设置。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 启用[[!UICONTROL 视频元数据]](/help/reporting/media-reports-enable.md)时，自动从上下文数据`a.media.type`收集。 |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## 维度项目

| 值 | 描述 |
| --- | --- |
| `0` | 整集 |
| `1` | 预览或预告片 |
| `2` | 剪辑 |
| `3` | 其他 |

这些值会报告为字符串。 接受自定义值，但不会将其汇总到四个内置存储桶中。
