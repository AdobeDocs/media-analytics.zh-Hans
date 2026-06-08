---
title: 设置适用于流媒体的Roku 2.x
description: 安装和配置适用于Roku的适用于Adobe Media SDK 2.x ，用于仅Analytics流媒体实施，包括SceneGraph渠道。
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# 设置适用于流媒体的Roku 2.x

Adobe Media SDK 2.x for Roku (`adbmobile.brs`)将使用BrightScript编写的Roku渠道中的流媒体数据直接发送到Adobe Analytics。 它还通过Audience Manager收集受众数据，并通过媒体事件测量参与度。

>[!NOTE]
>
>本页介绍了适用于Roku的仅适用于Analytics的Media SDK 2.x。 对于新的实施，Adobe建议使用[Roku Edge SDK](/help/implementation/edge/roku.md)，这样除Adobe Analytics之外，数据还可以供Customer Journey Analytics、Adobe Journey Optimizer和Real-Time CDP使用。

* **先决条件**：
   * 完成[仅限Analytics的实施概述](overview.md)。
   * [下载Roku的Media SDK](/help/getting-started/download-sdks.md)。
   * 在媒体播放器中包括API以订阅播放器事件，以及包括API以提供播放器信息，例如媒体名称和播放头位置。

## 安装SDK

`AdobeMobileLibrary-2.*-Roku.zip`下载包含两个组件：

* `adbmobile.brs`：库文件。 将其复制到渠道的`pkg:/source/`目录中。
* `ADBMobileConfig.json`：为您的应用程序自定义的SDK配置文件。

对于SceneGraph渠道，还将`adbmobileTask.brs`和`adbmobileTask.xml`复制到您的`pkg:/components/`目录中。 请参阅[SceneGraph支持](#scenegraph)。

## 配置ADBMobileConfig.json

配置JSON具有用于流媒体的专用`mediaHeartbeat`密钥。 将`ADBMobileConfig.json`添加到您的项目源并设置`mediaHeartbeat`、`marketingCloud`和`analytics`值：

```json
{
  "analytics": {
    "rsids": "your-report-suite-id",
    "server": "your-analytics-server"
  },
  "marketingCloud": {
    "org": "YOUR-MCORG-ID@AdobeOrg"
  },
  "mediaHeartbeat": {
    "server": "your-namespace.hb-api.omtrdc.net",
    "publisher": "your-publisher-id",
    "channel": "sample-channel",
    "ssl": true,
    "ovp": "sample-ovp",
    "sdkVersion": "sample-sdk",
    "playerName": "Roku Player"
  }
}
```

| 配置参数 | 描述 |
| --- | --- |
| `server` | 媒体跟踪端点的URL。 请参阅[仅限Analytics的实施概述](overview.md)。 |
| `publisher` | 内容发布者唯一标识符。 |
| `channel` | 内容分发渠道的名称。 报告为[内容渠道](/help/implementation/variables/core/content-channel.md)。 |
| `ssl` | SSL是否用于跟踪调用。 |
| `ovp` | 联机视频平台提供商的名称。 |
| `sdkVersion` | 应用程序或SDK的当前版本。 |
| `playerName` | 播放器的名称。 报告为[内容播放器名称](/help/implementation/variables/core/content-player-name.md)。 |

>[!IMPORTANT]
>
>如果未正确配置`mediaHeartbeat`，则媒体模块会进入错误状态并停止发送跟踪调用。 确保您的`marketingCloud.org`值包含`@AdobeOrg`。

## 初始化SDK并处理消息

使用`ADBMobile()`获取SDK的实例。 Experience Cloud访客ID服务会生成一个包含在所有点击中的访客ID。

>[!IMPORTANT]
>
>每隔250毫秒在主事件循环中调用`processMessages`和`processMediaMessages`，以便SDK正确发送ping。

```brightscript
adb = ADBMobile()

' In your main event loop, every ~250 ms:
adb.processMessages()
adb.processMediaMessages()
```

| 方法 | 描述 |
| --- | --- |
| `processMessages` | 将排队的Analytics事件传递到SDK。 |
| `processMediaMessages` | 将排队的媒体事件传递到SDK，包括自动Ping。 |

## 跟踪媒体事件

通过调用其SDK方法跟踪每个媒体事件。 有关确切的调用、生成器和常量，请参阅每个[事件](/help/implementation/events/overview.md)和[变量](/help/implementation/variables/overview.md)页面上的&#x200B;**Roku 2.x**&#x200B;选项卡。

典型的会话从构建媒体对象并调用`mediaTrackSessionStart`开始：

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("Mr. Robot", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

contextData = { "a.media.show": "Mr. Robot" }

adb.mediaTrackSessionStart(mediaInfo, contextData)
```

全局`adb_media_init_*`生成器创建跟踪调用使用的媒体、广告、广告时间、章节和QoS对象：

| 生成器 | 签名 |
| --- | --- |
| 媒体 | `adb_media_init_mediainfo(name, id, length, streamType, mediaType)` |
| 广告 | `adb_media_init_adinfo(name, id, position, length)` |
| 广告中断 | `adb_media_init_adbreakinfo(name, startTime, position)` |
| 章节 | `adb_media_init_chapterinfo(name, position, length, startTime)` |
| QoS | `adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)` |

标准元数据作为`a.media.*`键的关联数组传递（SDK还为这些键定义了命名常量，例如`MEDIA_VideoMetadataKeySHOW`）。 查看与每个维度对应的键的[变量](/help/implementation/variables/overview.md)页。

## 配置Experience Cloud访客ID、隐私和日志记录

`ADBMobile()`实例上的以下方法可管理身份、隐私和调试：

| 方法 | 描述 |
| --- | --- |
| `visitorMarketingCloudID()` | 检索Experience Cloud ID (ECID)。 |
| `visitorSyncIdentifiers(identifiers)` | 为同一访客设置其他客户ID。 |
| `setAdvertisingIdentifier(rida)` | 为Advertising (RIDA)设置Roku ID。 使用Roku [`getRIDA()`](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API获取它。 |
| `getAllIdentifiers()` | 返回由SDK存储的所有标识符，包括Analytics、Visitor、Audience Manager和自定义标识符。 |
| `setPrivacyStatus(status)` | 设置隐私状态。 传递`adb.PRIVACY_STATUS_OPT_IN`或`adb.PRIVACY_STATUS_OPT_OUT`。 请参阅[隐私](/help/implementation/opt-out-privacy.md)。 |
| `getPrivacyStatus()` | 返回当前的隐私状态。 |
| `setDebugLogging(flag)` | 启用或禁用调试日志记录。 |
| `getDebugLogging()` | 如果启用调试日志记录，则返回`true`。 |

## SceneGraph支持 {#scenegraph}

Roku SceneGraph XML框架无法直接调用旧版BrightScript SDK API，因为SDK使用的组件（如线程）不适用于SceneGraph应用程序。 为了弥补这一缺口，SDK提供了一个连接器，该连接器会返回一个公开相同API的SceneGraph兼容实例，以及一个用于返回数据的API的回调机制。

这座桥由三部分组成：

* **`adbmobileTask`节点**：在后台线程上执行SDK API并将数据返回到场景的SceneGraph任务节点。
* **连接器实例**：封装所有旧版公共API并与`adbmobileTask`节点通信。
* **`API_RESPONSE`回调**：应用程序观察到的从getter API接收返回值的字段。

要在SceneGraph渠道中初始化SDK，请执行以下操作：

1. 将`adbmobile.brs`导入您的场景：

   ```brightscript
   <script type="text/brightscript" uri="pkg:/source/adbmobile.brs" />
   ```

1. 创建`adbmobileTask`节点、获取连接器实例并加载SceneGraph常量：

   ```brightscript
   m.adbmobileTask = createObject("roSGNode", "adbmobileTask")
   m.adbmobile = ADBMobile().getADBMobileConnectorInstance(m.adbmobileTask)
   m.adbmobileConstants = m.adbmobile.sceneGraphConstants()
   ```

1. 注册回调以接收返回数据的API的响应对象：

   ```brightscript
   m.adbmobileTask.ObserveField(m.adbmobileConstants.API_RESPONSE, "onAdbmobileApiResponse")
   
   function onAdbmobileApiResponse() as void
       responseObject = m.adbmobileTask[m.adbmobileConstants.API_RESPONSE]
       if responseObject <> invalid
           methodName = responseObject.apiName
           retVal = responseObject.returnValue
           if methodName = m.adbmobileConstants.PRIVACY_STATUS
               print "Privacy status: " + retVal
           end if
       end if
   end function
   ```

连接器实例(`m.adbmobile`)公开与旧版SDK （`mediaTrackSessionStart`、`mediaTrackPlay`、`mediaTrackPause`、`mediaTrackComplete`、`mediaTrackSessionEnd`、`mediaTrackError`、`mediaTrackEvent`、`mediaUpdatePlayhead`和`mediaUpdateQoS`）相同的媒体方法，因此在事件和变量页面上显示的调用工作方式相同。 直接调用Setter API；getter API通过`API_RESPONSE`回调返回其值。

## 下一步

实施完成后，您可以[为仅限Analytics的实施设置报表](/help/reporting/setup/analytics-reporting.md)。

>[!MORELIKETHIS]
>
>* [事件概述](/help/implementation/events/overview.md)
>* [变量概述](/help/implementation/variables/overview.md)
>* [Roku Edge SDK](/help/implementation/edge/roku.md)
