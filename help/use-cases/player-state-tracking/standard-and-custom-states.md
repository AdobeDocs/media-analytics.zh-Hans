---
title: 关于标准状态和自定义状态
description: 了解播放器状态跟踪功能，包括实施和报告标准播放器状态与自定义播放器状态的要求和准则。
exl-id: 3c492055-d471-4147-aa78-b058d6b931f4
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: cdc5ea361829c749dfbb457288ac5ba51a530961
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 99%

---

# 关于标准状态和自定义状态

有五个标准播放器状态可用，而且您可以添加自己的自定义状态。

| 标准状态名称 | Media SDK 常数 | 媒体收集 API 名称 |
|-----------------------|------------------------------------------|-----------------------------|
| 全屏 | `ADB.Media.PlayerState.Fullscreen` | `fullScreen` |
| 隐藏式字幕 | `ADB.Media.PlayerState.ClosedCaptioning` | `closedCaptioning` |
| 静音 | `ADB.Media.PlayerState.Mute` | `mute` |
| 画中画 | `ADB.Media.PlayerState.PictureInPicture` | `pictureInPicture` |
| 聚焦 | `ADB.Media.PlayerState.InFocus` | `inFocus` |

在 Analytics 报表中，标准状态和自定义状态采用相同方式计算数据，但采用不同方式存储数据。

**对于标准状态** - 当您从“媒体管理”控制台的 Analytics 报告（管理员端）中启用播放器状态跟踪时，有 15 个解决方案变量可用于报表和数据导出。

**对于自定义状态** - 您可以创建自己的处理规则，将经过计算的值存储到自定义事件中，然后将这些规则用于报表和数据导出。

## 准则

* 一个视频会话仅限拥有 10 个播放器状态。
* 状态可以任意组合。
* 如果经过了多个播放器状态，则仅保留前 10 个状态并将其转发到下游的 VA 处理组件。
* 无论是否结束，所有状态的上限都是 10 个状态。
* 一个状态可以多次开始和结束，但只被计为单个状态。例如，`closedCapationing` 可以启动和停止五次，但它将计为单个状态。
* 状态数超过允许的最大数 10 个的每个状态都将被丢弃。

## 自定义状态

利用创建自定义状态的功能，您可以在播放会话期间捕获自定义操作和更新自定义元数据。

有关创建自定义状态的信息，请参参阅 [Media API 参考指南：`createStateObject`](https://developer.adobe.com/client-sdks/documentation/adobe-media-analytics/api-reference/)
