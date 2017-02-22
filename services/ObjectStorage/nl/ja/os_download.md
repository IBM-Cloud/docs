---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# オブジェクトのダウンロード

保管オブジェクトを、UI または CLI を使用して検討あるいは編集するために、ダウンロードすることができます。
{: shortdesc}


## UI からのオブジェクトのダウンロード {: #downloading-ui}

1. 偶発的な上書きによってデータが消滅しないようにするために、[オブジェクト・バージョン管理のセットアップ](/docs/services/ObjectStorage/os_versioning.html)を行います。オブジェクトのバージョン管理を望まない場合は、ダウンロードする前に、必要に応じてディレクトリーまたはファイルを名前変更します。
2. サービス・インスタンス・ダッシュボードで、ダウンロードしたいファイルを含むコンテナーを選択します。
3. ファイルを選択します。
4. **「アクション」**ドロップダウン・メニューから**「ファイルのダウンロード」**を選択します。


## Swift CLI によるオブジェクトのダウンロード {: #downloading-cli}

1.  {{site.data.keyword.Bluemix_notm}} にログインしていない場合は、{{site.data.keyword.objectstorageshort}} のインスタンスを含む組織およびスペースにログインします。

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. 偶発的な上書きによってデータが消滅しないようにするために、[オブジェクト・バージョン管理のセットアップ](/docs/services/ObjectStorage/os_versioning.html)を行います。オブジェクトのバージョン管理を望まない場合は、ストア内の既存のファイルをリストし、ダウンロード前に、必要に応じてディレクトリーまたはファイルの名前を変更します。

3. 以下のコマンドを実行して、ファイルをダウンロードします。

```
swift download <container_name> <file_name>
```
{: pre}
