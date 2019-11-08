---
title: 从独立的Media SDK迁移到Adobe Launch - iOS
description: 帮助从Media SDK迁移到Launch for iOS的说明和代码示例。
translation-type: tm+mt
source-git-commit: bc896cc403923e2f31be7313ab2ca22c05893c45

---


# 从独立的Media SDK迁移到Adobe Launch - iOS

## 配置

### 独立Media SDK

在独立的Media SDK中，您在应用程序中配置跟踪配置，并在创建跟踪器时将其传递给SDK。

```objective-c
ADBMediaHeartbeatConfig *config = 
  [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"v2.0.0";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:self config:config]; 
```

### 启动扩展

1. 在Experience Platform Launch中，单击移动 [!UICONTROL 属性的] “扩展”选项卡
1. 在“目 [!UICONTROL 录] ”选项卡上，找到“Adobe Media Analytics for Audio and Video”扩展，然后单击“安 [!UICONTROL 装”]。
1. 在扩展设置页面中，配置跟踪参数。
媒体扩展将使用已配置的参数进行跟踪。

   ![](assets/launch_config_mobile.png)

[配置媒体分析扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## 创建跟踪器

### 独立Media SDK

在独立的Media SDK中，您可以手动创建对 `ADBMediaHeartbeatConfig` 象并配置跟踪参数。 实现表示和的委托界面`getQoSObject()` , `getCurrentPlaybackTime()functions.`

创建用于跟踪的MediaHeartbeat实例：

```objective-c
@interface PlayerDelegate : NSObject<ADBMediaHeartbeatDelegate>
@end

@implementation PlayerDelegate {
}

- (NSTimeInterval) getCurrentPlaybackTime {
    // When called should return the current player time in seconds.
    return playhead_;
}

- (nonnull ADBMediaObject*) getQoSObject {
    // When called should return the latest qos values.
    return qosObject_;
}
@end

ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init];

config.trackingServer = @"namespace.hb.omtrdc.net";
config.channel = @"sample-channel";
config.appVersion = @"app-version";
config.ovp = @"video-provider";
config.playerName = @"native-player";
config.ssl = YES;
config.debugLogging = YES;
ADBMediaHeartbeatDelegate* delegate = [[PlayerDelegate alloc] init];

ADBMediaHeartbeat* tracker = 
  [[ADBMediaHeartbeat alloc] initWithDelegate:delegate config:config];
```

### 启动扩展

[媒体API参考——创建媒体跟踪器](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

在创建跟踪器之前，请使用移动核心注册媒体扩展和相关扩展。

```objective-c
// Register the extension once during app launch
#import <ACPCore.h>
#import <ACPAnalytics.h>
#import <ACPMedia.h>
#import <ACPIdentity.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [ACPCore setLogLevel:ACPMobileLogLevelDebug];
    [ACPCore configureWithAppId:@"your-launch-app-id"];
    [ACPMedia registerExtension];
    [ACPAnalytics registerExtension];
    [ACPIdentity registerExtension];
    [ACPCore start:nil];
    return YES;
}
```

注册媒体扩展后，可以使用以下API创建跟踪器。
该跟踪器会从已配置的启动属性中自动选取配置。

```objective-c
[ACPMedia createTracker:^(ACPMediaTracker * _Nullable mediaTracker) {
    // Use the instance for tracking media.
}];
```

## 更新播放头和体验质量值。

### 独立Media SDK

在独立的Media SDK中，在创建跟踪器期间会传递一个实现协议的委托对象`ADBMediaHeartbeartDelegate` 。
每当跟踪器调用和接口方法时，实现应返回最新的QoE `getQoSObject()` 和播 `getCurrentPlaybackTime()` 放头。

### 启动扩展

实现应通过调用跟踪器公开的方法来更新当前播放器播放头`updateCurrentPlayhead` 。 要进行准确跟踪，您应至少每秒调用一次此方法。

[媒体API参考——更新当前播放头](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

实现应通过调用跟踪器公开的方法`updateQoEObject` ，来更新QoE信息。 只要质量指标发生变化，您就应调用此方法。

[媒体API参考——更新QoE对象](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## 传递标准媒体／广告元数据

### 独立Media SDK

* 标准媒体元数据：

   ```objective-c
   ADBMediaObject *mediaObject = 
     [ADBMediaHeartbeat createMediaObjectWithName:@"media-name" 
                        mediaId:@"media-id" 
                        length:60 
                        streamType:ADBMediaHeartbeatStreamTypeVod 
                        mediaType:ADBMediaTypeVideo];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample show" forKey:ADBVideoMetadataKeySHOW];
   [standardMetadata setObject:@"Sample season" forKey:ADBVideoMetadataKeySEASON];
   [mediaObject setValue:standardMetadata forKey:ADBMediaObjectKeyStandardMediaMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *videoMetadata = [[NSMutableDictionary alloc] init];
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   
   [tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* 标准广告元数据:

   ```objective-c
   ADBMediaObject* adObject = 
     [ADBMediaHeartbeat createAdObjectWithName:[adData objectForKey:@"name"] 
                        adId:[adData objectForKey:@"id"]
                        position:[[adData objectForKey:@"position"] doubleValue]
                        length:[[adData objectForKey:@"length"] doubleValue]];
   
   // Standard metadata keys provided by adobe.
   NSMutableDictionary *standardMetadata = 
     [[NSMutableDictionary alloc] init];
   [standardMetadata setObject:@"Sample Advertiser" 
                     forKey:ADBAdMetadataKeyADVERTISER];
   [standardMetadata setObject:@"Sample Campaign" 
                     forKey:ADBAdMetadataKeyCAMPAIGN_ID];
   [adObject setValue:standardMetadata 
                     forKey:ADBMediaObjectKeyStandardAdMetadata];
   
   //Attaching custom metadata
   NSMutableDictionary *adDictionary = [[NSMutableDictionary alloc] init];
   [adDictionary setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ADBMediaHeartbeatEventAdStart 
            mediaObject:adObject 
            data:adDictionary];
   ```

### 启动扩展

* 标准媒体元数据：

   ```objective-c
   NSDictionary *mediaObject = 
     [ACPMedia createMediaObjectWithName:@"media-name" 
               mediaId:@"media-id" 
               length:60 
               streamType:ACPMediaStreamTypeVod 
               mediaType:ACPMediaTypeVideo];
   
   NSMutableDictionary *mediaMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [mediaMetadata setObject:@"Sample show" forKey:ACPVideoMetadataKeyShow];
   [mediaMetadata setObject:@"Sample season" forKey:ACPVideoMetadataKeySeason];
   
   // Custom metadata keys
   [mediaMetadata setObject:@"false" forKey:@"isUserLoggedIn"];
   [mediaMetadata setObject:@"Sample TV station" forKey:@"tvStation"];
   [_tracker trackSessionStart:mediaObject data:mediaMetadata];
   ```

* 标准广告元数据:

   ```objective-c
   NSDictionary* adObject = 
     [ACPMedia createAdObjectWithName:@"ad-name" 
               adId:@"ad-id" 
               position:1 
               length:15];
   
   NSMutableDictionary* adMetadata = 
     [[NSMutableDictionary alloc] init];
   
   // Standard metadata keys provided by adobe.
   [adMetadata setObject:@"Sample Advertiser" forKey:ACPAdMetadataKeyAdvertiser];
   [adMetadata setObject:@"Sample Campaign" forKey:ACPAdMetadataKeyCampaignId];
   
   // Custom metadata keys
   [adMetadata setObject:@"Sample affiliate" forKey:@"affiliate"];
   
   [tracker trackEvent:ACPMediaEventAdStart mediaObject:adObject data:adMetadata];
   ```
