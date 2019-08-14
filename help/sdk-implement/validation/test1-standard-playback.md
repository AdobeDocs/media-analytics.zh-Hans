---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f2
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# 测试 1：标准播放{#test-standard-playback}

此测试用例验证常规回放和排序。它是认证请求表的一部分。

**请在此处下载认证申请表：==&gt;**[认证请求表。](cert_req_form.docx)

媒体实现由以下类型的跟踪调用组成：
* 媒体和广告开始调用直接发送到AppMeasurement(Adobe Analytics)服务器。
* Media Analytics心跳调用会在开始和每10秒(对于内容)发送，或一秒钟(对于广告)发送到媒体分析跟踪服务器。

>[!NOTE]
>媒体跟踪在所有平台上的行为都相同。

您必须按以下顺序完成并记录这些操作：

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **AppMeasurement(Adobe Analytics)-** 对于Experience Cloud访问者ID服务，需要解析为RDC跟踪服务器的RDC跟踪服务器或CNAME。The Analytics tracking server should end in "`.sc.omtrdc.net`" or be a CNAME.

   * **Media Analytics(HeartBeats)-** 此服务器始终具有格式“`[namespace].hb.omtrdc.net`，在其中 `[namespace]` 指定您的公司名称。此名称由Adobe提供。
   您需要验证所有跟踪调用中通用的关键变量：

   **Adobe访问者ID(`mid`)：**`mid` 变量用于捕获AMCV cookie中设置的值。`mid` 该变量是网站和移动应用程序的主要标识值，还指示Experience Cloud访客ID服务设置正确。可在AppMeasurement和Media Analytics调用中找到它。

   * **Media Analytics Play调用**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | play |
      | `s:user:mid` | 30250035503789876473484580554595324209 |

   * **Media Analytics Start Call**

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

   * **心率开始调用**

      | 参数 | 值（示例） |
      |---|---|
      | `s:event:type` | start |

   * **VA 开始调用**

      >[!NOTE]
      >
      >On VA Start Calls (`s:event:type=start`) the `mid` values may not be present. 这种情况也是允许的。They may not appear until the VA Play Calls ( `s:event:type=play`).

      | 参数 | 值（示例） |
      |---|---|
      | `pev2` | ms_s |


1. **启动媒体播放器**

   当媒体播放器启动时，键调用按以下顺序发送：

   1. Media Analytics 开始
   1. 心率开始
   1. 心率分析开始
   以上两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md)

1. **观看广告时间（如果可用）**

   * **广告开始**
   媒体广告启动时，下列键调用按以下顺序发送：

   1. 媒体广告分析开始
   1. 心率广告开始
   1. 心率广告分析开始
   前两个调用包含额外的元数据和变量。有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **广告播放**

      在广告播放期间，每秒钟就会向心率服务器发送一次心率调用。

   * **广告结束**

      在媒体广告的100%处，将发送心跳完整呼叫。



1. **暂停广告播放至少 30 秒（如果可用）.**  **广告暂停**

   在广告暂停期间，每秒钟就会向心率服务器发送一次心率调用。

   >[!NOTE]
   >
   >在暂停期间，播放头值应保持不变。

1. **播放主要内容媒体10分钟不间断。**  **内容播放**

   在主要内容播放期间，心跳调用每隔十秒发送到Media Analytics服务器。

   注意：

   * 每发起一次播放调用，播放头位置应增加 10。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      有关调用参数和元数据，请参阅 [测试调用详细信息。](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b)

1. **播放期间至少暂停 30 秒.** 暂停媒体播放器时，将每隔10秒发送暂停事件调用。暂停结束后，播放事件应该恢复。

1. **搜索/划动媒体。** 在划动媒体播放头时，不会发送特殊跟踪调用，但是，在划动播放头值后继续播放媒体时，将在主内容中反映新位置。

1. **重放媒体(仅限VOD)。** 重放媒体时，应发送一组新的媒体开始调用，就像这是一个全新的媒体视图一样。

1. **查看播放列表中的下一个媒体。** 在播放列表中的下一个媒体的媒体开始时，应发送一组新的媒体开始调用。

1. **切换媒体或流。**&#x200B;在切换实时流时，不应该发送第一个流的心率完成调用。媒体开始调用和媒体播放调用应以新的显示和流名称开头，并具有新显示屏的正确播放头和持续时间值。

