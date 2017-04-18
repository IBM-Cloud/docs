---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter の例
{: #examples}

{{site.data.keyword.twittershort}} サービスを開始するには、提供されているサンプルを使用して、サービスの利用方法を確認してください。
{: shortdesc}

## Insights for Twitter デモ
{: #insights_twitter_demo}

{{site.data.keyword.twittershort}} サービスを使用して Twitter データ・ストリームを検索するためのサンプル・アプリケーションが用意されています。サンプル・アプリケーションには、[https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window} に移動するとアクセスできます。このアプリケーションはブラウザー上で開き、**「Twitter Search」**ボタンと**「Twitter Count」** ボタンがある検索フィールドが表示されます。 

![検索フィールドが表示されたユーザー・インターフェースのイメージ。](images/sample1_UI.jpg "検索フィールドが表示されたユーザー・インターフェースのイメージ。")

サンプル・アプリケーションから、[『クエリー言語』](twitter_rest_apis.html#querylanguage){: new.window}に説明されているように、サポートされているパラメーターと演算子を使用してツイートを検索できます。例えば、「IBM Twitter」(ブール AND 演算を示すためのスペースを含む) と入力して**「Twitter Search」**をクリックすると、両方の用語を含むツイートが返されます。

![クエリー用語と返された検索結果のイメージ。](images/sample1_tweet_search.jpg "クエリー用語と返された検索結果のイメージ。")

検索フィールドに「IBM Twitter」と指定して**「Twitter Count」**をクリックすると、両方の用語を含むツイートの数が返されます。

![クエリー用語と返されたカウント結果のイメージ。](images/sample1_tweet_count.jpg "クエリー用語と返されたカウント結果のイメージ。")

## ルール・トラックの作成
{: #creating_rule_track}

エントリー・プラン・ユーザーとして、PowerTrack データ・ストリームに収集されているツイートをフィルタリングするルール・ベースのトラックを作成できます。後述のセクション内の例で、トラックの編集と削除の方法、および PowerTrack ストリームを対象にした検索またはカウント API 呼び出しの実行方法を示します。ルール・トラックを作成するには、/api/v1/tracks を指定した **POST** 要求命令を発行し、トラック・タイプ (**Rule**) を指定し、「EndDate」を指示し、少なくとも 1 つのルールを組み込みます。以下のスニペットは、2 つのルールを組み込んだ要求の例です。

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

`username` と `password` は、アプリケーションおよびサービス・インスタンスに固有です。この情報は、**VCAP_SERVICES** 環境変数から取得できます。詳細については、[『{{site.data.keyword.twittershort}} の開始』](index.html#insights_twitter_overview){: new.window}を参照してください。

応答の本文は、以下のスニペットと同様のものになります。

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

応答には、新しく作成されたトラックに関連付けられた固有の ID が含まれます。さらに、各ルールには固有の ID が割り当てられます。「endDate」は、トラックがメッセージの収集を停止する日時を示し、UTC 形式 (`YYYY-MM-DD` または `YYYY-MM-DDTHH:MM:SSZ`) に準拠している必要があります。「type」プロパティーは、**Rule** または **Aggregated** のいずれかを指定する必要があります。この例はルール・ベースのトラックの作成について示しているので、**Rule** タイプが指定さています。

「state」プロパティーが要求で指定されていない場合、トラックが作成され、デフォルトでは **Active** になります。「name」プロパティーはオプションであり、固有である必要はありません。フィルターをより適切に管理するには、固有の記述名を選択する
ことをお勧めします。

ルールの構文の詳細については、{{site.data.keyword.twittershort}} [『クエリー言語』](twitter_rest_apis.html#querylanguage){: new.window}を参照してください。

## 集計トラックの作成
{: #creating_aggregated_track}

エントリー・プラン・ユーザーとして、2 つ以上の既存のトラックを組み合わせる集計トラックを作成できます。集計トラックには、ルール・ベースのトラックと他の集計トラックの両方を含めることができます。集計トラックからのツイートの検索では、その構成要素のトラックからの結果が返されます。集計トラックを作成するには、/api/v1/tracks を指定した **POST** 要求命令を発行し、トラック・タイプ (**Aggregated**) を指定し、2 つ以上のトラック ID を組み込みます。以下のスニペットは、2 つのトラックを組み込んだ要求の例です。

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
`username` と `password` は、アプリケーションおよびサービス・インスタンスに固有です。この情報は、**VCAP_SERVICES** 環境変数から取得できます。詳細については、[『{{site.data.keyword.twittershort}} の開始』](index.html#insights_twitter_overview){: new.window}を参照してください。応答の本文は、以下のスニペットと同様のものになります。

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

応答には、集計トラックに関連付けられた固有の ID が含まれます。ルール・ベースのトラックとは異なり、集計トラックには「endDate」プロパティーと「state」プロパティーは含まれません。これらのプロパティーは、ルール・ベースの個々のトラック内で管理されるためです。

## トラックの編集
{: #editing_tracks}

ルール・トラックおよび集計トラックは、PowerTrack ストリームでデータがフィルタリングされる方法を調整するために編集できます。既存のトラックにルールを追加 (または変更) した場合、以前のルールに基づいて取得されたメッセージがトラック内に存続します。検索結果で最新のルール・セットのデータが返されるようにするには、トラックを削除し、必要なルール・セットを使用して新しいトラックを作成する必要があります。

[『ルール・トラックの作成』](#creating_rule_track){: new.window}の例には、2 つのルールとトラック ID の `66ff1961-51fe-4475-8bcd-c02f071d6fd1` が含まれています。「Champions」という値を含む新しいルールを追加するには、POST /api/v1/tracks/{track Id} 命令を使用して、新しいルールを追加します。

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
同様に、GET /api/v1/tracks/{track Id} 命令を発行して、既存のトラックからルールを削除し、不要なルールを削除することができます。
[『集計トラックの作成』](#creating_aggregated_track)の例には、2 つのトラックが含まれています。以下の命令を発行することにより、もう 1 つのトラック (ID が `c4562594-1eeb-4a95-8fac-255428d74bce`) を既存の集計トラックに追加できます。

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

## トラックの削除
{: #deleting_tracks}

DELETE /api/v1/tracks/{trackId} 命令を発行することにより、不要になったトラックを削除できます。このアクションは、ルール・ベースのトラックと集計トラック
の両方に適用できます。集計トラックに含まれるトラックは、すべての集計トラックから除去されるまで、削除できません。以下の例は、ID が `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88` であるトラックを削除する方法を示しています。

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

あるいは、状態を「Inactive」に変更することで、特定のトラックからのツイートの収集を停止することもできます。以下の例は、トラックを削除する代わりに、トラックを使用不可にします。

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## ツイートの検索
{: #searching_tweets}

アプリケーションで GET 命令を発行して、いずれのデータ・ストリームからもツイートを取得できます。例えば、Decahose ツイートの検索を実装するには、`/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER` のように指定します。エントリー・プランのユーザーの場合、PowerTrack ストリームからのツイートの検索を実装するには、`/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER` のように指定します。

「size」パラメーターはクエリー応答で返すメッセージの数を指定し、「from」パラメーターは完全な結果セットで返す初期メッセージを示します。{trackId} 参照は、特定のトラックの固有 ID です。
cURL を利用すると、次のように入力して、「IBM」を含むツイートの Decahose ストリームを検索できます。

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

PowerTrack ストリームに対する同じ照会のサブミットには、以下のように入力します。 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

`username` と `password` は、アプリケーションおよびサービス・インスタンスに固有です。この情報は、**VCAP_SERVICES** 環境変数から取得できます。詳細については、[『{{site.data.keyword.twittershort}} の開始』](index.html#insights_twitter_overview){: new.window}を参照してください。

サービスは、応答を JSON 形式で戻します。可能性のある応答コードは、次の表のとおりです。


| **HTTP ステータス・コード** 	| **理由**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| 要求ペイロード・プロパティーが無効または欠落しています。                   	|
| 401              	| 認証に失敗しました。有効なユーザー名とパスワードが必要です。 	|
| 403              	| アクセス禁止、限界に達しました。                                        	|
| 500              	| 内部エラーが発生しました。                                  	|

** 表 1. 応答メッセージ

応答の本文は、以下のようなものになります。

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

次の URL エンコードのクエリー式は、指定された時間フレームと出現回数に基づいて、映画に関するツイートを取得します。この例は、映画の予告編に対する関心や反応の度合いを判断するために利用できます。

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5
```

URL をデコードすると、クエリーの構文と演算は「(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5」となります。

## ツイート数のカウント
{: #counting_tweets}

アプリケーションに GET 命令を適用して、指定されたクエリーと一致するツイートの数を
        取得できます。Decahose へのクエリーは `/api/v1/messages/count?q=QUERY` として発行されます。一方、PowerTrack ストリームに対する呼び出しには、以下の形式を使用します。 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

cURL を利用すると、Decahose で次のように入力して、「IBM」を含むツイート数を検索できます。

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

以下のように、同じ照会を PowerTrack データ・ソースに対して発行できます。 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

`username` と `password` は、アプリケーションおよびサービス・インスタンスに固有です。この情報は、**VCAP_SERVICES** 環境変数から取得できます。詳細については、[『{{site.data.keyword.twittershort}} の開始』](index.html#insights_twitter_overview){: new.window}を参照してください。

サービスは、応答を JSON 形式で戻します。戻される可能性のある応答メッセージは、次の表のとおりです。


| **HTTP ステータス・コード** 	| **理由**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| 要求ペイロード・プロパティーが無効または欠落しています。                   	|
| 401              	| 認証に失敗しました。有効なユーザー名とパスワードが必要です。 	|
| 403              	| アクセス禁止、限界に達しました。                                        	|
| 500              	| 内部エラーが発生しました。                                  	|

**表 2. 応答メッセージ**

応答の本文は、以下のようなものになります。
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

次のクエリー式は、「IBM」と「Bluemix」の両方を含む肯定的なツイートの数を取得します。この場合、Decahose からのツイートが、応答で返されます。

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

次の URL エンコードのクエリー式は、指定された期間における「IBM」を含むツイートの数を取得します。このサンプル照会は、その題材の人気を評価し、
          それが話題になっているかどうかを判断するのに役立ちます。PowerTrack ストリームからのツイートが、
この例で返されます。


`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

URL をデコードすると、クエリーの構文と演算は「(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)」となります。
