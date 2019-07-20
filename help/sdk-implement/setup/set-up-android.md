---
seo-title: 设置 Android
title: 设置 Android
uuid: ffe3276-a104-4182-9220-038729e9 f3 d5
translation-type: tm+mt
source-git-commit: 63fb6332694675cd03843995f8f86ae45973d399

---


# 设置 Android{#set-up-android}

## 先决条件

* **为媒体SDK获取有效配置参数**&#x200B;在设置分析帐户后，可以从Adobe代表获得这些参数。
* **在应用程序**中为Android实施AdbMobile有关Adobe
Mobile SDK文档的更多信息，请参阅 [适用于Experience Cloud解决方案的Android SDK4.x。](https://marketing.adobe.com/resources/help/en_US/mobile/android/)
* **在媒体播放器中提供以下功能：**
   * *可订阅播放器事件的 API -* Media SDK 要求您在播放器中发生事件时调用一组简单的 API。
   * *提供播放器信息的 API* - 此信息包括媒体名称和播放头位置等详细信息。

## SDK 实施

1. 将[下载](../../sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)的 Media SDK 添加到您的项目中。

   1. Expand the Android zip file (e.g., `MediaSDK-android-v2.*.zip`).
   1. Verify that the `MediaSDK.jar` file exists in the `libs/` directory.

   1. 将库添加到您的项目中。

      **IntelliJ IDEA：**

      1. 在&#x200B;**[!UICONTROL 项目导航]**&#x200B;面板中，右键单击您的项目。
      1. Select **[!UICONTROL Open Module Settings]**.
      1. Under **[!UICONTROL Project Settings]**, select **[!UICONTROL Libraries]**.

      1. Click **[!UICONTROL +]** to add a new library.
      1. 选择 **[!UICONTROL Java]** 并导航至 `MediaSDK.jar` 文件。

      1. 选择您计划在其中使用移动设备库的模块。
      1. 单击&#x200B;**[!UICONTROL 应用]**，然后单击&#x200B;**[!UICONTROL 确定]**&#x200B;以关闭“模块设置”窗口。
      **Eclipse：**

      1. 在 Eclipse IDE 中，右键单击项目名称。
      1. Click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Add External Archives]** .
      1. 选择 `MediaSDK.jar`.
      1. Click **[!UICONTROL Open]**.
      1. Right-click the project again, and click  **[!UICONTROL Build Path]** &gt; **[!UICONTROL Configure Build Path]** .
      1. 单击&#x200B;**[!UICONTROL 顺序]**&#x200B;和&#x200B;**[!UICONTROL 导出]**&#x200B;选项卡。

      1. 确保选中 `MediaSDK.jar` 文件。


1. 导入库。

   ```java
   import com.adobe.primetime.va.simple.MediaHeartbeat; 
   import com.adobe.primetime.va.simple.MediaHeartbeat.MediaHeartbeatDelegate; 
   import com.adobe.primetime.va.simple.MediaHeartbeatConfig; 
   import com.adobe.primetime.va.simple.MediaObject; 
   ```

1. Create the `MediaHeartbeatConfig` instance.

   以下是 `MediaHeartbeatConfig` 初始化示例:

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

1. Implement the `MediaHeartbeatDelegate` interface.

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

1. Create the `MediaHeartbeat` instance.

   Use the `MediaHeartbeatConfig` instance and the `MediaHertbeatDelegate` instance to create the `MediaHeartbeat` instance.

   ```java
   // Replace <MediaHertbeatDelegate> with your delegate instance 
   MediaHeartbeat _heartbeat =  
     new MediaHeartbeat(<MediaHeartbeatDelegate>, config);
   ```

   >[!IMPORTANT]
   >
   >Make sure that your `MediaHeartbeat` instance is accessible and *does not get deallocated until the end of the session*. 此实例将用于以下所有的跟踪事件。

**添加应用程序权限**

使用 Media SDK 的应用程序需要以下权限才能在跟踪调用中发送数据：

* `INTERNET`
* `ACCESS_NETWORK_STATE`

要添加这些权限，请将以下行添加到位于应用程序项目目录中的 `AndroidManifest.xml` 文件：

* `<uses-permission android:name="android.permission.INTERNET" />`
* `<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />`

**在 Android 中从版本 1.x 迁移到 2.x**

在版本 2.x 中，所有公共方法都已合并到 `com.adobe.primetime.va.simple.MediaHeartbeat` 类中，从而更加便于开发人员使用。此外，所有配置现在都已合并到 `com.adobe.primetime.va.simple.MediaHeartbeatConfig` 类中。

For detailed information about migrating from 1.x to 2.x, see [mig-1x-2x-overview.md.](../../sdk-implement/va-1x-to-2x/mig-1x-2x-overview.md)
