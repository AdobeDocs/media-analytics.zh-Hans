---
title: 迁移概述
description: 了解如何从1.x版本的Media SDK迁移到2.x版本。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 79%

---

# VHL 1.x到VHL 2.x的旧版迁移概述 {#migration-overview}

从VHL 1.x迁移到VHL 2.x的过程非常简单，新版本提供了用于初始化、配置和播放器代理的简化API。i

以下是 1.x 与 2.x 之间的主要差异：

* **插件、代理 -**&#x200B;您不再需要实施 Analytics、VideoPlayer 和心率的插件和代理。
* **配置 -**&#x200B;您不再需要实例化 1.x 插件的配置。

## 2.x 的优势 {#benefits-of-two-x}

* 所有公共方法都已合并到 `MediaHeartbeat` 类中，从而更加便于开发人员实施。
* 现在，所有配置都已合并到 `MediaHeartbeatConfig` 类中。
* 您不再需要实例化 Analytics 插件、VideoPlayer 插件和心率插件的配置。您只需要使用 `MediaHeartbeatDelegate` 和 `MediaHeartbeatConfig` 实例来实例化 `MediaHeartbeat` 类。这是初始化 Media Analytics 时所需的唯一实施。

   通过初始化 `MediaHeartbeat`，您可以安全地删除 Analytics 插件、VideoPlayer 插件和心率插件的所有实施。此外，对于将插件数组作为输入的 初始化，也应删除所有现有的实施。您可以在此处查看 1.x 实施与 2.x 实施的并列对比信息：[代码对比：1.x 与 2.x](./code-comparison-1x-2x.md)。

这里详细介绍了 2.x 中的新 API：[从 API 1.x 转换到 2.x](./1x-2x-api-change.md)。
