---
description: 'null'
seo-description: 'null'
seo-title: 在 iOS 中实施标准广告元数据
title: 在 iOS 中实施标准广告元数据
uuid: f15fb727-5a5b-46c5-bf12-93b376 c10 fd1
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 中实施标准广告元数据{#implement-standard-ad-metadata-on-ios}

## 广告常量

| 常量名称 | 描述   |
|---|---|
| `ADBMediaObjectKeyStandardAdMetadata` | Constant for attaching standard ad metadata on `AdInfo ADBMediaObject` |

## 实施标准广告元数据

对于标准广告元数据，使用平台密钥创建标准广告元数据密钥对的字典：

```
// Sample implementation for using standard metadata keys for Ad 
NSMutableDictionary *standardAdMetadata = [[NSMutableDictionary alloc] init]; 
[standardAdMetadata setObject:@"Sample Advertiser" forKey:ADBAdMetadataKeyADVERTISER]; 
[standardAdMetadata setObject:@"Sample Campaign" forKey:ADBAdMetadataKeyCAMPAIGN_ID]; 
 
[adObject setValue:standardAdMetadata forKey:ADBMediaObjectKeyStandardAdMetadata];
```

[iOS 元数据键](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)
