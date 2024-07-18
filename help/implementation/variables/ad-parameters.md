---
title: 广告参数
description: "了解广告参数，包括广告视频数据的实施、网络和报告变量。"
uuid: 92cd7f97-bb5a-4de6-8946-453d30271d0f
exl-id: 949e86cb-d265-4836-8825-a06b87203b15
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 917c87d759a43f124dfb3e3ac7f6a441c65fde94
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 96%

---

# 广告参数{#ad-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列视频广告数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或由 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示基本视频跟踪是否需要该参数。
   * *类型* - 指定要设置的变量的类型：字符串或数字。
   * *发送条件* - 指示何时发送数据：*媒体开始*&#x200B;表示在媒体开始播放时发送分析调用；*广告开始*&#x200B;表示在广告等开始播放时发送分析调用；*关闭*&#x200B;调用表示在媒体会话或广告、章节等结束时直接从心率服务器向分析服务器发送经过汇编的分析调用。在网络数据包调用中无法使用关闭调用。
   * *最低 SDK 版本* - 指示您访问该参数所需的 SDK 版本。
   * *示例值* - 提供常用变量用法的示例。
* **网络参数：**&#x200B;显示传递到 Adobe Analytics 或心率服务器的值。此列显示网络调用中由 Adobe Media SDK 生成的参数的名称。
* **报告：**&#x200B;有关如何查看和分析视频数据的信息。
   * *可用* - 指示在默认情况下数据在报表中可用（*是*），还是需要自定义设置（*自定义*）
   * *保留的变量* - 指示数据是作为保留变量中的事件、eVar、prop 还是分类而捕获的。
   * *报表名称* - 变量的 Adobe Analytics 报表名称
   * *上下文数据* - 传递到报表服务器并用于处理规则的 Adobe Analytics 上下文数据的名称。
   * *数据源* - Clickstream 或实时流数据源中的变量的列名称
   * *Audience Manager* - Adobe Audience Manager 中的特征名称

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
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.id </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本  </li> <li> **示例值：**<br/>&quot;2125&quot; </li><li> **描述：**<br/>&#x200B;广告的 ID。（任何整数和/或字母组合）  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>name) </li> <li> **心率：**<br/> (<code>s:asset:ad_id</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;访问时 </li> <li> **报表名称：**<br/>&#x200B;广告 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>name) </li> <li> **数据馈送：**<br/> videoad </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.name) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.@id </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.name </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.name </li> </ul> |



### 面板中的广告位置

|   实施   | 网络参数 | 报表 |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.podPosition </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>&#x200B;广告在父广告时间中的位置（索引）。第一个广告的索引是 0，第二个广告的索引是 1，以此类推。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podPosition) </li> <li> **心率：**<br/> (<code>s:asset:pod_position</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;面板中的广告位置 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podPosition) </li> <li> **数据馈送：**<br/> videoadinpod </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podPosition) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.index </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.index </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.index </li> </ul> |



### 广告长度

|   实施   | 网络参数 | 报表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.length </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>&quot;15&quot;  </li><li> **描述：**<br/>&#x200B;视频广告的长度，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>length) </li> <li> **心率：**<br/> (<code>l:asset:ad_length</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar 和分类 </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;广告长度和广告长度（变量） </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>length) </li> <li> **数据馈送：**<br/> videoadlength </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.length) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.<br/>xmpDM:duration </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.length </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.length </li> </ul> |



### 广告播放器名称

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.playerName </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;Freewheel&quot; </li><li> **描述：**<br/>&#x200B;负责呈现广告的播放器的名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>playerName) </li> <li> **心率：**<br/> (<code>s:sp:player_name</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;广告播放器名称 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>playerName) </li> <li> **数据馈送：**<br/> videoadplayername </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.playerName) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.playerName </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.<br/>playerName </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>playerName </li> </ul> |



### 广告时间名称

|   实施   | 网络参数 | 报表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.podFriendlyName </li> <li> **必需：**<br/> SDK：是；API：否。 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/>&quot;pre-roll&quot; </li><li> **描述：**<br/>&#x200B;广告时间的友好名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podFriendlyName) </li> <li> **心率：**<br/> (<code>s:asset:pod_name</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;面板名称 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podFriendlyName) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podFriendlyName) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.<br/>adBreak.dc:title </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingPodDetails.<br/>friendlyName </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingPodDetails.<br/>friendlyName </li> </ul> |



### 广告时间索引

|   实施   | 网络参数 | 报表 |
| --- | --- |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.podPosition </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/> </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>&#x200B;广告时间在内容中的索引，从 1 开始编号。此属性&#x200B;**仅**&#x200B;供 Media SDK 用于生成面板 ID。   </li> </ul> | <ul> <li> **Adobe Analytics:**<br/> </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;否 </li> <li> **保留的变量：**<br/>&#x200B;不适用 </li> <li> **报表名称：**<br/>&#x200B;不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager:**<br/> </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.index </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingPodDetails.index </li> </ul> |



### 广告时间位置

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.podSecond </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;数值 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 90 </li><li> **描述：**<br/>&#x200B;广告时间在内容中的偏移，以秒为单位。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>podSecond) </li> <li> **心率：**<br/> (<code>l:asset:pod_offset</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/>&#x200B;分类 </li> <li> **报表名称：**<br/>&#x200B;面板位置 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>podSecond) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.podSecond) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.adBreak.<br/>offset </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingPodDetails.<br/>offset </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingPodDetails.<br/>offset </li> </ul> |



### 广告时间 ID

|   实施   | 网络参数 | 报表 |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置 </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> c4a577424c84067899b807c76722d495_1  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>pod) </li> <li> **心率：**<br/> (<code>s:asset:pod_id</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;广告面板 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>pod) </li> <li> **数据馈送：**<br/> videoadpod </li> <li> **Audience Manager:**<br/> </li> <li> **XDM 字段路径：**<br/> advertising.adAssetViewDetails.adBreak.@id </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingPodDetails.<br/>ID </li> </ul> |



### 广告名称

|   实施   | 网络参数 | 报表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/> media.ad.name </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/>&quot;Ford F-150&quot; </li><li> **描述：**<br/>&#x200B;广告的友好名称。在报表中，“广告名称”是分类，“广告名称（变量）”是 eVar。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>friendlyName) </li> <li> **心率：**<br/> (<code>s:asset:ad_name</code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar 和分类 </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;广告名称和广告名称（变量） </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>friendlyName) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.friendlyName) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.dc:title </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.friendlyName </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.friendlyName </li> </ul> |



## 标准广告元数据 {#standard-ad-metadata}

### 广告商

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> ADVERTISER </li> <li> **API 密钥：**<br/> media.ad.advertiser </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;广告中展现的产品所属的公司/品牌。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>advertiser) </li> <li> **心率：**<br/> (<code>s:meta:</code><br/>a.media.ad.advertiser) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/> <i>广告商 </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>advertiser) </li> <li> **数据馈送：**<br/> videoadvertiser </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.advertiser) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.advertiser </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.advertiser </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.advertiser </li> </ul> |



### 促销活动 ID

|   实施   | 网络参数 | 报表 |
| --- | --- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> CAMPAIGN_ID </li> <li> **API 密钥：**<br/> media.ad.campaignId </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&#x200B;整数或名称（字符串）。  </li><li> **描述：**<br/>&#x200B;广告营销活动的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>campaign) </li> <li> **心率：**<br/> (<code>s:meta:</code><br/>a.media.ad.campaign) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/> <i>营销活动 ID </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>campaign) </li> <li> **数据馈送：**<br/> videocampaign </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.campaign) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.campaign </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.<br/>campaignID </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>campaignID </li> </ul> |



### 创作 ID

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> CREATIVE_ID </li> <li> **API 密钥：**<br/> media.ad.creativeId </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/>&#x200B;整数或名称（字符串）。  </li><li> **描述：**<br/>&#x200B;广告创作的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>creative) </li> <li> **心率：**<br/> (<code>s:meta:</code><br/>a.media.ad.creative) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/> <i>创作 ID </i> </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>creative) </li> <li> **数据馈送：**<br/> adclassificationcreative </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.creative) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.creativeID </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.creativeID </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.creativeID </li> </ul> |



### 网站 ID

|   实施   | 网络参数 | 报表 |
| --- | --- |----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> SITE_ID </li> <li> **API 密钥：**<br/> media.ad.siteId </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;广告网站的 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>site) </li> <li> **心率：**<br/> (<code>s:meta:</code><br/>a.media.ad.site) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;自定义 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>site) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.site) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.siteID </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.siteID </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.siteID </li> </ul> |



### 创作 URL

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> CREATIVE_URL </li> <li> **API 密钥：**<br/> media.ad.creativeURL </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;广告创作的 URL。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>creativeURL) </li> <li> **心率：**<br/> (<code>s:meta:&lt;c/ode><br/>a.media.ad.creativeURL) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;自定义 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>creativeURL) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.creativeURL) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.creativeURL </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.<br/>creativeURL </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>creativeURL </li> </ul> |



### 版面 ID

|   实施   | 网络参数 | 报表 |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/> PLACEMENT_ID </li> <li> **API 密钥：**<br/> media.ad.placementId </li> <li> **必需：**<br/>&#x200B;否 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始、广告关闭 </li> <li> **最低 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>&#x200B;广告的版面 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>placement) </li> <li> **心率：**<br/> (<code>s:meta:</code><br/>a.media.ad.placement) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则</i> </li> <li> **保留的变量：**<br/> eVar </li> <li> **过期时间：**<br/>&#x200B;点击时 </li> <li> **报表名称：**<br/>&#x200B;自定义 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>placement) </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.placement) </li> <li> **XDM 字段路径：**<br/> advertising.adAssetReference.placementID </li> <li> **收集 XDM 字段路径：**<br/> mediaCollection.advertisingDetails.<br/>placementID </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>placementID </li> </ul> |




## 广告量度 {#ad-metrics}

### 广告开始

|   实施   | 网络参数 | 报表 |
| --- | --- |-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置 </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告开始 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>&#x200B;视频广告开始的次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>view) </li> <li> **心率：**<br/> (<code>s:event:type=start</code>)<br/> (<code>s:asset:type=ad<code>) </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;广告开始 </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>view) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.view) </li> <li> **XDM 字段路径：**<br/> advertising.starts.value > 0 => &quot;TRUE&quot; </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.isStarted </li> </ul> |



### 广告结束

|   实施   | 网络参数 | 报表 |
| --- | --- |---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置 </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>&#x200B;视频广告完成的次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>complete) </li> <li> **心率：**<br/> (<code>s:event:type=complete</code>)<br/> (<code>s:asset:type=ad</code>)  </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;广告结束 </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>complete) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.complete) </li> <li> **XDM 字段路径：**<br/> advertising.completes.value > 0 => &quot;TRUE&quot; </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>isCompleted </li> </ul> |



### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <ul> <li> **SDK 密钥：**<br/>&#x200B;自动设置 </li> <li> **API 密钥：**<br/>&#x200B;不适用 </li> <li> **必需：**<br/>&#x200B;是 </li> <li> **类型：**<br/>&#x200B;字符串 </li> <li> **发送条件：**<br/>&#x200B;广告关闭 </li> <li> **最低 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 15 </li><li> **描述：**<br/>&#x200B;观看广告所花费的总时间，以秒为单位（即播放广告所用的秒数）。该值将以时间格式(<code>HH:MM:SS)显示</code>Analysis Workspace )以及Reports &amp; Analytics中的“禁止页面加载闪烁”。 而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/>(a.media.ad.<br/>timePlayed) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>&#x200B;是 </li> <li> **保留的变量：**<br/> event </li> <li> **报表名称：**<br/>&#x200B;广告逗留时间 </li> <li> **数据馈送：**<br/>&#x200B;不适用 </li> <li> **上下文数据：**<br/>(a.media.ad.<br/>timePlayed) </li> <li> **Audience Manager：**<br/>(c_contextdata.<br/>a.media.ad.timePlayed) </li> <li> **XDM 字段路径：**<br/> advertising.timePlayed.value </li> <li> **报告 XDM 字段路径：**<br/> mediaReporting.advertisingDetails.<br/>timePlayed </li> </ul> |



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
