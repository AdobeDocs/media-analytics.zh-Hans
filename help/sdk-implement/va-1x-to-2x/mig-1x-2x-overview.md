---
title: 迁移概述
description: 本主题概述了从1.x版本迁移到2.x版本的Media SDK。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 迁移概述{#migration-overview}

从 VHL 1.x 到 VHL 2.x 的迁移很简单，新版本中为初始化、配置和播放器代理提供了更为简单的 API。

以下是 1.x 与 2.x 之间的主要差异：

* **插件、代理 -**&#x200B;您不再需要实施 Analytics、VideoPlayer 和心率的插件和代理。
* **配置 -**&#x200B;您不再需要实例化 1.x 插件的配置。

## 2.x的优势 {#benefits-of-two-x}

* All of the public methods are consolidated into the `MediaHeartbeat` class to make implementation easier on developers.
* All configs are now consolidated into the `MediaHeartbeatConfig` class.
* 您不再需要实例化Analytics、VideoPlayer和Heartbeat插件的配置。 您只需将类实例化 `MediaHeartbeat` 为包含 `MediaHeartbeatDelegate` 和实 `MediaHeartbeatConfig` 例。 这是初始化Media Analytics所需的唯一实施。

   With the initialization of `MediaHeartbeat`, you can safely delete all of the implementation for Analytics Plugin, VideoPlayer Plugin, and Heartbeat Plugin. 此外，对于将插件数组作为输入的 初始化，也应删除所有现有的实施。您可以在此处查看 1.x 实施与 2.x 实施的并列对比信息：[代码对比：1.x 与 2.x.](./code-comparison-1x-2x.md)

这里详细介绍了 2.x 中新的 API: [API 1.x 至 2.x 的转换](./1x-2x-api-change.md)。
