---
description: 'null'
seo-description: 'null'
seo-title: 在 JavaScript 中实施标准广告元数据
title: 在 JavaScript 中实施标准广告元数据
uuid: ea10c5a-ae2 b-45d0-aad3-9f10028 ee7 c3
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 JavaScript 中实施标准广告元数据{#implement-standard-ad-metadata-on-javascript}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `StandardAdMetadata` | 用于将标准广告元数据附加到广告对象的常量 |

## 实施标准广告元数据

对于标准广告元数据，使用平台密钥创建标准广告元数据密钥对的字典：

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

