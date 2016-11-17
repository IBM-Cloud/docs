---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}} 概説
{: #insights_weather_overview}

{{site.data.keyword.weatherfull}} を使用して、The Weather Company (TWC) からの気象データをご使用の {{site.data.keyword.Bluemix}} アプリケーションに取り込みます。
{:shortdesc}

**重要:** 現在、次の国または地域では、{{site.data.keyword.weather_short}} サービスを購入および使用**いただけない**場合があります。アフガニスタン、アルメニア、アゼルバイジャン、バーレーン、バングラデシュ、ブータン、ブルネイ、カンボジア、中国、キプロス、ジョージア、インドネシア、イラン、イラク、日本、ヨルダン、カザフスタン、クウェート、キルギス、ラオス、レバノン、マレーシア、モルジブ、モンゴル、ミャンマー、ネパール、オマーン、パキスタン、フィリピン、カタール、ロシア、サウジアラビア、シンガポール、韓国、スリランカ、シリア、タジキスタン、東ティモール、トルコ、トルクメニスタン、アラブ首長国連邦、ウズベキスタン、ベトナム、イエメン。このリストは、追加情報があったときに更新されます。

[Insights for Weather サービス](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window}を使用する既存のアプリケーションがある場合は、そのアプリは、{{site.data.keyword.weather_short}} の導入後 90 日間、変更なしで動作し続けます。新規追加された API および改善された価格設定モデルを利用するには、アプリケーションを新しいサービスにマイグレーションできます。

始める前に、Liberty for Java などのランタイムでダッシュボードに {{site.data.keyword.Bluemix_notm}} Web アプリを作成します。アプリがプロビジョンされるまで待機してから、{{site.data.keyword.weather_short}} サービスをアプリに追加します。

アプリを {{site.data.keyword.weather_short}} にバインドすると、固有の資格情報を使用してサービス・インスタンスにプロビジョンされます。アプリはこれらの資格情報を
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} と一緒に使用して、気象データを取得します。

以下のステップに従って、`VCAP_SERVICES` からサービス資格情報を取得し、アプリにサービス・インスタンスを統合します。

1. アプリケーションの概要ページにナビゲートする
2. **「環境変数」**セクションに進みます。各サービスの `VCAP_SERVICES` 情報が表示されます。
3. {{site.data.keyword.weather_short}} サービスのユーザー名とパスワードの値をメモします。
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} を試行するには、
ログインのプロンプトが出されたときにこれらの資格情報を入力する必要があります。
`VCAP_SERVICES` は、以下の例のようになります。

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**注:** 地域はそれぞれ独立しています。ある地域でユーザーにプロビジョンされたサービス資格情報を、別の地域でサービスに対する認証のために使用することはできません。正しい資格情報が入力されないと、応答本文に*「無許可 (Unauthorized)」*というメッセージが表示されます。

# 関連リンク
{: #rellinks}
## サンプル
{: #samples}
* [{{site.data.keyword.weather_short}} デモ・アプリ](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} Deep Dive のビデオ](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights ハンズオン・ラボ](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather サンプル・アプリ](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data, and Insights for Weather (YouTube でのチュートリアル)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

## API
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 互換性のあるランタイム
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般
{: #general}
* [アプリケーションへのサービスの追加](/docs/services/reqnsi.html){: new_window}
* [エンドツーエンド開発](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 価格設定シート](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
