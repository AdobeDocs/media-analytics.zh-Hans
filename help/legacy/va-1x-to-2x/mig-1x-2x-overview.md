---
title: 迁移概述
description: 了解如何从 Media SDK 的 1.x 版本迁移到 2.x 版本。
uuid: d84f55bc-fa90-45c1-b97d-cb5fe58e80c0
exl-id: b3b8b9f8-a6e9-4ed1-85c1-80e61460e8a0
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/mM6vZFyx6BG5MZXrzOc5hkBM6pOdzBCLiSL3WgON9LU
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
  - id: c8add8f2-4250-4fd9-9cde-9707036c567d
  - id: e992d880-33bc-4949-a648-aa7d410276cd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 235
ht-degree: 94%

---

# VHL 1.x 到 VHL 2.x 的旧版迁移概述 {#migration-overview}

从 VHL 1.x 到 VHL 2.x 的迁移很简单，新版本中为初始化、配置和播放器代理提供了更为简单的 API。

以下是 1.x 与 2.x 之间的主要差异：

* **插件、代理 -**&#x200B;您不再需要实施 Analytics、VideoPlayer 和心跳的插件和代理。
* **配置 —**&#x200B;您不再需要实例化1.x插件的配置。

## 2.x 的优势 {#benefits-of-two-x}

* 所有公共方法都已合并到 `MediaHeartbeat` 类中，从而更加便于开发人员实施。
* 现在，所有配置都已合并到 `MediaHeartbeatConfig` 类中。
* 您不再需要实例化 Analytics 插件、VideoPlayer 插件和心跳插件的配置。 您只需要使用 `MediaHeartbeatDelegate` 和 `MediaHeartbeatConfig` 实例来实例化 `MediaHeartbeat` 类。 这是初始化 Media Analytics 时所需的唯一实施。

  通过初始化 `MediaHeartbeat`，您可以安全地删除 Analytics 插件、VideoPlayer 插件和心跳插件的所有实施。 此外，对于将插件数组作为输入的 初始化，也应删除所有现有的实施。 您可以在此处查看 1.x 实施与 2.x 实施的并列对比信息：[代码对比：1.x 与 2.x](./code-comparison-1x-2x.md)。

这里详细介绍了 2.x 中的新 API：[从 API 1.x 转换到 2.x](./1x-2x-api-change.md)。
