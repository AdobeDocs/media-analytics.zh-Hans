---
title: 测试 1：标准播放
description: 本主题介绍验证中使用的标准播放测试。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: ht
source-git-commit: cebf5697e3746721d29bfaa5356d5a2748fea435

---


# 测试 1：标准播放{#test-standard-playback}

此测试案例将验证常规播放和排序。

Media Analytics 实施包含两种类型的跟踪调用：
* 直接向 Adobe Analytics (AppMeasurement) 服务器发出的调用 - 这些调用发生在“媒体开始”和“广告开始”事件中。
* 向 Media Analytics（心率）服务器发出的调用 - 这些调用包括带内调用和带外调用：
   * 带内 - SDK 在内容播放期间每隔 10 秒发送一次计时播放调用或“ping”，在广告期间每隔 1 秒发送一次计时播放调用或“ping”。
   * 带外 - 这些调用可以在任何时间点发生，并且包括暂停、缓冲、错误、内容结束和广告结束等。

>[!NOTE]
>媒体跟踪在所有平台上的行为都相同。

## 测试步骤

完成并记录以下操作（按顺序）：

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **Adobe Analytics (AppMeasurement) 服务器 -** Experience Cloud 访客 ID 服务需要一个 RDC 跟踪服务器或可解析为 RDC 跟踪服务器的 CNAME。Adobe Analytics 跟踪服务器应该以“`.sc.omtrdc.net`”结尾，或者应该是一个 CNAME。

   * **Media Analytics（心率）服务器 -** 此服务器的格式始终为“`[namespace].hb.omtrdc.net`”，其中 `[namespace]` 指定您的公司名称。此名称由 Adobe 提供。
   您需要验证在所有跟踪调用中通用的某些关键变量：

   **Adobe 访客 ID (`mid`)：**`mid` 变量用于捕获 AMCV Cookie 中设置的值。`mid` 变量是网站和移动设备应用程序的主要标识值，它还指示已正确设置 Experience Cloud 访客 ID 服务。此变量在 Adobe Analytics (AppMeasurement) 调用和 Media Analytics（心率）调用中均可找到。

   * **Adobe Analytics 开始调用**

      | 参数 | 值（示例） |
      |---|---|
      | `pev2` | ms_s |
      | `mid` | 30250035503789876473484580554595324209 |

   * **网站页面调用**

      | 参数 | 值（示例） |
      |---|---|
      | `mid` | 30250035503789876473484580554595324209 |

   * **生命周期调用**

      | 参数 | 值（示例） |
      |---|---|
      | `pev2` | ADBINTERNAL:Lifecycle |
      | `mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics 开始调用**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >在进行 Media Analytics 开始调用 (`s:event:type=start`) 时，`mid` 值可能不存在。这是正常的。它们可能直到进行 Media Analytics 播放调用 (`s:event:type=play`) 才会出现。

   * **Media Analytics 播放调用**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **启动媒体播放器**

   媒体播放器启动时，Media SDK 会按以下顺序将关键调用发送到两个服务器：

   1. Adobe Analytics 服务器 - 开始调用
   1. Media Analytics 服务器 - 开始调用
   1. Media Analytics 服务器 -“请求的 Adobe Analytics 开始调用”
   上述前两个调用包含其他的元数据和变量。有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)。

   上述第三个调用告知 Media Analytics 服务器，Media SDK 已请求将 Adobe Analytics 开始调用 (`pev2=ms_s`) 发送到 Adobe Analytics 服务器。

1. **观看广告时间（如果可用）**

   * **广告开始**
   广告开始时，会按照以下顺序发送以下关键调用：

   1. Adobe Analytics 服务器 - 广告开始调用
   1. Media Analytics 服务器 - 广告开始调用
   1. Media Analytics 服务器 -“请求的 Adobe Analytics 广告开始调用”
   前两个调用包含其他的元数据和变量。有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)。

   第三个调用告知 Media Analytics 服务器，Media SDK 已请求将 Adobe Analytics 广告开始调用 (`pev2=msa_s`) 发送到 Adobe Analytics 服务器。

   * **广告播放**

      在广告播放期间，Media Analytics SDK 每秒会向 Media Analytics 服务器发送一次“广告”类型的播放事件。

   * **广告结束**

      当广告播放到 100% 时，则应发送 Media Analytics 结束调用。



1. **暂停广告播放 30 秒（如果可用）。**  **广告暂停**

   在广告暂停期间，SDK 每秒会向 Media Analytics 服务器发送一次 Media Analytics 心率或“ping”调用。

   >[!NOTE]
   >
   >在暂停期间，播放头值应该保持不变。

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)。

1. **无中断播放主内容 10 分钟。**  **内容播放**

   在主内容播放期间，Media SDK 每 10 秒会向 Media Analytics 服务器发送一次心率（播放调用）。

   注释：

   * 每发起一次播放调用，播放头位置应增加 10 秒。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#play-main-content)。

1. **播放期间暂停至少 30 秒。**&#x200B;在媒体播放器暂停时，SDK 每 10 秒会向 Media Analytics 服务器发送一次暂停事件调用。暂停结束后，播放事件应该恢复。

   有关调用参数和元数据，请参阅[测试调用详细信息](/help/sdk-implement/validation/test-call-details.md#pause-main-content)。

1. **搜寻/推移媒体。**&#x200B;在推移媒体播放头时，不会发送任何特殊的跟踪调用，但是在推移后媒体播放恢复时，播放头值应反映主内容中的新位置。

1. **重新播放媒体（仅限 VOD）。**&#x200B;重新播放媒体时，应发送一组新的“媒体开始”调用（就像它是一个全新的开始）。

1. **观看播放列表中的下一个媒体。**&#x200B;在播放列表中的下一个媒体开始播放时，应发送一组新的“媒体开始”调用。

1. **切换媒体或流。**&#x200B;在切换实时流时，不应发送第一个流的 Media Analytics 结束调用。媒体开始调用和播放调用应该以新的节目和流名称开始，并以新节目的正确播放头和持续时间值开始。
