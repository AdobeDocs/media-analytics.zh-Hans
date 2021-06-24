---
title: “选择禁用和隐私说明”
description: “了解如何处理选择启用、选择禁用和隐私。”
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 93%

---

# 选择禁用和隐私{#opt-out-and-privacy}

## 选择禁用/选择启用 {#opt-out-opt-in}

您可以控制是否允许在特定设备上进行跟踪活动。

* **移动设备应用程序 -** VA 库遵循 `AdobeMobile` 库的隐私和选择禁用设置。要选择禁用跟踪，您需要使用 `AdobeMobile` 库。有关 `AdobeMobile` 库的选择禁用和隐私设置的更多信息，请参阅[选择禁用和隐私设置](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html)。
* **JavaScript/浏览器应用程序 -** VA 库遵循 `VisitorAPI` 隐私和选择禁用设置。要选择禁用跟踪，您需要在访客 API 服务中选择禁用。有关选择禁用和隐私的更多信息，请参阅 [Adobe Experience Platform Identity Service](https://experienceleague.adobe.com/docs/id-service/using/home.html)。
* **OTT 应用程序（Chromecast、Roku）-** OTT SDK 提供了通用数据保护条例 (GDPR) 就绪 API，允许您为数据收集和传输设置 `opt` 状态标记，并检索本地存储的身份。

   >[!NOTE]
   >
   >如果将隐私状态设置为选择禁用，则也会禁用媒体心率跟踪调用。

   您可以使用以下设置来控制是否在特定设备上发送 Analytics 数据：

   * `ADBMobile.json` 配置文件中的 `privacyDefault` 设置。此设置控制初始设置，除非在代码中进行更改，否则将一直保留初始设置。

   * `ADBMobile().setPrivacyStatus()` 方法。

      * **选择禁用：**

         * **Chromecast：**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku：**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >当用户选择禁用跟踪时，所有保留的设备数据和 ID 将被清除，除非用户重新选择启用。

      * **选择退回：**

         * **Chromecast：**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku：**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **返回当前设置：**

         * **Chromecast：**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku：**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   使用 `setPrivacyStatus` 更改隐私设置后，除非再次使用此方法对该设置进行更改，或者卸载并重新安装应用程序，否则此更改将为永久性的。

## 检索存储的标识符（OTT 应用程序） {#retrieving-stored-identifiers-ott-apps}

此信息可帮助您从 Roku 应用程序中检索本地存储的用户身份。

>[!IMPORTANT]
>
>用于检索所有标识符的方法将获取 SDK 已知并且保留的所有用户身份。必须&#x200B;**先**&#x200B;调用此方法，用户才能选择退出。

将在 JSON 字符串中返回本地存储的身份，该字符串可能包含：

* 公司上下文 - IMS 组织 ID
* 用户 ID
* Experience Cloud ID (MCID)
* 数据源 ID (DPID、DPUUID)
* Analytics ID（AVID、AID、VID 和相关 RSID）
* Audience Manager ID (UUID)

例如：

* **Chromecast：**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku：**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```
