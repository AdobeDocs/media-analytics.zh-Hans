---
title: 播放器状态参数
description: 本主题描述播放器状态跟踪参数。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 1b48565bcc5c9a87e5fabbc906049ab791bf89cc
workflow-type: tm+mt
source-wordcount: '2236'
ht-degree: 26%

---


# 播放器状态参数{#player-state-parameters}

本主题提供一列表播放器状态数据，Adobe通过解决方案变量收集这些数据。

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
>请勿更改下面列出的在“报表/保留的变量”下描述为“分类”的任何变量的分类名称。\
>在启用报表包进行媒体跟踪后，将定义媒体分类。Adobe 会不时添加新属性，如果添加了新属性，客户必须重新启用其报表包才能访问新的媒体属性。在更新过程中，Adobe 会通过检查变量名称来确定是否启用了分类。如果任何变量名称缺失，Adobe 会再次添加缺失的变量名称。

## 播放器状态属性 {#player-state-properties}

播放器状态跟踪功能可以附加到音频或视频流。 标准化的播放器状态跟踪指标作为解决方案变量进行存储。 标准状态为： 全屏、静音、closeCaption、pictureInPicture和inFocus。

### 全屏属性

#### 受全屏影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受全屏影响的流数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受全屏影&#x200B;**<br/>响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### 全屏计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明全屏显示的次数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置了此事件，则计数等于视频处于“全屏”状态的次数。 如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.count)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>“全屏计数”</li> <li> **Context Data **<br/>(media.states.fullscreen.count)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.count</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.fullscreen.count)</li> </ul> |



#### 全屏总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述全屏显示的时长。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置此事件，则时间等于视频处于“全屏”状态的时间。 如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.fullscreen.time)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>“全屏”总持续时间</li> <li> **Context Data **<br/>(media.states.fullscreen.time)<br/> </li> <li> **Data Feed **<br/>media.states.fullscreen.time</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.fullscreen.time)</li> </ul> |


### 关闭题注属性

#### 受隐藏字幕影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受隐藏字幕影响的流数。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **隐藏字幕&#x200B;**<br/>影响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **Data Feed **<br/>media.states.closed字幕</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### 隐藏字幕计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明隐藏字幕的显示次数。 This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置了此事件，则计数等于视频处于“关闭字幕”状态的次数。 如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(C19)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>关闭的字幕计数</li> <li> **Context Data **<br/>(media.states.closedcaptioning.count)<br/> </li> <li> **Data Feed **<br/>media.states.closedcaptioning.count</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.closedcaptioning.count)</li> </ul> |


#### 隐藏字幕总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明显示隐藏式字幕的时长。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置此事件，则时间等于视频处于“关闭字幕”状态的时间。 如果未设置此事件，则不发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.closedcaptioning.time)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>关闭的字幕总持续时间</li> <li> **Context Data **<br/>(media.states.closedcaptioning.time)<br/> </li> <li> **Data Feed **<br/>media.states.closedcaptioning.time</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.closedcaptioning.time)</li> </ul> |


### 静音属性

#### 受静音影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述静音影响的流数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **静音影响&#x200B;**<br/>的报表名称流</li> <li> **上下文数据&#x200B;**<br/>(a.media.states.mute.set)<br/> </li> <li> **Data Feed **<br/>media.states.mute</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### 静音计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述静音显示的次数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置了此事件，则计数等于视频处于静音状态的次数。 如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.count)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>静音计数</li> <li> **上下文数&#x200B;**<br/>据(media.states.mute.count)<br/> </li> <li> **数据源&#x200B;**<br/>media.states.mute.count</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.mute.count)</li> </ul> |

#### 静音总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明显示静音的时长。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置此事件，则时间等于视频处于静音状态的时间。 如果未设置此事件，则不发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.mute.time)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>静音总持续时间</li> <li> **上下文数据&#x200B;**<br/>(media.states.mute.time)<br/> </li> <li> **Data Feed **<br/>media.states.mute.time</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.mute.time)</li> </ul> |


### 画中画属性


#### 受画中画影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受画中画影响的流数。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受画中画&#x200B;**<br/>影响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### 画中画计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示画中画的次数。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则计数等于视频处于“画中画”状态的次数。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.count)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>“图片计数”</li> <li> **Context Data **<br/>(media.states.pictureinpicture.count)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture.count</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.pictureinpicture.count)</li> </ul> |


#### 画中画总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示“画中画”的时间长度。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则时间等于视频处于“画中画”状态的时间。 如果未设置此事件，则不发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.pictureinpicture.time)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>“画中画”总持续时间</li> <li> **Context Data **<br/>(media.states.pictureinpicture.time)<br/> </li> <li> **Data Feed **<br/>media.states.pictureinpicture.time</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.pictureinpicture.time)</li> </ul> |


### 焦点属性

#### 受聚焦影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受焦点影响的流数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受焦点影响&#x200B;**<br/>的报表名称流</li> <li> **Context Data **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Data Feed **<br/>media.states.infocus</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### 聚焦计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述焦点显示的次数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要&#x200B;**<br/>：如果设置此事件，则计数等于视频处于“焦点”状态的次数。 如果不设置此事件，则不会发送任何值。</li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.count)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **焦点计数中&#x200B;**<br/>的报表名称</li> <li> **Context Data **<br/>(media.states.infocus.count)<br/> </li> <li> **Data Feed **<br/>media.states.infocus.count</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.infocus.count)</li> </ul> |


#### 聚焦总时长

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示“聚焦”的时间长度。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要**<br/> ：如果设置此事件，则时间等于视频处于“聚焦”状态的时间。 如果未设置此事件，则不发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(media.states.infocus.time)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **焦点中的报&#x200B;**<br/>告名称总持续时间</li> <li> **Context Data **<br/>(media.states.infocus.time)<br/> </li> <li> **Data Feed **<br/>media.states.infocus.time</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.media.states.infocus.time)</li> </ul> |

## XDM标识的属性列表

Analytics中存储的数据可用于任何目的，并且播放器状态指标可以使用XDM导入Adobe Experience Platform，并与客户旅程分析结合使用。

| 播放器状态属性 | 映射 |
|---------------------------------------|------------------------------------|
| a.media.states.fullScreen.set | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateSet |
| a.media.states.fullScreen.count | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateCount |
| a.media.states.fullScreen.time | media.mediaTimed.primaryAssetViewDetails.fullScreen.playerStateTime |
| a.media.states.mute.set | media.mediaTimed.primaryAssetViewDetails.mute.playerStateSet |
| a.media.states.mute.count | media.mediaTimed.primaryAssetViewDetails.mute.playerStateCount |
| a.media.states.mute.time | media.mediaTimed.primaryAssetViewDetails.mute.playerStateTime |
| a.media.states.closeCaption.set | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateSet |
| a.media.states.closeCaption.count | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateCount |
| a.media.states.closeCaption.time | media.mediaTimed.primaryAssetViewDetails.closeCaption.playerStateTime |
| a.media.states.pictureInPicture.set | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateSet |
| a.media.states.pictureInPicture.count | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateCount |
| a.media.states.pictureInPicture.time | media.mediaTimed.primaryAssetViewDetails.pictureInPicture.playerStateTime |
| a.media.states.inFocus.set | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateSet |
| a.media.states.inFocus.count | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateCount |
| a.media.states.inFocus.time | media.mediaTimed.primaryAssetViewDetails.inFocus.playerStateTime |

## 相关 API {#related_apis_section}

* Android - [createStateObject](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* iOS - [createStateObjectWithName](https://aep-sdks.gitbook.io/docs/using-mobile-extensions/adobe-media-analytics/media-api-reference#createstateobject)
* Javascript - [createStateObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript_3x/APIReference.html)
