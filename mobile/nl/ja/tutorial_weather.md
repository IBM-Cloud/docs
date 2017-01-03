---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# チュートリアル - Weather コード・スターター
{: #tutorial_weather}

{{site.data.keyword.Bluemix}} モバイルの Weather コード・スターターは、気象に関する作業を開始するためのスキャフォールド・プロジェクトを示します。これは、Swift を使用し、Push (プッシュ) および Analytics (分析) 統合ポイントを含んでいます。


## 必要条件
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) アカウント
* [Bluemix カタログ](https://console.{DomainName}/catalog/)から取得した [Weather Company Data](https://console.{DomainName}/catalog/services/weather-company-data/) サービス・インスタンス


## 開始
{: #tutorial_gs}

Weather コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} でモバイル・ダッシュボード・プロジェクトを作成します。

   1. モバイル・ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「新規プロジェクト」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Weather」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力し、**「作成」**をクリックします。

2. オプション: Push Notifications (プッシュ通知) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、**「Push Notifications」**に対して**「追加」**をクリックします。

      代替方法として、**「Push Notifications」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. iOS の場合、[Apple プッシュ通知サービスの構成](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}を行います。

   4. Android の場合、[Google クラウド・メッセージングの構成](/docs/services/mobilepush/t_push_provider_android.html){: new_window}を行います。
   
3. オプション: Analytics (分析) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Analytics (分析)」**に対して**「追加」**をクリックします。

      代替方法として、**「Analytics (分析)」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. アプリを実行した後、**「デモ・モード」**をオフに切り替えて、分析データを確認できます。

4. オプション: Authentication (認証) 機能を追加します。

   1. **「プロジェクト概要 (Project Overview)」** ページで、**「Authentication (認証)」**に対して**「追加」**をクリックします。

      代替方法として、**「Authentication (認証)」**ページから**「作成」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。
   
   3. **「Authentication (認証)」**をオンに切り替えます。
   
   4. ID プロバイダーを選択し、必要な情報を入力して構成します。ID プロバイダーは 1 つだけ有効にすることができます。

   5. 認証の構成については、[Mobile Client Access 概説](/docs/services/mobileaccess/index.html){: new_window}を参照してください。

5. プロジェクトをダウンロードします。

   1. **「コード」**をクリックし、優先言語を選択します。

   2. **「コードのダウンロード (Download Code)」**をクリックします。

5. アーカイブを解凍して、`README.md` ファイル内の指示に従います。


## 次のタスク
{: #tutorial_next}

[試してみてください](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}
