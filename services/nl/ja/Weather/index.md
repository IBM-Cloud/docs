---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather 概説
{: #insights_weather_overview}

*最終更新日: 2016 年 5 月 19 日*

{{site.data.keyword.weatherfull}} を使用して、The Weather Company (TWC) からの気象データをご使用の {{site.data.keyword.Bluemix}} アプリケーションに取り込みます。
{:shortdesc}

**注意:** 現在、日本では Insights for Weather サービス をご使用いただけません。 

始める前に、Liberty for Java などのランタイムでダッシュボードに {{site.data.keyword.Bluemix_notm}} Web アプリを作成します。アプリがプロビジョンされた後、以下の手順に従って、Insights for Weather サービスをアプリに追加します。

アプリを Insights for Weather にバインドすると、固有の資格情報を使用して
サービス・インスタンスがプロビジョンされます。アプリはこれらの資格情報を
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} と一緒に使用して、気象データを取得します。

以下のステップに従って、`VCAP_SERVICES` から資格情報を取得し、アプリにサービス・インスタンスを統合します。

1. アプリケーションの概要ページにナビゲートする
2. **「環境変数」**セクションに進みます。各サービスの `VCAP_SERVICES` 情報が表示されます。
3. Insights for Weather サービスのユーザー名とパスワードの値をメモします。
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window} を試行するには、
ログインのプロンプトが出されたときにこれらの資格情報を入力する必要があります。
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

**注:** 地域はそれぞれ独立しています。ある地域でユーザーにプロビジョンされたサービス資格情報を、別の地域でサービスに対する認証のために使用することはできません。正しい資格情報が入力されないと、応答本文に「無許可 (Unauthorized)」というメッセージが表示されます。 

# 関連リンク
{: #rellinks}
## サンプル
{: #samples}
* [Insights for Weather デモ](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights ハンズオン・ラボ](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

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
* [アプリケーションへのサービスの追加](../reqnsi.html){: new_window}
* [エンドツーエンド開発](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 価格設定シート](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
