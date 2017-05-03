---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

{{site.data.keyword.Bluemix}} 上の Runtime for Swift には、[IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) (つまり、swift_buildpack) が採用されています。
このビルドパックは、Swift アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Kitura ベースの Swift [スターター・アプリケーション](https://github.com/IBM-Bluemix/Kitura-Starter)が用意されています。Kitura スターター・アプリケーションは、Swift プログラミング言語を使用して開発可能なサーバー・アプリケーションのタイプを確認するために使用できる、シンプルな Swift アプリケーションです。このサンプル・アプリケーションは、HTML コンテンツをクライアントに返す、基本的な Kitura HTTP サーバーを作成します。

**注:** Kitura スターター・アプリケーションは、教育目的での使用を意図しています。機能拡張を行ってスターター・アプリケーションを試し、これらの変更を {{site.data.keyword.Bluemix}} 環境に対してプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## アプリケーションの名前変更
{: #renaming_your_app}

Kitura スターターから、またはより一般的な方法で、アプリケーションの名前を変更する場合は、対処する必要のある変更がいくつかあります。これによって混乱を避けることができ、さらに確実にエラーのないデプロイメントを実現できます。

- アプリケーションのプロジェクト・フォルダーの名前を、アプリケーションの名前と一致するように変更します。
- `Package.swift` - 次のエントリーを変更します。
    - `name` - アプリケーションの名前と一致している必要があります。
    - `targets[Target(name:)]` - アプリケーションの名前と一致している必要があります。
- `manifest.yml` - 次のエントリーを変更します。
    - `name` - アプリケーションの名前と一致している必要があります。
    - `command` - アプリケーションを開始する実行可能ファイルの名前 (Package.swift ファイルに指定した名前と一致している必要があります)。

## ランタイム・バージョン
{: #runtime_versions}

デフォルトでは、{{site.data.keyword.Bluemix}} 上でホストされる Runtime for Swift (swift_buildpack) は、最新の GA バージョンの Swift バイナリーを使用します。これは、IBM によって直接サポートされる唯一のバージョンの Swift であり、アプリケーションで使用するために推奨されるバージョンです。swift_buildpack の[最新のリリース情報](https://github.com/IBM-Swift/swift-buildpack/releases)を確認することで、このサポートされるバージョンを判別することができます。ビルドパックには、その [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) ファイル内に示されているように、他の Swift バージョンがリストされることがあります。これらの一般的であるにもかかわらずサポートされていないバージョンの Swift はビルドパック内に事前キャッシュされているので、プロビジョンの時間が短くなります。

アプリケーション用に {{site.data.keyword.Bluemix}} 上で別のバージョンの Swift を使用する場合は、リポジトリーのルートにある `.swift-version` ファイルを使用して、バージョンを指定できます。この `.swift-version` ファイルは、swift_buildpack によって使用される Swift バージョンを定義します。

```
$ cat .swift-version
3.0
```
{: pre}

Swift 言語は頻繁に更新されるため、連携して動くことがわかっている Swift バージョンにアプリケーションが「ピン留め」されるように、常に `.swift-version` ファイルを組み込む必要があります。

有効であればどのバージョンの Swift でも `.swift-version` ファイル内に指定できることに注意してください。これらの代替バージョンは、[Swift.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/download/) の命名と一致する必要があり、Swift.org から直接取得されます。非キャッシュ・バージョンを使用するとプロビジョンに少し時間がかかりますが、Swift アプリケーションのランタイム・パフォーマンスに相違はありません。

{{site.data.keyword.Bluemix}} のデフォルトの swift_buildpack は、アプリケーションのルート・ディレクトリーに `Package.swift` ファイルが含まれている場合に使用されます。代替のビルドパックを使用する場合は、`buildpack: {buildpackUrl}` エントリーをアプリケーションの manifest.yml ファイルに追加することでこれを指定する必要があります。または、デプロイメント時に `cf push -b {buildpackUrl}` コマンド引数を使用してこれを定義することができます。


## 開発者環境

開発者には、Swift を使用してサーバー・サイド・アプリケーションを作成するときにいくつかのオプションがあります。Apple の MacOS デバイスを使用する開発者は Xcode IDE を使用できますが、これは要件ではありません。{{site.data.keyword.Bluemix}} でデプロイおよび実行される Swift ベースのアプリケーションは、任意のプログラミング編集機能や IDE を使用できます。多くの一般的な編集機能では、Swift の構文の強調表示と lint 機能を使用できます。[Swift.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/) のバイナリーに組み込まれている Swift REPL コマンド・ライン・ツールを使用すると、{{site.data.keyword.Bluemix}} にデプロイする前に、ローカルでコンパイルとテストを行うことができます。

MaxOS ユーザーは、{{site.data.keyword.Bluemix}} で実行されるサーバー・サイドの Swift アプリケーションの作成、デプロイメント、管理、および制御を単純化する [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) を使用することができます。  


## 拡張された統合

[Kitura Web フレームワーク](http://ibm-swift.github.io/Kitura/)との連携により、多数の機能が提供されます。Kitura は実際にはモジュラーであるため、認証、Watson ベースのサービスへのアクセス、さまざまなデータベースなどのフィーチャーを提供するために、パッケージされた SDK を使用してすぐにその機能を拡張する必要が生じます。Kitura は多数のデータベースのサポートを直接提供しますが、その他のオープン・ソースのプロジェクトも多くのデータベース・プラットフォーム用の SDK を提供しています。Kitura で提供され、外部リソースを処理する SDK の一部を以下にリストします。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 および DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant および CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

アプリケーションに含める他の Swift パッケージを見つけるには、[IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) にアクセスして、ターゲット・サービスまたはデータベースで検索を実行します。Package Catalog は、Swift アプリケーションに含めることができるパッケージを簡単に見つける方法を提供します。パッケージは、パッケージの Git URL とバージョンの詳細をアプリケーションの `Package.swift` ファイルに含めることで Swift アプリケーションに追加することができます。パッケージ管理の詳細については、[Swift.org の『Package Manager』セクション](https://swift.org/package-manager/)を参照してください。


## 関連情報

Swift 開発者用のその他のオンライン・ツールも IBM から入手できます。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - すべての IBM Swift 情報の主なランディング・サイト。オファリング、ブログ、ソーシャル・イベント、資料などに関する情報を見つけることができます。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - このサイトは、さまざまなバージョンの Swift や場合によっては異なる Swift ランタイム・プラットフォームに対して、Swift コード・フラグメントを迅速かつ簡単にテストするための環境を提供します。コード・サンプルを保存して他のユーザーと共有したり、他のユーザーから提供された人気のあるサンプルを探索したりすることもできます。


# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura の資料および API](http://ibm-swift.github.io/Kitura/)
* [Bluemix 用の Kitura スターター・アプリケーション](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift リリース情報](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/)
* [Swift 言語の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://swift.org/documentation)
