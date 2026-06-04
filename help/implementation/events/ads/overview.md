---
title: 跟踪广告
description: 有关使用 Media SDK 实施广告跟踪的概述。
uuid: 1607798b-c6ef-4d60-8e40-e958c345b09c
exl-id: c714d31f-3d08-4ded-a413-2762d53bec75
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/PguxKIzAL95WbMl5c0yJq9rYSqZgOGbbAYtxOI4eVOs
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: f1f1a2d4-0976-4881-b091-c2bb8de7ffac
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: 513
ht-degree: 3%

---


# 跟踪广告

广告播放跟踪涵盖广告时间、广告开始、广告结束和广告跳过。 使用媒体播放器的API来识别关键播放器事件并填充所需的广告变量。

## 播放器事件

| 播放器事件 | 操作 |
| --- | --- |
| 广告时间开始 | 创建广告时间对象；调用AdBreakStart |
| 广告开始 | 创建广告对象；调用AdStart |
| 广告结束 | 调用Adcomplete |
| 广告跳过 | 调用AdSkip |
| 广告时间结束 | 调用AdBreakComplete |

## 实施步骤

1. 识别广告时间（包括前置广告）边界开始的时间，并创建广告时间对象。 有关字段定义，请参阅[广告时间名称](/help/implementation/variables/ads/ad-break-name.md)和[广告时间开始时间](/help/implementation/variables/ads/ad-break-start-time.md)。
1. 调用[广告时间开始](/help/implementation/events/ads/ad-break-start.md)以开始跟踪广告时间。
1. 识别广告何时开始并创建广告对象。 有关字段定义，请参阅[广告名称](/help/implementation/variables/ads/ad-name.md)、[广告ID](/help/implementation/variables/ads/ad-id.md)、[广告长度](/help/implementation/variables/ads/ad-length.md)、[面板中的广告位置](/help/implementation/variables/ads/ad-in-pod-position.md)和[广告播放器名称](/help/implementation/variables/ads/ad-player-name.md)。
1. （可选）附加标准广告元数据。 有关可用密钥，请参阅[广告商](/help/implementation/variables/ads/advertiser.md)、[促销活动ID](/help/implementation/variables/ads/campaign-id.md)、[Creative ID](/help/implementation/variables/ads/creative-id.md)、[Creative URL](/help/implementation/variables/ads/creative-url.md)、[版面ID](/help/implementation/variables/ads/placement-id.md)和[网站ID](/help/implementation/variables/ads/site-id.md)。
1. 调用[广告开始](/help/implementation/events/ads/ad-start.md)以开始跟踪广告。
1. 当广告播放到完成时，调用[广告结束](/help/implementation/events/ads/ad-complete.md)。
1. 如果查看器跳过了广告，请调用[广告跳过](/help/implementation/events/ads/ad-skip.md)而不是广告结束。
1. 对于同一广告时间内的其他广告，请重复步骤3至7。
1. 当广告时间结束时，调用[广告时间结束](/help/implementation/events/ads/ad-break-complete.md)。

>[!IMPORTANT]
>
>**前置广告：请勿在`AdBreakStart`和`AdStart`之前调用`trackPlay`。** 主内容增量[内容开始](/help/reporting/metrics/content-starts.md)上的前`play` Ping。 如果在前置广告事件触发之前调用`trackPlay`，并且在广告期间查看器退出，则即使从未播放任何主内容，内容开始次数也会增加。 对于前置方案，延迟`trackPlay`，直到发送`AdBreakStart`和`AdStart`之后。

>[!NOTE]
>
>广告播放期间报告的播放头值表示查看器在&#x200B;**主内容**&#x200B;中的位置，而不是广告中的位置。 对于10分钟视频之前的前置广告，播放头在整个广告中为`0`。 对于以5分钟标记开始的中置广告，播放头在广告持续时间内保持在`300`（秒）。

## 常见问题

### 在广告之间意外的main:play调用

如果您看到在连续广告之间发生`main:play`调用，则AdComplete调用和下一个AdStart调用之间存在的间隔超过250毫秒。 出现此间隔时，Media SDK回退到发送主内容Ping，这可以对前置场景提前设置内容开始量度。

**原因：** Media SDK没有设置广告信息，并且播放器处于播放状态，因此它将间隙持续时间计入主内容。

**分辨率：**&#x200B;延迟每个广告的AdComplete调用（最后一个除外），而不是在广告结束时立即调用。 按如下方式批处理调用：

* 在每个&#x200B;**广告开始**&#x200B;时：如果以前的广告存在且尚未标记为完成，请为新广告调用AdComplete *before*。
* 在每个&#x200B;**广告资源结束**&#x200B;时：不要立即调用AdComplete — 延迟它。
* 在&#x200B;**广告时间结束**&#x200B;时：调用上一个广告的AdComplete （如果尚未调用），然后调用AdBreakComplete。

此模式可确保AdComplete和下一个AdStart能够连续触发，从而消除任何缺口。
