---
title: 如何在Android中设置媒体SKD
description: 请按照以下步骤在Android中设置Media SDK应用程序。
uuid: 3ffe3276-a104-4182-9220-038729e9f3d5
exl-id: 261445bf-3c8b-4658-891d-9a878e0b26ea
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 95%

---

# 设置 Android{#set-up-android}

>[!IMPORTANT]
>
>Adobe 将于 2021 年 8 月 31 日终止支持版本 4 Mobile SDK，届时还将终止对适用于 iOS 和 Android 的 Media Analytics SDK 的支持。有关更多信息，请参阅 [Media Analytics SDK 支持终止常见问题解答](/help/sdk-implement/end-of-support-faqs.md)。


## 先决条件

* **获取 Media SDK 的有效配置参数**
在设置 Analytics 帐户后，您可以从 Adobe 代表处获取这些参数。
* **在应用程序中实施适用于 Android 的 ADBMobile**
有关 Adobe Mobile SDK 文档的更多信息，请参阅[适用于 Experience Cloud 解决方案的 Android SDK 4.x](https://experienceleague.adobe.com/docs/mobile-services/android/overview.html?lang=zh-Hans)。

* **在媒体播放器中提供以下功能：**
   * *用于订阅播放器事件的 API* - Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

## SDK 实施

1. 将[下载](/help/sdk-implement/download-sdks.md#download-2x-sdks)的 Media SDK 添加到您的项目中。

   1. 展开 Android zip 文件（例如，`MediaSDK-android-v2.*.zip`）。
   1. 验证 `MediaSDK.jar` 文件存在于 `libs/` 目录中。

   1. 将库添加到您的项目中。

      **IntelliJ IDEA：**

      1. 在&#x200B;**[!UICONTROL 项目导航]**&#x200B;面板中，右键单击您的项目。
      1. 选择&#x200B;**[!UICONTROL 打开模块设置]**。
      1. 在&#x200B;**[!UICONTROL 项目设置]**&#x200B;下，选择&#x200B;**[!UICONTROL 库]**。

      1. 单击 **[!UICONTROL +]** 以添加新库。
      1. 选择 **[!UICONTROL Java]** 并导航至 `MediaSDK.jar` 文件。

      1. 选择您计划在其中使用移动设备库的模块。
      1. 单击&#x200B;**[!UICONTROL 应用]**，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭“模块设置”窗口。

      **Eclipse：**

      1. 在 Eclipse IDE 中，右键单击项目名称。
      1. 单击&#x200B;**[!UICONTROL 生成路径]** > **[!UICONTROL 添加外部存档]**。
      1. 选择 `MediaSDK.jar`。
      1. 单击&#x200B;**[!UICONTROL 打开]**。
      1. 再次右键单击项目，然后选择&#x200B;**[!UICONTROL 生成路径]** > **[!UICONTROL 配置生成路径]**。
      1. 单击&#x200B;**[!UICONTROL 顺序]**&#x200B;和&#x200B;**[!UICONTROL 导出]**&#x200B;选项卡。

      1. 确保选中 `MediaSDK.jar` 文件。


1. 导入库。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat;
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate;
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig;
   import com.adobe.primetime.va.simple.MediaObject;
   ```

1. 创建 `MediaHeartbeatConfig` 实例。

   以下是 `MediaHeartbeatConfig` 初始化示例：

   ```java
   // Media Heartbeat Initialization
   config.trackingServer = _<SAMPLE_HEARTBEAT_TRACKING_SERVER>_;
   config.channel = <SAMPLE_HEARTBEAT_CHANNEL>;
   config.appVersion = <SAMPLE_HEARTBEAT_SDK_VERSION>;
   config.ovp =  <SAMPLE_HEARTBEAT_OVP_NAME>;
   config.playerName = <SAMPLE_PLAYER_NAME>;
   config.ssl = <true/false>;
   config.debugLogging = <true/false>;
   ```

1. 实施 `MediaHeartbeatDelegate` 接口。

   ```java
   public class VideoAnalyticsProvider implements Observer, MediaHeartbeatDelegate{}
   ```

   ```java
   // Replace <bitrate>, <startupTime>, <fps>, and  
   // <droppeFrames> with the current playback QoS values.  
   @Override
   public MediaObject getQoSObject() {
       return MediaHeartbeat.createQoSObject(<bitrate>,  
                                             <startupTime>,  
                                             <fps>,  
                                             <droppedFrames>);
   }
   
   //Replace <currentPlaybackTime> with the video player current playback time
   @Override
   public Double getCurrentPlaybackTime() {
       return <currentPlaybackTime>;
   }
   ```

1. 创建 `MediaHeartbeat` 实例。

   使用 `MediaHeartbeatConfig` 实例和 `MediaHertbeatDelegate` 实例创建 `MediaHeartbeat` 实例。

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >在会话结束前，请确保您的 `MediaHeartbeat` 实例可以访问且“未被取消分配”**。此实例将用于以下所有的跟踪事件。

**添加应用程序权限**

使用 Media SDK 的应用程序需要以下权限才能在跟踪调用中发送数据：

* `INTERNET`
* `ACCESS_NETWORK_STATE`

要添加这些权限，请将以下行添加到位于应用程序项目目录中的 `AndroidManifest.xml` 文件：

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**在 Android 中从版本 1.x 迁移到 2.x**

在版本 2.x 中，所有公共方法都已合并到 `com.adobe.primetime.va.simple.MediaHeartbeat` 类中，从而更加便于开发人员使用。此外，所有配置现在都已合并到 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 类中。

有关从 1.x 迁移到 2.x 的详细信息，请参阅 [mig-1x-2x-overview.md](/help/sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)。
