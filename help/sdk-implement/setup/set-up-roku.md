---
seo-title: 设置 Roku
title: 设置 Roku
uuid: 904dfda0-4782-41da-b4 ab-212e8115663
translation-type: tm+mt
source-git-commit: ab400b673e97f9b47c6088e09b7e7d9e7b1c9ee6

---


# 设置 Roku{#set-up-roku}

## 先决条件

* **获得HeartBeats的有效配置参数**&#x200B;在设置媒体分析帐户之后，可以从Adobe代表获得这些参数。
* **在媒体播放器中提供以下功能：**
   * _可订阅播放器事件的 API -_ Media SDK 要求您在播放器中发生事件时调用一组简单的 API。
   * _提供播放器信息的 API_ - 此信息包括媒体名称和播放头位置等详细信息。

Adobe Mobile Services 提供了新的用户界面，以整合 Adobe Marketing Cloud 中针对移动设备应用程序的移动营销功能。最初，Mobile 服务无缝集成了 Adobe Analytics 和 Adobe Target 解决方案的应用程序分析和目标定位功能。

Learn more at [Adobe Mobile Services documentation.](https://marketing.adobe.com/resources/help/en_US/mobile/)

适用于 Experience Cloud 解决方案的 Roku SDK 2.x 让您能够测量使用 BrightScript 编写的 Roku 应用程序，通过受众管理收集并利用受众数据，以及通过视频心率测量视频参与。

## SDK 实施

1. 将[下载](/help/sdk-implement/download-sdks.md#section_551A10AD7880426BB29AE52482BB4211)的 Roku 库添加到您的项目中。

   1. `AdobeMobileLibrary-2.*-Roku.zip` 下载文件包含以下软件组件：

      * `adbmobile.brs`：此库文件将包含在Roku应用程序源文件夹中。

      * `ADBMobileConfig.json`：为您的应用程序自定义此SDK配置文件。
   1. 将库文件和 JSON 配置文件添加到您的项目源。

      用于配置 Adobe Mobile 的 JSON 具有一个用于媒体心率的专有密钥，其名称为 `mediaHeartbeat`。这是媒体心率的配置参数所属的位置。

      >[!TIP]
      >
      >A sample `ADBMobileConfig` JSON file is provided with the package. 请与 Adobe 代表联系以获取有关设置。

      例如：

      ```
      {
        "version":"1.0", 
        "analytics":{
          "rsids":"",
          "server":"",
          "charset":"UTF-8", 
          "ssl":false, 
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
         "ssl":false,
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
      >`mediaHeartbeat` 如果配置错误，媒体模块(VHL)输入错误状态，并将停止发送跟踪调用。


1. 配置 Experience Cloud 访客 ID。

   Experience Cloud 访客 ID 服务可以跨多个 Experience Cloud 解决方案提供一个通用的访客 ID。访客 ID 服务是视频心率和其他 Marketing Cloud 集成所必需的。

   Verify that your `ADBMobileConfig` config contains your `marketingCloud` organization ID.

   ```
   "marketingCloud": {
       "org": YOUR-MCORG-ID"
   }
   ```

   Experience Cloud organization IDs uniquely identify each client company in the Adobe Marketing Cloud and appear similar to the following value: `016D5C175213CCA80A490D05@AdobeOrg`.

   >[!IMPORTANT]
   >
   >Ensure that you include `@AdobeOrg`.

   配置完成后，将生成一个 Experience Cloud 访客 ID，并将其包含在所有点击中。Other Visitor IDs, such as `custom` and `automatically-generated`, continue to be sent with each hit.

   **Experience Cloud 访客 ID 服务方法**

   >[!TIP]
   >
   >Experience Cloud Visitor ID methods are prefixed with `visitor`.

   |  方法   | 描述 |
   | --- | --- |
   | `visitorMarketingCloudID` | Retrieves the Experience Cloud visitor ID from the visitor ID service.  <br/><br/>`ADBMobile().visitorMarketingCloudID()` |
   | `visitorSyncIdentifiers` | 除了 Experience Cloud 访客 ID 之外，您还可以设置其他与每个访客关联的客户 ID。访客 API 接受同一访客具有多个客户 ID，并且使用客户类型标识符区分不同客户 ID 的适用范围。This method corresponds to `setCustomerIDs`. For example: <br/><br/>`identifiers={}` <br/>`identifiers["idType"]="idValue"` <br/>`ADBMobile().visitorSyncIdentifiers(identifiers)` |
   | `setAdvertisingIdentifier` | 用于在SDK上设置Roku ID for Advertising(RDA)。For example: <br/><br/> `ADBMobile().setAdvertisingIdentifier(`<br/>`"<sample_roku_identifier_for_advertising>")`<br/><br/><br/>使用Roku SDK [GetTria()](https://developer.roku.com/docs/references/brightscript/interfaces/ifdeviceinfo.md#getrida-as-dynamic) API获取Roku ID for Advertising(RDA)。 |

   <!--
    Roku Api Reference: 
    * [Integrating the Roku Advertising Framework](https://sdkdocs.roku.com/display/sdkdoc/Integrating+the+Roku+Advertising+Framework)  
    * [GetRIDA()](https://sdkdocs.roku.com/display/sdkdoc/ifDeviceInfo#ifDeviceInfo-GetRIDA())
    -->

<!--    **Postbacks -** For more information about configuring postbacks, see [Configure Postbacks.](https://marketing.adobe.com/resources/help/en_US/mobile/signals_.html) -->
