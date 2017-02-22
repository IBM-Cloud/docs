---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# コードの取得
{: #Get_Code}

選択された機能を備えたモバイル・プロジェクトの構成とセットアップを完了した後、コードをダウンロードし、Xcode または Android Studio でコードを実行できます。ダウンロードしたプロジェクトは、構成した各機能に必要な SDK 依存関係と資格情報で事前構成済みです。

ダウンロードしたプロジェクト内で構成可能ではないサービスについては、資格情報の入力が必要になります。スターター・プロジェクトの `README.md` ファイルに指示が含まれています。`README.md` ファイルを Markdown ビューアーで表示して確認し、セットアップを完了してください。

### 前提条件開発者ツール
{: #prereq-dev-tools}

生成されたコードについての作業を {{site.data.keyword.Bluemix_notm}} 「モバイル」ダッシュボードから行うときには、以下の開発者ツールが必要です。

#### Android
* [Android Studio 2.2 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.android.com/studio "外部リンク・アイコン")
	* [Android 7.0 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.android.com/versions/nougat-7-0/ "外部リンク・アイコン")ランタイムをインストールします。

#### iOS
* [Xcode 8.0 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.apple.com/xcode/ "外部リンク・アイコン") (推奨)
	* 最新の [iOS 10 ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.apple.com/ios/ios-10/ "外部リンク・アイコン")ランタイムをインストールします。
* [Homebrew ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://brew.sh/ "外部リンク・アイコン")
	* 他のツールおよびランタイム (CocoaPods や Carthage など) のインストールを支援する、Apple 開発者向けのコマンド・ライン・ツール。
* iOS SDK 依存関係をインストールするための [CocoaPods ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://cocoapods.org/ "外部リンク・アイコン") の依存関係マネージャー。最新バージョンを使用してください。

	```
	$ sudo gem install cocoapods --pre
	```
* Watson Developer Cloud SDK をインストールするための [Carthage ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/Carthage/Carthage "外部リンク・アイコン")の依存関係マネージャー。

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* API Connect Loopback およびその他の Bluemix 生産性向上ツールの実行を支援する NodeJS (Node および NPM ランタイム)。

	API Connect ツールをローカルで実行するには、Node 5.x を使用します。
	```
	$ brew install Node5
	```

* [Bluemix CLI ツール![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](http://clis.ng.bluemix.net/ui/home.html "外部リンク・アイコン")。
Bluemix とのコマンド・ライン・インターフェースから簡単に Cloud Foundry ランタイムをデプロイするためのコマンド・ライン・ツール。  
