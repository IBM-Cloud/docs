---

copyright:
  years: 2016
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# API 集約
{: #api_aggregation}

一部の {{site.data.keyword.weather_short}} API は集約することができます。集約を使用して、複数のアトミック API 呼び出しを結合して単一の HTTP 要求にすることができます。
{: shortdesc}

アトミック API 呼び出しは、集約の別名を定義している任意の API を参照します。API が集約可能である場合は、各 API のユーザー文書の URL 形式のセクションに、集約名の別名が含まれています。例えば、標準の毎日の予報の API には、集約された要求の一部として 10 日間の毎日の予報を取得するために使用できる
`v2fcstdaily10` という集約の別名があります。

集約には、次のような制限事項があります。

* 集約全体の圧縮解除された応答の合計サイズは、1 M バイト未満でなければなりません。
* URL の長さは、おおよそ 4,096 文字未満 (プロトコル、ホスト名、パス、およびクエリー・ストリングを含む) でなければなりません。
* アトミック API を最大 10 個まで集約できます。

**注:** 要求または応答がこれらの制限事項に 1 つでも違反している場合、HTTP 状況コード 500 の エラー応答を受け取ります (通常は 500 または 502 ですが、他のコードが返される可能性もあります)。

## 集約 API の URL
集約 API の URL は `/v2/aggregate/` で始まり、セミコロンで分離された別名が続きます。
例えば、10 日間の毎日の予報 API (`v2fcstdaily10`) を現在の観測
(`v2obscurrent`) と集約するには、次の形式を使用します。

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## アトミック API および集約のクエリー・パラメーターの規則
すべての要求でクエリー・パラメーターが必要です。集約のクエリー・パラメーターは、アトミック API 呼び出しと同じように渡されますが、いくつかの追加規則があります。以下のセクションでは、クエリー・パラメーターを適用してさまざまな集約を形成する方法を示します。

### すべてのアトミック API に適用されるクエリー・パラメーターの指定

集約の最も単純な形式は、クエリー・パラメーターがすべてのアトミック API に適用される場合です。この場合、クエリー・パラメーターは標準形式 `?param1=value1&amp;param2=value2` です。

次の例では、アトミック API `v2fcstdaily10` および `v2obscurrent` の要求に `geocode=31.44,84.33&amp;language=en&amp;units=e` を適用します。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### どのアトミック API がどのクエリー・パラメーターを受け取るかの指定

特定のアトミック API のパラメーターを指定する必要がある場合は、クエリー・パラメーターで位置表記法 `?R1.param1=value1&amp;R2.param2=value2` を使用できます。この形式では、最初のアトミック API に `param1` を使用し、2 番目のアトミック API に `param2` を使用します。

次の例では、`geocode=31.44,84.33&amp;language=en&amp;units=e` を `v2fcstdaily10` に、
また `geocode=44.44,50.23&amp;language=en&amp;units=e` を `v2obscurrent` に適用します。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### 特定のアトミック API に適用されるクエリー・パラメーターのグループ化

コンマ区切り形式 `?R1,R2.param1=value1&amp;param2=value2` の位置表記法を使用して、パラメーターをグループ化することができます。
この形式では、最初と 2 番目のアトミック API に `param1` を使用し、すべてのアトミック API に `param2` を使用します。

次の例では、`geocode=34.06,84.21&amp;language=enUS&amp;units=e` を `v2fcstdaily10` と `v2obscurrent` に適用します。それは `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` を `v2loc` に適用します。

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### 同じリソースのさまざまな方法での要求

同じリソースをさまざまな方法で (別の言語、別の計測単位など) 要求できます。この形式の場合、要求の中でアトミック API を繰り返すことが可能 (`/v2/aggregate/v2fcstdaily10;v2fcstdaily10` ) で、
パラメーターの位置表記法を使用して、どの方法でどの API を要求するかを指定できます (`?R1.param1=value1&amp;R2.param1=value2`)。この場合、ユーザーは、別の方法で形式設定または翻訳された同じリソースを受け取ります。

次の例では、`geocode=31.44,84.33&amp;language=en&amp;units=e` を最初の `v2fcstdaily10` に適用し、`geocode=31.44,84.33&amp;language=fr&amp;units=m` を 2 番目の `v2fcstdaily10` に適用します。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

次の例では、`geocode=31.44,84.33&amp;language=en&amp;units=e` を最初の `v2fcstdaily10` に適用し、`geocode=33.54,85.43&amp;language=en&amp;units=e` を 2 番目の `v2fcstdaily10` に適用して、
同じデータについて複数の位置を取得します。

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




