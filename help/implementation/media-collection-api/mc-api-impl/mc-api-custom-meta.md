---
title: 自定义元数据支持
description: 了解如何在sessionStart、chapterStart和adStart事件中提供自定义键：值对。
uuid: df4109dd-9fca-4c33-a7d5-8e6eec257527
exl-id: 672fa804-4a4f-4f06-b29b-b0aad27ca2f3
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/sEVJa-FPqZiSc4Hdr7lQfNbECS2lxckBmqAYhGHmx2w
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 449
ht-degree: 7%

---

# 自定义元数据支持{#custom-metadata-support}

媒体收集API允许您在`sessionStart`、`adStart`和`chapterStart`事件中随标准参数一起发送自定义键值对。 自定义元数据通过相应的媒体关闭事件转发到&#x200B;**Adobe Analytics**。

要使此数据在Analysis Workspace中可用，客户必须定义自定义eVar并配置处理规则，以根据其用例填充这些数据。 在映射到eVar或prop后，如果配置了[Analytics源连接器](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics)，则数据也可以通过相应的eVar路径在Adobe Experience Platform中可用。

对于使用Experience Edge的基于XDM的实施，请参阅[自定义元数据支持 — XDM格式](/help/implementation/edge/custom-metadata.md)。

## 概述

自定义元数据作为`customMetadata`对象包含在请求正文中，位于`params`键旁边。 它适用于三种事件类型：

| 事件 | 元数据应用于 |
|-------|-------------------|
| `sessionStart` | 主要内容（整个会话） |
| `adStart` | 个人广告 |
| `chapterStart` | 内容章节或区段 |

## 结构

自定义元数据是事件级别的平面&#x200B;**对象**（键值对），与`params`键一起使用：

```json
{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "field": "value"
  }
}
```

### 按事件类型列出的必需参数

| 事件 | 必需`params` |
|-------|-------------------|
| `sessionStart` | `analytics.trackingServer`, `analytics.reportSuite`, `visitor.marketingCloudOrgId`, `media.id`, `media.length`, `media.contentType`, `media.playerName`, `media.channel` |
| `adStart` | `media.ad.id`, `media.ad.length`, `media.ad.podPosition`, `media.ad.playerName` |
| `chapterStart` | `media.chapter.length`, `media.chapter.offset`, `media.chapter.index` |

### 关键命名要求

* 避免在自定义元数据键中使用`media.`前缀 — 它映射到标准媒体字段，并且可能会在Analytics报表中覆盖它们
* `a.`前缀是为Adobe标准元数据保留的，不得使用

## 主内容自定义元数据

与`sessionStart`一起发送。 适用于被跟踪的主媒体，并在整个广告和章节调用中保持可用。 此处定义的任何自定义元数据都将由媒体后端在相应的关闭调用中自动合并。 它将与为广告和章节定义的任何特定自定义元数据一起包含。

```sh
curl -X POST "https://{uri}/api/v1/sessions" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 0,
    "ts": 1646938800000
  },
  "eventType": "sessionStart",
  "params": {
    "analytics.trackingServer": "example.sc.omtrdc.net",
    "analytics.reportSuite": "example-rsid",
    "analytics.visitorId": "visitor123",
    "visitor.marketingCloudOrgId": "0123456789@AdobeOrg",
    "media.id": "sample-video-id",
    "media.name": "Sample Video",
    "media.length": 3600,
    "media.contentType": "vod",
    "media.playerName": "HTML5 Player",
    "media.channel": "Sports"
  },
  "customMetadata": {
    "contentCategory": "Live Sports",
    "leagueType": "Professional",
    "broadcastRights": "Premium"
  }
}'
```

## 广告自定义元数据

与`adStart`一起发送。 特定于每个单独广告。 来自`sessionStart`的自定义元数据也将由广告关闭调用上的媒体后端与此处定义的任何特定于广告的自定义元数据自动合并。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 30,
    "ts": 1646938830000
  },
  "eventType": "adStart",
  "params": {
    "media.ad.id": "summer-sale-2026",
    "media.ad.name": "Summer Sale Ad",
    "media.ad.length": 30,
    "media.ad.playerName": "HTML5 Player",
    "media.ad.podPosition": 1
  },
  "customMetadata": {
    "campaignId": "SUMMER2026",
    "targetAudience": "18-34",
    "adFormat": "skippable"
  }
}'
```

## 章节自定义元数据

与`chapterStart`一起发送。 特定于每个内容章节或区段。 来自`sessionStart`的自定义元数据也将由媒体后端在章节关闭调用中自动合并，以及此处定义的任何特定于章节的自定义元数据。

```sh
curl -X POST "https://{uri}/api/v1/sessions/{sid}/events" \
--header 'Content-Type: application/json' \
--data '{
  "playerTime": {
    "playhead": 600,
    "ts": 1646938200000
  },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Introduction",
    "media.chapter.length": 300,
    "media.chapter.index": 1,
    "media.chapter.offset": 600
  },
  "customMetadata": {
    "chapterType": "tutorial",
    "difficulty": "beginner",
    "instructor": "Jane Smith"
  }
}'
```

## 行为

* 所有自定义元数据值必须是&#x200B;**字符串**。 发送之前转换数字和布尔值。
* 自定义元数据显示在Analytics中，前缀为`c.`（例如，`contentCategory`→`c.contentCategory`）
* 通过Analytics处理规则将自定义元数据映射到eVar、prop或上下文数据变量
* `sessionStart`元数据在整个会话中持续存在；更新需要新会话
* 每个`adStart`和`chapterStart`事件都可以携带不同的自定义元数据

## 相关文档

* [自定义元数据支持 — XDM格式](/help/implementation/edge/custom-metadata.md) — 通过Experience Edge将自定义元数据发送到Analytics和AEP
* [报告包数据的Adobe Analytics源连接器](https://experienceleague.adobe.com/zh-hans/docs/experience-platform/sources/connectors/adobe-applications/analytics) — 将Analytics数据引入Adobe Experience Platform

<!--
* [Session endpoints](sessions.md) — Session lifecycle management
* [Ad endpoints](ads.md) — Track advertising impressions
* [Chapter endpoints](chapters.md) — Segment content into chapters
-->
