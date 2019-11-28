---
title: 在 iOS 中实施标准元数据
description: 介绍如何在 iOS 中设置要与跟踪调用一起发送的标准视频和广告元数据。
uuid: 75a80f08-4a95-49d4-a27a-8ce531d64d31
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 iOS 中实施标准元数据{#implement-standard-metadata-on-ios}

## 元数据常量

| 常量名称 | 描述   |
|---|---|
| `ADBMediaObjectKeyStandardMediaMetadata` | 用于将标准元数据附加到 `MediaInfo ADBMediaObject` 的常量 |

## 实施

1. 使用 `ADBStandardMetadataKeys` 创建标准元数据键值对的字典
   [iOS 元数据键](/help/sdk-implement/track-av-playback/impl-std-metadata/ios-metadata-keys.md)

1. 在 `MediaInfo` `ADBMediaObject` 实例中使用元数据的标准元数据常量设置标准元数据字典。

1. 调用 `trackSessionStart` API 时提供此 `MediaInfo` 对象。

### 实施示例

实例化一个标准元数据对象，填充所需变量，并在媒体心率对象中设置该元数据对象。例如：

```
// Sample implementation for using standard video metadata keys 
 
NSMutableDictionary *standardVideoMetadata = [[NSMutableDictionary alloc] init]; 
 
[standardVideoMetadata setObject:@"Sample Show" forKey:ADBVideoMetadataKeySHOW]; 
 
[standardVideoMetadata setObject:@"Sample Season" forKey:ADBVideoMetadataKeySEASON]; 
 
[standardVideoMetadata setObject:@"Sample Episode" forKey:ADBVideoMetadataKeyEPISODE]; 
 
[mediaObject setValue:standardVideoMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

```
// Sample implementation for using standard audio metadata keys 
 
NSMutableDictionary *standardAudioMetadata = [[NSMutableDictionary alloc] init];  
 
[standardAudioMetadata setObject:@"Sample Album"   forKey:ADBAudioMetadataKeyALBUM];  
 
[standardAudioMetadata setObject:@"Sample Label"   forKey:ADBAudioMetadataKeyLABEL]; 
 
[mediaObject setValue:standardAudioMetadata   forKey:ADBMediaObjectKeyStandardMediaMetadata];
```

