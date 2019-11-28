---
title: 在 Roku 中跟踪搜寻
description: 本主题介绍如何在 Roku 中使用 Media SDK 实施搜寻跟踪。
uuid: 0572252b-397f-4aa2-b4b5-c5346b75244a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Roku 中跟踪搜寻{#track-seeking-on-roku}

>[!IMPORTANT]
>
>下面的说明为所有 2.x SDK 实施提供了指南。如果您实施的是 1.x 版本的 SDK，可以在此处下载 1.x 开发人员指南：[下载 SDK](/help/sdk-implement/download-sdks.md)。

## 搜寻跟踪常量

| 常量名称 | 描述     |
|---|---|
| `SeekStart` | 用于跟踪搜寻开始事件的常量。 |
| `SeekComplete` | 用于跟踪搜寻结束事件的常量。 |

## 实施搜寻

1. 监听媒体播放器中的播放搜寻事件，并在发出搜寻开始事件通知时，使用 `SeekStart` 事件跟踪搜寻。

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_START, seekInfo, seekContextData)
   ```

1. 在从媒体播放器发出搜寻结束通知时，使用 `SeekComplete` 事件跟踪搜寻的结束。

   ```
   seekContextData = {}
   seekContextData = {}
   ADBMobile().mediaTrackEvent(MEDIA_SEEK_COMPLETE, seekInfo, seekContextData)
   ```

有关更多信息，请参阅跟踪方案[在主内容中进行搜寻的 VOD 播放](/help/sdk-implement/tracking-scenarios/vod-seeking.md)。
