---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# モバイル・ダッシュボードの新機能
{: #what_is_new}

### 最新情報: 2016 年 12 月
{: #dec-2016}

2016 年 12 月の {{site.data.keyword.Bluemix}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * 接続済みサービスをプロジェクトから削除することができます。これにより、そのサービスを削除したり別のプロジェクトで再使用したりすることができます。 
   * 既存のサービスをプロジェクトに追加することができます。
   * コード・スターターを使用する時に、既存の Cloudant NoSQL サービスをデータ・ソースとして作成したり接続したりできます。
   * サポートされている場合、既存の Object Storage サービスをプロジェクトのデータ・ソースとして作成したり接続したりできます。
   * UI スターターを使用して作成しているアプリのナビゲーション設計をカスタマイズできます。 
   

### 最新情報: 2016 年 11 月
{: #nov-2016}

2016 年 11 月の {{site.data.keyword.Bluemix}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * **「コード」**ページからプロジェクトの SDK 成果物を生成できるようになりました。
   * ベーシック・コード・スターターで Cordova がサポートされるようになりました。
   * {{site.data.keyword.mobileanalytics_short}} コンソールの**「ネットワーク要求 (Network Requests)」**ページで[ネットワーク・イベントの報告![外部リンク・アイコン ](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/sdk.html#network-requests "外部リンク・アイコン"){: new_window}および[ネットワーク・イベントのモニター![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "外部リンク・アイコン"){: new_window}を行えるようになりました。
   * {{site.data.keyword.mobileanalytics_short}} コンソールで [dashDB にデータをエクスポート![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "外部リンク・アイコン"){: new_window}できるようになりました。


### 最新情報: 2016 年 10 月
{: #oct-2016}

2016 年 10 月の {{site.data.keyword.Bluemix_notm}} モバイル・ダッシュボードの更新で、以下の変更が導入されました。

   * {{site.data.keyword.mobilepushshort}} 機能と Analytics 機能をダッシュボードから直接プロジェクトに追加できるようになりました。
   * [コード・スターター](starters.html#Code_Starter)が使用可能になりました。
   * コード・スターターから作成したプロジェクトに Authentication (認証) を追加できます。
   * Swift がサポートされるようになりました。


#### 分析
{: #analytics}

   * Analytics (分析) 機能を追加すると、デフォルトでデモ・モードが有効になります。デモ・モードをオフに切り替えることによって、アプリを実行した後に分析を表示できます。


#### UI ビルダー
{: #ui_builder}

   * **{{site.data.keyword.mobilepushshort}}** 機能には、プロジェクトからアクセスするようになりました。
   * **「プロジェクト設定」**タブは**「設定」**タブに名前変更されました。
   * **「認証」**タブは**「ユーザー・アクセス (User Access)」**タブに名前変更されました。


#### コード
{: #code}

   * iOS 向けの生成された Objective-C コードおよび Swift コードは、依存関係を管理するために CocoaPods を使用するようになりました。これは、CocoaPods をインストールする必要があることを意味します。インストールするには、`sudo gem install cocoapods` を実行します。CocoaPods がインストールされた後、`pod setup` を実行して構成します (まだ構成されていない場合)。最後に、`.xcworkspace` ファイルを Xcode で開く前に、`pod install` を実行して、必要なプロジェクト依存関係のダウンロードとインストールを行います。詳しい追加情報は、ダウンロードされたコード・アーカイブ内の `README.md` ファイルに入っています。詳しくは、[前提条件開発者ツール](get_code.html#prereq-dev-tools)をお読みください。

絶えず新しい更新を適用できるように、たびたび確認し直してください。
