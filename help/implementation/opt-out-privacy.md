---
title: 解释选择禁用和隐私
description: 了解如何处理选择启用、选择禁用和隐私。
uuid: 7e60c7bd-8dba-4c7a-9c3c-0c634b815397
exl-id: 64f5ef2b-7850-43d8-8f32-3d008ea4f156
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 69%

---

# 选择禁用和隐私{#opt-out-and-privacy}

## 选择禁用/选择启用 {#opt-out-opt-in}

您可以控制是否允许在特定设备上进行跟踪活动。

* **移动设备应用程序 —** VA库遵循`AdobeMobile`库的隐私和选择退出设置。 要选择禁用跟踪，您需要使用 `AdobeMobile` 库。 有关`AdobeMobile`库的选择退出和隐私设置的详细信息，请参阅[选择退出和隐私设置](https://experienceleague.adobe.com/docs/mobile-services/android/gdpr-privacy-android/privacy.html?lang=zh-Hans)。
* **JavaScript/浏览器应用程序 -** VA 库遵循 `VisitorAPI` 隐私和选择禁用设置。 要选择禁用跟踪，您需要在访客 API 服务中选择禁用。 有关选择禁用和隐私的更多信息，请参阅 [Adobe Experience Platform 身份标识服务](https://experienceleague.adobe.com/docs/id-service/using/home.html?lang=zh-Hans)。
* **OTT 应用程序（Chromecast、Roku）-** OTT SDK 提供了通用数据保护条例 (GDPR) 就绪 API，允许您为数据收集和传输设置 `opt` 状态标记，并检索本地存储的身份标识。

  >[!NOTE]
  >
  >如果将隐私状态设置为选择禁用，则也会禁用媒体心跳跟踪调用。

  您可以使用以下设置来控制是否在特定设备上发送 Analytics 数据：

   * `ADBMobile.json` 配置文件中的 `privacyDefault` 设置。 此设置控制初始设置，除非在代码中进行更改，否则将一直保留初始设置。

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

  使用 `setPrivacyStatus` 更改隐私设置后，更改将保持有效，直至再次使用此方法更改设置或卸载并重新安装应用程序。

## 检索存储的标识符（OTT 应用程序） {#retrieving-stored-identifiers-ott-apps}

此信息可帮助您从 Roku 应用程序中检索本地存储的用户身份标识。

>[!IMPORTANT]
>
>用于检索所有身份标识符的方法将获取 SDK 已知并且保留的所有用户身份标识。 必须&#x200B;**先**&#x200B;调用此方法，用户才能选择退出。

将在 JSON 字符串中返回本地存储的身份标识，该字符串可能包含：

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

## Analytics选择退出参数 {#analytics-opt-out}

通过两个保留的参数，可禁止将Media Analytics数据从服务器端转发到Audience Manager以及与第三方共享数据。 这些参数和会话参数一起在API级别传递，而不是在SDK配置对象中设置。

| 参数 | API密钥 | 上下文数据 |
| --- | --- | --- |
| 选择退出服务器端转发 | `analytics.optOutServerSideForwarding` | `cm.dmp` |
| 选择退出数据共享 | `analytics.optOutSellToThirdParty` | `cm.sell` |

* **`analytics.optOutServerSideForwarding`**：当`true`时，禁止将此点击服务器端转发到Audience Manager和其他Adobe目标。
* **`analytics.optOutSellToThirdParty`**：当`true`时，禁止与第三方合作伙伴共享此点击数据。

>[!NOTE]
>
>这些参数记录在[媒体收集API会话引用](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md)中。 它们适用于媒体收集API和Media Edge API实施。 上述SDK级别的选择退出控件适用于Mobile和OTT实施。
