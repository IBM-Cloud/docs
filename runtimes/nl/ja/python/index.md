---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Python
{: #python_runtime}
*最終更新日時: 2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} の Python ランタイムには python_buildpack が採用されています。
python_buildpack は、Python アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

python_buildpack は、アプリケーションのルート・ディレクトリーに requirements.txt ファイルまたは setup.py ファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Python スターター・アプリケーションが用意されています。Python スターター・アプリケーションは、アプリケーションに使用できるテンプレートを提供する、シンプルな Python アプリケーションです。スターター・アプリケーションを試し、{{site.data.keyword.Bluemix}} 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

## ランタイム・バージョン
{: #runtime_versions}

アプリケーションのルートにある runtime.txt ファイルで python-versionnumber を設定することにより、アプリケーションで使用する Python のバージョンを指定できます。例えば、次のように指定します。

```
python-3.4.3
```
{: codeblock}

バージョンを指定しない場合は、デフォルトでバージョン 2.7.10 が選択されます。

### 使用可能なバージョン:
{: #available_versions}

現在 {{site.data.keyword.Bluemix}} にインストールされている [Python ビルドパック](https://github.com/cloudfoundry/python-buildpack/releases/tag/v1.5.1)では、以下の Python バージョンが使用できます。

* 2.7.9
* 2.7.10
* 3.3.5
* 3.3.6
* 3.4.2
* 3.4.3
* 3.5.0

アプリケーションが、リストされていない Python バージョンを必要とする場合は、外部の [Python ビルドパック](https://github.com/cloudfoundry/python-buildpack)を使用してアプリケーションをデプロイできます。

# 関連リンク
## 一般
* [Cloud Foundry buildpack for the Python Language](https://github.com/cloudfoundry/python-buildpack)
