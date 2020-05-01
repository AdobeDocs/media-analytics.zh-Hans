---
title: 在 Adobe Analytics 中测量音频和视频
description: Adobe Analytics for Media（也称为 Media Analytics）可为客户提供针对内容、音频和广告的可靠媒体测量。
uuid: b3cbe240-b94d-42b8-a99c-0280334aaa14
translation-type: tm+mt
source-git-commit: bddcbcd844145788518c60399bee9e4744e42d3a

---


# 在 Adobe Analytics 中测量音频和视频{#measuring-audio-and-video-in-adobe-analytics}

![横幅](./assets/media_analytics_banner.png)

## 关于Adobe Analytics for Audio和Video

Adobe Analytics for Audio and Video是Adobe Analytics的一个附加组件，它为音频、视频和广告提供强大的测量工具。 Adobe Analytics是Adobe Experience Platform的一部分。

Adobe Analytics for Audio和Video使您能够跟踪整个网站的客户旅程。 这些指标可轻松集成到Adobe Analytics Reports和其他Adobe Experience Cloud产品中。 媒体测量允许您将数据分为多个维度和细分，捕获完成完整、详细分析所需的所有元数据。 然后，您可以分析数据并将成功标准归因于完全消费的媒体、平均花费时间和已完成的广告。

您可以衡量与QoS相关的重要投放指标，如丢帧、缓冲时间和平均比特率。 这些指标可以与您的网站或应用程序数据相结合，以可视化客户路径和兴趣——借助Adobe Experience Cloud提供增强的推荐和个性化客户体验。

## 功能 {#features}

Adobe Analytics的音频和视频优势包括实时监控、详细分析、切实可行的洞察和盈利机会。
* **实时分析**-跨多个渠道利用持续时间、ex2和ex3等关键绩效指标，做出实时、可操作的决策。 以 10 秒为间隔，测量主内容事件，可及时捕获发生的所有活动。广告跟踪事件的发生间隔为 1 秒。
* **推动参与**-通过减少缓冲事件，了解广告在内容中的播放位置和时间，提供顺畅、不太打扰的体验，实现用户的完全参与。
* **整体图**-将多个数据点整合到所有内容分发商，全面视图所有媒体活动。 通过Federated Analytics功能衡量所有可能渠道的参与度和视图/倾听。
* **增加的粒度**-评估最精细级别的查看行为，包括每天的单个访客时间、按分钟分钟的并发查看器／监听器以及内容消耗的平均持续时间。
* **精确衡量**-跨多种媒体消费设备进行衡量，包括OTT、智能手机、平板电脑、台式机等，以监控用户参与模式和习惯。
* **细分**-将分类应用于您的播放器、设备、类型、章节，并通过内容、音频、广告和组合显示每个分类对您的整体视图/监听和客户参与度有何影响。

## 心跳测量 {#heartbeat}

Adobe Analytics使用“心跳”收集视频指标。 在视频播放期间，心跳会发送到心跳跟踪服务器以测量所播放的时间。 心跳呼叫每十秒发送一次。 心跳会产生精细的视频参与度指标和更准确的视频流失报告。 Adobe Analytics for Audio和Video使用Adobe Launch和Media Analytics扩展、Media SDK和Media Collection API测量心跳。 该 `AppMeasurement` 和 `VisitorID` 组件用于接收视频数据。

使用Adobe Analytics的音频和视频心跳功能可提供以下优势：

| 功能 | 描述 |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 媒体事件 | 详细和自定义事件每10秒发送一次，用于主要内容，每1秒发送一次，用于广告 |
| 量度和维度 | 明确的标准化指标、维度和跨供应商的<br>基准通过跨所有平台的标准化解决方案，您可以跨所有媒体和平台使用一致的标准化变量，从而实现更有效的跨活动、设备和供应商比较。 |
| 集成 | Experience Cloud ID已链接到Adobe Experience Cloud，可更轻松地进行交叉<br>分析借助Adobe Experience Cloud自动集成，您可以对媒体受众进行细分、目标，并根据用户偏好提出媒体推荐。 |
| 定价 | 按媒体流（单个）进行透明的跟踪 |
| 实施与支持 | 通过不断更新和改进简化<br>的配置通过简化的实施流程，您可以通过播放器API快速映射变量并使用Adobe Debug Tool验证实施，以确保准确跟踪所有必要变量。 |
| 合作伙伴共享 | Federated Analytics and Certified Metrics<br>With shared data through Federated Analytics, you can capitalize on our industry-first media sharing capabilities, to evaluate data holistically across all of your media distribution partners—operators, programmers, and distributors. |
| 高级跟踪 | 下载的内容跟踪、错误恢复跟踪和<br>并发查看器您可以跟踪在设备上下载和播放的音频和视频内容，无论其连接性如何。 |



## 安全性 {#security}

在Adobe，我们非常重视您数字资产的安全性。 从我们将安全性严格集成到内部软件开发过程和工具，到跨职能事件响应团队，我们努力做到主动、灵活。 此外，我们与合作伙伴、研究人员和其他行业组织的协作有助于我们了解最新的威胁和安全最佳实践，并不断将安全性构建到我们优惠的产品和服务中。


### 传输层安全性 {#transport-layer-security}

**TLS 声明 --** Adobe 制定了要求终止使用旧版安全协议的安全合规标准。为了继续满足不断演变的安全协议标准，Adobe 正逐渐转为使用 TLS 1.2，以便使用最新的安全协议版本。从 2019 年 2 月 20 日起，Adobe 将仅支持 TLS 1.1 或更高版本。伴随这项变化，对于使用部署了 TLS 1.0 的较旧设备或 Web 浏览器的最终用户，Adobe 将不再收集他们的数据。迁移到 TLS 1.2 可提高安全性。您应务必了解具体细节，并且针对更改做出规划以实现顺利迁移。

>[!NOTE]
>
>TLS 是目前最广泛部署的安全协议，适用于 Web 浏览器和其他需要通过网络安全交换数据的应用程序。
