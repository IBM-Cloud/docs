---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter 範例
{: #examples}

若要開始使用 {{site.data.keyword.twittershort}} 服務，請使用提供的範例來瞭解如何利用此服務。
{: shortdesc}

## Insights for Twitter 展示
{: #insights_twitter_demo}

範例應用程式可供您搜尋使用 {{site.data.keyword.twittershort}} 服務的 Twitter 資料串流。您可以導覽至 [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window} 來存取此應用程式。應用程式會在您的瀏覽器中開啟，並顯示搜尋欄位，以及 **Twitter Search** 與 **Twitter Count** 按鈕。 

![含搜尋欄位的使用者介面影像。](images/sample1_UI.jpg "含搜尋欄位的使用者介面影像。")

從範例應用程式中，您可以使用[查詢語言](twitter_rest_apis.html#querylanguage){: new.window}中所說明的支援參數及運算子來搜尋推文。例如，輸入 "IBM Twitter"（以空格表示布林 AND 運算）並按一下 **Twitter Search**，將傳回同時包含這兩個詞彙的推文。

![查詢詞彙與所傳回搜尋結果的影像。](images/sample1_tweet_search.jpg "查詢詞彙與所傳回搜尋結果的影像。")

在搜尋欄位中指定 "IBM Twitter" 時，按一下 **Twitter Count** 會傳回同時包含這兩個詞彙的推文數目。

![查詢詞彙與計數結果的影像。](images/sample1_tweet_count.jpg "查詢詞彙與所傳回計數結果的影像。")

## 建立規則追蹤
{: #creating_rule_track}

作為「入門方案」使用者，您可以建立規則型追蹤，來過濾 PowerTrack 資料串流中收集的推文。後面幾節中的範例將示範如何編輯及刪除追蹤，以及對 PowerTrack 串流執行 search 或 count API 呼叫。若要建立規則追蹤，請利用 /api/v1/tracks 作業發出 **POST** 要求、指定追蹤類型 (**Rule**)、指出 'EndDate'，然後至少包括一個規則。下列 Snippet 是包括兩個規則的範例要求：

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

`username` 及 `password` 對您的應用程式及服務實例是唯一的。可以從 **VCAP_SERVICES** 環境變數取得這個資訊。如需相關資訊，請參閱[開始使用 {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}。

回應主體將類似下列 Snippet：

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

回應包括與新建的追蹤相關聯的唯一 ID。此外，還會指派唯一 ID 給每一個規則。endDate 指出追蹤何時停止收集訊息，而且必須符合 UTC 格式（`YYYY-MM-DD` 或 `YYYY-MM-DDTHH:MM:SSZ`）。type 內容必須指定為 **Rule** 或 **Aggregated**。因為此範例示範如何建立規則型追蹤，所以已指定 **Rule** 類型。

如果未在要求中指定 state 內容，則依預設會建立追蹤，而且其為 **Active**。name 是選用內容，不必是唯一的。若要更能管理您的過濾器，建議選取唯一的敘述性名稱。

如需規則語法的詳細資訊，請參閱 {{site.data.keyword.twittershort}} [查詢語言](twitter_rest_apis.html#querylanguage){: new.window}。

## 建立聚集的追蹤
{: #creating_aggregated_track}

作為「入門方案」使用者，您可以建立聚集的追蹤，結合兩個以上的現有追蹤。聚集的追蹤可同時包括規則型追蹤及其他聚集的追蹤。從聚集的追蹤中搜尋推文時，會從其組成的追蹤中傳回結果。若要建立聚集的追蹤，請利用 /api/v1/tracks 作業發出 **POST** 要求、指定追蹤類型 (**Aggregated**)，然後包括兩個以上的追蹤。下列 Snippet 是包括兩個追蹤的範例要求：

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
`username` 及 `password` 對您的應用程式及服務實例是唯一的。可以從 **VCAP_SERVICES** 環境變數取得這個資訊。如需相關資訊，請參閱[開始使用 {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}。回應主體將類似下列 Snippet：

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

回應包括與聚集的追蹤相關聯的唯一 ID。不同於規則型追蹤，聚集的追蹤不包括 endDate 或 state 內容，因為這些內容是在個別規則型追蹤內管理。

## 編輯追蹤
{: #editing_tracks}

可以編輯規則追蹤及聚集的追蹤，來精簡資料在 PowerTrack 串流中的過濾方式。在現有追蹤中新增（或修改）規則時，根據先前規則收到的訊息將持續保存在追蹤中。若要確保搜尋結果傳回最新規則集的資料，請刪除追蹤，並建立具有所需規則集的新追蹤。

[建立規則追蹤](#creating_rule_track){: new.window}中的範例包括兩個追蹤 ID 為 `66ff1961-51fe-4475-8bcd-c02f071d6fd1` 的規則。若要新增值為 "Champions" 的新規則，請使用 POST /api/v1/tracks/{track Id} 作業，並附加新規則。

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
同樣地，您可以發出 GET /api/v1/tracks/{track Id} 作業，從現有追蹤中移除規則，然後移除不需要的規則。

[建立聚集的追蹤](#creating_aggregated_track)中的範例包括兩項追蹤。您可以發出下列作業，將另一個 ID 為 `c4562594-1eeb-4a95-8fac-255428d74bce` 的追蹤新增至現有聚集的追蹤：

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

## 刪除追蹤
{: #deleting_tracks}

您可以發出 DELETE /api/v1/tracks/{trackId} 作業，刪除不再需要的追蹤。此動作同時適用於規則型追蹤及聚集的追蹤。直到從所有聚集的追蹤中移除追蹤後，才能刪除聚集的追蹤中包括的追蹤。下列範例示範如何刪除 ID 為 `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88` 的追蹤：

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

或者，您可以停止從特定追蹤中收集推文，方法是將其狀態變更為 Inactive。下列範例不會刪除追蹤，而是停用追蹤：

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## 搜尋推文
{: #searching_tweets}

您可以在應用程式中發出 GET 作業，以從任一資料串流中擷取推文。例如，搜尋 Decahose 推文會實作為：`/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`。對於「入門方案」使用者，從 PowerTrack 串流搜尋推文會實作為：`/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`。

"size" 參數指定要在查詢回應中傳回的訊息數目，而 "from" 參數則指出要在完整結果集中傳回的起始訊息。{trackId} 參照是特定追蹤的唯一 ID。您可以使用 cURL，搜尋 Decahose 串流，以取得包含 "IBM" 的推文，方法是鍵入：

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

對 PowerTrack 串流提交相同的查詢，將輸入如下：
 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

`username` 及 `password` 對您的應用程式及服務實例是唯一的。可以從 **VCAP_SERVICES** 環境變數取得這個資訊。如需相關資訊，請參閱[開始使用 {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}。

此服務會傳回 JSON 格式的回應。下表列出可能的回應碼。

| **HTTP 狀態碼** 	| **原因**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| 正常                                                               	|
| 400              	| 無效或遺漏要求有效負載內容。                   	|
| 401              	| 鑑別失敗。需要有效的使用者名稱及密碼。 	|
| 403              	| 禁止，已達限制。                                        	|
| 500              	| 發生內部錯誤。                                  	|

*表 1. 回應訊息*

回應主體可能顯示為：

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

下列 URL 編碼的查詢表示式會根據指定的時間範圍及出現次數擷取有關電影片推文。此範例可用來判定對電影預告的興趣或反應層次。

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

藉由解碼 URL，查詢語法及作業會成為 "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5"。

## 計算推文數目
{: #counting_tweets}

您可以在應用程式中套用 GET 作業，以擷取符合所指定查詢的推文數目。對 Decahose 的查詢發出為：`/api/v1/messages/count?q=QUERY`，而對 PowerTrack 串流的呼叫則使用下列格式： 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

您可以使用 cURL，在 Decahose 中尋找包含 "IBM" 的推文數目，方法是使用：

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

可對 PowerTrack 資料來源發出相同的查詢，如下所示： 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

`username` 及 `password` 對您的應用程式及服務實例是唯一的。可以從 **VCAP_SERVICES** 環境變數取得這個資訊。如需相關資訊，請參閱[開始使用 {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}。

此服務會傳回 JSON 格式的回應。下表列出可能的回應訊息。

| **HTTP 狀態碼** 	| **原因**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| 正常                                                               	|
| 400              	| 無效或遺漏要求有效負載內容。                   	|
| 401              	| 鑑別失敗。需要有效的使用者名稱及密碼。 	|
| 403              	| 禁止，已達限制。                                        	|
| 500              	| 發生內部錯誤。                                  	|

**表 2. 回應訊息**

回應主體可能顯示為：
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

下列查詢表示式會擷取同時含有 "IBM" 及 "Bluemix" 的正面推文數目。在此情況下，回應中會傳回來自 Decahose 的推文。

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

下列 URL 編碼的查詢表示式會擷取所指定期間且含有 "IBM" 的推文數目。此範例查詢可能有助於估計主題的熱門程度，並判定其趨勢。在此範例中，會傳回來自 PowerTrack 串流的推文。


`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

藉由解碼 URL，查詢語法及作業會成為 "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)"。
