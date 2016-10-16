{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter の開始 {: #insights_twitter_overview}

*最終更新日: 2016 年 5 月 13 日*
{: .last-updated}

{{site.data.keyword.twitterfull}} を使用して、Twitter [Decahose](http://support.gnip.com/apis/firehose/overview.html){: new_window} または [PowerTrack](http://support.gnip.com/apis/powertrack/overview.html){: new_window} ストリームの Twitter の内容を {{site.data.keyword.Bluemix}} アプリケーションに組み込みます。
{:shortdesc}

{{site.data.keyword.twittershort}} の使用を開始するには、最初に、Liberty for Java などのランタイムを使用して Bluemix Web アプリケーションを作成し、次に、作成したアプリケーションに {{site.data.keyword.twittershort}} サービスを追加します。{{site.data.keyword.twittershort}} サービスがアプリケーションにバインドされると、サービス・インスタンスは固有の資格情報を使用してプロビジョンされます。アプリケーションは、REST API でこれらの資格情報を使用して、Twitter の内容を検索して取り込みます。VCAP_SERVICES から資格情報を取得して、サービス・インスタンスをアプリケーションと統合するには、以下の手順に従います。

1. アプリケーションの概要ページに移動します。
2. **「環境変数」**セクションに進みます。各サービスの `VCAP_SERVICES` 情報が表示されます。
3. {{site.data.keyword.twittershort}} サービスのユーザー名とパスワードの値をメモします。「REST API リファレンス」資料内の操作をテストするためには、これらの資格情報を入力する必要があります。例えば、`VCAP_SERVICES` は、以下のスニペットのようになります。

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

<!--
## Adding Insights for Twitter to your application {: #adding_twitter}

The following instructions guide you through the process of creating an application, binding the application to the {{site.data.keyword.twittershort}} service, and retrieving the service credentials to interact with REST API operations in the provided API reference documentation.

### Create an application
For demonstration purposes, you'll create an application using the Liberty for Java&trade;  runtime, but the general process described below can be applied to other runtimes. If you don't have an existing application, click **CREATE AN APP** in the dashboard. When asked to confirm the type of app, click **WEB**.

1. Open the **Catalog** menu.
2. From the **Runtimes** section, click **Liberty for Java**.
3. Click **Create**.
4. In the **App Name** field, specify the name of your app.
5. Click **Finish**. Wait for your application to provision.

### Add the Insights for Twitter service
Follow these steps to add the {{site.data.keyword.twittershort}} service to your app.

1. Open the **Catalog** menu.
2. From the **Data & Analytics** section, click the {{site.data.keyword.twittershort}} tile.
3. In the **App** field, select the name of your app.
4. Click **Create**.
5. When prompted, click **Restage** to restart your application.
-->

# 関連リンク
{: #rellinks}
## サンプル
{: #samples}
* [対話式 Decahose 検索デモ](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Decahose 検索デモのチュートリアルおよびソース・コード](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Analyzing "American Sniper" box office data (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights ハンズオン・ラボ](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
{: #api}
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## 互換性のあるランタイム
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## 一般
{: #general}
* [{{site.data.keyword.Bluemix_notm}} サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [アプリケーションへのサービスの追加](../reqnsi.html){: new_window}
* [エンドツーエンド開発](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 価格設定シート](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} の前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

