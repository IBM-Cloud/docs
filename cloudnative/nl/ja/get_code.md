---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# コードの取得
{: #Get_Code}

選択された機能でプロジェクトの構成とセットアップを完了したら、実行できるコードをダウンロードできます。ダウンロードしたプロジェクトは、構成した各機能に必要な SDK 依存関係と資格情報で事前構成済みです。

ダウンロードしたプロジェクト内で構成可能ではないサービスについては、資格情報の入力が必要になります。スターター・プロジェクトの `README.md` ファイルに指示が含まれています。`README.md` ファイルを Markdown ビューアーで表示して確認し、セットアップを完了してください。

## 前提条件開発者ツール
{: #prereq-dev-tools}

生成されたコードについての作業を {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} から行うときには、以下の開発者ツールが必要です。


### 一般
{: #general notoc}

* [Homebrew ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://brew.sh/)
	* 他のツールおよびランタイム (CocoaPods や Carthage など) のインストールを支援する、Apple 開発者向けのコマンド・ライン・ツール。

* [Docker ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.docker.com/get-docker)
	* コンテナーでのアプリケーションの実行およびデバッグを支援するオープン・ソース・プロジェクト。非モバイル・プロジェクトの場合にのみ必要です。

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* {{site.data.keyword.apiconnect_short}} Loopback およびその他の {{site.data.keyword.Bluemix_notm}} 生産性向上ツールの実行を支援する Node.js (Node および npm のランタイム)。

	{{site.data.keyword.apiconnect_short}} ツールをローカルで実行するには、Node 5.x を使用します。
	
	```
	$ brew install Node5
	```

* [Bluemix CLI ツール ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://clis.ng.bluemix.net/ui/home.html)

   {{site.data.keyword.Bluemix_notm}} とのコマンド・ライン・インターフェースから Cloud Foundry ランタイムをデプロイするためのコマンド・ライン・ツール。  

* [{{site.data.keyword.dev_cli_notm}} ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](dev_cli.html)

	Web およびモバイルのプロジェクトを作成、実行、テスト、およびデプロイするための {{site.data.keyword.Bluemix_notm}} CLI プラグイン。
	
* [SDK Generator プラグイン ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](sdk_cli.html)

	[Open API 仕様 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.openapis.org/) 準拠の REST API 定義から SDK を生成する {{site.data.keyword.Bluemix_notm}} CLI プラグイン。

### Android
{: #android notoc}

* [Android Studio 2.2 以上![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.android.com/studio)
	* 最新の [Android 7.0 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.android.com/versions/nougat-7-0/) ランタイムをインストールします。

### iOS
{: #ios notoc}

* [Xcode 8 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.apple.com/xcode/) (推奨)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* iOS SDK 依存関係をインストールするための [CocoaPods ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/) の依存関係マネージャー。最新バージョンを使用してください。

	```
	$ sudo gem install cocoapods --pre
	```
* {{site.data.keyword.watson}} Developer Cloud SDK をインストールするための [Carthage ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage) の依存関係マネージャー。

	```
	$ brew install carthage
	```
