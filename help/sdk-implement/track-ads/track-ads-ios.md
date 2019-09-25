---
seo-title: 在 iOS 中跟踪广告
title: 在 iOS 中跟踪广告
uuid: e979e679-cde5-4c30-8f34-867feceac13a
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 在 iOS 中跟踪广告{#track-ads-on-ios}

>[!IMPORTANT]
>
>以下说明为使用2.x SDK实施提供了指导。 如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK.](/help/sdk-implement/download-sdks.md)

## 广告跟踪常量

| 常量名称 | 描述   |
|---|---|
| `ADBMediaHeartbeatEventAdBreakStart` | 用于跟踪 AdBreak 开始事件的常量 |
| `ADBMediaHeartbeatEventAdBreakComplete` | 用于跟踪 AdBreak 结束事件的常量 |
| `ADBMediaHeartbeatEventAdStart` | 用于跟踪广告开始事件的常量 |
| `ADBMediaHeartbeatEventAdComplete` | 用于跟踪广告结束事件的常量 |
| `ADBMediaHeartbeatEventAdSkip` | 用于跟踪广告跳过事件的常量 |

## 实施步骤

1. 识别广告时间（包括前置广告）边界开始的时间，然后使用广告时间信息创建 `AdBreakObject`。

   `AdBreakObject` 参考：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告时间的名称，例如前置广告、中置广告或后置广告。 | 是 |
   | `position` | 内容中广告时间的位置编号，从 1 开始编号。 | 是 |
   | `startTime` | 广告时间开始的播放头值。 | 是 |

   广告时间对象创建：

   ```
   id adBreakObject = [ADBMediaHeartbeat createAdBreakObjectWithName:[ADBREAK_NAME] 
                               position:[POSITION]  
                               startTime:[START_TIME]];
   ```

1. Call `trackEvent()` with `AdBreakStart` in the `MediaHeartbeat` instance to begin tracking the ad break:

   ```
   - (void)onAdBreakStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakStart  
                        mediaObject:adBreakObject  
                        data:nil]; 
   }
   ```

1. 识别广告的开始时间，然后使用广告信息创建 `AdObject` 实例。

   `AdObject` 参考：

   | 变量名称 | 描述 | 必需 |
   | --- | --- | :---: |
   | `name` | 广告的友好名称。 | 是 |
   | `adId` | 广告的唯一标识符。 | 是 |
   | `position` | 广告时间中广告的位置编号，从 1 开始编号。 | 是 |
   | `length` | 广告长度 | 是 |

   广告对象创建：

   ```
   id adObject = [ADBMediaHeartbeat createAdObjectWithName:[AD_NAME] 
                                    adId:[AD_ID] 
                                    position:[POSITION] 
                                    length:[LENGTH]];
   ```

1. （可选）通过上下文数据变量将标准和／或广告元数据附加到媒体跟踪会话。

   * [在 iOS 中实施标准广告元数据](/help/sdk-implement/track-ads/impl-std-ad-metadata/impl-std-ad-metadata-ios.md)
   * **自定义广告元数据 -** 对于自定义元数据，请为自定义数据变量创建变量对象，然后使用当前广告的数据进行填充：

      ```
      NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init]; 
      [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"]; 
      [adDictionary setObject:@"Sample campaign" forKey:@"campaign"]; 
      [adDictionary setObject:@"Sample creative" forKey:@"creative"];
      ```

1. Call `trackEvent()` with the `AdStart` event in the `MediaHeartbeat` instance to begin tracking the ad playback.

   在事件调用中添加对自定义元数据变量（或空对象）的引用，以将其作为第三个参数：

   ```
   - (void)onAdStart:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdStart  
                        mediaObject:adObject  
                        data:adDictionary]; 
   }
   ```

1. When the ad playback reaches the end of the ad, call `trackEvent()` with the `AdComplete` event.

   ```
   - (void)onAdComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 如果由于用户选择跳过广告而使广告播放未能完成，则跟踪 `AdSkip` 事件。

   ```
   - (void)onAdSkip:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdSkip  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

1. 如果同一个 `AdBreak` 中存在任何其他广告，请重复执行步骤 3 至 7。
1. 当广告时间结束时，使用 `AdBreakComplete` 事件进行跟踪：

   ```
   - (void)onAdBreakComplete:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventAdBreakComplete  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

有关更多信息，请参阅跟踪方案[包含前置广告的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-preroll-ads.md)。
