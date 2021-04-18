---
title: 区段
description: 区段
uuid: 61906b8c-3362-4463-82be-fe0e741a5eb3
exl-id: a450801c-0d6b-4e2a-8662-f00aaaa6e4e0
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 100%

---

# 区段{#segments}

>[!NOTE]
>
>这些与媒体流类型相关的报表区段是在 2018 年 9 月 13 日与 `streamType` 参数一起引入的。

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
