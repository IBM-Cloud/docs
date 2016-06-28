{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift ランタイム
{: #swift_runtime}
*最終更新日時: 2016 年 6 月 10 日*
{: .last-updated}

{{site.data.keyword.Bluemix}} の Swift ランタイムには、Swift buildpack for Bluemix (つまり、swift_buildpack) が採用されています。
swift_buildpack は、Swift アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

swift_buildpack は、アプリケーションのルート・ディレクトリーに Package.swift ファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Swift スターター・アプリケーションが用意されています。Swift スターター・アプリケーションは、Swift プログラミング言語を使用して開発可能なサーバー・アプリケーションのタイプを確認するために使用できる、シンプルな Swiftアプリケーションです。このサンプル・アプリケーションは、HTML コンテンツをクライアントに返す、基本的な HTTP サーバーを作成します。

**注:** このスターター・アプリケーションは実動対応のアプリケーションではありません。教育目的での使用を意図されています。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

Bluemix にインストールされた swift_buildpack は、Swift バイナリーの `DEVELOPMENT-SNAPSHOT-2016-05-03-a` バージョンをサポートします。アプリケーション用に Bluemix 上で別のバージョンの Swift を使用する場合は、リポジトリーのルートにある `.swift-version` ファイルを使用して、バージョンを指定できます。

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

`.swift-version` ファイルを組み込むことに加えて、以下に示すように、`cf push` コマンドに `-b https://github.com/IBM-Swift/swift-buildpack` パラメーターを追加することも必要です。

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Swift でサポートされる全バージョンのリストについては、ビルドパックの [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) ファイルを参照してください。

{{site.data.keyword.Bluemix}} にインストールされている Swift ビルドパックの現行バージョンについて詳しくは、ビルドパックの[リリース情報](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1)を参照してください。

Swift 言語は頻繁に変更されるため、連携することが分かっている Swift バージョンにアプリケーションを「ピン留め」するために、`.swift-version` ファイルを組み込む必要があります。`DEVELOPMENT-SNAPSHOT-2016-05-03-a` 以外の Swift バージョンを使用する場合は、アプリケーションをプッシュするときに `-b https://github.com/IBM-Swift/swift-buildpack` パラメーターを指定する必要があることにも注意してください (上記を参照)。

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Swift buildpack for Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* [Swift 言語の資料](https://swift.org/)
