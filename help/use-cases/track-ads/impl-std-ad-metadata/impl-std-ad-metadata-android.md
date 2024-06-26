---
title: 了解如何在 Android 中实施标准广告元数据
description: 如何在 Android 上的广告跟踪中使用标准广告元数据。
uuid: 19b98bc1-c659-4182-a4ff-b3340fe2453c
exl-id: f1aa017f-b2ae-40ca-b4d9-b508cf45cb0c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 100%

---

# 在 Android 中实施标准广告元数据{#implement-standard-ad-metadata-on-android}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `MediaHeartbeat.MediaObjectKey.StandardAdMetadata` | 用于将标准广告元数据附加到广告 `MediaObject` 的常量。 |

## 实施标准广告元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```java
// Setting standard Ad Metadata 
Map <String, String> standardAdMetadata = new HashMap<String, String>(); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, "Sample Advertiser"); 
standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, "Sample Campaign"); 
adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, standardAdMetadata); 
```
