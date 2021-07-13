---
title: 心率参数描述
description: 探索Adobe在Media Analytics（心率）服务器上收集和处理的心率参数。
uuid: e9ddda32-0952-43d0-a702-49f5b1bfd8cf
exl-id: ffa67b5e-ee54-4a5b-8064-decd108f944b
feature: '"Media Analytics， Variables"'
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '813'
ht-degree: 79%

---

# Media Analytics（心率）参数描述{#heartbeat-parameter-descriptions}

Adobe 在 Media Analytics（心率）服务器上收集和处理的 Media Analytics 参数列表：

## 所有事件

| 名称 | 数据源 |  描述  |
| ---  | --- | --- |
| s:event:类型 | Media SDK | （必需）<br/><br/>被跟踪的事件的类型。事件类型： <ul> <li> s:event:type=start </li> <li> s:event:type=complete </li> <li> s:event:type=chapter_start </li> <li> s:event:type=chapter_complete </li> <li> s:event:type=buffer </li> <li> s:event:type=pause </li> <li> s:event:type=resume </li> <li> s:event:type=bitrate_change </li> <li> s:event:type=aa_start </li> <li> s:event:type=stall </li> <li> s:event:type=end </li> </ul> |
| l:event:prev_ts | Media SDK | （必需）<br/><br/>此会话中具有相同类型的最后一个事件的时间戳。值为 -1。 |
| l&lt;a0/ts:event: | Media SDK | （必需）<br/><br/>事件的时间戳。 |
| l:event:持续时间 | Media SDK | （必需）<br/><br/>此值由 Media SDK 在内部设置（以毫秒为单位），而不是由播放器设置。它用于在后端计算花费时间量度。例如：a.media.totalTimePlayed 计算为所生成的所有播放 (type=play) 心率的持续时间总和。<br/>*注意：*&#x200B;对于某些事件，由于它们是“状态更改事件”（例如，type=complete、type=chapter_complete 或 type=bitrate_change），此参数将设置为 0。 |
| l:event:播放头 | VideoInfo | （必需）<br/><br/>当事件被记录时，播放头位于当前活动的资产（主资产或广告）内。 |
| s&lt;a0/sid:event: | Media SDK | （必需）<br/><br/>会话 ID（随机生成的字符串）。特定会话中的所有事件（视频 + 广告）应当相同。 |
| l:asset:持续时间/ l:asset:length <br/>（从长度持续时间重命名） | VideoInfo | （必需）<br/><br/>主资产的视频资产长度。 |
| s:asset:发布者 | MediaHeartbeatConfig | （必需）<br/><br/>资产的发布者。 |
| s:asset:video_id | VideoInfo | （必需）<br/><br/>发布者目录中的视频的唯一标识 ID。 |
| s:asset:类型 | Media SDK | （必需）<br/><br/>资产类型（主资产或广告）。 |
| s:stream:类型 | VideoInfo | （必需）<br/><br/>流类型。可以是以下任一类型： <ul> <li> 实时 </li> <li> VOD </li> <li> 线性 </li> </ul> |
| s:user:id | 移动设备应用程序测量 VisitorID 的配置对象 | （可选）<br/><br/>专门设置的用户访客 ID。 |
| s&lt;a0/aid:user: | Experience Cloud 组织 | （可选）<br/><br/>用户的 Analytics 访客 ID 值。 |
| s&lt;a0/mid:user: | Experience Cloud 组织 | （必需）<br/><br/>用户的 Experience Cloud 访客 ID 值。 |
| s:cuser:customer_user_ids_x | MediaHeartbeatConfig | （可选）<br/><br/>在 Audience Manager 中设置的所有客户用户 ID。 |
| l:aam:loc_hint | MediaHeartbeatConfig | （必需）<br/><br/>在 aa_start 之后的每次负载中发送的 AAM 数据 |
| s&lt;a0/blob:aam: | MediaHeartbeatConfig | （必需）<br/><br/>在 aa_start 之后的每次负载中发送的 AAM 数据 |
| s&lt;a0/rsid:sc: | 单个或多个报表包 ID | （必需）<br/><br/>应将报表发送到的 Adobe Analytics RSID。 |
| s:sc:tracking_server | MediaHeartbeatConfig | （必需）<br/><br/>Adobe Analytics 跟踪服务器。 |
| h&lt;a0/ssl:sc: | MediaHeartbeatConfig | （必需）<br/><br/>流量是经由 HTTPS（设置为 1）还是经由 HTTP（设置为 0）。 |
| s:sp:ovp | MediaHeartbeatConfig | （可选）<br/><br/>对于 Primetime 播放器，设置为“primetime”；对于其他播放器，则设置为实际的 OVP。 |
| s:sp:sdk | MediaHeartbeatConfig | （必需）<br/><br/>OVP 版本字符串。 |
| s:sp:player_name | VideoInfo | （必需）<br/><br/>视频播放器名称（实际的播放器软件，用于标识播放器）。 |
| s:sp:通道 | MediaHeartbeatConfig | （可选）<br/><br/>用户从中观看内容的渠道。对于移动应用程序，显示应用程序名称。对于网站，显示域名。 |
| s:sp:hb_version | Media SDK | （必需）<br/><br/>发出调用的 Media SDK 库的版本号。 |
| l:stream:bitrate | QoSInfo | （必需）<br/><br/>流比特率的当前值（以 bps 为单位）。 |

## 错误事件

| 名称 | 数据源 | 描述   |
| ---  | --- | --- |
| s:event:源 | Media SDK | （必需）<br/><br/>错误的来源，播放器内部或应用程序级别。 |
| s:event:id | Media SDK | （必需）<br/><br/>错误 ID，用于唯一标识错误。 |

## 广告事件

| 名称 | 数据源 | 描述   |
| ---  | --- | --- |
| s:asset:ad_id | AdInfo | （必需）<br/><br/>广告的名称。 |
| s:asset:ad_sid | Media SDK | （必需）<br/><br/>由 Media SDK 生成的唯一标识符，附加到所有与广告相关的 ping 之后。 |
| s:asset:pod_id | Media SDK | （必需）<br/><br/>视频内部的面板 ID。此值基于以下公式自动计算：<br/>`MD5(video_id) + `<br/>`"_" + `<br/>`[pod index]` |
| s:asset:pod_position | AdBreakInfo | （必需）<br/><br/>面板内部的广告索引（第一个广告的索引为 0，第二个广告的索引为 1，依此类推）。 |
| s:asset:解析程序 | AdBreakInfo | （必需）<br/><br/>广告解析程序。 |
| s:meta:custom_ad_metadata.x | MediaHeartbeat | （可选）<br/><br/>自定义广告元数据。 |

## 章节事件

| 名称 | 数据源 | 描述   |
| ---  | --- | --- |
| s:stream:chapter_sid | Media SDK | （必需）<br/><br/>与章节的播放实例关联的唯一标识符。<br/> **注意：**&#x200B;一个章节可因用户执行的向后搜寻操作而播放多次。 |
| s:stream:chapter_name | ChapterInfo | （可选）<br/><br/>章节的友好（即人类可读）名称。 |
| s:stream:chapter_id | Media SDK | （必需）<br/><br/>章节的唯一 ID。此值基于以下公式自动计算：<br/>`MD5(video_id) +`<br/>` "_" +`<br/>`chapter_pos` |
| l:stream:chapter_pos | ChapterInfo | （必需）<br/><br/>章节列表中的章节索引（从 1 开始）。 |
| l:stream:chapter_offset | ChapterInfo | （必需）<br/><br/>主内容（不包括广告）中的章节偏移（以秒为单位）。 |
| l:stream:chapter_length | ChapterInfo | （必需）<br/><br/>章节的持续时间（以秒为单位）。 |
| s:meta:custom_chapter_metadata.x | ChapterInfo | （可选）<br/><br/>自定义章节元数据。 |

## 会话结束事件

| 名称 | 数据源 | 描述   |
| ---  | --- | --- |
| s:event:type=end | Media SDK | （必需）<br/><br/> `end` 和 `close` |
