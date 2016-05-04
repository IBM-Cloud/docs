---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather 入門
{: #insights_weather_overview}

*最終更新日: 2016 年 4 月 6 日*

{{site.data.keyword.weatherfull}} を使用して、The Weather Company (TWC) からの気象データをご使用の {{site.data.keyword.Bluemix}} アプリケーションに取り込みます。
{:shortdesc}

以下の手順では、アプリケーションの作成、
Insights for Weather サービスへのアプリケーションのバインディング、
および [REST API](https://twcservice.{APPDomain}/rest-api/) と相互作用するためのサービス資格情報の取得のプロセスについて説明します。

### アプリケーションの作成
{: #create_an_app}

デモの目的で、Liberty for Java ランタイムを使用してアプリケーションを作成しますが、
以下の一般的なプロセスは、ほかのランタイムにも適用できます。


1. 既存のアプリケーションがない場合は、ダッシュボードの**「アプリの作成」**をクリックします。
2. アプリケーション・テンプレートを選択するように求められたら、**「WEB」**をクリックします。
3. スターターを選択するように求められたら、**「Liberty for Java」**をクリックします。
4. **「続行」**をクリックします。

5. **「アプリ」**フィールドに、アプリの名前を入力します。
6. **「完了」**をクリックします。アプリケーションのプロビジョンを待ちます。

### Insights for Weather サービスの追加
{: #add_insights_for_weather_service}

以下の手順に従って、Insights for Weather サービスをアプリに追加します。
1. **「カタログ」**メニューを開きます。
2. **「データと分析 (Data & Analytics)」**セクションで、**「Insights for Weather」**タイルをクリックします。
3. **「アプリ」**ドロップダウン・リストで、ご使用のアプリを選択します。
4. **「使用」**をクリックします。
5. プロンプトが出されたら、**「再ステージング (Restage)」**をクリックしてアプリケーションを再起動します。

### Insights for Weather 資格情報の取得
{: #retrieve_weather_credentials}

アプリケーションを Insights for Weather にバインドすると、固有の資格情報を使用して
サービス・インスタンスがプロビジョンされます。これらの資格情報は、アプリケーションの
`VCAP_SERVICES` に保存され、サービス間の相互作用のサポートに不可欠です。

1. アプリケーションの概要ページにナビゲートする
2. **「環境変数」**セクションに進みます。各サービスの `VCAP_SERVICES` 情報が表示されます。
3. Insights for Weather サービスの username 値と password 値をメモします。
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} を試行するには、
これらの資格情報をログインのプロンプトが出されたときに入力する必要があります。
`VCAP_SERVICES` は、以下の例のようになります。

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

# 関連リンク
## サンプル
* [Insights for Weather デモ](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights ハンズオン・ラボ](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## API
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 互換性のあるランタイム{:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 一般
* [Insights for Weather の概要](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [アプリケーションへのサービスの追加](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [エンドツーエンド開発](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 価格設定シート](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
