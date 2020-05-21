---
title: 播放器状态参数
description: 本主题描述播放器状态跟踪参数。
uuid: 2a6b9247-a694-46e9-98e1-424c08c27ec2
translation-type: tm+mt
source-git-commit: 3c24b69265287084393be830193da14ae85cc5ba
workflow-type: tm+mt
source-wordcount: '2103'
ht-degree: 28%

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

“播放器状态跟踪”属性表按以下五个部分进行组织：

* 全屏幕
   * 受全屏影响的流
   * 全屏计数
   * 全屏总持续时间
* 关闭题注
   * 受隐藏字幕影响的流
   * 隐藏字幕计数
   * 隐藏式字幕总持续时间
* 静音
   * 静音影响的流
   * 静音计数
   * 静音总持续时间
* 画中画
   * 受画中画影响的流
   * 画中画计数
   * 画中画总持续时间
* 焦点
   * 受焦点影响的流
   * 焦点计数
   * 焦点内总持续时间

### 全屏属性

#### 受全屏影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受全屏影响的流数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.fullscreen.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受全屏影&#x200B;**<br/>响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.fullscreen.set)<br/> </li> <li> **数据源&#x200B;**<br/>videostatefullscreen</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.fullscreen.set)</li> </ul> |

#### 全屏计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明全屏显示的次数。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreencount)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>“全屏计数”</li> <li> **Context Data **<br/>(videostatefullscreencount)<br/> </li> <li> **数据源&#x200B;**<br/>videostatefullscreencount</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostatefullscreencount)</li> </ul> |



#### 全屏总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述全屏显示的时长。 This metric is set to 1 only if at least one Full Screen State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatefullscreentime)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>“全屏”持续时间</li> <li> **Context Data **<br/>(videostatefullscreentime)<br/> </li> <li> **Data Feed **<br/>videostatefullscreentime</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostatefullscreentime)</li> </ul> |


### 关闭题注属性

#### 受隐藏字幕影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受隐藏字幕影响的流数。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.closedcaptioning.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **隐藏字幕&#x200B;**<br/>影响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.closedcaptioning.set)<br/> </li> <li> **Data Feed **<br/>videostateclosed字幕</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.a.media.states.closedcaptioning.set)</li> </ul> |


#### 隐藏字幕计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明选择隐藏字幕的次数。 This metric is set to 1 only if at least one Closed Captioning State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningcount)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>关闭的字幕计数</li> <li> **上下文数据&#x200B;**<br/>(videostateclosedcaptioningcount)<br/> </li> <li> **数据源&#x200B;**<br/>videostateclosedcaptioningcount</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostateclosedcaptioncount)</li> </ul> |


#### 隐藏式字幕总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明选择隐藏字幕的时长。 This metric is set to 1 only if at least one Closed Caption State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateclosedcaptioningtime)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>“隐藏”字幕持续时间</li> <li> **Context Data **<br/>(videostateclosedcaptioningtime)<br/> </li> <li> **Data Feed **<br/>videostateclosedcaptioningtime</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostateclosedcaptiontime)</li> </ul> |


### 静音属性

#### 静音影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述静音影响的流数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.mute.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **静音影响&#x200B;**<br/>的报表名称流</li> <li> **上下文数据&#x200B;**<br/>(a.media.states.mute.set)<br/> </li> <li> **Data Feed **<br/>videostatementute</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.mute.set)</li> </ul> |

#### 静音计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明选择静音的次数。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateutecount)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>静音计数</li> <li> **上下文数据&#x200B;**<br/>(videostateutecount)<br/> </li> <li> **Data Feed **<br/>videostatecount</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostateutecount)</li> </ul> |

#### 静音总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **说&#x200B;**<br/>明选择静音的时长。 This metric is set to 1 only if at least one Mute State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatemettime)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报告名称&#x200B;**<br/>静音持续时间</li> <li> **Context Data **<br/>(videostateutetime)<br/> </li> <li> **Data Feed **<br/>videostatetime</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostatemettime)</li> </ul> |


### 画中画属性


#### 受画中画影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受画中画影响的流数。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.pictureinpicture.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受画中画&#x200B;**<br/>影响的报表名称流</li> <li> **Context Data **<br/>(a.media.states.pictureinpicture.set)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicture</li> <li> **受众管理&#x200B;**<br/>器(c_contextdata.a.media.states.pictureinpicture.set)</li> </ul> |


#### 画中画计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示画中画的次数。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturescount)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>“图片计数”</li> <li> **Context Data **<br/>(videostatepictureinpicturescount)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicturescount</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostatepictureinprecount)</li> </ul> |


#### 画中画总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示“画中画”的时间长度。 This metric is set to 1 only if at least one Picture in Picture State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostatepictureinpicturetime)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **报表名称&#x200B;**<br/>“画中画”持续时间</li> <li> **Context Data **<br/>(videostatepictureinpicturetime)<br/> </li> <li> **Data Feed **<br/>videostatepictureinpicturetime</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostatepictureinpicturetime)</li> </ul> |


### 焦点属性

#### 受焦点影响的流

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述受焦点影响的流数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(a.media.states.infocus.set)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **受焦点影响&#x200B;**<br/>的报表名称流</li> <li> **Context Data **<br/>(a.media.states.infocus.set)<br/> </li> <li> **Data Feed **<br/>videostateinfocus</li> <li> **受众管&#x200B;**<br/>理器(c_contextdata.a.media.states.infocus.set)</li> </ul> |


#### 焦点计数

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述焦点显示的次数。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocuscount)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **焦点计数中&#x200B;**<br/>的报表名称</li> <li> **上下文数据&#x200B;**<br/>(videostateinfocuscount)<br/> </li> <li> **数据源&#x200B;**<br/>videostateinfocuscount</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostateinfocuscount)</li> </ul> |


#### 焦点内总持续时间

|   实施   | 网络参数 | 报表 |
| --- | --- | --- |
| <ul> <li> **SDK密钥&#x200B;**<br/>自动设置</li> <li> **API密钥&#x200B;**<br/>N/A</li> <li> **必需&#x200B;**<br/>否</li> <li> **类型&#x200B;**<br/>编号</li> <li> **通过媒体关闭&#x200B;**<br/>发送</li> <li> **最低 SDK Version **<br/>3.0</li> <li> **示例值&#x200B;**<br/>TRUE</li><li> **描&#x200B;**<br/>述显示“聚焦”的时间长度。 This metric is set to 1 only if at least one In Focus State occurred during a playback session.<br/> **重要** ：如果设置了此事件，则唯一可能的值为TRUE。 如果不设置此事件，则不会发送任何值。   </li> </ul> | <ul> <li> **Adobe Analytics **<br/>(videostateinfocustime)<br/></li> <li> **心跳&#x200B;**<br/>N/A</li> </ul> | <ul> <li> **可用&#x200B;**<br/>：是</li> <li> **保留变量&#x200B;**<br/>事件</li> <li> **焦点持续时间&#x200B;**<br/>中的报表名称</li> <li> **上下文数据&#x200B;**<br/>(videostateinfocustime)<br/> </li> <li> **数据源&#x200B;**<br/>videostateinfocustime</li> <li> **受众管理器&#x200B;**<br/>(c_contextdata.videostateinfocustime)</li> </ul> |



## 相关 API {#related_apis_section}

需要： 向文档添加API链接：
* Android - [createStateObject](https://need)
* iOS - [createStateObjectWithName](https://need)
* Javascript - [createStateObject](https://need)
