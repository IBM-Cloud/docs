---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} の新機能
{: #what-is-new}


## 最新情報: 2017 年 3 月
{: #mar-2017}

2017 年 3 月の {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} の更新で、以下の変更が導入されました。

   * {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードが {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} になりました。
   * プロジェクト作成の設計が変更され、Node.js、Java、および Swift のサポートとともに、Web アプリ、BFF、およびマイクロサービスのサーバー・パターン・タイプが組み込まれました。
   * 新規および改良された {{site.data.keyword.appid_full}} サービスとの統合により、モバイルおよび Web プロジェクトの認証が行われます。
   * [SDK Generator プラグイン](sdk_cli.html)を使用して、プロジェクトに SDK を追加で生成できるようになりました。{{site.data.keyword.dev_console}} での SDK の生成は、モバイル・プロジェクトにのみ可能です。
   * [{{site.data.keyword.dev_cli_short}}](dev_cli.html) を使用してプロジェクトを追加で作成できるようになりました。


## 最新情報: 2017 年 1 月
{: #jan-2017}

2017 年 1 月の {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * 1 月 31 日時点で、UI スターターは非推奨になりました。UI スターターから作成された既存のプロジェクトは、2017 年 4 月 30 日まで使用できます。マイグレーション・ステップと削除の日付について詳しくは、[非推奨の告知に関するブログ投稿![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/) を参照してください。
{: deprecated}
   * プロジェクトを削除して新しいプロジェクトを作成する代わりに、プロジェクト・スターター・タイプを更新できるようになりました。
   * [Watson Conversation](tutorial_conversation.html) コード・スターターを使用してプロジェクトを作成できるようになりました。
   * サポートされている場合、プロジェクトの SDK を生成できるようになりました。
   * 既存の[コンピュート](sdk_compute.html)・インスタンスを追加し、クライアント SDK を生成してプロジェクトに追加できるようになりました。


## 最新情報: 2016 年 12 月
{: #dec-2016}

2016 年 12 月の {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * 接続済みサービスをプロジェクトから削除できるようになりました。これにより、そのサービスを削除したり別のプロジェクトで再使用したりすることが可能になりました。 
   * 既存のサービスをプロジェクトに追加できるようになりました。
   * コード・スターターを使用する時に、既存の Cloudant NoSQL サービスをデータ・ソースとして作成したり接続したりできるようになりました。
   * サポートされている場合、既存の Object Storage サービスをプロジェクトのデータ・ソースとして作成したり接続したりできるようになりました。
   * UI スターターを使用して作成しているアプリのナビゲーション設計をカスタマイズできるようになりました。 
   

## 最新情報: 2016 年 11 月
{: #nov-2016}

2016 年 11 月の {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * **「コード」**ページからプロジェクトの SDK 成果物を生成できるようになりました。
   * ベーシック・コード・スターターで Cordova がサポートされるようになりました。
   * {{site.data.keyword.mobileanalytics_short}} コンソールの**「ネットワーク要求」**ページで[ネットワーク・イベントの報告 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} と[ネットワーク要求のモニター ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} を行えるようになりました。
   * {{site.data.keyword.mobileanalytics_short}} コンソールで[データを dashDB にエクスポート ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} できるようになりました。


## 最新情報: 2016 年 10 月
{: #oct-2016}

2016 年 10 月の {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * {{site.data.keyword.mobilepushshort}} 機能と Analytics 機能をダッシュボードから直接プロジェクトに追加できるようになりました。
   * [コード・スターター](starters.html#Code_Starter)が使用可能になりました。
   * コード・スターターから作成したプロジェクトに Authentication (認証) を追加できます。
   * Swift がサポートされるようになりました。


### 分析
{: #analytics notoc}

   * Analytics (分析) 機能を追加すると、デフォルトでデモ・モードが有効になります。デモ・モードをオフに切り替えることによって、アプリを実行した後に分析を表示できます。


### UI ビルダー
{: #ui_builder notoc}

   * **{{site.data.keyword.mobilepushshort}}** 機能には、プロジェクトからアクセスするようになりました。
   * **「プロジェクト設定」**タブは**「設定」**タブに名前変更されました。
   * **「認証」**タブは**「ユーザー・アクセス (User Access)」**タブに名前変更されました。


### コード
{: #code notoc}

   * iOS 向けの生成された Objective-C コードおよび Swift コードは、依存関係を管理するために CocoaPods を使用するようになりました。これは、CocoaPods をインストールする必要があることを意味します。インストールするには、`sudo gem install cocoapods` を実行します。CocoaPods がインストールされた後、`pod setup` を実行して構成します (まだ構成されていない場合)。最後に、`.xcworkspace` ファイルを Xcode で開く前に、`pod install` を実行して、必要なプロジェクト依存関係のダウンロードとインストールを行います。詳しい追加情報は、ダウンロードされたコード・アーカイブ内の `README.md` ファイルに入っています。詳しくは、[前提条件開発者ツール](get_code.html#prereq-dev-tools)をお読みください。

絶えず新しい更新を適用できるように、たびたび確認し直してください。
