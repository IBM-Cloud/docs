{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift ランタイム
{: #swift_runtime}
*最終更新日時: 2016 年 2 月 19 日*

{{site.data.keyword.Bluemix}} の Swift ランタイムには swift_buildpack が採用されています。
swift_buildpack は、Swift アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

swift_buildpack は、アプリケーションのルート・ディレクトリーに Package.swift ファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Swift スターター・アプリケーションが用意されています。Swift スターター・アプリケーションは、Swift プログラミング言語を使用して開発可能なサーバー・アプリケーションのタイプを確認するために使用できる、シンプルな Swiftアプリケーションです。このサンプル・アプリケーションは、HTML グリーティングをクライアントに返す基本的なサーバーを作成します。  

**注:** このスターター・アプリケーションは実動対応のアプリケーションではありません。教育目的での使用を意図されています。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

リポジトリーのルートにある `.swift`-version ファイルにより、アプリケーションで使用する Swift のバージョンを指定できます。

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Swift でサポートされる全バージョンのリストについては、ビルドパックの [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) ファイルを参照してください。

{{site.data.keyword.Bluemix}} にインストールされている Swift ビルドパックの現行バージョンについて詳しくは、ビルドパックの[リリース情報](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3)を参照してください。

Swift 言語は頻繁に変更されるため、アプリケーションが連携すると認識されている Swift バージョンにそのアプリケーションが「ピン留め」されるように、.swift-version ファイルを組み込む必要があります。

# 関連リンク
## 一般
* [Apple Swift buildpack for Cloud Foundry](https://github.com/cloudfoundry-community/swift-buildpack)
* [Swift 言語の資料](https://swift.org/)
