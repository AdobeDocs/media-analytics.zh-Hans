---
title: 了解如何在iOS中实施标准广告元数据
description: 如何在 iOS 上的广告跟踪中使用标准广告元数据。
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 86%

---

# 在 iOS 中实施标准广告元数据{#implement-standard-ad-metadata-on-ios}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | 用于将标准广告元数据附加到 `AdInfo ADBMediaObject` 的常量 |

## 实施标准广告元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 元数据键](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
