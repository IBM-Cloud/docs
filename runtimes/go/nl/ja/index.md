{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 12 日*

# Go ランタイム
{: #go_runtime}

{{site.data.keyword.Bluemix}} の Go ランタイムでは go_buildpack が採用されています。
go_buildpack は、Go アプリのための完全なランタイム環境を提供します。
{: shortdesc}

go_buildpack は、ご使用のアプリケーションに *.go という名前のファイルが含まれている場合に使用できます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は Go スターター・アプリケーションを提供します。Go スターター・アプリケーションは、ご使用のアプリに使用できるテンプレートを提供するシンプルな Go アプリです。このスターター・アプリを試し、Bluemix 環境に変更を加えてプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[「スターター・アプリケーションの使用 (Using the starter applications)」](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションのルートに置かれた Godeps/Godeps.json ファイル内の GoVersion プロパティーを設定することで、そのアプリが使用する Go のバージョンを指定することができます。例えば、次のとおりです。

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
詳細については、
『[godep](https://github.com/tools/godep)』を参照してください。

### 使用可能なバージョン:
{: #available_versions}

{{site.data.keyword.Bluemix}} に現在インストールされている [Go ビルドパック](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2)では、以下の Go のバージョンを使用できます。

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

ご使用のアプリが必要とする Go のバージョンがリストにない場合は、外部の
[Go ビルドパック](https://github.com/cloudfoundry/go-buildpack.git)を使用してアプリケーションをデプロイできます。

## 関連リンク
{: #related_links}
* [GoLang](http://golang.org/)
* [Go 用 Cloud Foundry ビルドパック](https://github.com/cloudfoundry/go-buildpack)
