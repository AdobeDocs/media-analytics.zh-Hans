---
title: 创建新的调试报告
description: 了解如何创建新的调试报告。
uuid: 438fde3d-98f9-46d1-9672-75d204361568
exl-id: 047acf35-8c1c-4493-9ee7-e2bad47c351e
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: a73ba98e025e0a915a5136bb9e0d5bcbde875b0a
workflow-type: ht
source-wordcount: '203'
ht-degree: 100%

---

# 创建新的调试报告{#create-a-new-debug-report}

要创建新的调试报告，请执行以下步骤：

1. 在[!UICONTROL 创建新的调试报告]中，选择以下选项：

   ![](assets/create-new-debug-report.png)

1. 使用以下信息填写各个字段：

   * **命名报告** - 输入播放器名称和日期，以便在认证过程中可以轻松地跟踪播放器，并将品牌与平台区分开。
   * **Adobe Analytics**

      * [!UICONTROL 用户名]和[!UICONTROL 共享密钥] - 这两个字段为可选字段，但您可以将 Web 服务 API 凭据添加到 Adobe Debug，以显示报表包的变量名称和变量设置。

         您可以通过以下方法之一访问相应设置：

         * [!UICONTROL Analytics > 管理员 > 公司设置 > Web 服务]
         * [!UICONTROL Analytics > 管理员 > 用户管理 > 用户 > 个人用户设置]要为新用户创建 Web 服务 API 凭据，请在[!UICONTROL 用户管理]中，将用户添加到 **Web 服务访问**&#x200B;用户组。
      * [!UICONTROL 默认端点] – 此字段中的数据由 Adobe 提供，无法更改。
      * [!UICONTROL 附加端点] – 如果需要使用，为诸如 `metrics.companyname.com` 之类的跟踪服务器添加 `CNAMES`
   * **视频心跳 (Media Analytics)**

      * [!UICONTROL 默认端点] – 此字段中的数据由 Adobe 提供，无法更改。
      * [!UICONTROL 附加端点] – 如果需要使用，为诸如 `metrics.companyname.com` 之类的跟踪服务器添加 `CNAMES`。
