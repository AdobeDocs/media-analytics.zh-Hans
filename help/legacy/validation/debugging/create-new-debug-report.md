---
title: 创建新的调试报告
description: 了解如何创建新的调试报告。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 44%

---

# 创建新的调试报告{#create-a-new-debug-report}

要创建新的调试报告，请执行以下步骤：

1. 在[!UICONTROL 创建新的调试报告]中，选择以下选项：

   ![](assets/create-new-debug-report.png)

1. 在字段中填写以下信息：

   * **为报告命名** — 输入播放器名称和日期，以便在认证期间轻松跟踪播放器，并将品牌和平台分开。
   * **Adobe Analytics**

      * [!UICONTROL 用户名]和[!UICONTROL 共享密钥] — 这些字段是可选的，但您可以将网站服务API凭据添加到Adobe Debug以显示报表包的变量名称和变量设置。

        您可以通过以下方式之一进行访问：

         * [!UICONTROL Analytics >管理员>公司设置> Web服务]
         * [!UICONTROL Analytics >管理员>用户管理>用户>个人用户设置]若要为新用户创建Web服务API凭据，请在[!UICONTROL 用户管理]中，将该用户添加到&#x200B;**Web服务访问**&#x200B;用户组。

      * [!UICONTROL 默认端点] – 此字段中的数据由 Adobe 提供，无法更改。
      * [!UICONTROL 附加端点] – 如果需要使用，为诸如 `metrics.companyname.com` 之类的跟踪服务器添加 `CNAMES`

   * **视频心跳 (Media Analytics)**

      * [!UICONTROL 默认端点] – 此字段中的数据由 Adobe 提供，无法更改。
      * [!UICONTROL 附加端点] – 如果需要使用，为诸如 `metrics.companyname.com` 之类的跟踪服务器添加 `CNAMES`。
