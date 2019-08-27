---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f2
translation-type: tm+mt
source-git-commit: f2b08663a928e27625a9ff63f783c510f41e7a8c

---


# 测试 1：标准播放{#test-standard-playback}

此测试用例验证常规回放和排序。它是认证请求的必需元素。

## 认证申请表

**请在此处下载认证申请表：==&gt;**[认证请求表。](cert_req_form.docx)

## Certification Test概述

媒体分析实现包括两种类型的跟踪调用：
* 直接向Adobe Analytics(AppMeasurement)服务器发出调用-这些调用在“媒体开始”和“广告开始”事件上进行。
* 调用Media Analytics(heartbeats)服务器-包括带内和带外呼叫：
   * 带内- SDK在内容播放期间以10秒的间隔发送定时播放或“ping”，在广告期间以秒间隔播放。
   * 带外-这些调用可能在任意点发生，包括暂停、缓冲、错误、内容完成、广告完成等。

>[!NOTE]
>媒体跟踪在所有平台上的行为都相同。

## 测试过程

完成并记录以下操作(按顺序)：

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **Adobe Analytics(AppMeasurement)服务器-** Experience Cloud访问者ID服务需要解析为RDC跟踪服务器的RDC跟踪服务器或CNAME。The Adobe Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(HeartBeats)服务器-** 此服务器始终具有格式“`[namespace].hb.omtrdc.net`，其中 `[namespace]` 指定您的公司名称。此名称由Adobe提供。
   您需要验证所有跟踪调用中通用的关键变量：

   **Adobe访问者ID(`mid`)：**`mid` 变量用于捕获AMCV cookie中设置的值。`mid` 该变量是网站和移动应用程序的主要标识值，还指示Experience Cloud访客ID服务设置正确。它位于Adobe Analytics(AppMeasurement)和Media Analytics(心跳)调用中。

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
      >在Media Analytics开始调用(`s:event:type=start`) `mid` 中，这些值可能不存在。这种情况也是允许的。在Media Analytics Play调用( `s:event:type=play`)之前，它们可能不会显示。

   * **Media Analytics Play电话**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |


1. **启动媒体播放器**

   媒体播放器启动时，Media SDK按以下顺序发送对两台服务器的键调用：

   1. Adobe Analytics服务器-开始电话
   1. 媒体分析服务器-开始电话
   1. 媒体分析服务器-“请求的Adobe Analytics开始电话”
   以上两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#start-the-media-player)

   上面的第三个调用告知Media SDK媒体SDK已请求将Adobe Analytics Start调用(`pev2=ms_s`)发送到Adobe Analytics服务器。

1. **观看广告时间（如果可用）**

   * **广告开始**
   广告开始时，下列键调用按以下顺序发送：

   1. Adobe Analytics服务器-广告开始电话
   1. 媒体分析服务器-广告开始电话
   1. 媒体分析服务器-“请求的Adobe Analytics Ad Start调用”
   前两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#view-ad-playback)

   第三个调用告诉媒体分析服务器，媒体SDK要求将Adobe Analytics Ad Start调用(`pev2=msa_s`)发送到Adobe Analytics服务器。

   * **广告播放**

      在广告播放过程中，媒体分析SDK每秒将“广告”类型的“广告”发送给Media Analytics服务器。

   * **广告结束**

      在广告的100%点，应发送Media Analytics完成电话。



1. **暂停广告播放至少 30 秒（如果可用）.**  **广告暂停**

   在Ad Pause中，媒体分析心跳或“ping”调用每秒都由SDK发送到Media Analytics服务器。

   >[!NOTE]
   >
   >在暂停期间，播放头值应保持不变。

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#ma-ad-pause-call)

1. **播放主内容10分钟不间断。**  **内容播放**

   在主要内容播放过程中，Media SDK每10秒向Media Analytics服务器发送心跳(播放调用)。

   注意：

   * 每次播放调用时，播放头位置应增加10。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#play-main-content)

1. **播放期间至少暂停 30 秒.** 暂停媒体播放器时，每隔10秒SDK将由SDK发送暂停事件调用。暂停结束后，播放事件应该恢复。

   有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#pause-main-content)

1. **搜索/划动媒体。** 在划动媒体播放头时，不会发送特殊的跟踪调用，但是，在划动之后，当播放后恢复媒体播放时，播放头值应反映主内容内的新位置。

1. **重放媒体(仅限VOD)。** 重放媒体时，应发送一组新的媒体开始调用(就像它是一个新开始一样)。

1. **查看播放列表中的下一个媒体。** 在播放列表中的下一个媒体的“媒体开始”中，应发送一组新的媒体开始调用。

1. **切换媒体或流。** 切换实时流时，不应发送对第一个流的Media Analytics完整调用。媒体开始调用和播放调用应以新的显示和流名称开头，并具有新显示的正确播放头和持续时间值。

