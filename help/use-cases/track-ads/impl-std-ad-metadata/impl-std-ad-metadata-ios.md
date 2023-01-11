---
title: 了解如何在 iOS 中实施标准广告元数据
description: 如何在 iOS 上的广告跟踪中使用标准广告元数据。
uuid: f15fb727-5a5b-46c5-bf12-93b376c10fd1
exl-id: 018ae833-51d9-4ff0-80e7-3dbcaefb997c
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '65'
ht-degree: 100%

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

[iOS 元数据键](/help/use-cases/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
