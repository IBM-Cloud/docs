---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# オブジェクトの管理

Swift CLI、API、または Bluemix UI を使用してオブジェクトとコンテナーを管理することができます。
{: shortdesc}

オブジェクトを管理する前に、サービス・インスタンスを認証し、サービス資格情報を生成し、Swift CLI を構成しておくようにしてください。

サービスを処理している時にオブジェクトを保管、ダウンロード、および削除することができます。オブジェクトを管理する際に留意すべき点がいくつかあります。
  * 保管できるデータ量には制限はありませんが、各アップロードは 5 GB を超えてはなりません。5 GB を超えるファイルをアップロードする必要がある場合は、[ラージ・オブジェクトの保管](/docs/services/ObjectStorage/os_large_files.html)に記載されている手順に従ってください。
  * Swift には真のディレクトリー構造がありませんが、[既存のディレクトリー](/docs/services/ObjectStorage/os_directories.html)をコマンドに追加することができます。
  * 非意図的にファイルを上書きしないようにするには、[オブジェクト・バージョン管理をセットアップ](/docs/services/ObjectStorage/os_versioning.html)します。
  * オブジェクトを削除する[時刻をスケジュール](/docs/services/ObjectStorage/os_deletion.html)に入れることができます。
