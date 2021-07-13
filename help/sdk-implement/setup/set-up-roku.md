---
title: 如何为Roku设置媒体SKD
description: 按照以下步骤在Roku中设置Media SDK应用程序。
uuid: 904dfda0-4782-41da-b4ab-212e81156633
exl-id: b8de88d0-3a93-4776-b372-736bf979ee26
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 79%

---

# 设置 Roku{#set-up-roku}

## 先决条件

* **获取心率的有效配置参数**
在设置 Media Analytics 帐户后，您可以从 Adobe 代表处获取这些参数。
* **在媒体播放器中提供以下功能：**
   * _用于订阅播放器事件的 API_ - Media SDK 要求在播放器中发生事件时调用一组简单的 API。
   * _提供播放器信息的 API_ - 此信息包括媒体名称和播放头位置等详细信息。

Adobe Mobile Services 提供了新的 UI，以将 Adobe Marketing Cloud 中针对移动设备应用程序的移动营销功能整合到一起。最初，移动服务可无缝集成 Adobe Analytics 和 Adobe Target 解决方案的应用程序分析和定位功能。

请参阅 [Adobe Mobile Services 文档](https://experienceleague.adobe.com/docs/mobile-services/using/home.html?lang=zh-Hans)，以了解更多信息。

适用于 Experience Cloud 解决方案的 Roku SDK 2.x 让您能够测量使用 BrightScript 编写的 Roku 应用程序，通过受众管理收集并利用受众数据，以及通过视频心率测量视频参与。

## SDK 实施

1. 将[下载](/help/sdk-implement/download-sdks.md#download-2x-sdks)的 Roku 库添加到您的项目中。

   1. `AdobeMobileLibrary-2.*-Roku.zip` 下载文件包含以下软件组件：

      * `adbmobile.brs`：此库文件将包含在您的 Roku 应用程序源文件夹中。

      * `ADBMobileConfig.json`：这是为您的应用程序自定义的 SDK 配置文件。
   1. 将库文件和 JSON 配置文件添加到您的项目源。

      用于配置 Adobe Mobile 的 JSON 具有一个用于媒体心率的专有密钥，其名称为 `mediaHeartbeat`。这是媒体心率的配置参数所属的位置。

      >[!TIP]
      >
      >此包中提供了一个 `ADBMobileConfig` JSON 文件示例。有关设置，请与 Adobe 代表联系。

      例如：

      ```
      {
        "version":"1.0",
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8",
          "ssl":true,
          "offlineEnabled":false,
          "lifecycleTimeout":30,
          "batchLimit":50,
          "privacyDefault":"optedin",
          "poi":[ ]
      },
      "marketingCloud":{
        "org":""
      },
      "target":{
        "clientCode":"",
        "timeout":5
      },
      "audienceManager":{
        "server":""
      },
      "acquisition":{
        "server":"example.com",
        "appid":"sample-app-id"
      },
      
      "mediaHeartbeat":{
         "server":"example.com",
         "publisher":"sample-publisher",
         "channel":"sample-channel",
         "ssl":true,
         "ovp":"sample-ovp",
         "sdkVersion":"sample-sdk",
         "playerName":"roku"
         }    
      }
      ```

      | 配置参数 | 描述     |
      | --- | --- |
      | `server` | 表示后端跟踪端点的 URL 的字符串。 |
      | `publisher` | 表示内容发布者唯一标识符的字符串。 |
      | `channel` | 表示内容分发渠道名称的字符串。 |
      | `ssl` | 布尔值，表示是否应使用 SSL 来跟踪调用。 |
      | `ovp` | 表示视频播放器提供程序名称的字符串。 |
      | `sdkversion` | 表示应用程序/SDK 当前版本的字符串。 |
      | `playerName` | 表示播放器名称的字符串。 |

      >[!IMPORTANT]
      >
      >如果未正确配置 `mediaHeartbeat`，则媒体模块 (VHL) 会进入错误状态并将停止发送跟踪调用。


1. 配置 Experience Cloud 访客 ID。

   Experience Cloud 访客 ID 提供了一个跨 Experience Cloud 解决方案的通用访客 ID。视频心率和其他 Marketing Cloud 集成都需要使用访客 ID 服务。

   验证您的 `ADBMobileConfig` 配置包含 `marketingCloud` 组织 ID。

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud 组织 ID 唯一标识 Adobe Marketing Cloud 中的每个客户公司，它类似于以下值：`016D5C175213CCA80A490D05@AdobeOrg`。

   >[!IMPORTANT]
   >
   >确保包含 `@AdobeOrg`。

   配置完成后，将生成一个 Experience Cloud 访客 ID，并将其包含在所有点击中。其他访客 ID（如 `custom` 和 `automatically-generated`）将继续随每次点击一起发送。

   **Experience Cloud 访客 ID 服务方法**

   >[!TIP]
   >
   >Experience Cloud 访客 ID 方法以 `visitor` 为前缀。

   |  方法   | 描述 |
   | --- | --- |
   | `visitorMarketingCloudID` | 从访客 ID 服务中检索 Experience Cloud 访客 ID。<br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | 使用 Experience Cloud 访客 ID，您可以设置其他可与每个访客关联的客户 ID。访客 API 接受同一访客具有多个客户 ID，并且使用客户类型标识符区分不同客户 ID 的适用范围。此方法对应于 `setCustomerIDs`。例如：<br/><br/>`identifiers={}`<br/>`identifiers["idType"]="idValue"`<br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | 用于在 SDK 上设置 Roku ID for Advertising (RIDA)。例如：<br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>  `"<sample_roku_identifier_for_advertising>")` <br/><br/><br/>使用 Roku SDK [getRIDA()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API 获取 Roku ID for Advertising (RIDA)。 |
   | `getAllIdentifiers` | 返回由SDK存储的所有标识符列表，包括Analytics、访客、Audience Manager和自定义标识符。<br/><br/> `identifiers = ADBMobile().getAllIdentifiers()` |
   <!--
    Roku Api Reference:
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

   <br/><br/>

   **其他公共API**

   **DebugLogging**
 |方法   |描述 | | — | — | |  `setDebugLogging` |用于启用或禁用SDK的调试日志记录。<br/><br/>`ADBMobile().setDebugLogging(true)` | |  `getDebugLogging` |如果启用了调试日志记录，则返回true。   <br/><br/>`isDebugLoggingEnabled = ADBMobile().getDebugLogging()` |

   <br/><br/>

   **PrivacyStatus**
 |常量   |描述 | | — | — | |  `PRIVACY_STATUS_OPT_IN` |在调用setPrivacyStatus以选择启用时要传递的常量。<br/><br/>`optInString = ADBMobile().PRIVACY_STATUS_OPT_IN`| |  `PRIVACY_STATUS_OPT_OUT` |在调用setPrivacyStatus以选择禁用时要传递的常量。  <br/><br/>`optOutString = ADBMobile().PRIVACY_STATUS_OPT_OUT`|

   <br/>

   |  方法   | 描述 |
   | --- | --- |
   | `setPrivacyStatus` | 在SDK中设置隐私状态。 <br/><br/>`ADBMobile().setPrivacyStatus(ADBMobile().PRIVACY_STATUS_OPT_IN)` |
   | `getPrivacyStatus` | 获取在SDK中设置的当前隐私状态。 <br/><br/>`privacyStatus = ADBMobile().getPrivacyStatus()` |

   <br/><br/>
   >[!IMPORTANT]
   >
   >确保每250毫秒在主事件循环中调用一次`processMessages`和`processMediaMessages`函数，以确保SDK正确发送ping。

   |  方法   | 描述 |
   | --- | --- |
   | `processMessages` | 负责将Analytics事件传递到SDK以进行处理。 <br/><br/>`ADBMobile().processMessages()` |
   | `processMediaMessages` | 负责将媒体事件传递到SDK以进行处理。<br/><br/>`ADBMobile().processMediaMessages()` |


<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://experienceleague.adobe.com/docs/mobile-services/using/manage-app-settings-ug/configuring-app/signals.html) -->
