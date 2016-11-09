---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# チュートリアル - Watson Language コード・スターター
{: #tutorial_watson_language}

最終更新日: 2016 年 10 月 13 日
{: .last-updated}

{{site.data.keyword.Bluemix}} モバイルの Watson Language コード・スターターは、Watson の Text to Speech (音声合成) サービスおよび Language Translation (言語翻訳) サービスを示し、各 {{site.data.keyword.Bluemix_notm}} モバイル・サービスの統合ポイントを提供します。


## 必要条件
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) アカウント
* [Bluemix カタログ](https://console.{DomainName}/catalog/)から取得した [Language Translator](https://console.{DomainName}/catalog/services/language-translator/) サービス・インスタンスおよび [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/) サービス・インスタンス


## 開始
{: #tutorial_gs}

Watson Language コード・スターターを使用して素早く稼働中にするには、以下のステップに従ってください。

1. {{site.data.keyword.Bluemix_notm}} 「モバイル」ダッシュボードでプロジェクトを作成します。

   1. 「モバイル」ダッシュボードの**「開始」**ページで**「プロジェクトの作成」**をクリックします。

      代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

   2. **「コード・スターター (Code Starters)」**をクリックします。

   3. **「Watson Language」**を選択し、**「プロジェクトの作成」**をクリックします。

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

5. アーカイブを解凍し、`README.md` ファイルを Markdown ビューアーで表示して、セットアップを完了してください。


## 次のタスク
{: #tutorial_next}

[試してみてください](http://new-console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}


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
* [ブログ投稿: Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.event.ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [ブログ投稿: Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [ブログ投稿: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## チュートリアルおよびサンプル
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
