---
title: 选择禁用和隐私
description: 如何处理选择加入、选择退出和隐私。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# 选择禁用和隐私{#opt-out-and-privacy}

## 选择禁用/选择启用 {#opt-out-opt-in}

您可以控制是否允许在特定设备上进行跟踪活动。

* **移动设备应用程序 -** VA 库遵循 `AdobeMobile` 库的隐私和选择禁用设置。要选择禁用跟踪，您需要使用 `AdobeMobile` 库。有关 `AdobeMobile` 库的选择禁用和隐私设置的更多信息，请参阅[选择禁用和隐私设置](https://docs.adobe.com/content/help/en/mobile-services/android/gdpr-privacy-android/privacy.html)。
* **JavaScript/浏览器应用程序 -** VA 库遵循 `VisitorAPI` 隐私和选择禁用设置。要选择禁用跟踪，您需要在访客 API 服务中选择禁用。For further information on opt­out and privacy, see [Adobe Experience Platform Identity Service.](https://marketing.adobe.com/resources/help/en_US/mcvid/).
* **OTT Apps(Chromecast, Roku)**`opt` -OTT SDK提供符合一般数据保护规定(GDPR)的API，允许您为数据收集和传输设置状态标志，并检索本地存储的身份。

   >[!NOTE]
   >
   >如果隐私状态设置为“退出”，则还会禁用媒体心跳跟踪调用。

   您可以使用以下设置来控制是否在特定设备上发送 Analytics 数据：

   * The `privacyDefault` setting in the `ADBMobile.json` config file. 此设置控制初始设置，除非在代码中进行更改，否则将一直保留初始设置。

   * `ADBMobile().setPrivacyStatus()` 方法。

      * **选择禁用:**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_OUT)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_OUT)
            ```
         >[!IMPORTANT]
         >
         >当用户退出跟踪时，将清除所有保留的设备数据和ID，直到用户返回。

      * **重新选择启用：**

         * **Chromecast:**

            ```
            ADBMobile.config.setPrivacyStatus(ADBMobile.config.PRIVACY_STATUS_OPT_IN)
            ```

         * **Roku:**

            ```
            ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)
            ```
      * **返回当前设置：**

         * **Chromecast:**

            ```
            ADBMobile.config.getPrivacyStatus()
            ```

         * **Roku:**

            ```
            ADBMobile().getPrivacyStatus()
            ```
   使用 `setPrivacyStatus` 更改隐私设置后，除非再次使用此方法对该设置进行更改，或者卸载并重新安装应用程序，否则此更改将为永久性的。

## Retrieving Stored Identifiers (OTT Apps) {#retrieving-stored-identifiers-ott-apps}

此信息可帮助您从 Roku 应用程序中检索本地存储的用户身份。

>[!IMPORTANT]
>
>检索所有标识符的方法获取SDK已知并保留的所有用户标识。 您必须在用户选择禁用&#x200B;**之前**&#x200B;调用此方法。

本地存储的身份在 JSON 字符串中返回，其中可能包含以下项：

* 公司上下文 - IMS 组织 ID
* 用户 ID
* Experience Cloud ID (MCID)
* 数据源 ID（DPID、DPUUID）
* Analytics ID（AVID、AID、VID 和关联的 RSID）
* Audience Manager ID (UUID)

例如：

* **Chromecast:**

   ```
   ADBMobile.config.getAllIdentifiersAsync(callback)
   ```

* **Roku:**

   ```
   vids = ADBMobile().getAllIdentifiers()
   ```

