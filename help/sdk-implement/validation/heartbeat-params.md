---
seo-title: 心率参数描述
title: 心率参数描述
uuid: e9dda32-0952-43d0-a702-49f5 b1 bfd8 cf
translation-type: tm+mt
source-git-commit: 1b785378750349c4f316748d228754cb64f70bca

---


# Media Analytics(Heartbat)参数描述{#heartbeat-parameter-descriptions}

Adobe收集和处理心率服务器上的媒体分析参数的列表：

## 所有事件

| 名称 | 必需/可选 | 数据源 | 描述   |
| ---  | :---: | --- | --- |
| `s:event:type` | R | Media SDK | 被跟踪的事件的类型。事件类型： <ul> <li> `s:event:type=start` </li> <li> `s:event:type=complete` </li> <li> `s:event:type=chapter_start` </li> <li> `s:event:type=chapter_complete` </li> <li> `s:event:type=buffer` </li> <li> `s:event:type=pause` </li> <li> `s:event:type=resume` </li> <li> `s:event:type=bitrate_change` </li> <li> `s:event:type=aa_start` </li> <li> `s:event:type=stall` </li> <li> `s:event:type=end` </li> </ul> |
| `l:event:prev_ts` | R | Media SDK | 此会话中具有相同类型的最后一个事件的时间戳。The value is `-1` |
| `l:event:ts` | R | Media SDK | 事件的时间戳。 |
| `l:event:duration` | R | Media SDK | 此值通过 VHL 库在内部设置（以毫秒为单位），而不通过播放器进行设置。它用于在后端计算花费时间量度。For example `a.media.totalTimePlayed` `type=play` Note:  For some of the HB that are sent This parameter is set to 0 for certain events because they are "state change events" (e.g., `type=complete` `type=chapter_complete` `type=bitrate_change` |
| `l:event:playhead` | R | `VideoInfo` | 当事件被记录时，播放头位于当前活动的资产（主资产或广告）内。 |
| `s:event:sid` | R | Media SDK | 会话 ID（随机生成的字符串）。特定会话中的所有事件（视频 + 广告）应当相同。 |
| `l:asset:duration / l:asset:length` (重命名自 `length``duration` | R | `VideoInfo` | 主资产的视频资产长度。 |
| `s:asset:publisher` | R | `MediaHeartbeatConfig` | 资产的发布者。 |
| `s:asset:video_id` | R | `VideoInfo` | 在发布者的目录中唯一识别视频的 ID。 |
| `s:asset:type` | R | Media SDK | 资产类型（主资产或广告）。 |
| `s:stream:type` | R | `VideoInfo` | 流类型。可以为以下类型之一： <ul> <li> `live` </li> <li> `vod` </li> <li> `linear` </li> </ul>。 |
| `s:user:id` | O | 移动设备应用程序测量 VisitorID 的配置对象 | 专门设置的用户访客 ID。 |
| `s:user:aid` | O | Experience Cloud 组织 | 用户的 Analytics 访客 ID 值。 |
| `s:user:mid` | R | Experience Cloud 组织 | 用户的 Experience Cloud 访客 ID 值。 |
| `s:cuser:customer_user_ids_x` | O | `MediaHeartbeatConfig` | 在 Audience Manager 中设置的所有客户用户 ID。 |
| `l:aam:loc_hint` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:aam:blob` | R | `MediaHeartbeatConfig` | AAM data sent on each payload after `aa_start` |
| `s:sc:rsid` | R | 单个或多个报表包 ID | 应发送报告的Adobe Analytics RSID。 |
| `s:sc:tracking_server` | R | `MediaHeartbeatConfig` | Adobe Analytics跟踪服务器。 |
| `h:sc:ssl` | R | `MediaHeartbeatConfig` | 流量是经由 HTTPS（设置为 1）还是经由 HTTP（设置为 0）。 |
| `s:sp:ovp` | O | `MediaHeartbeatConfig` | 对于 Primetime 播放器，设置为“primetime”；对于其他播放器，则设置为实际的 OVP。 |
| `s:sp:sdk` | R | `MediaHeartbeatConfig` | OVP 版本字符串。 |
| `s:sp:player_name` | R | `VideoInfo` | 视频播放器名称（实际的播放器软件，用于识别播放器）。 |
| `s:sp:channel` | O | `MediaHeartbeatConfig` | 用户从中观看内容的渠道。对于移动设备应用程序，为应用程序名称。对于网站，则为域名。 |
| `s:sp:hb_version` | R | Media SDK | 发出调用的 VideoHeartbeat 库的版本号。 |
| `l:stream:bitrate` | R | `QoSInfo` | 流比特率的当前值（以 bps 为单位）。 |

## 错误事件

| 名称 | 必需/可选 | 数据源 | 描述   |
| ---  | :---: | --- | --- |
| `s:event:source` | R | Media SDK | 错误的来源，播放器内部或应用程序级别。 |
| `s:event:id` | R | Media SDK | 错误 ID，用于唯一识别错误。 |

## 广告事件

| 名称 | 必需/可选 | 数据源 | 描述   |
| ---  | :---: | --- | --- |
| `s:asset:ad_id` | R | `AdInfo` | 广告的名称。 |
| `s:asset:ad_sid` | R | Media SDK | 由 Media SDK 生成的唯一标识符，附加到所有与广告相关的 ping 之后。 |
| `s:asset:pod_id` | R | Media SDK | 视频内部的面板 ID。此值基于以下公式自动计算： `MD5(video_id) + "_" + [pod index]` |
| `s:asset:pod_position` | R | `AdBreakInfo` | 面板内部的广告索引（第一个广告的索引为 0，第二个广告的索引为 1，依此类推）。 |
| `s:asset:resolver` | R | `AdBreakInfo` | 广告解析器。 |
| `s:meta:custom_ad_metadata.x` | O | `MediaHeartbeat` | 自定义广告元数据 |

## 章节事件

| 名称 | 必需/可选 | 数据源 | 描述   |
| ---  | :---: | --- | --- |
| `s:stream:chapter_sid` | R | Media SDK | 与章节的播放实例关联的唯一标识符。注意：一个章节可因用户执行的向后搜寻操作而播放多次。 |
| `s:stream:chapter_name` | O | `ChapterInfo` | 章节的友好（即人类可读）名称。 |
| `s:stream:chapter_id` | R | Media SDK | 章节的唯一 ID。此值基于以下公式自动计算： `MD5(video_id) + "_" + chapter_pos` |
| `l:stream:chapter_pos` | R | `ChapterInfo` | 章节在章节列表中的索引（从 1 开始）。 |
| `l:stream:chapter_offset` | R | `ChapterInfo` | 主内容（不包括广告）中的章节偏移（以秒为单位）。 |
| `l:stream:chapter_length` | R | `ChapterInfo` | 章节的持续时间（以秒为单位）。 |
| `s:meta:custom_chapter_metadata.x` | O | `ChapterInfo` | 自定义章节元数据。 |

## 会话结束事件

| 名称 | 必需/可选 | 数据源 | 描述   |
| ---  | :---: | --- | --- |
| `s:event:type=end` | R | Media SDK |  `end` `close` |

