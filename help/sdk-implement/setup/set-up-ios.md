---
seo-title: 设置 iOS
title: 设置 iOS
uuid: a1c6be79-a6dc-47b6-93b3-ac7b42f1f3eb
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 设置 iOS{#set-up-ios}

## 先决条件

* **获取Media SDK的有效配置参数**&#x200B;在设置分析帐户后，可以从Adobe代表处获取这些参数。
* **在您的应用程序中实施** ADBMobile for iOS有关Adobe Mobile SDK文档的更多信息，请参阅 [iOS SDK 4.x for Experience cloud解决方案。](https://marketing.adobe.com/resources/help/en_US/mobile/ios/)

   >[!IMPORTANT]
   >
   >Beginning with iOS 9, Apple introduced a feature called App Transport Security (ATS). 此功能旨在通过确保应用程序仅使用行业标准协议和密码来提高网络安全性。默认情况下此功能处于启用状态，但您也可以通过配置选项来选择是否使用 ATS。For details on ATS, see App Transport Security.[](https://marketing.adobe.com/resources/help/en_US/mobile/ios/app_transport_security.html)

* **在媒体播放器中提供以下功能：**

   * _可订阅播放器事件的 API -_ Media SDK 要求您在播放器中发生事件时调用一组简单的 API。
   * _提供播放器信息的 API_ - 此信息包括媒体名称和播放头位置等详细信息。

## SDK 实施

1. 将[下载](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)的 Media SDK 添加到您的项目中。

   1. 验证以下软件组件存在于 `libs` 目录中：

      * `ADBMediaHeartbeat.h`：用于 iOS 心率跟踪 API 的 Objective-C 头文件。
      * `ADBMediaHeartbeatConfig.h`：用于 SDK 配置的 Objective-C 头文件。
      * `MediaSDK.a`：启用了 bitcode 的胖二进制文件，其中包含用于 iOS 设备（armv7、armv7s、arm64）和模拟器（i386 和 x86_64）的库生成。

         当目标面向 iOS 应用程序时，应该关联此二进制文件。

      * `MediaSDK_TV.a`：启用了 bitcode 的胖二进制文件，其中包含用于新 Apple TV 设备 (arm64) 和模拟器 (x86_64) 的库生成。

         当目标面向 Apple TV (tvOS) 应用程序时，应该关联此二进制文件。
   1. 将库添加到您的项目中：

      1. 启动 Xcode IDE 并打开您的应用程序。
      1. 在&#x200B;**[!UICONTROL 项目导航器]**&#x200B;中，将 `libs` 目录拖放到您的项目下。

      1. 确保选中&#x200B;**[!UICONTROL 需要时复制项目]**&#x200B;复选框，选定&#x200B;**[!UICONTROL 创建群组]，且未选中**&#x200B;添加到目标]中的任何复选框。**[!UICONTROL **

         ![](assets/choose-options_ios.png)

      1. Click **[!UICONTROL Finish]**.
      1. In **[!UICONTROL Project Navigator]**, select your app and select your targets.
      1. 在&#x200B;**[!UICONTROL 常规]**&#x200B;选项卡上的&#x200B;**[!UICONTROL 链接的框架]**&#x200B;和&#x200B;**[!UICONTROL 库]**&#x200B;区域，链接所需的框架和库。

         **iOS 应用程序目标:**

         * **AdobeMobileLibrary.a**
         * **MediaSDK.a**
         * **libsqlite3.0.tbd**
         **Apple TV (tvOS) 目标：**

         * **AdobeMobileLibrary_TV.a**
         * **MediaSDK_TV.a**
         * **libsqlite3.0.tbd**
         * **SystemConfiguration.framework**
      1. 验证您的应用程序在生成时没有出现错误。




1. 导入库。

   ```
   #import "ADBMediaHeartbeat.h" 
   #import "ADBMediaHeartbeatConfig.h" 
   ```

1. Create a `ADBMediaHeartbeatConfig` instance.

   本节将帮助您了解 `MediaHeartbeat` 配置参数并在您的 `MediaHeartbeat` 实例中设置正确的配置值，以便进行准确跟踪。

   以下是 `ADBMediaHeartbeatConfig` 初始化示例:

   ```
   // Media Heartbeat Initialization 
   ADBMediaHeartbeatConfig *config = [[ADBMediaHeartbeatConfig alloc] init]; 
   config.trackingServer = <SAMPLE_HEARTBEAT_TRACKING_SERVER>; 
   config.channel        = <SAMPLE_HEARTBEAT_CHANNEL>; 
   config.appVersion     = <SAMPLE_HEARTBEAT_SDK_VERSION>; 
   config.ovp            = <SAMPLE_HEARTBEAT_OVP_NAME>; 
   config.playerName     = <SAMPLE_PLAYER_NAME>; 
   config.ssl            = <YES/NO>; 
   config.debugLogging   = <YES/NO>; 
   ```

1. Implement the `ADBMediaHeartbeatDelegate` protocol.

   ```
   @interface VideoAnalyticsProvider : NSObject <ADBMediaHeartbeatDelegate> 
   
   @end 
   
   @implementation VideoAnalyticsProvider 
   
   // Replace <bitrate>, <startuptime>, <fps> and <droppeFrames>  
   // with the current playback QoS values. 
   - (ADBMediaObject *)getQoSObject { 
       return [ADBMediaHeartbeat createQoSObjectWithBitrate:<bitrate>  
                                 startupTime:<startuptime>   
                                 fps:<fps>  
                                 droppedFrames:<droppedFrames>]; 
   } 
   
   // Return the current video player playhead position. 
   // Replace <currentPlaybackTime> with the video player current playback time 
   - (NSTimeInterval)getCurrentPlaybackTime { 
       return <currentPlaybackTime>; 
   } 
   
   @end
   ```

1. Use the `ADBMediaHeartBeatConfig` and `ADBMediaHeartBeatDelegate` to create the `ADBMediaHeartbeat` instance.

   ```
   //Replace <ADBMediaHeartBeatDelegate> with your delegate instance 
   _mediaHeartbeat = [[ADBMediaHeartbeat alloc] initWithDelegate: 
     <ADBMediaHeartBeatDelegate> config:config];
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `ADBMediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. 此实例将用于以下所有的跟踪事件。

## 在 iOS 中从版本 1.x 迁移到 2.x {#migrate-to-two-x}

在版本 2.x 中，所有公共方法都已合并到 `ADBMediaHeartbeat` 类中，从而更加便于开发人员使用。所有配置都已合并到 `ADBMediaHeartbeatConfig` 类中。

For more information about migrating from 1.x to 2.x, see [VHL 1.x to 2.x Migration.](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)

## 配置适用于 tvOS 的本地应用程序

现在，随着新 Apple TV 的发布，您能够创建可在本地 tvOS 环境中运行的应用程序。您可以使用 iOS 中提供的任何几种框架创建纯本地应用程序，也可以使用 XML 模板和 JavaScript 创建应用程序。从 MediaSDK 版本 2.0 起，开始支持 tvOS。For more information about tvOS, see [tvOS Developer site.](https://developer.apple.com/tvos/documentation/)

在您的 Xcode 项目中执行以下步骤：本指南假定您的项目旨在开发适用于 tvOS 的 Apple TV 应用程序：

1. Drag the `VideoHeartbeat_TV.a` library file into your project’s `lib` folder.

1. 在 tvOS 应用程序目标的&#x200B;**[!UICONTROL 构建阶段]**&#x200B;选项卡中，展开&#x200B;**[!UICONTROL 链接二进制文件和库]**&#x200B;部分，并添加以下库:

   * `MediaSDK_TV.a`
   * `AdobeMobileLibrary_TV.a`
   * `libsqlite3.0.tbd`
   * `SystemConfiguration.framework`

