---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter 示例
{: #examples}

要开始使用 {{site.data.keyword.twittershort}} 服务，请使用提供的样本来了解如何利用该服务。
{: shortdesc}

## Insights for Twitter 演示
{: #insights_twitter_demo}

为您提供的样本应用程序可搜索使用 {{site.data.keyword.twittershort}} 服务的 Twitter 数据流。通过浏览至 [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window}，可访问该应用程序。该应用程序将在浏览器中打开，并显示具有 **Twitter 搜索**和 **Twitter 计数**按钮的搜索字段。 

![具有搜索字段的用户界面的图像](images/sample1_UI.jpg "具有搜索字段的用户界面的图像")

在样本应用程序中，可以使用[查询语言](twitter_rest_apis.html#querylanguage){: new.window}中所述的受支持参数和运算符来搜索推文。例如，输入“IBM
Twitter”（其中空格表示布尔 AND 运算），并单击 **Twitter 搜索**将返回同时包含这两项的推文。

![查询项和搜索结果的图像](images/sample1_tweet_search.jpg "查询项和返回的搜索结果的图像")

在搜索字段中指定“IBM Twitter”后，单击 **Twitter 计数**将返回包含这两项的推文数。

![查询项和计数结果的图像](images/sample1_tweet_count.jpg "查询项和返回的计数结果的图像")

## 创建规则跟踪
{: #creating_rule_track}

作为入门套餐的用户，您可以创建基于规则的跟踪来过滤在 PowerTrack 数据流中收集的推文。
稍后各节中的示例将演示如何编辑和删除跟踪，以及对 PowerTrack 流执行 search 或 count API 调用。要创建规则跟踪，请发出带 /api/v1/tracks 操作的 **POST** 请求，指定跟踪类型 (**Rule**)，指示“EndDate”，并至少包含一个规则。以下片段是包含两个规则的示例请求：

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"}
    ]
}
```

`username` 和 `password` 对于应用程序和服务实例是唯一的。这些信息可从 **VCAP_SERVICES** 环境变量中获取。有关更多信息，请参阅 [{{site.data.keyword.twittershort}} 入门](index.html#insights_twitter_overview){: new.window}。

显示的响应主体类似于以下片段：

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
    "id": "66ff1961-51fe-4475-8bcd-c02f071d6fd1",
    "type": "Rule",
    "state": "Active",
    "createdDate": "2015-08-06T20:38:28.940Z",
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "rules": [
        {
          "id": "06497963-4fe3-47e8-90cd-aaef25f31314"
          "value": "Canada"
        },
        {
          "id": "d021165d-85e2-456a-af16-b9c026d76208",
          "value": "sport hockey"
        }
    ]
}
```

响应包含与新创建的跟踪相关联的唯一标识。此外，每个规则都分配有一个唯一标识。endDate 指示跟踪将停止收集消息的时间，且必须符合 UTC 格式（`YYYY-MM-DD` 或 `YYYY-MM-DDTHH:MM:SSZ`）。type 属性必须指定为 **Rule** 或 **Aggregated**。由于此示例演示的是创建基于规则的跟踪，因此指定了 **Rule** 类型。

如果在请求中未指定 state 属性，那么缺省情况下将创建跟踪，并且该跟踪的状态为 **Active**。name 属性是可选的，并且不需要唯一。为了更好地管理过滤器，建议选择唯一的描述性名称。

有关规则语法的更多详细信息，请参阅{{site.data.keyword.twittershort}} [查询语言](twitter_rest_apis.html#querylanguage){: new.window}。

## 创建聚合跟踪
{: #creating_aggregated_track}

作为入门套餐的用户，您可以创建将两个或更多现有跟踪组合在一起的聚合跟踪。
聚合跟踪可包含基于规则的跟踪和其他聚合跟踪。从聚合跟踪中搜索推文将返回其组成跟踪中的结果。要创建聚合跟踪，请发出带 /api/v1/tracks 操作的 **POST** 请求，指定跟踪类型 (**Aggregated**)，并包含两个或更多跟踪标识。以下片段是包含两个跟踪的示例请求：

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "name": "My Aggregated Track",
    "type": "Aggregated",
    "trackIds": [
       {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
       {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"}
     ]
}
```
`username` 和 `password` 对于应用程序和服务实例是唯一的。这些信息可从 **VCAP_SERVICES** 环境变量中获取。有关更多信息，请参阅 [{{site.data.keyword.twittershort}} 入门](index.html#insights_twitter_overview){: new.window}。显示的响应主体类似于以下片段：

```
HTTP/1.1 201 Created 
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
  "id": "9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6",
  "type": "Aggregated",
  "createdDate": "2015-08-07T17:05:51.214Z",
  "name": "My Aggregated Track",
  "trackIds": [
    {
      "id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"
    },
    {
      "id": "180356df-9a78-491e-b070-f3ffbe00bdf2"
    }
  ]
}
```

响应包含与聚合跟踪相关联的唯一标识。与基于规则的跟踪不同，聚合跟踪不包含 endDate 或 state 属性，因为这两个属性是在单个基于规则的跟踪中进行管理的。

## 编辑跟踪
{: #editing_tracks}

可以对规则和聚合跟踪进行编辑，以优化数据在 PowerTrack 流中的过滤方式。
在现有跟踪中添加（或修改）规则后，基于较早规则检索到的消息仍将持久存储在该跟踪中。要确保搜索结果返回最新规则集的数据，请删除该跟踪，并使用所需的规则集来创建新跟踪。

[创建规则跟踪](#creating_rule_track){: new.window}中的示例包含两条规则，跟踪标识为 `66ff1961-51fe-4475-8bcd-c02f071d6fd1`。要添加值为“Champions”的新规则，请使用 POST /api/v1/tracks/{track Id} 操作，并附加新规则。

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"},
        {"value": "Champions"}
    ]
}
```
与此类似，可以通过发出 GET /api/v1/tracks/{track Id} 操作从现有跟踪中除去规则，并除去不需要的规则。

[创建聚合跟踪](#creating_aggregated_track)中的示例包含两个跟踪。通过发出以下操作，可将标识为 `c4562594-1eeb-4a95-8fac-255428d74bce` 的另一个跟踪添加到现有聚合跟踪：

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6
HTTP/1.1 Content-Type: application/json
{
  "trackIds": [
    {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
    {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"},
    {"id": "c4562594-1eeb-4a95-8fac-255428d74bce"}
  ]
}
```

## 删除跟踪
{: #deleting_tracks}

您可以通过发出 DELETE /api/v1/tracks/{trackId} 操作来删除不再需要的跟踪。此操作可以应用于基于规则的跟踪和聚合跟踪。无法删除包含在某个聚合跟踪中的跟踪，除非从所有聚合跟踪中除去该跟踪。以下示例演示了如何删除标识为 `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88` 的跟踪：

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

或者，可以通过将特定跟踪的状态更改为 Inactive，以停止从该跟踪收集推文。以下示例不删除跟踪，而是禁用跟踪：

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## 搜索推文
{: #searching_tweets}

您可以在应用程序中发出 GET 操作从任一数据流中检索推文。例如，搜索 Decahose 推文可以通过以下方式实现：`/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`。对于入门套餐用户，从 PowerTrack 流中搜索推文可以通过以下方式实现：`/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`。

“size”参数指定要在查询响应中返回的消息数，“from”参数指示要在完整结果集中返回的初始消息。{trackId} 引用是特定跟踪的唯一标识。使用 cURL，通过输入以下内容可以在 Decahose 流中搜索包含“IBM”的推文：

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

提交针对 PowerTrack 流的相同查询时应输入为：
 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

`username` 和 `password` 对于应用程序和服务实例是唯一的。这些信息可从 **VCAP_SERVICES** 环境变量中获取。有关更多信息，请参阅 [{{site.data.keyword.twittershort}} 入门](index.html#insights_twitter_overview){: new.window}。

服务将返回 JSON 格式的响应。下表列出了可能的响应代码。

| **HTTP 状态码** 	| **原因**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| 正常                                                               	|
| 400              	| 请求有效内容属性无效或缺少这些属性。                   	|
| 401              	| 认证失败。需要有效的用户名和密码。 	|
| 403              	| 已禁止，达到了限值。                                        	|
| 500              	| 出现内部错误。                                  	|

** 表 1. 响应消息

响应主体可能显示为：

```
{
    "search": {
        "results": 16283624
    },
    "tweets": [{
        "message": {
            ...
            "body": "this is a nice tweet",
            "actor": {
                "followersCount”: 456,
                "displayName": "IBM Tweeter"
                ...
            },
            "cde": {
                "sentiment": {"polarity": "POSITIVE"...
                },
                "author": {"gender": "male"...
                },
                ...
            }
        }
    }]
}
```

以下 URL 编码的查询表达式会根据指定的时间范围和出现次数来检索有关一部电影的推文。此示例可用于确定对该电影的关注度或对电影预告片的反应。

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

对该 URL 解码后，查询语法和运算符变成“(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5”。

## 计算推文数
{: #counting_tweets}

您可以在应用程序中应用 GET 操作来检索与指定查询相匹配的推文数。对 Decahose 的查询可通过以下方式发出：`/api/v1/messages/count?q=QUERY`，而对 PowerTrack 流的调用将使用以下格式： 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

使用 cURL，通过以下查询可以在 Decahose 中找到包含“IBM”的推文数：

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

可以对 PowerTrack 数据源发出相同的查询，格式为：
 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

`username` 和 `password` 对于应用程序和服务实例是唯一的。这些信息可从 **VCAP_SERVICES** 环境变量中获取。有关更多信息，请参阅 [{{site.data.keyword.twittershort}} 入门](index.html#insights_twitter_overview){: new.window}。

服务将返回 JSON 格式的响应。下表列出了可能的响应消息。

| **HTTP 状态码** 	| **原因**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| 正常                                                               	|
| 400              	| 请求有效内容属性无效或缺少这些属性。                   	|
| 401              	| 认证失败。需要有效的用户名和密码。 	|
| 403              	| 已禁止，达到了限值。                                        	|
| 500              	| 出现内部错误。                                  	|

**表 2. 响应消息**

响应主体可能显示为：
```
{
  "related": {
      "search": {
          "href": "https://server.bluemix.net/api/v1/messages/search?q=ibm" 
      }
  },
  "search": {
      "results": 21695
  }
}
```

以下查询表达式将检索同时包含“IBM”和“Bluemix”的正面推文数。在本例中，响应中将返回 Decahose 中的推文。

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

以下 URL 编码的查询表达式将检索在指定期间内包含“IBM”的推文数。此样本查询可帮助测量主题的热门程度，并确定其是否为热门话题。在此示例中将返回 PowerTrack 流中的推文。


`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

对该 URL 解码后，查询语法和运算符变成“(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)”。
