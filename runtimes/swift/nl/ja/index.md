{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
最終更新日: 2016 年 9 月 19 日
{: .last-updated}

{{site.data.keyword.Bluemix}} 上の Runtime for Swift は、[IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) (つまり swift_buildpack) を採用しています。このビルドパックは、Swift アプリケーション用の完全なランタイム環境を提供します。
{: shortdesc}

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は、Kitura ベースの Swift [スターター・アプリケーション](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)を提供しています。Kitura スターター・アプリは単純な Swift アプリで、Swift プログラミング言語を使用して開発できるサーバー・アプリケーションのタイプについて学ぶのに使用します。このサンプル・アプリは、HTML のコンテンツをクライアントに返す基本的な Kitura HTTP サーバーを作成します。

**注:** Kitura スターター・アプリは、教育目的で使用することを意図しています。機能拡張するとスターター・アプリを試すことができ、その変更内容を {{site.data.keyword.Bluemix}} 環境にプッシュすることができます。スターター・アプリケーションの使用に役立つ情報については、[スターター・アプリケーションの使用](../../cfapps/starter_app_usage.html)を参照してください。

## アプリの名前変更
{: #renaming_your_app}

アプリの名前を Kitura Starter やさらに一般的な名前から変更する際には、以下のように変更を加える必要があります。こうすると、混同することがなくなり、エラーのないデプロイメントであることが保証されます。

- アプリのプロジェクト・フォルダーの名前を、アプリの名前と一致するように変更します。
- `Package.swift` - 以下のエントリーを変更します。
    - `name` - アプリの名前と一致している必要があります。
    - `targets[Target(name:)]` - アプリの名前と一致している必要があります。
- `manifest.yml` - 以下のエントリーを変更します。
    - `name` - アプリの名前と一致している必要があります。
    - `host` - アプリの URL の 1 次ホスト・セグメントを表します。
- `Procfile` - `web` の値がアプリのディレクトリー名と一致している必要があります。これは、コンパイル後に実行されて Web アプリを開始するコマンドです。


## ランタイム・バージョン
{: #runtime_versions}

デフォルトでは、{{site.data.keyword.Bluemix}} でホストされる Runtime for Swift (swift_buildpack) は、最新の GA バージョンの Swift バイナリーを使用します。このバージョンの Swift のみ IBM で直接サポートされており、アプリ内で使用することが推奨されています。swift_buildpack の[最新リリース情報](https://github.com/IBM-Swift/swift-buildpack/releases)を調べると、このサポートされているバージョンを判別できます。ビルドパックの [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) ファイル内に、その他の Swift バージョンがリストされている場合があります。これらの一般的であるにもかかわらずサポートされていないバージョンの Swift はビルドパック内に事前キャッシュされているので、プロビジョンの時間が短くなります。

{{site.data.keyword.Bluemix}} 上で別のバージョンの Swift をアプリケーションに使用する場合には、リポジトリーのルートにある `.swift-version` ファイルを使用してバージョンを指定できます。この `.swift-version` ファイルは、swift_buildpack で使用される Swift のバージョンを定義します。

```
$ cat .swift-version
3.0
```
{: pre}

Swift の言語は頻繁に更新されるので、必ず `.swift-version` ファイルを組み込んで、アプリケーションが正しく機能することが確認されている Swift バージョンにアプリを「ピン留め」できるようにする必要があります。

有効であればどのバージョンの Swift でも `.swift-version` ファイル内に指定できることに注意してください。それらの代替バージョンは、[Swift.org](https://swift.org/download/) の命名と一致していて、Swift.org から直接プルする必要があります。キャッシュされていないバージョンを使用すると多少プロビジョンに時間がかかりますが、Swift アプリのランタイム・パフォーマンスには違いはありません。

{{site.data.keyword.Bluemix}} 内のデフォルトの swift_buildpack は、アプリのルート・ディレクトリーに `Package.swift` ファイルが含まれている場合に使用されます。代替ビルドパックを使用する場合には、`buildpack: {buildpackUrl}` エントリーをアプリの manifest.yml ファイルに追加して、このビルドパックを指定する必要があります。または、デプロイメント時に `cf push -b {buildpackUrl}` コマンド引数を使用して、このビルドパックを定義できます。


## 開発者の環境

開発者が Swift を使用してサーバー・サイドのアプリケーションを作成する際には、複数のオプションがあります。Apple の MacOS デバイスの使用者は Xcode IDE を好むかもしれませんが、これは要件ではありません。{{site.data.keyword.Bluemix}} 上でデプロイされて実行される Swift ベースのアプリは、いずれのプログラミング編集機能や IDE も使用できます。多数の一般的なエディターで、Swift の構文の強調表示や lint を実行できます。[Swift.org](https://swift.org/) のバイナリーに含まれている Swift REPL コマンド・ライン・ツールを使用すると、{{site.data.keyword.Bluemix}} にデプロイメントする前にローカルでコンパイルしてテストできます。

MaxOS ユーザーの場合、[IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) を使用できます。これを使用すると、{{site.data.keyword.Bluemix}} 上で実行されるサーバー・サイドの Swift アプリの作成、デプロイメント、管理、制御が簡単になります。  


## 拡張統合

[Kitura Web フレームワーク](http://ibm-swift.github.io/Kitura/)を使って作業すると、多数の機能を得られます。Kitura は実質的にモジュラーで、パッケージ化された SDK を使用して機能を拡張し、認証、Watson ベースのサービスへのアクセス、広範な種類のデータベースなどのフィーチャーを提供できるようになります。Kitura は多数のデータベースのサポートを直接提供しますが、その他のオープン・ソースのプロジェクトも多数のデータベース・プラットフォーム用の SDK を提供します。Kitura で提供され、外部リソースを処理する SDK の一部を以下にリストします。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 と DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant と Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

アプリケーション内に組み込む Swift パッケージをさらに見つけるには、[IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) に進み、ターゲットのサービスかデータベースの検索を実行してください。この Package Catalog を利用すると、Swift アプリケーション内に組み込めるパッケージを簡単に見つけることができます。パッケージを Swift アプリケーションに追加するには、パッケージの Git URL とバージョンの詳細情報をアプリの `Package.swift` ファイル内に組み込みます。パッケージの管理について詳しくは、[Swift.org の「Package Manager」のセクション](https://swift.org/package-manager/)を参照してください。


## 関連情報

IBM から入手できる Swift 開発者用のオンライン・ツールは他にもあります。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - すべての IBM Swift 情報に関する主なランディング・サイト。弊社のオファリング、ブログ、ソーシャル･イベント、資料などに関する情報を見つけることができます。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - このサイトは、Swift コード・フラグメントをさまざまなバージョンの Swift に対して、さらにはさまざまな Swift ランタイム・プラットフォームに対しても即時かつ簡単にテストできる環境を提供します。また、コード・サンプルを保存して他者と共有したり、他者から提供された人気のある例を検討したりできます。


# RELLINK
{: #rellinks}
## 一般
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 資料と API](http://ibm-swift.github.io/Kitura/)
* [Bluemix 用 Kitura スターター・アプリ](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift リリース情報](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Swift 言語の資料](https://swift.org/documentation)
