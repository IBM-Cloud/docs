---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# 「モバイル」ダッシュボードの新機能
{: #what_is_new}

最終更新日: 2016 年 10 月 18 日
{: .last-updated}

{{site.data.keyword.Bluemix}} 「モバイル」ダッシュボードに関する 10 月の更新での変更内容は次のとおりです。

   * Push Notifications (プッシュ通知) 機能および Analytics (分析) 機能をプロジェクトにダッシュボードから直接追加できるようになりました。
   * [コード・スターター](starters.html#Code_Starter)が使用可能になりました。
   * Swift がサポートされるようになりました。


### 分析
{: #analytics}

   * Analytics (分析) 機能を追加すると、デフォルトでデモ・モードが有効になります。デモ・モードをオフに切り替えることによって、アプリを実行した後に分析を表示できます。


### UI ビルダー
{: #ui_builder}

   * **Push Notifications** 機能がプロジェクトからアクセスされるようになりました。
   * **「プロジェクト設定」**タブは**「設定」**タブに名前変更されました。
   * **「認証」**タブは**「ユーザー・アクセス (User Access)」**タブに名前変更されました。


### コード
{: #code}

   * iOS 向けの生成された Objective-C コードおよび Swift コードは、依存関係を管理するために CocoaPods を使用するようになりました。これは、CocoaPods をインストールする必要があることを意味します。インストールするには、`sudo gem install cocoapods` を実行します。CocoaPods がインストールされた後、`pod setup` を実行して構成します (まだ構成されていない場合)。最後に、`.xcworkspace` ファイルを Xcode で開く前に、`pod install` を実行して、必要なプロジェクト依存関係のダウンロードとインストールを行います。詳しい追加情報は、ダウンロードされたコード・アーカイブ内の `README.md` ファイルに入っています。詳しくは、[前提条件開発者ツール](get_code.html#prereq-dev-tools)をお読みください。

絶えず新しい更新を適用できるように、たびたび確認し直してください。


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
