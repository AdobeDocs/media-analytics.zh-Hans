---
title: Test 1 Standard回放
description: 本主题介绍了在验证中使用的标准播放测试。
uuid: c4b3fead-1b27-484b-ab6a-39f1ae0f03f2
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

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
   * 带外——这些调用可以在任何点发生，包括暂停、缓冲、错误、内容完成和完成等。

>[!NOTE]
>媒体跟踪在所有平台上的行为都相同。

## 测试过程

完成并记录以下操作（按顺序）:

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **Adobe Analytics(AppMeasurement)服务器-** Experience cloud访客ID服务需要解析到RDC跟踪服务器的RDC跟踪服务器或CNAME。 The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(Heartbeats)服务器-** 此服务器始终采用“`[namespace].hb.omtrdc.net`”格式，其中指 `[namespace]` 定您的公司名称。 此名称由Adobe提供。
   您需要验证所有跟踪调用中具有通用性的特定关键变量：

   **`mid`Adobe访客ID(**):该 `mid` 变量用于捕获在AMCV cookie中设置的值。 The `mid` variable is the primary identification value for both websites and mobile apps, and also indicates that the Experience Cloud Visitor ID service is set up properly. 它可在Adobe Analytics(AppMeasurement)和Media Analytics（心率）调用中找到。

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
      >在媒体分析开始调用(`s:event:type=start`)时， `mid` 可能不存在这些值。 这种情况也是允许的。在Media Analytics play调用()之前，它们才会显 `s:event:type=play`示。

   * **媒体分析播放电话**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **启动媒体播放器**

   当媒体播放器启动时，Media SDK会按以下顺序将密钥调用发送到两台服务器：

   1. Adobe Analytics Server —— 开始电话联系
   1. Media Analytics服务器——开始调用
   1. Media Analytics Server -“已请求Adobe Analytics开始调用”
   上述前两次调用包含其他元数据和变量。 有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上述第三个调用告知Media Analytics服务器，Media SDK请求将Adobe Analytics开始调用(`pev2=ms_s`)发送到Adobe Analytics服务器。

1. **观看广告时间（如果可用）**

   * **广告开始**
   广告开始时，将按以下顺序发送以下关键呼叫：

   1. Adobe Analytics Server —— 广告开始电话
   1. Media Analytics Server —— 广告开始调用
   1. Media Analytics Server -“已请求Adobe Analytics广告开始呼叫”
   前两个调用包含其他元数据和变量。 有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   第三次调用告知Media Analytics服务器，Media SDK请求将Adobe Analytics广告开始调用(`pev2=msa_s`)发送到Adobe Analytics服务器。

   * **广告播放**

      在广告播放过程中，Media Analytics SDK每秒会向Media Analytics服务器发送“ad”类型的播放事件。

   * **广告结束**

      在广告达到100%时，应发送媒体分析完整计划电话。



1. **暂停广告播放至少 30 秒（如果可用）.**  **广告暂停**

   在广告暂停期间，SDK会每秒将Media Analytics心跳或“ping”调用发送到Media Analytics服务器。

   >[!NOTE]
   >
   >播放头值在暂停期间应保持不变。

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **10分钟不间断地播放主内容。**  **内容播放**

   在主内容播放期间，Media SDK每10秒向Media Analytics服务器发送心跳（播放调用）。

   注释:

   * 每次播放调用时，播放头位置应增加10。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **播放期间至少暂停 30 秒.** 在媒体播放器暂停时，SDK将每10秒向Media Analytics服务器发送一次暂停事件调用。 暂停结束后，播放事件应该恢复。

   有关调用参数和元数据，请参阅测 [试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **搜索／擦洗媒体。** 在擦洗媒体播放头时，不会发送任何特殊跟踪调用，但是，当在擦洗后恢复媒体播放时，播放头值应反映主内容中的新位置。

1. **重放媒体（仅限VOD）。** 重播媒体时，应发送一组新的“媒体开始”调用（好像它是一个新的开始）。

1. **查看播放列表中的下一个媒体。** 在播放列表中下一个媒体的“媒体开始”上，应发送一组新的“媒体开始”调用。

1. **切换媒体或流。** 切换实时流时，不应发送对第一个流的Media Analytics完整调用。 “媒体开始”调用和“播放”调用应以新节目和流名称开头，并以新节目的正确播放头和持续时间值开头。

