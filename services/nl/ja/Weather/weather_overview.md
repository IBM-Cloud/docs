---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather の概要
{: #about_weather}

*最終更新日: 2016 年 5 月 19 日*

{{site.data.keyword.weatherfull}} を使用して、The Weather Company (TWC) からの気象データをご使用の {{site.data.keyword.Bluemix}} アプリケーションに取り込みます。
{:shortdesc}

[Insights for Weather REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} を使用して、{{site.data.keyword.Bluemix_notm}} アプリケーションに気象観測および予報を追加し、地理的位置によって指定されたエリアの気象データを表示することができます。
The Weather Company は、気象の履歴データおよび予測データの最も包括的なプロバイダーです。降水量、気圧、風、雷雨など、気象についてのあらゆる形式のデータを収集します。

REST API を使用すると、以下の情報を取得できます。

* 指定した地理的位置についての、現在時刻から次の 24 時間の毎時の天気予報。
* 指定した地理的位置についての、日中および夜間の区分の予報を含む、今後 10 日間の毎日の天気予報。この予報には、要求された言語での、その位置に適した計測単位を使用した、予報の説明テキスト・ストリング (256 文字以内) が含まれます。
* 指定した地理的位置についての、現在の観測気象データ。この気象データには、気温、降水量、風向と風速、湿度、気圧、露点、視程、および紫外線 (UV) 放射のデータが含まれます。
* 指定した地理的位置および時刻範囲についての、観測気象データ。このデータは物理的な観測所から供給されます。この API は、現在の条件の気象観測および前の 24 時間以内の過去の観測を返します。

The Weather Company の天気の表現およびアイコンについて詳しくは、[Icon Code, Phrases and Images](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window} を参照してください。アプリで使用するために、[アイコンのセットをダウンロードする](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window}こともできます。

## 価格設定モデル
{: #pricing_models}

価格設定モデルは、毎日の Insights for Weather API の呼び出し回数に基づいており、お客様への課金は月単位です。任意の地理的地域、予報タイプ、または時系列の観測について、呼び出し回数だけを制限して、アプリケーション内で気象データをテストできます。無料、基本、およびプレミアムの各プランは、契約せずに購入することができます。これらのプランでは、アプリケーションでそれぞれ 1 日 500 回、5,000 回、または 50,000 回の API 呼び出しを実行できます。

請求期間中にデプロイされる各サービス・インスタンスに対して複数のプレミアム・プランを購入することもできます。アプリケーションで使用する呼び出し回数が 1 日当たり 50,000 回または 1 分当たり 1,000 回を超える場合は、サービスの継続的提供について IBM と契約する必要があります。

選択したプランに基づいて実行を許可される API 呼び出しの制限にアプリケーションが達した場合、それ以降の API 呼び出しは、アプリケーションで追加の API 呼び出し要求を許可されるまで成功しません。

例えば、基本プランを利用している場合に、プランの制限を超えるにもかかわらずアプリケーションで 1 分に 500 回の API 呼び出しを実行できますが、次の API 呼び出しは 5 分後まで許可されません。そのため、ユーザーはアプリケーションの気象データの更新に遅延を感じる可能性があります。
これらの制限に対処するようにアプリケーションを開発し、API 呼び出しを無制限に要求しないようにする必要があります。代わりに、アプリの API 呼び出しの使用状況をモニターできます。API 呼び出しにより返された項目の数をチェックすることで、アプリケーションがプランの制限に達しているかどうかを検証できます。

## フィードバックとサポート
{: #feedback_support}

Insights for Weather を使用するアプリの作成方法について技術的な質問がある場合は、[Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window} に質問を投稿し、
質問に **bluemix** と **weather** のタグを付けてください。

このサービスに関して問題がある場合は、[IBM developerWorks Answers フォーラム](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}をご利用ください。
**insights-weather** タグや **bluemix** タグを含めると、IBM からより良いサポートをご提供できます。

Bluemix の問題を解決するための情報は、[トラブルシューティング](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}を参照してください。
フォーラムを介して情報を探したり質問する方法、サポートに連絡する方法について詳しくは、[お客様サポートの利用](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}を参照してください。
