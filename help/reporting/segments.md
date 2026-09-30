---
title: 媒体流区段解释
description: 了解与媒体流类型相关的报表区段，包括媒体流类型的区段、描述和规则。
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
feature: Streaming Media, Segmentation
role: User, Admin, Developer
TQID: 'https://experienceleague.adobe.com/7RwJQtw-jHlMMV1yc80lUyEYIwIxR-3oh7vN04cPcRg'
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b069d60e-95f3-44d6-95a8-ddc862a4bc38
    internal-label: Reports
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
    internal-label: API
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
  - id: c47a19a5-f47b-4e53-afe0-e230da195ebe
    internal-label: Segmentation
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '189'
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
