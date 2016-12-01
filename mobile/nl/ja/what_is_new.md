---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# 「モバイル」ダッシュボードの新機能
{: #what_is_new}

{{site.data.keyword.Bluemix}} 「モバイル」ダッシュボードに関する 10 月の更新での変更内容は次のとおりです。

   * Push Notifications (プッシュ通知) 機能および Analytics (分析) 機能をプロジェクトにダッシュボードから直接追加できるようになりました。
   * [コード・スターター](starters.html#Code_Starter)が使用可能になりました。
   * コード・スターターから作成したプロジェクトに Authentication (認証) を追加できます。
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
