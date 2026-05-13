---
title: 有关心跳测量
description: 了解如何使用心跳收集视频量度。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 180dd9b1-877a-4ec1-8e81-c293800069c0
TQID: https://experienceleague.adobe.com/t6Y8Nj7WaEP76UOj8cCp40zSc3mHMfZuC9j5CifVIOg
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: b069d60e-95f3-44d6-95a8-ddc862a4bc38id: b3f03848-ae12-48b2-8aab-cad18567eb32id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7aid: eb9732ab-8232-4b21-bc4c-89de86dbe4d7id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2: id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fdid: e6c28e30-8689-4bf4-8fa8-561343d308a9id: e7d92df1-c5ba-4e93-85df-f83171b889beid: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c2be0313-b3ae-45e0-b454-d20bf54b23f2
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 316
ht-degree: 31%

---

# 有关心跳测量

Adobe流媒体服务使用“心率”收集视频量度。 在视频播放期间，心跳会发送到心跳跟踪服务器以测量播放时长。 每十秒发送一次心跳调用。 心跳会生成精细的视频参与量度，以及更准确的视频流失报表。 流媒体服务使用包含Media Analytics扩展的Adobe Launch、Media SDK和媒体收集API来测量心率。 `AppMeasurement` 和 `VisitorID` 组件用于接收视频数据。

在流媒体服务中使用心率具有以下优势：

| 功能 | 描述 |
|---|---|
| 媒体事件 | 对于主内容，每 10 秒发送一次详细事件和自定义事件；对于广告，则每 1 秒发送一次。 |
| 量度和维度 | 跨供应商的明确标准化量度、维度和基准。 借助跨所有平台的标准化解决方案，您可以跨所有媒体和平台使用一致的标准化变量，从而更有效地跨促销活动、设备和供应商进行比较。 |
| 集成 | Experience Cloud ID已链接到Adobe Experience Cloud，以便进行交叉分析。 通过自动Adobe Experience Cloud集成，您可以对媒体受众进行细分、定位这些受众，并根据用户偏好提供媒体推荐。 |
| 定价 | 透明的按媒体流跟踪（单个） |
| 实施和支持 | 通过不断更新和改进简化配置。 通过简化实施流程，您可以通过播放器API快速映射变量并使用Adobe Debug Tool验证实施，以确保准确跟踪所有必要变量。 |
| 合作伙伴共享 | 联合媒体和认证量度。 通过Federated Media共享数据，您可以利用我们业界领先的媒体共享功能，全面评估您的所有媒体分发合作伙伴（运营商、节目制作商和分发商）的数据。 |
| 高级跟踪 | 下载内容跟踪、错误恢复跟踪和并行查看者。 您可以跟踪在设备上下载和播放的流媒体内容，而不论该设备是否联网。 |
