---
title: 使用JavaScript 3.x实现标准广告元数据
description: 如何在浏览器中使用JavaScript 3.x应用程序在广告跟踪中使用标准广告元数据。
translation-type: tm+mt
source-git-commit: 83b38ac8f7fc88f982d194e776efccf8d5b983e4
workflow-type: tm+mt
source-wordcount: '54'
ht-degree: 44%

---


# 使用JavaScript 3.x实现标准广告元数据{#implement-standard-ad-metadata-on-javascript}

## 实施标准广告元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```js
var adObject =
ADB.Media.createAdObject(<AD_NAME>,
                              <AD_ID>,
                              <POSITION>,
                              <LENGTH>);

// Set standard Ad Metadata
var adMetadata = {};
adMetadata[MediaHeartbeat.AdMetadataKeys.Advertiser] = "Sample Advertiser";
adMetadata[MediaHeartbeat.AdMetadataKeys.CampaignId] = "Sample Campaign";

tracker.trackEvent(ADB.Media.Event.AdStart, adObject, adMetadata);
```
