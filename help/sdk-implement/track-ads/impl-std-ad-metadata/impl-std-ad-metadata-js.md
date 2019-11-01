---
title: 在 JavaScript 中实施标准广告元数据
description: 如何在浏览器(JS)应用程序中的广告跟踪中使用标准广告元数据。
uuid: 4ea10c5a-ae2b-45d0-aad3-9f10028ee7c3
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 JavaScript 中实施标准广告元数据{#implement-standard-ad-metadata-on-javascript}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `StandardAdMetadata` | 用于将标准广告元数据附加到广告对象的常量 |

## 实施标准和元数据

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

