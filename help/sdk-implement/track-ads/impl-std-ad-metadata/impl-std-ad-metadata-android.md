---
description: 'null'
seo-description: 'null'
seo-title: 在 Android 中实施标准广告元数据
title: 在 Android 中实施标准广告元数据
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# 在 Android 中实施标准广告元数据{#implement-standard-ad-metadata-on-android}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 用于将标准广告元数据附加到广告 `MediaObject` 的常量。 |

## 实施标准和元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```

