---
seo-title: 在 Roku 中跟踪体验质量
title: 在 Roku 中跟踪体验质量
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: tm+mt
source-git-commit: a8e8ac5a808ff785a348b456dd7d183540c1d594

---


# 在 Roku 中跟踪体验质量{#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。If you are implementing a 1.x version of the SDK, you can download the 1.x Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implemement QOS

1. Identify when the bitrate changes during media playback, and use the `mediaUpdateQoS` API to update the QoS info on the Media SDK.

   QoSObject 变量：

   >[!TIP]
   >
   >These variables are only required if you are tracking QoS.

   | 变量 | 描述 | 必需 |
   | --- | --- | :---: |
   | `bitrate` | 当前比特率 | 是 |
   | `startupTime` | 开始时间 | 是 |
   | `fps` | FPS 值 | 是 |
   | `droppedFrames` | 丢帧的数量 | 是 |

   例如：

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. 当播放切换比特率时， `trackEvent(BitrateChange)` 调用以通知Media SDK比特率已更改。

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >您需要使用更 `updateQoSObject` 新的比特率值进行调用。

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (请参阅 [概述](/help/sdk-implement/track-errors/track-errors-overview.md)。)

   >[!TIP]
   >
   >跟踪媒体播放器错误不会停止媒体跟踪会话。 If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

