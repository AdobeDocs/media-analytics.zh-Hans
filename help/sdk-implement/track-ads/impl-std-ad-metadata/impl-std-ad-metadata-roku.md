---
title: 在 Roku 中实施标准广告元数据
description: 如何在Roku上的广告跟踪中使用标准广告元数据。
uuid: 20a437d7-18b8-4099-ac81-9f3628384236
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 在 Roku 中实施标准广告元数据{#implement-standard-ad-metadata-on-roku}

## 实施标准和元数据

对于标准广告元数据，请使用适用于您的平台的键创建标准广告元数据键值对的字典：

```
standardAdMetadata = {} 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyCAMPAIGN_ID] = "sample campaign" 
standardAdMetadata[ADBMobile().MEDIA_AdMetadataKeyADVERTISER] = "sample advertiser" 

adInfo[ADBMobile().MEDIA_STANDARD_AD_METADATA] = standardAdMetadata 
```

