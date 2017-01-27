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

# ディレクトリーの処理 

Swift には本当のディレクトリー構造はありませんが、ディレクトリー・レイアウトを表す命名法が使用されています。ディレクトリー名を指定すると、相対パスの一部としてすべてのファイル名にそのディレクトリー名が付加されます。
{: shortdesc}

## Swift CLI によるコンテナーへのディレクトリーの追加

コンテナーにディレクトリーを追加するには、ローカル・デバイスにディレクトリー構造が設定されている必要があります。

1. ローカルに、ディレクトリーを作成し、ファイルを保存します。
2. 以下のコマンドを実行して、ディレクトリーをコンテナーにアップロードします。

    ```
  swift upload <container_name> <directory_name>
  ```
    {: pre}

## CLI を使用したディレクトリーのダウンロード
ディレクトリー構造をダウンロードするには、`-prefix` パラメーターを使用して、ダウンロードするディレクトリーまたはディレクトリー構造を示します。

1. 以下のコマンドを実行して、ディレクトリーをダウンロードします。

    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
