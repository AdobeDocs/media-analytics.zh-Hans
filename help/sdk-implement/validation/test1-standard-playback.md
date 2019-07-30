---
seo-title: Test Standard播放
title: Test Standard播放
uuid: c4b3fead-1b27-484b-ab6 a-39f1 ae0 f03 f2
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# 测试 1：标准播放{#test-standard-playback}

此测试用例验证常规回放和排序，并且是认证请求表的一部分。Download the certification request form here: [Certification Request Form.](cert_req_form_nielsen.docx)

视频实施由以下类型的跟踪调用组成：
* 将视频和广告开始调用直接发送到 AppMeasurement 服务器。
* Media Analytics(MA)心跳调用在开始和每隔十秒发送到Adobe VA跟踪服务器。

>[!NOTE]
>视频跟踪在所有平台、桌面和移动设备上的表现都是相同的。

您必须按照以下顺序完成并记录操作：

1. **加载页面或应用程序**

   **跟踪服务器**（适用于所有网站和移动设备应用程序）：

   * **AppMeasurement (Adobe Analytics) -** Experience Cloud 访客 ID 服务需要一个 RDC 跟踪服务器或可解析为 RDC 服务器的 CNAME。The analytics tracking server should end in `.sc.omtrdc.net` or be a CNAME.

   * **Media Analytics(HeartBeats)-** 此服务器始终具有格式 `[namespace].hb.omtrdc.net`，由 `[namespace]` 您的登录公司定义，由Adobe提供。
   您需要在所有跟踪调用中验证某些关键的通用变量：

   **Adobe访问者ID(`mid`)：**`mid` 变量用于捕获AMCV cookie中设置的值。`mid` 该变量是网站和移动应用程序的主要标识值，还指示Experience Cloud访客ID服务设置正确。它位于AppMeasurement和Media Analytics(MA)调用中。

   * **心率播放调用**

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
      >On VA Start Calls ( `s:event:type=start`) the `mid` values may not be present. 这种情况也是允许的。They may not appear until the VA Play Calls ( `s:event:type=play`).

      | 参数 | 值（示例） |
      |---|---|
      | `pev2` | ms_s |


1. **启动视频播放器**

   视频播放器启动时，会按照以下顺序发送关键调用：

   1. Video Analytics 开始
   1. 心率开始
   1. 心率分析开始
   以上两个调用包含额外的元数据和变量。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md)

1. **观看广告时间（如果可用）**

   * **广告开始**
   视频广告开始时，会按照以下顺序发送关键调用：

   1. 视频广告分析开始
   1. 心率广告开始
   1. 心率广告分析开始
   前两个调用包含额外的元数据和变量。For call parameters and metadata, see [Test call details.](/help/sdk-implement/validation/test-call-details.md#section_wz3_yff_f2b)

   * **广告播放**

      在广告播放期间，每秒钟就会向心率服务器发送一次心率调用。

   * **广告结束**

      当视频广告播放到 100% 时，将发送广告结束调用。



1. **暂停广告播放至少 30 秒（如果可用）.**  **广告暂停**

   在广告暂停期间，每秒钟就会向心率服务器发送一次心率调用。

   >[!NOTE]
   >
   >在暂停期间，播放头值应保持不变。

1. **无中断播放主内容视频 10 分钟。** **内容播放 **

   在常规主内容播放期间，每十秒就会向心率服务器发送一次心率调用。

   注意：

   * 每发起一次播放调用，播放头位置应增加 10。
   * `l:event:duration` 值表示自上次跟踪调用后所经过的毫秒数，该参数在每次 10 秒调用中的值应该大致相同。

      For call parameters and metadata, see [Test call details](/help/sdk-implement/validation/test-call-details.md#section_u1l_1gf_f2b) in *Test Call Details*

1. **播放期间至少暂停 30 秒.**&#x200B;视频播放器暂停时，将每 10 秒发送一次暂停事件调用。暂停结束后，播放事件应该恢复。

1. **搜寻/推移视频。**&#x200B;在推移视频播放头时，不会发送任何特殊的跟踪调用，但是在推移后视频播放恢复时，播放头值应反映主内容中的新位置。

1. **重新播放视频（仅限 VOD）。**&#x200B;在重新播放视频时，应该发送一组新的视频开始调用，就好像这是一个全新的视频视图一样。

1. **观看播放列表中的下一个视频。**&#x200B;在播放列表中的下一个视频开始时，将发送一组新的视频开始调用。

1. **切换视频或流。**&#x200B;在切换实时流时，不应该发送第一个流的心率完成调用。视频开始调用和视频播放调用应该以新的视频和流名称开始，并以新视频的正确播放头和持续时间值开始。

