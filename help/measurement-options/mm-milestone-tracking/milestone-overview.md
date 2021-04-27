---
title: 里程碑概述
description: 里程碑概述
uuid: 2f9ec6bb-8860-4863-98bc-5cffb356ccc5
exl-id: 960785e3-f507-4f09-8f85-6eeca57dd2f3
translation-type: ht
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: ht
source-wordcount: '3346'
ht-degree: 100%

---

# 里程碑概述{#milestone-overview}

>[!CAUTION]
>
>此测量选项已被弃用。

[旧版里程碑文档](milestone_analytics_video.pdf)

## 配置 {#configuration}

### 里程碑视频配置

要跟踪视频，请指定一组“自定义转化变量”**(eVar) 和“自定义事件”**，以用于跟踪和报告。有一个“自定义分析”**&#x200B;变量 (`s.prop`) 也用于路径分析。

将您为每个量度选择的变量添加到视频配置页面。这样，系统就可以自动生成标准视频报告并设置其格式。*视频名称* eVar 和&#x200B;*视频查看次数*&#x200B;计数器都是必需的。其他变量是可选的，但建议使用这些变量来完成测量。启用视频跟踪后，您可以查看基于使用视频跟踪报告的视频数据生成的报表。

您还可以跟踪任意数量的其他视频量度。例如，如果您在站点上使用多个视频播放器，则可能会用播放器名称填充 eVar。您选择的某些变量也可能还会用于站点的其他区域。例如，如果在整个网站中使用&#x200B;*内容类型*&#x200B;变量，则让您可以测量来自视频的页面查看次数百分比，还可以将转化事件与视频相关联。

### 里程碑报表配置

要设置里程碑实施的视频报告，请转到&#x200B;**[!UICONTROL 管理员 > 报表包管理器]。**&#x200B;选择相应的报表包，然后选择&#x200B;**[!UICONTROL 视频管理 > 视频报告]：**

<!--
![](assets/0clip_image002_1537416456.png){width="248"}
-->

![](assets/rs1.png)

在第一个屏幕中，只有“视频核心”可以使用里程碑数据。选择&#x200B;**[!UICONTROL 视频核心]**，然后单击&#x200B;**[!UICONTROL 保存]。**

![](assets/video-core-check.png)

在下一个屏幕中，选择&#x200B;**[!UICONTROL 使用自定义变量]。**

<!--
![](assets/0clip_image006_-1561510960.png){width="470"}
-->

![](assets/rs2.png)

在最后一个屏幕中，选择要用于视频测量的两个 eVar 和三个事件：

<!--
![](assets/0clip_image008_-92166399.png)
-->

![](assets/rs3.png)

## 视频变量引用 {#video-variable-reference}

下表包含有关视频的商务变量和自定义事件的其他详细信息：

| 视频量度 | 变量类型 | 描述 |
| --- | --- | --- |
| 内容 | eVar <br/>默认过期：访问 | （必需）收集实施中指定的视频名称。 |
| 内容类型 | eVar <br/>默认过期：页面查看 | 收集由访客查看的内容类型相关数据。由视频测量发送的点击量会被分配 `video.` 内容类型。<br/>无需专门为视频跟踪保留此变量。通过使用此相同变量让其他内容报告内容类型，您可以分析访客在不同内容类型之间的分布。例如，您可以使用此变量通过 `article` 或 `product page` 之类的值标记其他内容类型。<br/>从视频测量的角度来看，“内容类型”**&#x200B;允许您识别视频访客，从而计算视频转化率。 |
| 内容逗留时间 | 事件 <br/>类型：计数器 | 以秒为单位，计算自上次数据收集流程（图像请求）以来，观看视频所花费的时间。 |
| 视频初始化 | 事件 <br/>类型：计数器 | 表明访客已查看了视频的某些部分。但是，它并不提供有关访客查看了视频中的多少内容或哪一部分的信息。 |
| 视频结束 | 事件 <br/>类型：计数器 | 表明用户已查看了完整的视频。默认情况下，完整的事件会在视频结束前 1 秒进行测量。<br/>在实施过程中，您可以指定希望在距离视频结束有多少秒时被视为查看完成。对于直播视频和其他没有定义结尾的流，您可以指定一个测量完成的自定义点。例如，在查看特定时间后。 |

## 媒体模块变量 {#media-module-variables}

以下变量允许您配置视频测量。您必须在“必需变量”表中定义变量的值。此外，要跟踪视频播放器中的事件，您必须启用 autoTrack（对于支持的播放器）或使用打开、播放、停止和关闭方法实施自定义播放器事件跟踪。

| 变量    | 描述 |
| --- | --- |
| `Media.trackUsingContextData` | **语法:** <br/><br/> `s.Media.trackUsingContextData = true;`<br/>此选项可启用集成的视频跟踪。如果设置为 true，则媒体模块会生成用于媒体跟踪的上下文数据，而不是旧版 `pev3`。<br/>可使用 `Media.contextDataMapping` 将上下文数据映射到选定的 eVar 和 event。<br/>默认值：`false` |
| `Media.contextDataMapping` | **语法:** <br/><br/> `s.Media.contextDataMapping = {`<br/>      `"a.media.name":"eVar2, prop2",` <br/>     `"a.media.segment":"eVar3",` <br/>     `"a.contentType":"eVar1",` <br/>     `"a.media.timePlayed":"event3",` <br/>     `"a.media.view":"event1",` <br/>     `"a.media.segmentView":"event2",` <br/>     `"a.media.complete":"event7",` <br/>     `"a.media.milestones":{` <br/>         `25:"event4",` <br/>         `50:"event5",` <br/>         `75:"event6"` <br/>     ` }` <br/> `};`<br/><br/>一个对象，可定义映射到要用于视频测量的 eVar 和 event 的变量。此对象必须映射以下字段：<br/><br/> **a.media.name：**（必需）在变量中填充视频名称。提供您选择用来存储视频名称的 eVar，以及要用于视频路径的“自定义分析视频”变量 (`s.prop`)。以逗号分隔列表的形式提供值。<br/><br/> **a.media.segment：**（可选）要用于存储媒体区段名称的 eVar。a.contentType：（可选）要用于存储视频值的 eVar，其中包含已启用的用于生成视频访问和访客报表的访问和访客跟踪。您选择的变量可能已用于存储文章幻灯片或产品页面之类的数据 <br/><br/> **a.media.view：**（必需）要用于计数媒体查看次数的事件。<br/><br/> **a.media.segmentView：**（可选）要用于计数区段查看次数的事件。<br/><br/> **a.media.complete：**（可选）要用于计数完整查看次数的事件。<br/><br/> **a.media.timePlayed：**（可选，但强烈推荐）要用于存储已播放视频秒数的数字事件。<br/><br/> **a.media.milestones：**（可选）一个对象，可将 s.Media.trackMilestones 里程碑映射到计数器事件。如果您定义里程碑，则应将 Media.segmentByMilestones 设置为 true。<br/><br/> **广告跟踪** 要跟踪广告，可使用以下上下文数据变量：<br/> **a.media.ad.name：**（必需）在变量中填充广告名称。提供您选择用来存储广告名称的 eVar，以及要用于路径的“自定义分析视频”变量 (`s.prop`)。以逗号分隔列表的形式提供值。<br/><br/> **a.media.ad.pod：**&#x200B;广告在主内容中播放的位置。<br/><br/> **a.media.ad.podPosition**：广告在面板中播放的位置。<br/><br/> **a.media.ad.CPM**：应用于此播放的 CPM 或加密 CPM（具有前缀“~”）。<br/><br/> **a.media.ad.view：**&#x200B;与 `a.media.view` 的工作方式相同<br/><br/> **a.media.ad.clicked：**&#x200B;计数广告的点击次数（`Media.click` 调用）<br/><br/> **a.media.ad.timePlayed：**&#x200B;与 `a.media.timePlayed` 的工作方式相同<br/><br/> **a.media.ad.complete：**&#x200B;与 `a.media.complete` 的工作方式相同 a.media.ad.segment：与 `a.media.segment` 的工作方式相同<br/><br/> **a.media.ad.segmentView：**&#x200B;与 `a.media.segmentView` 的工作方式相同<br/><br/> **a.media.ad.milestones：**&#x200B;与 `a.media.milestones` 的工作方式相同<br/><br/> **a.media.ad.offsetMilestones：**&#x200B;与 `a.media.offsetMilestones` 的工作方式相同 |
| `Media.trackVars` | **语法:** <br/><br/> `s.Media.trackVars =` <br/>    `"events,` `prop2,` `eVar1,` `eVar2,` `eVar3";` <br/><br/>在您的视频跟踪代码中设置的所有变量的逗号分隔列表。 |
| `Media.trackEvents` | **语法:** <br/><br/> `s.Media.trackEvents =` <br/>    `"event1,` `event2,` `event3,` `event4,` `event5,` `event6,` `event7"` <br/><br/>在您的视频跟踪代码中设置的所有事件的逗号分隔列表。 |

## 可选变量 {#optional-variables}

|  变量    | 描述 |
| --- | --- |
| `Media.autoTrack` | **语法:** <br/><br/> `s.Media.autoTrack = true`<br/><br/>为支持的播放器启用自动跟踪功能。支持的播放器包括： <ul> <li> Open Source Media Framework (OSMF) </li> <li> FLVPlayback（Flash Professional 中的导入视频向导创建的视频播放器） </li> <li> Silverlight </li> <li> MediaDisplay </li> <li> MediaPlayback </li> <li> Brightcove API 版本 2 和 3（请参阅 [Brightcove](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/media-overview.html)） </li> <li> 使用 JavaScript 的 Windows Media Player、Quicktime 或 Real Player </li> </ul> <br/><br/>如果您没有使用以上任何一款播放器，则可以使用 `Media.open`、`Media.play`、`Media.stop` 和 `Media.close` 来跟踪播放器事件。 |
| `Media.autoTrackNetStreams` | **语法:** <br/><br/> `s.Media.autoTrackNetStreams = true`<br/><br/>Flash 10.3 在 NetStream 组件中引入了新功能，以增强视频跟踪。如果您使用自定义 Flash NetStream 播放器，则可以启用此变量以实现类似于 autoTrack 的功能。此方法要求在 Flash 10.3 或更高版本中查看视频。 |
| `Media.completeByCloseOffset` | **语法:** <br/><br/> <br/><br/>`s.Media.completeByCloseOffset = true`<br/><br/>此设置允许您在视频实际结束前几秒计为一次完整的视频查看。<br/><br/>该事件基于 `completeCloseOffsetThreshold` 中指定的秒数发送。如果视频播放器从不报告等于视频长度的偏移，您便可以通过此方法测量结束。<br/><br/>默认情况下，此值设置为 true，阈值设置为 1 秒。使用这些默认设置，结束事件会在视频结束前 1 秒发送。 |
| `Media.completeCloseOffsetThreshold` | **语法:** <br/><br/> `s.Media.completeCloseOffsetThreshold = 1`<br/><br/>此阈值允许您在视频实际结束前几秒计为一次完整的视频查看。`Media.completeByCloseOffset` 必须设置为 true 才能使用此阈值。<br/><br/>您提供的整数值可决定在关闭时距离视频长度的偏移秒数，并且这仍将计为一次结束。如果视频播放器从不报告等于视频长度的偏移，您便可以通过此方法测量结束。<br/><br/>默认的阈值为 1 秒。 |
| `Media.playerName` | **语法:** <br/><br/> `s.Media.playerName = "Custom Player Name"`<br/><br/>指定一个自定义视频播放器名称。 |
| `Media.trackSeconds` | **语法:** <br/><br/> `s.Media.trackSeconds = 15`<br/><br/>定义在视频播放时将视频跟踪数据发送到 Adobe 数据收集服务器的间隔，以秒为单位。此值必须以 5 秒为增量进行设置。<br/><br/>启用 `Media.trackSeconds` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 Media.Monitor. |
| `Media.trackMilestones` | 跟踪里程碑，以视频长度的百分比表示。<br/><br/> **语法:** <br/><br/> `s.Media.trackMilestones = "25, 50, 75";`<br/><br/>定义将视频跟踪数据发送到 Adobe 数据收集服务器的间隔，以视频长度的百分比表示。以逗号分隔整数列表的形式指定里程碑。例如：10 = 10%，23 = 23%。<br/><br/>由于这些里程碑是视频中的固定时间点，因此如果访客查看超过了 10% 里程碑，然后快退并再次超过 10% 里程碑，则媒体模块会发送跟踪数据多次。同样，如果访客快进超过了某个里程碑，则媒体模块不会发送该里程碑的跟踪数据。<br/><br/>启用 `Media.trackMilestones` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 Media.Monitor. |
| `Media.trackOffsetMilestones` | 跟踪里程碑，以自视频开始后经过的秒数表示。<br/><br/> **语法:** <br/><br/> `s.Media.trackOffsetMilestones = "20, 40, 60";`<br/><br/>定义将视频跟踪数据发送到 Adobe 数据收集服务器的间隔，以自视频开始后经过的秒数表示。以逗号分隔整数列表的形式指定里程碑。例如：20 = 20 秒，40 = 40 秒。<br/><br/>由于这些里程碑是视频中的固定时间点，因此如果访客查看超过了 20 秒里程碑，然后快退并再次超过 20 秒里程碑，则媒体模块会发送跟踪数据多次。同样，如果访客快进超过了某个里程碑，则媒体模块不会发送该里程碑的跟踪数据。<br/><br/>启用 `Media.trackOffsetMilestones` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 Media.Monitor. |
| `Media.segmentByMilestones` | **语法:** <br/><br/> `s.Media.segmentByMilestones = true;` <br/><br/>根据媒体长度和在 `Media.trackMilestones` 中指定的里程碑，自动生成区段名称、区段编号和区段长度数据<br/><br/>如果使用 `autoTrack`，则按里程碑进行划分是定义区段的唯一方法。<br/><br/>默认值：`false` |
| `Media.segmentByOffsetMilestones` | **语法:** <br/><br/> `s.Media.segmentByOffsetMilestones = true;` <br/><br/>根据媒体长度和在 `Media.trackOffsetMilestones` 中指定的里程碑，自动生成区段名称、区段编号和区段长度数据<br/><br/>如果使用 `autoTrack`，则按里程碑进行划分是定义区段的唯一方法。<br/><br/>默认值：`false` |

## 广告跟踪变量 {#ad-tracking-variables}

这些变量用于结合 openAd 方法发送广告信息。请参阅 [VAST 视频广告跟踪。](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/media-overview.html)

| 变量    | 描述 |
| --- | --- |
| `Media.adTrackSeconds` | **语法:** <br/><br/> `s.Media.adTrackSeconds = 15;`<br/><br/>定义在视频播放时将视频广告跟踪数据发送到 Adobe 数据收集服务器的间隔，以秒为单位。此值必须以 5 秒为增量进行设置。<br/><br/>启用 `Media.adTrackSeconds` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 `Media.monitor`。 |
| `Media.adTrackMilestones` | 跟踪广告里程碑，以广告长度的百分比表示。<br/><br/> **语法:** <br/><br/> `s.Media.adTrackMilestones = "25, 50, 75";`<br/><br/>定义将广告跟踪数据发送到 Adobe 数据收集服务器的间隔，以广告长度的百分比表示。以逗号分隔整数列表的形式指定里程碑。例如：10 = 10%，23 = 23%。<br/><br/>由于这些里程碑是广告中的固定时间点，因此如果访客查看超过了 10% 里程碑，然后快退并再次超过 10% 里程碑，则媒体模块会发送跟踪数据多次。同样，如果访客快进超过了某个里程碑，则媒体模块不会发送该里程碑的跟踪数据。<br/><br/>启用 `Media.adTrackMilestones` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 `Media.monitor`。 |
| `Media.adTrackOffsetMilestones` | 跟踪广告里程碑，以自广告开始后经过的秒数表示。<br/><br/> **语法:** <br/><br/> `s.Media.adTrackOffsetMilestones = "20, 40, 60";`<br/><br/>定义将广告跟踪数据发送到 Adobe 数据收集服务器的间隔，以自广告开始后经过的秒数表示。以逗号分隔整数列表的形式指定里程碑。例如：20 = 20 秒，40 = 40 秒。<br/><br/>由于这些里程碑是广告中的固定时间点，因此如果访客查看超过了 20 秒里程碑，然后快退并再次超过 20 秒里程碑，则媒体模块会发送跟踪数据多次。同样，如果访客快进超过了某个里程碑，则媒体模块不会发送该里程碑的跟踪数据。<br/><br/>启用 `Media.adTrackOffsetMilestones` 只会触发在 `Media.contextDataMapping` 中定义的事件。要发送为视频测量指定的变量以外的其他变量，您必须使用 `Media.monitor`。 |
| `Media.adSegmentByMilestones` | **语法:** <br/><br/> `s.Media.adSegmentByMilestones = true;` <br/><br/>根据媒体长度和在 `Media.adTrackMilestones` 中指定的里程碑，自动生成区段名称、区段编号和区段长度数据<br/><br/>如果使用 `autoTrack`，则按里程碑进行划分是定义区段的唯一方法。<br/><br/>默认值：`false` |
| `Media.adSegmentByOffsetMilestones` | **语法:** <br/><br/> `s.Media.adSegmentByOffsetMilestones = true;` <br/><br/>根据媒体长度和在 `Media.adTrackOffsetMilestones` 中指定的里程碑，自动生成区段名称、区段编号和区段长度数据<br/><br/>如果使用 `autoTrack`，则按里程碑进行划分是定义区段的唯一方法。<br/><br/>默认值：`false` |

## 媒体模块方法 {#media-module-methods}

媒体模块方法用于手动跟踪播放器事件，以及跟踪未包含在标准视频报表中的其他量度。

如果您使用 `Media.autoTrack`，并且没有跟踪其他量度，则无需直接调用下面的任何方法。除非指定为可选，否则所有参数都是必需的。

| 方法    | 描述 |
| --- | --- |
| `Media.open` | **语法:** <br/><br/> `s.Media.open(mediaName, mediaLength, mediaPlayerName)`<br/><br/>准备好媒体模块以收集视频跟踪数据。此方法采用以下参数： <ul><li> **mediaName：**（必需）您希望在视频报表中显示的视频名称。 </li><li>  **mediaLength：**（必需）视频的长度，以秒为单位。  </li><li> **mediaPlayerName：**（必需）您希望在视频报表中显示的用来查看视频的媒体播放器名称。 </li></ul> |
| `Media.openAd` | **语法:** <br/><br/> `s.Media.openAd(name, length, playerName, parentName,`<br/>`parentPod, parentPodPosition, CPM)`   <br/><br/> 准备好媒体模块以收集广告跟踪数据。此方法采用以下参数： <ul> <li> **name：**（必需）广告的名称或 ID。  </li> <li> **length：**（必需）广告的长度。  </li> <li> **playerName：**（必需）用来查看广告的媒体播放器名称。  </li> <li> **parentName：**&#x200B;广告被嵌入到的主内容的名称或 ID。  </li> <li> **parentPod：**&#x200B;广告在主内容中播放的位置。  </li> <li> **parentPodPosition：**&#x200B;广告在面板中播放的位置。  </li> <li> **CPM：**&#x200B;应用于此播放的 CPM 或加密 CPM（具有前缀“~”）。  </li> </ul> |
| `Media.click` | **语法:** <br/><br/> `s.Media.click(name, offset)`<br/><br/>跟踪广告何时在视频中被点击。此方法采用以下参数： <ul> <li> **name：**&#x200B;广告的名称。此名称必须匹配 Media.openAd 中使用的名称。  </li> <li> **offset：**&#x200B;发生单击时广告的偏移量。  </li> </ul> |
| `Media.close` | **语法:** <br/><br/> `s.Media.close(mediaName)`<br/><br/>结束视频数据收集并向 Adobe 数据收集服务器发送信息。在视频的结尾调用此方法。此方法采用以下参数：<br/><br/> **mediaName：**&#x200B;视频的名称。此名称必须匹配 `Media.open` 中使用的名称。 |
| `Media.complete` | **语法:** <br/><br/> `s.Media.complete(name, offset)`<br/><br/>此方法可手动跟踪结束事件。如果您在触发事件时需要使用的特殊逻辑无法使用 `Media.completeByCloseOffset` 进行处理，则可以使用此方法。<br/><br/>例如，如果您测量的实时流未定义结尾，您可能会在用户查看实时流长达 X 秒后触发一次结束。您可以使用基于内容长度和类型的百分比计算来测量完成情况。此方法采用以下参数： <ul> <li> **mediaName：**&#x200B;视频的名称。此名称必须匹配 Media.open 中使用的名称。  </li> <li> **mediaOffset：**&#x200B;应发送完整事件时视频的秒数。从零秒开始，指定基于视频的偏移。<br/><br/>如果您的媒体播放器使用毫秒跟踪，请确保将此值转化为调用 Media.complete 之前的秒数。  </li> </ul> 如果您计划手动调用 complete，请设置 <br/><br/> `s.Media.completeByCloseOffset = false`。 |
| `Media.play` | **语法:** <br/><br/> `s.Media.play(name, offset, segmentNum, segment, segmentLength)`<br/><br/>无论视频何时开始播放，都调用此方法。在使用手动视频测量时，您可以在发送视频测量数据时提供当前区段数据。<br/><br/>无论出于什么原因，如果您的播放器从一个区段更改为另一个区段，则应该调用 `Media.stop` 和 `Media.play`。<br/><br/>此方法采用以下参数：<br/><br/> **mediaName：**&#x200B;视频的名称。此名称必须匹配 Media.open 中使用的名称。<br/><br/> **mediaOffset:**&#x200B;开始播放的视频中的秒数。从零秒开始，指定基于视频的偏移。如果您的媒体播放器使用毫秒跟踪，请确保将此值转化为调用 Media.play 之前的秒数。<br/><br/> **segmentNum：**（可选）当前区段编号，市场营销报告使用它对报表中显示的区段进行排序。segmentNum 参数必须大于零。<br/><br/> **segment：**（可选）当前区段名称。<br/><br/> **segmentLength：**（可选）<br/><br/>当前区段长度，以秒为单位。<br/><br/>例如：<br/><br/> `s.Media.play("My Video", 1800, 2,"Second Quarter", 1800)` <br/><br/> `s.Media.play("My Video", 0, 1,"Preroll", 30)` |
| `Media.stop` | **语法:** <br/><br/> `s.Media.stop(mediaName, mediaOffset)`<br/><br/>跟踪指定视频的停止事件（停止、暂停等）。此方法采用以下参数： <ul> <li> **mediaName：**&#x200B;视频的名称。此名称必须匹配 `Media.open` 中使用的名称。  </li> <li> **mediaOffset：**&#x200B;停止或暂停事件在视频中发生的秒数。从零秒开始，指定基于视频的偏移。  </li> </ul> |
| `Media.monitor` | **语法:** <br/><br/> `s.Media.monitor(s, media)` <br/><br/> **Silverlight 语法：**<br/><br/> `s.Media.monitor =` <br/>   `new AppMeasurement_Media_Monitor(myMediaMonitor);` <br/><br/>Silverlight 应用程序媒体监视器可实施 Objective-C 代理设计模式。`myMediaMonitor` 类方法采用 `s` 和 `media` 参数。<br/><br/>使用此方法可发送其他视频量度。您可以设置其他变量（prop、eVar、event），并基于所播放视频的当前状态使用 `Media.track` 发送它们。<br/><br/>请参阅[使用 Media.monitor 测量其他量度。](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/media-overview.html)<br/><br/>此方法采用以下参数：<br/><br/>  **s：**`AppMeasurement` 实例（或 JavaScript `s` 对象）。<br/><br/> **media：**&#x200B;包含提供视频状态的成员的对象。这些成员包括：  <ul><li> `media.name:` 视频的名称。此名称必须匹配 `Media.open` 中使用的名称； </li><li> `media.length:` 在对 `Media.open` 的调用中给定的视频长度，以秒为单位； </li><li> `media.playerName:` 在对 `Media.open` 的调用中给定的媒体播放器名称； </li><li> `media.openTime:` 一个 NSDate 对象，其中包含有关何时调用了 `Media.open` 的数据； </li><li> `media.offset:` 视频中的当前偏移，以秒为单位（视频中的实际时间点）。偏移从零开始（视频的第一秒为零秒）； </li><li> `media.percent:` 已播放视频的当前百分比，基于视频长度和当前偏移；  </li><li> `media.timePlayed:` 截至目前播放的总秒数；  </li><li> `media.eventFirstTime:` 指明这是否是第一次为该视频调用此媒体事件； </li><li> `media.mediaEvent:` 一个字符串，其中包含可导致监视器调用的事件名称。 </li></ul> |
|  | `media.mediaEvent` 事件： <ul><li> `OPEN:` 通过 `Media.autoTrack` 首次观察到播放，或者调用 `Media.play` 时； </li><li> `CLOSE:` 通过 `Media.autoTrack` 观察到播放在视频完成时结束，或者调用 `Media.close` 时；</li><li> `PLAY:` 通过 `Media.autoTrack` 观察到播放在暂停或推移后恢复，或者第二次调用 `Media.play` 时；</li><li> `STOP:` 通过 `Media.autoTrack` 观察到播放由于暂停或开始推移而停止，或者调用 `Media.stop` 时；</li><li> `MONITOR:` 我们的自动监视检查正在播放的视频的状态（每秒检查一次）；</li><li> `SECONDS:` 处于由 `Media.trackSeconds` 变量定义的秒数间隔时；</li><li> `MILESTONE:` 处于由 `Media.trackMilestones` 变量定义的里程碑时； </li></ul> |
| `Media.track` | **语法:** <br/><br/> `s.Media.track(mediaName)`<br/><br/>立即发送当前视频状态，以及您定义的任何 `Media.trackVars` 和 Media.trackEvents。此方法在 `Media.monitor` 内使用。<br/><br/>请参阅[使用 Media.monitor 测量其他量度。](https://docs.adobe.com/content/help/zh-Hans/media-analytics/using/media-overview.html)<br/><br/>在调用此方法之前，应对视频调用 `Media.open` 和 `Media.play`。此方法采用以下参数： <ul> <li> **mediaName：**&#x200B;视频的名称。此名称必须匹配 `Media.open` 中使用的名称。</li> </ul> 此方法是在播放视频时发送其他变量的唯一方法。它将秒数间隔和百分比里程碑计数器重置为零以防止多次跟踪点击。 |


## 跟踪视频播放器事件 {#track-video-player-events}

您可以通过创建附加到视频播放器事件处理程序的函数来跟踪媒体播放器。这让您能够在适当的时间调用 `Media.open`、`Media.play`、`Media.stop` 和 `Media.close`。例如：

* **加载：**&#x200B;调用 `Media.open` 和 `Media.play`
* **暂停：**&#x200B;调用 `Media.stop`。例如，如果用户在 15 秒后暂停视频，则会调用 `s.Media.stop("Video1", 15)`
* **缓冲：**&#x200B;视频缓冲时调用 `Media.stop`。恢复播放时调用 `Media.play`。
* **恢复：**&#x200B;调用 `Media.play`。例如，当用户恢复最初播放了 15 秒的视频时，则会调用 `s.Media.play("Video1", 15)`。
* **推移（滑块）：**&#x200B;用户拖动视频滑块时，调用 `Media.stop`。用户释放视频滑块时，调用 `Media.play`。
* **结束：**&#x200B;调用 `Media.stop`，然后调用 `Media.close`。例如，在 100 秒视频结束时，调用 `s.Media.stop("Video1", 100)`，然后调用 `s.Media.close("Video1")`。

要完成此过程，您可以定义四个自定义函数，以从媒体播放器事件处理程序调用。传递到 `Media.open`、`Media.play`、`Media.stop` 和 `Media.close` 的各种参数均来自播放器。以下伪代码显示此过程：

```javascript
/* Call on video load */ 
function startMovie() { 
    s.Media.open(mediaName, mediaLength, mediaPlayerName); 
    playMovie(); 
} 
 
/* Call on video resume from pause and slider release */ 
function playMovie() { 
    s.Media.play(mediaName, 
                 mediaOffset,  
                 segmentNum,  
                 segment,  
                 segmentLength); 
} 
/* Call on video pause and slider grab */ 
function stopMovie() { 
    s.Media.stop(mediaName, mediaOffset); 
} 
 
/* Call on video end */ 
/* Measuring Video for Developers 43 */ 
function endMovie() { 
    stopMovie(); 
    s.Media.close(mediaName); 
} 
```

## JavaScript autotrack {#javascript-autotrack}

JavaScript 媒体模块可识别页面 HTML 中的所有 `<embed>` 或 `<object>` 标记。然后，它会搜索每个标记中的数据，以确定使用的是哪种媒体播放器（如果有）。如果播放器是 Windows Media Player、Quicktime 或 Real Player，则可以使用 `autoTrack`，不过适用于 Windows Media Player 的 `autoTrack` 只能在 Internet Explorer 中使用。要支持其他所有浏览器，需要手动跟踪 Windows Media Player。

您必须在要跟踪的对象中设置 `classid` 属性。需要 `classid` 才能公开媒体模块使用的事件处理程序，从而自动跟踪视频。

```javascript
s.Media.autoTrack = true
```

## JavaScript 代码示例 {#javascript-sample-code}

```javascript
// Sample implementation 
s.usePlugins=true 
function s_doPlugins(s) { 
    /* Add manual calls to modules and plugins here */ 
} 
 
s.doPlugins=s_doPlugins 
 
/*********Media Module Calls**************/ 
s.loadModule("Media") 
 
/*Configure Media Module Functions */ 
s.Media.autoTrack= true; 
s.Media.trackVars="events, prop2, eVar1, eVar2, eVar3"; 
s.Media.trackEvents="event1, event2, event3, event4, event5, event6, event7" 
s.Media.trackMilestones="25, 50, 75"; 
s.Media.playerName="My Media Player"; 
s.Media.segmentByMilestones = true; 
s.Media.trackUsingContextData = true; 
s.Media.contextDataMapping = { 
    "a.media.name":"eVar2, prop2", 
    "a.media.segment":"eVar3", 
    "a.contentType":"eVar1", 
    "a.media.timePlayed":"event3", 
    "a.media.view":"event1", 
    "a.media.segmentView":"event2", 
    "a.media.complete":"event7", 
    "a.media.milestones":{ 
        25:"event4", 
        50:"event5", 
        75:"event6" 
    } 
} 
 
s.Media.monitor = function (s, media) { } //If Needed

/* Turn on and configure debugging here */ 
s.debugTracking = true; 
s.trackLocal = true; 
 
/* WARNING: Changing any of the below variables will cause drastic changes to how your visitor 
data is collected. Changes should only be made when instructed to do so by your account 
manager.*/ 
s.visitorNamespace = "yourNamespace"; 
s.trackingServer="metrics.mysite.com" //Use only if using first party cookies 
s.trackingServerSecure="smetrics.mysite.com" // Use only if using first party cookies in  
                                             // conjunction with SSL 
s.dc = '122'; 
 
/************************** PLUGINS SECTION *************************/ 
/* Insert any plugins code you want to use here. */ 
 
/****************************** MODULES *****************************/ 
/* Insert the media module tracking code here. */ 
```
