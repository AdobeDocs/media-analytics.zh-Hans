---
title: 使用JavaScript 2.x实现标准广告元数据
description: 如何在浏览器中使用JavaScript 2.x应用程序在广告跟踪中使用标准广告元数据。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 30ed54924c75a9c33e6122b2d7ddbb84c06b8c0c
workflow-type: tm+mt
source-wordcount: '68'
ht-degree: 55%

---


# 使用JavaScript 2.x实现标准广告元数据{#implement-standard-ad-metadata-on-javascript}

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
