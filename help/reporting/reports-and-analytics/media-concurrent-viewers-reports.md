---
title: 媒体并行查看者
description: 了解用于显示一天中的并行查看者的“媒体并行查看者”仪表板。 数据可以按内容、设备类型或国家/地区进行过滤。
uuid: e61c50e5-8196-4538-b67c-ebc01c6e6ba7
exl-id: 2c679c1a-a4bd-44fc-8e11-173c8544ab06
feature: Streaming Media, Workspace Basics
role: User, Admin
TQID: https://experienceleague.adobe.com/8pqoGpVCRXvovD-cNPNOvFQFvJco3sWUq3SuXEOVeJI
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: e38cbddc-1633-4cd5-bed5-9f289f2a6029
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 299
ht-degree: 91%

---

# 媒体并行查看者报表 {#media-concurrent-viewers}

“媒体并行查看者”仪表板显示一天内的并行查看者。 数据可以按内容、设备类型或国家/地区进行过滤。

>[!TIP]
>
> 此报表基于并行活动媒体会话。  要按独特访客以及通过应用区段、进行细分和比较的附加功能查看并行查看者，请使用 [Analysis Workspace 中的“媒体并行查看者”面板](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/panels/media-concurrent-viewers.html?lang=zh-Hans)。
>

![](assets/video-concurrent-viewers.png)

## 报表特点 {#report-features}

以下是此报表的一些特点：

* 非实时。 具有正常 Adobe Analytics 延迟。
* 报表涵盖 24 小时时间范围。 x 轴是基于报表包时区的每日时间。
* 以分钟粒度显示并行查看者。
* 有一个“媒体并行查看者报表”**，其中显示了在所有内容中正在观看或收听的查看者数量。
* “媒体详细信息”**&#x200B;报表内有一个“并行查看者”报告，其中显示了正在观看或收听某一特定媒体项目的查看者数量。
* 报表仅在一天内有效。
* 客户可以查看并行查看者历史报表（仅限一天）。

## 限制 {#limitations}

以下是此报表的一些限制：

* 如果选择的间隔不是一整天，则不会显示任何数据。
* 无法导出数据，如 ReportBuilder。
* 不能以表格式显示数据。
* 无法通过电子邮件发送报表。
* 即使不跟踪广告，也必须重新启用媒体跟踪并选择“媒体广告”模块。
* 在使用具有暂停跟踪功能的心跳库时，此功能将提供准确的数据。
