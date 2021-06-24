---
title: “从独立Media SDK迁移到AdobeLaunch - Android”
description: 了解如何从Media SDK迁移到Launch for Android。
exl-id: 26764835-4781-417b-a6c0-ea6ae78d76ae
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 93%

---

# 从独立 Media SDK 迁移到 Adobe Launch - Android

## 配置

### 独立 Media SDK

在独立 Media SDK 中，您可以在应用程序中配置跟踪，并在创建跟踪器时将其传递给 SDK。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeat tracker = new MediaHeartbeat(... , config);
```

### Launch 扩展

1. 在 Experience Platform Launch 中，单击适用于您的移动属性的[!UICONTROL 扩展]选项卡。
1. 在[!UICONTROL 目录]选项卡上，找到 Adobe Media Analytics for Audio and Video 扩展，然后单击[!UICONTROL 安装]。
1. 在扩展设置页面中，配置跟踪参数。
Media 扩展将使用已配置的参数进行跟踪。

![](assets/launch_config_mobile.png)

[使用移动扩展](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics)

## 创建跟踪器

### 独立 Media SDK

在独立 Media SDK 中，您可以手动创建 `MediaHeartbeatConfig` 对象并配置跟踪参数。实施公开 `getQoSObject()` 和 `getCurrentPlaybackTime()functions.` 的委派接口。创建用于跟踪的 `MediaHeartbeat` 实例。

```java
MediaHeartbeatConfig config = new MediaHeartbeatConfig();
config.trackingServer = "namespace.hb.omtrdc.net";
config.channel = "sample-channel";
config.appVersion = "v2.0";
config.ovp = "video-provider"; 
config.playerName = "native-player";
config.ssl = true;
config.debugLogging = true;

MediaHeartbeatDelegate delegate = new MediaHeartbeatDelegate() {
    @Override 
    public MediaObject getQoSObject() {
        // When called should return the latest qos values.
        return MediaHeartbeat.createQoSObject(<bitrate>,  
                                              <startupTime>,  
                                              <fps>,  
                                              <droppedFrames>); 
    } 

    @Override 
    public Double getCurrentPlaybackTime() { 
        // When called should return the current player time in seconds.
        return <currentPlaybackTime>; 
    }

    MediaHeartbeat tracker = new MediaHeartbeat(delegate, config);
}
```

### Launch 扩展

[媒体 API 引用 - 创建媒体跟踪器](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#create-a-media-tracker)

在创建跟踪器之前，应先使用移动核心注册媒体扩展和从属扩展。

```java
// Register the extension once during app launch
try {
    // Media needs Identity and Analytics extension 
    // to function properly
    Identity.registerExtension();
    Analytics.registerExtension();

    // Initialize media extension.
    Media.registerExtension();                
    MobileCore.start(new AdobeCallback () {
        @Override
        public void call(Object o) {
            // Launch mobile property to pick extension settings.
            MobileCore.configureWithAppID("LAUNCH_MOBILE_PROPERTY");
        }
    });
} catch (InvalidInitException ex) {
    ...
}
```

注册媒体扩展后，请使用以下 API 创建跟踪器。
该跟踪器会自动从已配置的 Launch 属性中选取配置。

```java
Media.createTracker(new AdobeCallback<MediaTracker>() {
    @Override
    public void call(MediaTracker tracker) {
        // Use the instance for tracking media.
    }
});
```

## 更新“播放头”和“体验质量”值。

### 独立 Media SDK

在独立 Media SDK 中，在创建跟踪器期间传递实施 `MediaHeartbeartDelegate` 接口的委派对象。每当跟踪器调用 `getQoSObject()` 和 `getCurrentPlaybackTime()` 接口方法时，该实施应返回最新的 QoE 和播放头。

### Launch 扩展

该实施应通过调用跟踪器公开的 `updateCurrentPlayhead` 方法来更新当前播放器的播放头。要进行准确跟踪，您应至少每秒调用一次此方法。

[媒体 API 引用 - 更新当前播放器](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updatecurrentplayhead)

该实施应通过调用跟踪器公开的 `updateQoEObject` 方法来更新 QoE 信息。我们希望每当质量量度发生变化都要调用此方法。

[媒体 API 引用 - 更新 QoE 对象](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#updateqoeobject)

## 传递标准媒体/广告元数据

### 独立 Media SDK

* 标准媒体元数据：

   ```java
   MediaObject mediaInfo = 
     MediaHeartbeat.createMediaObject("media-name", 
                                      "media-id", 
                                      60D, 
                                      MediaHeartbeat.StreamType.VOD, 
                                      MediaHeartbeat.MediaType.Video);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardVideoMetadata = 
     new HashMap<String, String>(); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.EPISODE, 
                             "Sample Episode"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SHOW, 
                             "Sample Show"); 
   standardVideoMetadata.put(MediaHeartbeat.VideoMetadataKeys.SEASON, 
                             "Sample Season"); 
   mediaInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardMediaMetadata, 
                      standardVideoMetadata);
   
   // Custom metadata keys
   HashMap<String, String> mediaMetadata = new HashMap<String, String>();
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 标准广告元数据:

   ```java
   MediaObject adInfo = 
     MediaHeartbeat.createAdObject("ad-name", 
                                   "ad-id", 
                                   1L, 
                                   15D);
   
   // Standard metadata keys provided by adobe.
   Map <String, String> standardAdMetadata = 
     new HashMap<String, String>(); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.ADVERTISER, 
                          "Sample Advertiser"); 
   standardAdMetadata.put(MediaHeartbeat.AdMetadataKeys.CAMPAIGN_ID, 
                          "Sample Campaign"); 
   adInfo.setValue(MediaHeartbeat.MediaObjectKey.StandardAdMetadata, 
                   standardAdMetadata); 
   
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   
   tracker.trackEvent(MediaHeartbeat.Event.AdStart, 
                      adObject, 
                      adMetadata);
   ```

### Launch 扩展

* 标准媒体元数据：

   ```java
   HashMap<String, Object> mediaObject = 
     Media.createMediaObject("media-name", 
                             "media-id", 
                             60D, 
                             MediaConstants.StreamType.VOD, 
                             Media.MediaType.Video);
   
   HashMap<String, String> mediaMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.EPISODE, 
                     "Sample Episode");
   mediaMetadata.put(MediaConstants.VideoMetadataKeys.SHOW, 
                     "Sample Show");
   
   // Custom metadata keys
   mediaMetadata.put("isUserLoggedIn", "false");
   mediaMetadata.put("tvStation", "Sample TV Station");
   
   tracker.trackSessionStart(mediaInfo, mediaMetadata);
   ```

* 标准广告元数据:

   ```java
   HashMap<String, Object> adObject = 
     Media.createAdObject("ad-name", 
                          "ad-id", 
                          1L, 
                          15D);
   HashMap<String, String> adMetadata = 
     new HashMap<String, String>();
   
   // Standard metadata keys provided by adobe.
   adMetadata.put(MediaConstants.AdMetadataKeys.ADVERTISER, 
                  "Sample Advertiser");
   adMetadata.put(MediaConstants.AdMetadataKeys.CAMPAIGN_ID, 
                  "Sample Campaign");
   
   // Custom metadata keys
   adMetadata.put("affiliate", 
                  "Sample affiliate");
   _tracker.trackEvent(Media.Event.AdStart, 
                       adObject, 
                       adMetadata);
   ```
