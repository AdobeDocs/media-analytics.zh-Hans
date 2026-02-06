---
title: 上传计划数据以跟踪实时内容
description: 了解如何上传计划数据以跟踪实时内容。
feature: Streaming Media
role: User, Admin, Developer
exl-id: 875c4513-ea4e-4c5f-bfc1-34ea175007ca
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '1381'
ht-degree: 5%

---

# 上传计划数据以跟踪实时内容

>[!AVAILABILITY]
>
>本文中描述的功能处于发布的有限测试阶段，因此可能在您的环境中尚不可用。当该功能正式发布时，将删除此说明。有关发布过程的信息，请参阅[Customer Journey Analytics功能发布](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/releases)。

您可以上传过去实时流媒体内容的计划数据，以更轻松准确地跟踪实时内容的收视率。 您可以跟踪各个项目甚至特定主题或项目群区段的收视率。

以下是支持计划数据上传的直播内容示例：

* FAST（免费广告支持电视）平台

* 本地流

* 直播体育赛事

* 新闻或主题节目

## 功能

在使用以往直播流媒体内容的计划数据上传时，可以使用各种功能。 本节介绍有助于分析程序性能的一些关键功能。

无论您如何实现流媒体收集，这些功能都是可用的。

* **准确地跟踪节目计划**：在要分析的时间段内，确定实时流中每个节目的开始和结束时间。 通过精确的开始和结束时间，精确的运行时间可以精确反映并可以对每个查看者会话进行分析。

  例如，在直播体育赛事结束之前，并不总是知道具体的开始和结束时间。 计划数据上传允许您通过在程序完成后更新开始和结束时间来获得准确的报告。

* **跟踪单个主题或项目群区段**：为给定项目群中的特定主题或项目群区段（时隙）创建新的基于时间的维度。 这些基于时间的维度允许您在更具体的级别分析节目的收视率，有助于收集关于哪些主题或节目片段最能引起共鸣的见解。

  例如，在分析直播体育赛事（如足球比赛）时，您可以为上半场、下半场创建单独的维度。 通过这种方式跟踪项目中的特定主题或区段，可以更详细地划分查看者行为。

* **在Journey Optimizer中构建用户历程**：跟踪某人在给定会话中查看了哪些程序（甚至该人查看了哪些主题或项目群），然后在Adobe Journey Optimizer中使用此数据为观看了某个程序或对某个特定主题表现出兴趣的客户构建用户历程。

## 了解计划数据如何用于流媒体

流媒体的计划数据功能通过以下方式工作：

1. 从计划项目数据集中读取计划项目记录，并按计划日期进行筛选。

   仅适用于过去24小时到48小时发生的项目。

2. 从媒体数据集中读取媒体关闭事件，按日期以及计划程序记录中的XDM路径进行过滤。

3. 对于每个媒体关闭事件，生成的媒体计划开始事件数与显示的媒体会话数相同。

   每个媒体时间表开始事件都包含时间表的名称和长度。

   此外，名为&#x200B;**scheduleTimePlayed**&#x200B;的新时间量度包含媒体会话与计划节目重叠的秒数。 计划开始事件的时间戳是节目开始的时间戳。

4. 将新的计划开始事件写入AEP媒体数据集中。

## 先决条件

要上传过去实时内容的计划数据，您的流媒体环境必须满足以下先决条件：

* 必须启用流媒体收集以跟踪您要为其上传计划数据的内容，如[跟踪概述](/help/use-cases/track-av-playback/track-core-overview.md)中所述。<!--specifics??? -->

* 将流媒体收集与Customer Journey Analytics结合使用。 Adobe Analytics不提供上传计划数据的功能。

## 在AEP中创建项目计划数据集

在推送计划信息之前，必须在Experience Platform中创建项目计划数据集：

1. 基于&#x200B;**Media Analytics计划程序** XDM类创建架构。

   ![Media Analytics计划计划架构](assets/media_schedule_finish_schema_creation.png)

   这是Media Analytics计划程序类的XDM定义。

   [https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json](https://github.com/adobe/xdm/blob/master/components/fieldgroups/tv-schedule/media-analytics-scheduled-program.schema.json)

1. 根据您创建的架构创建数据集。

1. 继续下面的部分，[推送计划信息](#push-schedule-information)。

## 推送计划信息

在您[创建项目计划数据集](#create-a-program-schedule-dataset-in-aep)之后，您可以推送计划信息：

1. 创建包含计划信息的.json文件。

   .json文件必须按照XDM架构包含计划程序对象数组。

1. 上传.json文件：

   >[!NOTE]
   >
   >本节中的cURL示例使用以下变量：
   >
   >* 要通过Adobe Developer进行身份验证：
   >     * CUSTOMER_API_KEY
   >     * AUTH_TOKEN
   >* 组织标识：CUSTOMER_ORG_ID
   >* 在设置中创建的记录数据集的数据集ID： DATASET_ID
   >* 在文件上载中使用的第一个请求中创建的批次ID：BATCH_ID
   >* 用于推送记录的文件名：FILE_NAME

   1. 创建新批次，然后从响应中获取批次ID。

      考虑以下使用cURL创建新AEP批次的示例：

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches' \
          -X POST \
          -H 'Accept: application/json' \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --data-raw '{"datasetId":"<DATASET_ID>","inputFormat":{"format":"json","isMultiLineJson":true},"tags":{"test":["2"]}}'
      
          HTTP/1.1 201 Created
          {
              "id": "BATCH_ID",
              "imsOrg": "CUSTOMER_ORG_ID",
              "updated": 1749838941763,
              "status": "loading",
              "created": 1749838941763,
              "relatedObjects": [
                  {
                      "type": "dataSet",
                      "id": "DATASET_ID"
                  }
              ],
              "version": "1.0.0",
              ............
          }
      ```

   1. 推送包含使用批次ID的程序计划数据记录的.json文件。

      要推送计划信息，您应使用AEP批处理API，如[批处理摄取API概述](https://experienceleague.adobe.com/en/docs/experience-platform/ingestion/batch/overview)中所述。

      考虑以下使用cURL推送包含计划记录的文件示例：

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>/datasets/<DATASET_ID>/files/<FILE_NAME>' \
          -X PUT \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>' \
          --upload-file ./schedule_21_05_2025.json`
      ```

   1. 完成批处理。

      请考虑以下使用cURL完成批次的示例：

      ```
          curl -i 'https://platform.adobe.io/data/foundation/import/batches/<BATCH_ID>?action=COMPLETE' \
          -X POST \
          -H 'x-api-key: <CUSTOMER_API_KEY>' \
          -H 'x-gw-ims-org-id: <CUSTOMER_ORG_ID>' \
          -H 'Content-Type: application/json' \
          -H 'Authorization: Bearer <OAUTH_TOKEN>'
      ```

1. 继续下面的部分，[向Adobe客户关怀部门提交支持服务单](#log-a-support-ticket-with-adobe-customer-care)。

## 向Adobe客户关怀部门提交支持工单

向Adobe客户关怀部门提交支持工单，并提供以下信息：

* **媒体数据集**：指定从中读取媒体会话数据的数据集的数据集ID。

* **计划数据集**：指定计划记录被推送到的数据集的数据集ID。

* **输出媒体数据集**：指定保存计划开始事件的数据集的数据集ID。

  此数据集ID可以是用于媒体数据集的相同数据集ID。 如果是不同的数据集ID，则它仍应具有与媒体数据集相同的XDM架构。

* **组织ID**：指定您的组织ID。

## 包含两个记录的计划.json文件示例

以下示例是包含两个记录的计划.json文件。 每个.json文件都应包含一天内的所有计划程序。

```
   [
        {
            "_id": "any_identifier_as_id_1",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 1800,
                "name": "Show Name",
                "startTimestamp": "2025-05-01T00:30:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            },
        },
        {
            "_id": "any_identifier_as_id_2",
            "customMetadata": [
                {
                    "name": "Sample value",
                    "value": "Sample value"
                }
            ],
            "defaultMetadata": {
                "album": "Sample value",
                "artist": "Sample value",
                "assetID": "Sample value",
                "author": "Sample value",
                "cdn": "Sample value",
                "dayPart": "Sample value",
                "episode": "Sample value",
                "feed": "Sample value",
                "firstAirDate": "Sample value",
                "firstDigitalDate": "Sample value",
                "genreList": [
                    "Sample value"
                ],
                "label": "Sample value",
                "network": "Sample value",
                "originator": "Sample value",
                "publisher": "Sample value",
                "rating": "Sample value",
                "season": "Sample value",
                "show": "Sample value",
                "showType": "Sample value",
                "station": "Sample value",
                "streamFormat": "Sample value"
            },
            "mediaProgramDetails": {
                "length": 3600,
                "name": "Show Name 2",
                "startTimestamp": "2025-05-01T01:00:00+00:00"
            },
            "scheduleDate": "2025-05-01",
            "scheduleFilter": {
                "filterPath": "xdm.mediaReporting.sessionDetails.channel",
                "filterValue": "Channel Name"
            }
        }
    ]
```

### 了解示例中的计划项目字段

1. **mediaProgramDetails**：应包含创建计划开始事件所需的最少信息：
   * **startTimestamp**：节目开始的时间。
   * **name**：节目的友好名称。
   * **length**：节目持续的秒数。

     >[!IMPORTANT]
     >
     >如果您有多个计划数据请求，则它们的开始时间和结束时间不能重叠。

1. **scheduleDate**：节目播出的日期。 格式应为YYYY-MM-DD。 它用于筛选计划数据集并获取adobe创建计划启动的所有计划。
1. **scheduleFilter**：用于筛选所有媒体会话关闭事件。
   * **filterPath**：用于筛选的字段的XDM路径。
   * **filterValue**：用于筛选的值。
1. **customMetadata**：要添加到计划的自定义元数据启动事件。 此元数据用于覆盖会话关闭事件上存在的自定义元数据。
1. **defaultMetadata**：可以添加或覆盖媒体关闭调用中默认元数据的维度特定列表。

   请考虑以下维度示例，您可以在Customer Journey Analytics中创建并报告维度：

   * **[“_剧集名称_”](https://experienceleague.adobe.com/cn/docs/media-analytics/using/implementation/variables/audio-video-parameters#episode)**：此维度可以帮助您了解特定系列中的哪些剧集表现最佳。

   * **[资产ID](https://experienceleague.adobe.com/cn/docs/media-analytics/using/implementation/variables/audio-video-parameters#asset-id)**

1. 继续[在Customer Journey Analytics](#analyze-data-in-customer-journey-analytics)中分析数据。

## 在Customer Journey Analytics中分析数据

在上传数据文件（如[请求并上传计划数据文件](#request-and-upload-the-schedule-data-file)中所述）的一天内，您的数据就可以在Customer Journey Analytics中报告了。

要在Customer Journey Analytics中报告过去的实时流媒体数据，请执行以下操作：

1. 创建新项目或打开现有项目。

1. 通过创建分析过去的实时流媒体数据所需的任何表或可视化图表来构建项目。

   在构建项目时，请使用您在计划数据文件中包含并发送到Adobe客户关怀团队的信息。 这包括匹配的键值、维度和任何其他元数据。 有关详细信息，请参阅[请求并上载计划数据文件](#request-and-upload-the-schedule-data-file)。




<!-- 

Extra

Things they need to upload:
Everything on that slide + other metadata
You can't overlap 2 schedules.
You can build a journey in AJO for the people who watch Mike, Mike, and Mike. e.g. 
This is recurring.
Available to all SKUs? "Increases cost for updated data by 22%, but included in the new higher tier Streaming Media SKU."

You can now upload schedule data of past live content to more easily and accurately track viewership. Live content includes content from FAST (Free Ad Supported TV) platforms or local streams.
You can track which programs a person viewed in a given session, or even which topics or program segments they viewed. These capabilities are available regardless of how you implemented Streaming Media Collection.
Previously, it was difficult to accurately tie a given session to specific programs when analyzing live content, and it wasn't possible to tie a given session to individual topics or program segments.
Schedule data uploads of live content in Streaming Media Collection includes the following capabilities:
Upload schedules for past live content, regardless of your Streaming Media Collection implementation.
Identify the start and end times of each individual program in the live stream for the period of time that you want to analyze. With accurate start and end times, the precise running time is accurately reflected and can be analyzed against each viewer session.
For example, precise beginning and end times are not always known for a live sporting event until the event is over. Schedule data uploads allow you to get accurate reporting by updating the start and end times after the program finishes.
Create new time-based dimensions for specific topics or program segments (time slots) within a given program. These time-based dimensions allow you to analyze viewership of a program at a more specific level, helping to gather insights about which topics or program segments resonated best.
For example, when analyzing a live sporting event, such as a soccer match, you can create separate dimensions for the first half, half time, and second half. This allows for more detailed breakdowns of viewer behavior for specific segments of a program.
These capabilities allow you to:
Analyze show viewership to understand performance.
Target users based on program viewership.
Analyze viewership based on metadata like topic, sports league, sponsorship, and so forth.
Target based on metadata viewership.
Correct media metrics for show dimensions of live sports/events for easier analysis at scale.
Increased ease of use for live sports

-->
