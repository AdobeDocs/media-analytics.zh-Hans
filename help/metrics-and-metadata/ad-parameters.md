---
title: 广告参数
description: null
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
translation-type: ht
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 广告参数{#ad-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列视频广告数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *发送条件* - 指示何时发送数据：*媒体开始*&#x200B;表示在媒体开始播放时发送分析调用；*广告开始*&#x200B;表示在广告等开始播放时发送分析调用；*关闭*&#x200B;调用表示在媒体会话或广告、章节等结束时直接从心率服务器向分析服务器发送经过汇编的分析调用。在网络数据包调用中无法使用关闭调用。
   * *最低 SDK 版本* - 指示访问参数时所需的 SDK 版本。
   * *示例值* - 提供变量的常用值示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示的是在由 Adobe Media SDK 生成的网络调用中看到的参数的名称。
* **报表：**&#x200B;关于如何查看和分析视频数据的信息。
   * *提供* - 指示是默认在报告中提供该数据（“是”**），还是需要自定义设置（“自定义”**）
   * *保留的变量* - 指示是否将数据作为保留变量中的事件、eVar、属性或分类进行捕获。
   * *报表名称* - Adobe Analytics 变量报表的名称
   * *上下文数据* - 传递到报表服务器并在处理规则中使用的 Adobe Analytics 上下文数据的名称。
   * *数据馈送* - Clickstream 或 Live Stream 数据馈送中存在的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中存在的特征名称

>[!IMPORTANT]
>
>请勿更改下面列出的在“报表/保留的变量”下描述为“分类”
>的任何变量的分类名称。
>在启用报表包进行媒体跟踪时，将定义媒体分类
>。Adobe 会不时添加新属性，如果添加了新属性，
>客户必须重新启用其报表包才能访问新的媒体
>属性。在更新过程中，Adobe 会
>通过检查变量名称来确定是否启用了分类。如果任何
>变量名称缺失，Adobe 会再次添加缺失的变量名称。

## 广告视频数据 {#ad-video-data}

### 广告 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.id </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本  </li> <li> **示例值：**<br/>"2125" </li><li> **描述：**<br/>广告的 ID。（任何整数和/或字母组合）  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>name) </li> <li> **心率：**<br/>(s:asset:ad_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>广告 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>name) </li> <li> **数据馈送：**<br/>videoad </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.name) </li> </ul> |



### 面板中的广告位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podPosition </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>1 </li><li> **描述：**<br/>广告在父广告时间中的位置（索引）。第一个广告的索引是 0，第二个广告的索引是 1，以此类推。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podPosition) </li> <li> **心率：**<br/>(s:asset:pod_position) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>面板中的广告位置 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podPosition) </li> <li> **数据馈送：**<br/>videoadinpod </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podPosition) </li> </ul> |



### 广告长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"15"  </li><li> **描述：**<br/>视频广告的长度，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>length) </li> <li> **心率：**<br/>(l:asset:ad_length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar 和分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告长度和广告长度（变量） </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>length) </li> <li> **数据馈送：**<br/>videoadlength </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.length) </li> </ul> |



### 广告播放器名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.playerName </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"Freewheel" </li><li> **描述：**<br/>负责呈现广告的播放器的名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>playerName) </li> <li> **心率：**<br/>(s:sp:player_name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告播放器名称 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>playerName) </li> <li> **数据馈送：**<br/>videoadplayername </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.playerName) </li> </ul> |



### 广告时间名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podFriendlyName </li> <li> **必需：**<br/>SDK：是；API：否。 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>"pre-roll" </li><li> **描述：**<br/>广告时间的友好名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podFriendlyName) </li> <li> **心率：**<br/>(s:asset:pod_name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>分类 </li> <li> **报表名称：**<br/>面板名称 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podFriendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 广告时间索引

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podPosition </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/> </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>1 </li><li> **描述：**<br/>广告时间在内容中的索引，从 1 开始编号。此属性&#x200B;**仅**&#x200B;供 Media SDK 用于生成面板 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>否 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 广告时间位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podSecond </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>90 </li><li> **描述：**<br/>广告时间在内容中的偏移，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podSecond) </li> <li> **心率：**<br/>(l:asset:pod_offset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>分类 </li> <li> **报表名称：**<br/>面板位置 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podSecond) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podSecond) </li> </ul> |



### 广告时间 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>pod) </li> <li> **心率：**<br/>(s:asset:pod_id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告面板 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>pod) </li> <li> **数据馈送：**<br/>videoadpod </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 广告名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>"Ford F-150" </li><li> **描述：**<br/>广告的友好名称。在报表中，“广告名称”是分类，“广告名称（变量）”是 eVar。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>friendlyName) </li> <li> **心率：**<br/>(s:asset:ad_name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar 和分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告名称和广告名称（变量） </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>friendlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.friendlyName) </li> </ul> |



## 标准广告元数据 {#standard-ad-metadata}

### 广告商

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ADVERTISER </li> <li> **API 密钥：**<br/>media.ad.advertiser </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告中展现的产品所属的公司/品牌。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>advertiser) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>广告商 </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>advertiser) </li> <li> **数据馈送：**<br/>videoadvertiser </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.advertiser) </li> </ul> |



### 促销活动 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CAMPAIGN_ID </li> <li> **API 密钥：**<br/>media.ad.campaignId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>整数或名称（字符串）。  </li><li> **描述：**<br/>广告营销活动的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>campaign) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>营销活动 ID </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>campaign) </li> <li> **数据馈送：**<br/>videocampaign </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.campaign) </li> </ul> |



### 创作 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CREATIVE_ID </li> <li> **API 密钥：**<br/>media.ad.creativeId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>整数或名称（字符串）。  </li><li> **描述：**<br/>广告创作的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>creative) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.creative) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>创作 ID </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>creative) </li> <li> **数据馈送：**<br/>adclassificationcreative </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.creative) </li> </ul> |



### 网站 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SITE_ID </li> <li> **API 密钥：**<br/>media.ad.siteId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告网站的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>site) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.site) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>site) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.site) </li> </ul> |



### 创作 URL

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CREATIVE_URL </li> <li> **API 密钥：**<br/>media.ad.creativeURL </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告创作的 URL。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>creativeURL) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>creativeURL) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.creativeURL) </li> </ul> |



### 版面 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>PLACEMENT_ID </li> <li> **API 密钥：**<br/>media.ad.placementId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告的版面 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>placement) </li> <li> **心率：**<br/>(s:meta:<br/>a.media.ad.placement) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>placement) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.placement) </li> </ul> |




## 广告量度 {#ad-metrics}

### 广告开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li><li> **描述：**<br/>视频广告开始的次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>view) </li> <li> **心率：**<br/>(s:event:type=start)<br/> (s:asset:type=ad) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告开始 </li> <li> **数据馈送：**<br/>不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>view) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.view) </li> </ul> |



### 广告结束

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>TRUE </li><li> **描述：**<br/>视频广告完成的次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>complete) </li> <li> **心率：**<br/>(s:event:type=complete)<br/> (s:asset:type=ad)  </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告结束 </li> <li> **数据馈送：**<br/>不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>complete) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.complete) </li> </ul> |



### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>15 </li><li> **描述：**<br/>观看广告所花费的总时间，以秒为单位（即播放广告所用的秒数）。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>timePlayed) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告逗留时间 </li> <li> **数据馈送：**<br/>不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.timePlayed) </li> </ul> |



## 相关 API {#section_Related_APIs}

### createAdObject API：

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdBreakObject API：

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartbeatConfig API：

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

