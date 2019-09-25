---
seo-title: Test 1 Standard回放
title: Test 1 Standard回放
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# 测试 1：标准播放{#test-standard-playback}

此测试用例可验证常规播放和排序。 它是您的认证请求中的必需元素。

## 认证申请表

**请单击此处下载认证申请表：==&gt;认证**&#x200B;申 [请表。](cert_req_form.docx)

## Certification Test 1概述

媒体分析实施包括两种类型的跟踪调用：
* 直接向Adobe Analytics(AppMeasurement)服务器发出的调用——这些调用发生在“媒体开始”和“广告开始”事件上。
* 对Media Analytics（心率）服务器发出的调用——这些调用包括带内和带外调用：
   * 带内- SDK在内容播放期间以10秒的间隔发送定时播放调用或“ping”，在广告期间以一秒的间隔发送。
   * Out-of-band - These calls can happen at any point, and include Pause, Buffering, errors, content complete, ad complete, etc.

>[!NOTE]
>媒体跟踪在所有平台上的行为都相同。

## 测试过程

完成并记录以下操作（按顺序）:

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **Adobe Analytics (AppMeasurement) server - An RDC tracking server or CNAME that resolves to an RDC tracking server is required for the Experience Cloud Visitor ID service.** The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics (Heartbeats) server - This server always has the format "", where  specifies your company name.**`[namespace].hb.omtrdc.net``[namespace]`此名称由Adobe提供。
   You need to validate certain key variables that are universal across all tracking calls:

   **`mid`Adobe Visitor ID (): The  variable is used to capture the value set in the AMCV cookie.**`mid`The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. It is found in both Adobe Analytics (AppMeasurement) and Media Analytics (heartbeats) calls.

   * **Adobe Analytics开始电话**

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

   * **媒体分析开始电话**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | start |

      >[!NOTE]
      >
      >On Media Analytics Start calls () the  values may not be present. `s:event:type=start``mid`这种情况也是允许的。They may not appear until the Media Analytics Play calls ( ).`s:event:type=play`

   * **Media Analytics Play call**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **启动媒体播放器**

   When the media player starts, the Media SDK sends the key calls to the two servers in the following order:

   1. Adobe Analytics Server —— 开始电话联系
   1. Media Analytics服务器——开始调用
   1. Media Analytics Server -“已请求Adobe Analytics开始调用”
   上述前两次调用包含其他元数据和变量。 有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上述第三个调用告知Media Analytics服务器，Media SDK请求将Adobe Analytics开始调用(`pev2=ms_s`)发送到Adobe Analytics服务器。

1. **观看广告时间（如果可用）**

   * **广告开始**
   广告开始时，将按以下顺序发送以下关键呼叫：

   1. Adobe Analytics Server —— 广告开始电话
   1. Media Analytics server - Ad Start call
   1. Media Analytics Server -“已请求Adobe Analytics广告开始呼叫”
   前两个调用包含其他元数据和变量。 For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   第三次调用告知Media Analytics服务器，Media SDK请求将Adobe Analytics广告开始调用(`pev2=msa_s`)发送到Adobe Analytics服务器。

   * **广告播放**

      During ad playback, the Media Analytics SDK sends play events of type "ad" to the Media Analytics server every second.

   * **广告结束**

      在广告达到100%时，应发送媒体分析完整计划电话。



1. **暂停广告播放至少 30 秒（如果可用）.**  **广告暂停**

   During Ad Pause, Media Analytics heartbeat or "ping" calls are sent by the SDK to the Media Analytics server every second.

   >[!NOTE]
   >
   >播放头值在暂停期间应保持不变。

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **10分钟不间断地播放主内容。**  **内容播放**

   During main content playback, the Media SDK sends heartbeats (Play calls) to the Media Analytics server every 10 seconds.

   注意：

   * 每次播放调用时，播放头位置应增加10。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      For call parameters and metadata, see Test call details.[](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **播放期间至少暂停 30 秒.** 在媒体播放器暂停时，SDK将每10秒向Media Analytics服务器发送一次暂停事件调用。 暂停结束后，播放事件应该恢复。

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **搜索／擦洗媒体。** 在擦洗媒体播放头时，不会发送任何特殊跟踪调用，但是，当在擦洗后恢复媒体播放时，播放头值应反映主内容中的新位置。

1. **重放媒体（仅限VOD）。** 重播媒体时，应发送一组新的“媒体开始”调用（好像它是一个新的开始）。

1. **View next media in playlist.** 在播放列表中下一个媒体的“媒体开始”上，应发送一组新的“媒体开始”调用。

1. **切换媒体或流。** 切换实时流时，不应发送对第一个流的Media Analytics完整调用。 “媒体开始”调用和“播放”调用应以新节目和流名称开头，并以新节目的正确播放头和持续时间值开头。

