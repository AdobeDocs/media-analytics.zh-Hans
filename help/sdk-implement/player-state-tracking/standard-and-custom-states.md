---
title: 关于标准和自定义状态
description: 本主题描述播放器状态跟踪功能，包括实施和报告标准和自定义播放器状态的要求和准则。
translation-type: tm+mt
source-git-commit: f7a45dfbabe71fa9e1de7a4f4b2a7e64849e4ef4
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 1%

---


# 关于标准和自定义状态

有五个标准播放器状态可用，您可以添加您自己的自定义状态。

| 标准状态名称 | Media SDK常数 | Media Collection API名称 |
|-----------------------|------------------------------------------|-----------------------------|
| 全屏幕 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隐藏字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 静音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 画中画 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 焦点 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

对于标准状态和自定义状态，数据的计算方式相同，但对于Analytics报告，数据的存储方式不同。

**对于标准状态**-当您从Analytics报告（管理员端）的媒体管理控制台启用播放器状态跟踪时，有15个解决方案变量可用于报告和数据导出。

**对于自定义状态**-您可以创建自己的处理规则，将计算值存储到自定义事件中，然后使用这些规则进行报告和数据导出。

## 准则

* 一个视频会话仅限10个播放器状态。
* 允许任意状态组合。
* 如果多个播放器状态通过，则仅保留前10并在下游转发到VA处理组件。
* 无论是否关闭，所有状态都应用最多10个状态。
* 一个状态可以多次开始和结束，它被计为单个状态。 例如，可 `closedCapationing` 以启动和停止五次，但它将计为单个状态。
* 超过10个允许状态的最大值的每个状态都将被丢弃。

## 自定义状态

利用创建自定义状态的功能，您可以在播放会话期间捕获自定义操作和更新自定义元数据。

有关创建自定义状态的信息，请参 [阅《Media API参考指南》: `createStateObject`](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
