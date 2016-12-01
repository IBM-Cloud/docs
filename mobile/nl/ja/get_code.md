---

copyright:
  years: 2016
lastupdated: "2016-10-13"

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
* [Android Studio 2.2](https://developer.android.com/studio)
	* 最新の [Android 7.0](https://www.android.com/versions/nougat-7-0/) ランタイムをインストールしてください。

#### iOS
* [Xcode 8.0](https://developer.apple.com/xcode/) (推奨)
	* 最新の [iOS 10](http://www.apple.com/ios/ios-10/) ランタイムをインストールしてください。
* [Homebrew](http://brew.sh/)
	* 他のツールおよびランタイム (CocoaPods や Carthage など) のインストールを支援する、Apple 開発者向けのコマンド・ライン・ツール。
* iOS SDK 依存関係のインストールのための [CocoaPods](https://cocoapods.org/) 依存関係マネージャー。最新バージョンを使用してください。

	```
	$ sudo gem install cocoapods --pre
	```
* Watson Developer Cloud SDK のインストールのための [Carthage](https://github.com/Carthage/Carthage) 依存関係マネージャー。

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* API Connect Loopback およびその他の Bluemix 生産性向上ツールの実行を支援する NodeJS (Node および NPM ランタイム)。

	API Connect ツールをローカルで実行するには、Node 5.x を使用します。
	```
	$ brew install Node5
	```

* [Bluemix CLI ツール](http://clis.ng.bluemix.net/ui/home.html)。
Bluemix とのコマンド・ライン・インターフェースから簡単に Cloud Foundry ランタイムをデプロイするためのコマンド・ライン・ツール。  
