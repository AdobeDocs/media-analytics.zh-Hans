---
title: 了解如何使用 JavaScript 2.x 实施标准广告元数据
description: 如何使用 JavaScript 2.x 应用程序在浏览器中的广告跟踪中使用标准广告元数据。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
exl-id: b331db87-ab4e-44fa-a97c-9691974cacd4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 100%

---

# 使用 JavaScript 2.x 实施标准广告元数据{#implement-standard-ad-metadata-on-javascript}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `StandardAdMetadata` | 用于将标准广告元数据附加到广告对象的常量 |

## 实施标准广告元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```js
var adObject =  
MediaHeartbeat.createAdObject(<AD_NAME>,  
                              <AD_ID>,  
                              <POSITION>,  
                              <LENGTH>);

// Set standard Ad Metadata
var standardAdMetadata = {};
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.ADVERTISER] = "Sample Advertiser";
standardAdMetadata[MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID] = "Sample Campaign";
adObject.setValue(MediaObjectKey.StandardAdMetadata, standardAdMetadata);
```
