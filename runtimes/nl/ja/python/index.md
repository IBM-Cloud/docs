{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 12 日*

# Python ランタイム
{: #python_runtime}

{{site.data.keyword.Bluemix}} の Python ランタイムでは python_buildpack が採用されています。
python_buildpack は、Python アプリのための完全なランタイム環境を提供します。
{: shortdesc}

ご使用のアプリのルート・ディレクトリーに requirements.txt ファイルまたは setup.py ファイルが含まれている場合、python_buildpack が使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は Python スターター・アプリケーションです。Python スターター・アプリケーションは、ご使用のアプリに使用できるテンプレートを提供するシンプルな Python アプリです。このスターター・アプリを試し、{{site.data.keyword.Bluemix}} 環境に変更を加えてプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[「スターター・アプリケーションの使用 (Using the starter applications)」](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションのルートに置かれた runtime.txt ファイル内の python-versionnumber を設定することで、そのアプリが使用する Python のバージョンを指定することができます。例えば、次のとおりです。

```
python-3.4.3
```
{: codeblock}


### 使用可能なバージョン:
{: #available_versions}

{{site.data.keyword.Bluemix}} に現在インストールされている [Python ビルドパック](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)では、以下の Python のバージョンを使用できます。

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

ご使用のアプリケーションが必要とする Python のバージョンがリストにない場合は、外部の [Python ビルドパック](https://github.com/cloudfoundry/python-buildpack)を使用してアプリをデプロイできます。

## 関連リンク
{: #related_links}
* [Python 用 Cloud Foundry ビルドパック](https://github.com/cloudfoundry/python-buildpack)
