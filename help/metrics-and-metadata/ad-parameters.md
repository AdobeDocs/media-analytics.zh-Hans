---
seo-title: 广告参数
title: 广告参数
uuid: 92cd7f97-bb5 a-4de6-849-453d30271 d0 f
translation-type: tm+mt
source-git-commit: 180eafdfc536039820ade0b52e5c55f874719d8e

---


# 广告参数{#ad-parameters}

本主题介绍 Adobe 通过解决方案变量收集的一系列视频广告数据，包括上下文数据值。

表格数据描述：

* **实施：**&#x200B;关于实施值和要求的信息
   * *密钥* - 在应用程序中手动设置或通过 Adobe Media SDK 自动设置的变量。
   * *必需* - 指示该项是否为进行基本视频跟踪所必需的参数。
   * *类型* - 指定要设置的变量类型：字符串或数值。
   * *随附-* 指示数据何时发送： *媒体开始* 是在媒体开始时发送的分析调用， *广告开始* 是在广告开始时发送的分析调用，依此类推； *结束* 调用是在媒体会话结束时直接从心跳服务器发送到分析服务器的编译的分析调用，或者广告、章节等结尾处的分析调用。close调用在网络包调用中不可用。
   * *最小 SDK 版本* - 指示访问参数时所需的 SDK 版本。
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
>请勿更改以下所列变量的分类名称，如“报告/保留变量”下所述的“分类”。\
>在启用了媒体跟踪的情况下，将定义媒体分类。Adobe时常会添加新属性，当发生这种情况时，客户必须重新启用报告套件才能访问新媒体属性。在更新过程中，Adobe通过检查变量的名称来确定是否启用了分类。如果其中任何一项缺失，Adobe将再次添加缺失的组件。

## 广告视频数据 {#section_hq3_nbv_51b}

### 广告 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [adId](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.id </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本  </li> <li> **示例值：**<br/> “2125” </li><li> **描述：**<br/>广告的ID。（任何整数和/或字母组合）  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.na我) </li> <li> **心跳：**<br/> (s：资产：ad_ id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>访问时 </li> <li> **报表名称：**<br/>广告 </li> <li> **上下文数据：**<br/> (a.media.ad.na我) </li> <li> **数据馈送：**<br/>videoad </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.name) </li> </ul> |



### 面板中的广告位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/> [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podPosition </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>父广告段内广告的位置(索引)。第一个广告的索引是 0，第二个广告的索引是 1，以此类推。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.podocPosition) </li> <li> **心跳：**<br/> (s：资产：pod_ position) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>面板中的广告位置 </li> <li> **上下文数据：**<br/> (a.media.ad.podocPosition) </li> <li> **数据馈送：**<br/>videoadinpod </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.podPosition) </li> </ul> |



### 广告长度

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [length](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.length </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/> “15”  </li><li> **描述：**<br/>视频广告长度(以秒为单位)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.length) </li> <li> **心跳：**<br/> (l：资产：ad_ length) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar 和分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告长度和广告长度（变量） </li> <li> **上下文数据：**<br/> (a.media.ad.length) </li> <li> **数据馈送：**<br/>videoadlength </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.length) </li> </ul> |



### 广告播放器名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [playerName](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.playerName </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> “FreeWheel” </li><li> **描述：**<br/>负责渲染广告的播放器的名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.plAyerName) </li> <li> **心跳：**<br/> (s：sp：player_ name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告播放器名称 </li> <li> **上下文数据：**<br/> (a.media.ad.plAyerName) </li> <li> **数据馈送：**<br/>videoadplayername </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.playerName) </li> </ul> |



### 广告时间名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podFriendlyName </li> <li> **必需：**<br/> SDK：是；API：不会。 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> “预滚动” </li><li> **描述：**<br/>广告中断的友好名称。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.podristrilyName) </li> <li> **心跳：**<br/> (s：资产：pod_ name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>面板名称 </li> <li> **上下文数据：**<br/> (a.media.ad.podristrilyName) </li> <li> **数据馈送：**<br/>videoadpod </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.podFriendlyName) </li> </ul> |



### 广告时间索引

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [position](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podPosition </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/> </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 1 </li><li> **描述：**<br/>内容中广告中断的索引，从开始。此属性&#x200B;**仅**&#x200B;供 Media SDK 用于生成面板 ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>否 </li> <li> **保留的变量：**<br/>不适用 </li> <li> **报表名称：**<br/>不适用 </li> <li> **上下文数据：**<br/> </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 广告时间位置

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [startTime](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.podSecond </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>数值 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 90 </li><li> **描述：**<br/>内容在内容内的偏移量(以秒为单位)。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.podSecond) </li> <li> **心跳：**<br/> (l：资产：pod_ offset) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留变量：**<br/>分类 </li> <li> **报表名称：**<br/>面板位置 </li> <li> **上下文数据：**<br/> (a.media.ad.podSecond) </li> <li> **数据馈送：**<br/> </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.podSecond) </li> </ul> |



### 广告时间 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> c4a577424c84067899b807c7672d495_1  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (dogd) </li> <li> **心跳：**<br/> (l：资产：pod_ id) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告面板 </li> <li> **上下文数据：**<br/> (dogd) </li> <li> **数据馈送：**<br/>videoadpod </li> <li> **Audience Manager：**<br/> </li> </ul> |



### 广告名称

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>  [name](./ad-parameters.md#section_Related_APIs) </li> <li> **API 密钥：**<br/>media.ad.name </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.1 </li> <li> **示例值：**<br/> “福特F-150” </li><li> **描述：**<br/>广告的友好名称。在报表中，“广告名称”是分类，“广告名称（变量）”是 eVar。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.friEnlyName) </li> <li> **心跳：**<br/> (s：资产：ad_ name) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar 和分类 </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/>广告名称和广告名称（变量） </li> <li> **上下文数据：**<br/> (a.media.ad.friEnlyName) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.friendlyName) </li> </ul> |



## 标准广告元数据 {#section_EFB805867916411E84DE1BA5A183D86A}

### 广告商

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>ADVERTISER </li> <li> **API 密钥：**<br/>media.ad.advertiser </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告中特色产品的公司/品牌。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.ad版本选择器) </li> <li> **心跳：**<br/> (s：meta：<br/>a.media.ad.ad版本选择器) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>广告商 </i> </li> <li> **上下文数据：**<br/> (a.media.ad.ad版本选择器) </li> <li> **数据馈送：**<br/>videoadvertiser </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.advertiser) </li> </ul> |



### 促销活动 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CAMPAIGN_ID </li> <li> **API 密钥：**<br/>media.ad.campaignId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> 整数或名称(字符串)。  </li><li> **描述：**<br/>广告营销活动的ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.camblan) </li> <li> **心跳：**<br/> (s：meta：<br/>a.media.ad.cambresn) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>营销活动 ID </i> </li> <li> **上下文数据：**<br/> (a.media.ad.camblan) </li> <li> **数据馈送：**<br/>videocampaign </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.campaign) </li> </ul> |



### 创作 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CREATIVE_ID </li> <li> **API 密钥：**<br/>media.ad.creativeId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> 整数或名称(字符串)。  </li><li> **描述：**<br/>广告创意的ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (可填写) </li> <li> **心跳：**<br/> (s：meta：<br/>信息性) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i>创作 ID </i> </li> <li> **上下文数据：**<br/> (可填写) </li> <li> **数据馈送：**<br/>adclassificationcreative </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.creative) </li> </ul> |



### 网站 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>SITE_ID </li> <li> **API 密钥：**<br/>media.ad.siteId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告站点的ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (试用版) </li> <li> **心跳：**<br/> (s：meta：<br/>试用版) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则 </i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/> (试用版) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.site) </li> </ul> |



### 创作 URL

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>CREATIVE_URL </li> <li> **API 密钥：**<br/>media.ad.creativeURL </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告创意的URL。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.creativeURL) </li> <li> **心跳：**<br/> (s：meta：<br/>loc eativeURL) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则 </i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/> (a.media.ad.creativeURL) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.creativeURL) </li> </ul> |



### 版面 ID

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>PLACEMENT_ID </li> <li> **API 密钥：**<br/>media.ad.placementId </li> <li> **必需：**<br/>否 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始、广告关闭 </li> <li> **最小 SDK 版本：** 1.5.7 </li> <li> **示例值：**<br/> </li><li> **描述：**<br/>广告的放置ID。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.pl实习) </li> <li> **心跳：**<br/> (s：meta：<br/>a.media.ad.pl管理) </li> </ul> | <ul> <li> **可用：**<br/> <i>使用自定义处理规则 </i> </li> <li> **保留的变量：**<br/>eVar </li> <li> **过期时间：**<br/>点击时 </li> <li> **报表名称：**<br/> <i> </i> </li> <li> **上下文数据：**<br/> (a.media.ad.pl实习) </li> <li> **数据馈送：**<br/>不适用 </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.placement) </li> </ul> |




## 广告量度 {#section_22AA1565F11C4F3990E2AB51CD3213F7}

### 广告开始

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告开始 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>视频广告的开始次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (试用版) </li> <li> **心跳：**<br/> (s：event：type= start)<br/> (s：资产：type= ad) </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告开始 </li> <li> **数据馈送：**<br/>videoadstart </li> <li> **上下文数据：**<br/> (试用版) </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.view) </li> </ul> |



### 广告结束

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> TRUE </li><li> **描述：**<br/>视频广告的完成次数。   </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.com摘录) </li> <li> **心跳：**<br/> (s：event：type= complete)<br/> (s：资产：type= ad)  </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告结束 </li> <li> **数据馈送：**<br/>videoadcomplete </li> <li> **上下文数据：**<br/> (a.media.ad.com摘录) </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.complete) </li> </ul> |



### 平均逗留时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK 密钥：**<br/>自动设置 </li> <li> **API 密钥：**<br/>不适用 </li> <li> **必需：**<br/>是 </li> <li> **类型：**<br/>字符串 </li> <li> **发送条件：**<br/>广告关闭 </li> <li> **最小 SDK 版本：**&#x200B;任何版本 </li> <li> **示例值：**<br/> 15 </li><li> **描述：**<br/>观看广告所花费的总时间(即，播放的秒数)。在 Analysis Workspace 和 Reports &amp; Analytics 中，该值将以时间格式 (HH:MM:SS) 显示。而在数据馈送、Data Warehouse 和报表 API 中，该值将以秒数显示。<br/>**发行日期：2018 年 9 月 13 日**  </li> </ul> | <ul> <li> **Adobe Analytics：**<br/> (a.media.ad.tiMested) </li> <li> **心率：**<br/> </li> </ul> | <ul> <li> **可用：**<br/>是 </li> <li> **保留的变量：**<br/>event </li> <li> **报表名称：**<br/>广告逗留时间 </li> <li> **数据馈送：**<br/>videoadtime </li> <li> **上下文数据：**<br/> (a.media.ad.tiMested) </li> <li> **Audience Manager：**<br/> (c_ contextData)。<br/>a.media.ad.timePlayed) </li> </ul> |



## Related APIs {#section_Related_APIs}

### CreateAdobeObject API：

* Android - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdObject-java.lang.String-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdObjectWithName:adId:position:length:)
* JavaScript - [createAdObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdObject)

### createAdbreject API：

* Android - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeat.html#createAdBreakObject-java.lang.String-java.lang.Long-java.lang.Double-)
* iOS - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeat.html#//api/name/createAdBreakObjectWithName:position:startTime:)
* JavaScript - [createAdBreakObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#-static-createAdBreakObject)

### MediaHeartBeatConfig API：

* Android - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/android/com/adobe/primetime/va/simple/MediaHeartbeatConfig.html)
* iOS - [ADBMediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/ios/Classes/ADBMediaHeartbeatConfig.html)
* JavaScript - [MediaHeartbeatConfig](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeatConfig.html#toc0)

