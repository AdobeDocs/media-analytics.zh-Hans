---
title: 从1.x API转换到2.x API
description: 浏览API引用，并列出1.x和2.x版Media SDK的必需和可选跟踪API。
uuid: 6e619288-c082-4cb4-8685-e90823dadf4a
exl-id: 8d06b7df-f246-49e6-aa58-91a9d6fa889a
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 87%

---

# 从 API 1.x 转换到 2.x {#one-x-to-two-x-conv}

## Media SDK 2.x API 引用

* [Android API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/index.html)
* [iOS API 引用](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/index.html)
* [JS API 参考](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/index.html)
* [Chromecast API 引用](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/index.html)

## 必需跟踪* API：

|  VHL 1.x  | VHL 2.x |
|---|---|
| `videoPlayerPlugin.trackVideoLoad()` | 不适用 |
| `videoPlayerPlugin.trackSessionStart()` | [mediaHeartbeat.trackSessionStart(mediaObject, mediaCustomMetadata)](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionStart) |
| `videoPlayerPlugin.trackPlay()` | [mediaHeartbeat.trackPlay()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPlay) |
| `videoPlayerPlugin.trackPause()` | [mediaHeartbeat.trackPause()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackPause) |
| `videoPlayerPlugin.trackComplete()` | [mediaHeartbeat.trackComplete()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackComplete) |
| `videoPlayerPlugin.trackVideoUnload()` | [mediaHeartbeat.trackSessionEnd()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackSessionEnd) |
| `videoPlayerPlugin.trackApplicationError()` | 不适用 |
| `videoPlayerPlugin.trackVideoPlayerError()` | [mediaHeartbeat.trackError()](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackError) |

现在，所有的可选跟踪 API（例如，广告、章节、比特率更改、搜寻和缓冲）都纳入到单个 `trackEvent` API 中。[trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#trackEvent) API 接收代表要跟踪的事件类型的常量参数：

## 可选 trackEvent API：

| VHL 1.x | VHL 2.x |
|---|---|
| 在 `VideoPlayerPlugin.getAdBreakInfo()` 中返回有效的 `AdBreakInfo` | `trackEvent(Event.AdBreakStart)` |
| 在 `VideoPlayerPlugin.getAdBreakInfo()` 中返回空值 | `trackEvent(Event.AdBreakComplete)` |
| `playerPlugin.trackAdStart()` | `trackEvent(Event.AdStart, adObject, adCustomMetadata)` |
| `playerPlugin.trackAdComplete()` | `trackEvent(Event.AdComplete)` |
| 在 `VideoPlayerPlugin.getAdInfo()` 中返回空值 | `trackEvent(Event.AdSkip)` |
| `playerPlugin.trackChapterStart()` | `trackEvent(Event.ChapterStart, chapterObject, chapterCustomMetadata)` |
| `playerPlugin.trackChapterComplete()` | `trackEvent(Event.ChapterComplete)` |
| 在 `VideoPlayerPlugin.getChapterInfo()` 中返回空值 | `trackEvent(Event.ChapterSkip)` |
| `playerPlugin.trackSeekStart()` | `trackEvent(Event.SeekStart)` |
| `playerPlugin.trackSeekComplete()` | `trackEvent(Event.SeekComplete)` |
| `playerPlugin.trackBufferStart()` | `trackEvent(Event.BufferStart)` |
| `playerPlugin.trackBufferComplete()` | `trackEvent(Event.BufferComplete)` |
| `playerPlugin.trackBitrateChange()` | `trackEvent(Event.BitrateChange)` |
| `playerPlugin.trackTimedMetadata()` | `trackEvent(Event.TimedMetadataUpdate)` |
