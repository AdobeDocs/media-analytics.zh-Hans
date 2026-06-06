---
title: 媒体流区段解释
description: 了解与媒体流类型相关的报表区段，包括媒体流类型的区段、描述和规则。
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
source-git-commit: cb3770abd06eb8debe4ff92641835f04f62471f7
workflow-type: tm+mt
source-wordcount: 189
ht-degree: 75%

---

# 流媒体区段

您可以使用区段根据特性或网站交互来确定访客子集。 利用流媒体区段，您可以确定访客流类型，例如音频流、实时流或播客流。 有关Adobe Analytics区段的信息，请参阅《Adobe Analytics组件指南》中的[关于区段](https://experienceleague.adobe.com/zh-hans/docs/analytics/components/segmentation/seg-overview)。

| 区段 | 描述 | 规则 |
|---|---|---|
| 媒体流类型: 全部 | 对所有&#x200B;*媒体*&#x200B;流数据进行分段 | “存在内容 (ID)” |
| 媒体流类型: 音频 | 对所有&#x200B;*音频*&#x200B;流数据进行分段 | “存在内容 (ID)”且“媒体流类型 = `audio`” |
| 媒体流类型: 视频 | 对所有&#x200B;*视频*&#x200B;流数据进行分段 | “存在内容 (ID)”且“媒体流类型 != `audio`” |
| 媒体内容类型: VoD | 对所有 VoD 内容进行分段 | &quot;内容类型 = `vod`&quot; |
| 媒体内容类型: 直播 | 对所有实时内容进行分段 | &quot;内容类型 = `live`&quot; |
| 媒体内容类型: 线性 | 对所有线性内容进行分段 | &quot;内容类型 = `linear`&quot; |
| 媒体内容类型: 播客 | 对所有播客内容进行分段 | &quot;内容类型 = `podcast`&quot; |
| 媒体内容类型: 有声书 | 对所有有声读物内容进行分段 | &quot;内容类型 = `audiobook`&quot; |
| 媒体内容类型: AoD | 对所有 AoD 内容进行分段 | &quot;内容类型 = `aod`&quot; |
