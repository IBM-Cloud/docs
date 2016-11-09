---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# チュートリアル - Weather コード・スターター
{: #tutorial_weather}

最終更新日: 2016 年 10 月 13 日
{: .last-updated}

{{site.data.keyword.Bluemix}} モバイルの Weather コード・スターターは、気象に関する作業を開始するためのスキャフォールド・プロジェクトを示します。これは、Swift を使用し、Push (プッシュ) および Analytics (分析) 統合ポイントを含んでいます。


## 必要条件
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) アカウント
* [Bluemix カタログ](https://console.{DomainName}/catalog/)から取得した [Weather Company Data](https://console.{DomainName}/catalog/services/weather-company-data/) サービス・インスタンス


## 開始
{: #tutorial_gs}

Weather コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} 「モバイル」ダッシュボードでプロジェクトを作成します。

   1. 「モバイル」ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「新規プロジェクト」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Weather」**を選択し、**「プロジェクトの作成」**をクリックします。

   4. プロジェクト名を入力し、**「作成」**をクリックします。

2. オプション: Push Notifications (プッシュ通知) を追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、**「Push Notifications」**に対して**「追加」**をクリックします。

      代替方法として、**「Push Notifications」**ページから**「作成」**をクリックすることもできます。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. iOS の場合、[Apple プッシュ通知サービスの構成](../services/mobilepush/t_push_provider_ios.html){: new_window}を行います。

   4. Android の場合、[Google クラウド・メッセージングの構成](../services/mobilepush/t_push_provider_android.html){: new_window}を行います。

3. オプション: その他のサービスを追加します。

   1. **「プロジェクト概要 (Project Overview)」**ページで、追加するサービスに対して**「追加」**をクリックします。

   2. サービス名を入力し、**「作成」**をクリックします。

   3. サービスの指示に従ってサービスをセットアップします。

4. プロジェクトをダウンロードします。

   1. **「コード」**をクリックし、優先言語を選択します。

   2. **「コードのダウンロード (Download Code)」**をクリックします。

5. アーカイブを解凍して、`README.md` ファイル内の指示に従います。


## 次のタスク
{: #tutorial_next}

[試してみてください](http://new-console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}


# 関連リンク
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## ブログ投稿
{: #general}
* [ブログ投稿: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## チュートリアルおよびサンプル
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
