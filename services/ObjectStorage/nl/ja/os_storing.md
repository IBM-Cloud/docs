---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# オブジェクトの保管

UI または CLI を使用してオブジェクトをストレージにアップロードすることができます。オブジェクトのアップロードは、単一のアップロードで最大サイズ 5 GB に制限されています。ただし、ラージ・オブジェクトは、小さいオブジェクトにセグメント化することによりアップロードできます。
{: shortdesc}


## UI を使用したコンテナーへのオブジェクトの保管 {: #storing-ui}

**注**: 同じ名前のファイルをアップロードすると、{{site.data.keyword.objectstorageshort}} は、保管されているファイルを新しいファイルに置換します。ファイルをダウンロードして編集する場合は、ファイルに別の名前を付けるか、アップロードする前に[オブジェクトのバージョン管理をセットアップ](/docs/services/ObjectStorage/os_versioning.html)して、ファイルの両方のバージョンを保持するようにしてください。


1. サービス・インスタンス・ダッシュボードで、**「アクション」**ドロップダウン・メニューからコンテナーを追加します。
2. コンテナーに名前を付け、**「作成」**をクリックします。
3. **「アクション」**ドロップダウン・メニューから**「ファイルの追加」**を選択します。ダイアログ・ボックスが開きます。
4. アップロードする 1 つ以上のファイルを選択し、**「開く」**をクリックします。



## CLI によるコンテナーへのオブジェクトの保管 {: #storing-cli}

1. {{site.data.keyword.Bluemix_notm}} にログインしていない場合は、{{site.data.keyword.objectstorageshort}} のインスタンスを含む組織およびスペースにログインします。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 次のコマンドを実行して、{{site.data.keyword.objectstorageshort}} コンテナーを作成します。*container_name* 変数をこの時点で設定します。

  ```
  swift post <container_name>
  ```
  {: pre}

  **注**: エラー・メッセージを受け取った場合は、[前提ソフトウェア](/docs/services/ObjectStorage/os_configuring.html#install-swift-client)がインストールされていることを確認してください。

3. オプション: コンテナーが作成されたことを確認するには、以下のコマンドを実行してコンテナーをリストします。

  ```
  swift list
  ```
  {: pre}

4. 偶発的な上書きによってデータが消滅しないようにするために、[オブジェクト・バージョン管理のセットアップ](/docs/services/ObjectStorage/os_versioning.html)を行います。オブジェクトのバージョン管理を望まない場合は、ストア内の既存のファイルをリストし、アップロード前に、必要に応じてディレクトリーまたはファイルの名前を変更します。

5. 以下のコマンドを実行して、ファイルをコンテナーにアップロードします。

  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

  **注**: 5 GB を超えるファイルをアップロードするには、[追加の手順が必要です](/docs/services/ObjectStorage/os_large_files.html)。

6. オプション: アップロードが成功したことを確認するには、以下のコマンドを実行してコンテナーの内容を表示します。

  ```
  swift list <container_name>
  ```
  {: pre}
