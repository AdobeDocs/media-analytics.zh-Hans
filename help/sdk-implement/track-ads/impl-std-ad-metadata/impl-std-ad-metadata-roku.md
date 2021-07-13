---
title: 了解如何在Roku中实施标准广告元数据
description: 如何在 Roku 上的广告跟踪中使用标准广告元数据。
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
exl-id: d2c0a1e0-8d40-4f60-a82d-5860550ac152
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '52'
ht-degree: 82%

---

# 在 Roku 中实施标准广告元数据{#implement-standard-ad-metadata-on-roku}

## 实施标准广告元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```
