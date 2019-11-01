---
title: 获取并行查看者 JSON 报表数据
description: null
uuid: 9168f114-2459-4951-a06c-57b735d09dc0
translation-type: tm+mt
source-git-commit: 0d2d75dd411edea2a7a853ed425af5c6da154b06

---


# 获取并行查看者 JSON 报表数据{#get-concurrent-viewers-json-report-data}

您可以使用 _* 1.4版Analytics API获取并发查看器报告数据&#x200B;*_ :
* [Analytics API](https://github.com/AdobeDocs/analytics-1.4-apis)
* [斯瓦格](https://adobedocs.github.io/analytics-1.4-apis/swagger-docs.html#/Report/Report.Get)

1. 使用在UI上构建的任何区段过滤数据。 要按特定内容ID进行筛选，请创建新区段。
1. 将请 `elements` 求主体 `id` 中的-&gt;设置为 `videoconcurrentviewers`。
1. 请求足够数量的数据。 Adobe建议使用3200个数据点，以确保数据中不存在任何间隙。

   * 您在报告中指定的数据范围在视频会话结束时收 _集所有并发查看器数据。_
因此，您必须考虑从一天开始到午夜（即第二天）结束的会话。

   * 请求一天以上的数据，但在分析中 _*&#x200B;只使用第一天的数据。*_

此方案的请求有效负荷示例如下：

```
{
  "reportDescription":{
    "reportSuiteID":"[YOUR_RSID]",
    "dateFrom":"2018-07-01",
    "dateTo":"2018-07-02",
    "metrics":[
      {
        "id":"instances"
      }
    ],
    "elements":[
      {
        "id":"videoconcurrentviewers",
        "top":"3200"
      }
    ],
    "segments":[
      {
        "id":"s1234_58ca4fc7e4b0abc238707bb9"                                         
      }
    ],
    "sortBy":"instances",
    "locale":"en_US"
  }
}
```

<!--
You can extract the concurrent viewers report data using the Experience Cloud API Explorer as follows. 

1. Navigate to: [https://marketing.adobe.com/developer/api-explorer.](https://marketing.adobe.com/developer/api-explorer)
1. Select and enter the following information in the API Explorer form:

    * **API -** Select "Report".
    * **Method -** Select "Queue".
    * **Environment -** Select your data center.
    * Request JSON - Specify the following:

        * `reportSuiteID` - For info on reports suites: [Report Suites](https://marketing.adobe.com/resources/help/en_US/sc/implement/ref-reports-report-suites.html)
        
        * `dateTo` - End date of the report.         
        
          >[!NOTE]
          >
          >The maximum time period supported is two days.

        * `dateFrom` - Start date of the report.
        * `elements : id` - Set to `"videoconcurrentviewers"`
        
        * `elements : top` - Specify the number of entries to be returned.

      Sample request body:

      ```    
      {
          "reportDescription": {
              "reportSuiteID": "[Your Report Suite ID]",
              "dateTo": "2017-09-07",
              "dateFrom": "2017-09-07"
              "metrics": [
                  {
                      "id": "instances"
                  }
              ],
              "elements": [
                  {
                      "id": "videoconcurrentviewers",
                      "top": 2880
                  }
              ]
              "locale": "en_US"
          }
      }
      
      ```

      >[!TIP]
      >
      >Some sessions are ended on the next day, and at that point the data will be available for reporting. In that case the best approach is to select 2 days (2880 minutes) of data, and use only the data for the first day (1440 minutes).

1. Click **Get Response**.

   In the Response field, you should get a `reportID`.
1. In the form, change **Method** to "Get".
1. Enter the value of the `reportID` you received in Step 3, and click **Get Response**.

   The concurrent viewers report data, in JSON format, is presented in the Response field.
   
   For example:
   
   ![](assets/api_helper_2.png) 

   ![](assets/api_helper_1.png)

-->
