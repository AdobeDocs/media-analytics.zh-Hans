---
title: 已下载媒体
description: 标记播放下载的离线内容的会话。
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# 已下载媒体

>[!BEGINSHADEBOX]

*本页介绍&#x200B;**下载的媒体**报告维度。 有关如何收集此变量，请参阅[媒体下载标志](/help/implementation/variables/core/media-downloaded-flag.md)。*

>[!ENDSHADEBOX]

**下载的媒体**&#x200B;维度标记播放先前下载的离线内容而不是来自Internet的实时流的会话。 在比较参与度、完成度或质量时，使用它可将离线播放与流式处理会话分离。

## 如何填充此维度

播放器可通过以下三种方式之一设置下载的标志。 使用标志(Mobile SDK)初始化跟踪器，将`sessionStart`发送到`/downloaded`端点变量（Media Edge API直接），或在`sessionStart`参数（媒体收集API）中包含`media.downloaded: true`。

| 报告系统 | 来源 |
| --- | --- |
| Adobe Analytics | 创建将`a.media.downloaded`映射到eVar的[处理规则](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview)。 |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| 数据馈送 | `evar1`-`evar250`，`post_evar1`-`post_evar250` （您的处理规则将`a.media.downloaded`映射到的eVar） |
| Audience Manager | `c_contextdata.a.media.downloaded` |

## 维度项目

| 值 | 描述 |
| --- | --- |
| `true` | 会话播放了下载的离线内容。 |
| （空） | 会话播放了实时流。 该字段被省略，而不是设置为`false`。 |
