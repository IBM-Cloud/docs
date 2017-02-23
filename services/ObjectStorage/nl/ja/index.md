---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# {{site.data.keyword.objectstorageshort}} 概説 {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} では、構造化されていないクラウド・データ・ストレージを提供します。コンテンツを保管してアクセスするほかに、アプリおよびサービスを対話的に構成して接続することが可能です。
{: shortdesc}

{{site.data.keyword.objectstorageshort}} サービスの一般的なユース・ケースとして、以下があります。

* インスタンスからのボリューム・データのバックアップ
* 大量のデータを転送する場合の中継場所として使用
* 直接接続されていない環境間でのデータの転送
* 中央リポジトリーとして機能


{{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} を利用すると、完全にプロビジョンされた Swift {{site.data.keyword.objectstorageshort}} アカウントにアクセスしてデータを管理することができます。プロバイダー・サイドの暗号化は提供されません。


1.	{{site.data.keyword.Bluemix_notm}} カタログからサービス・インスタンスをプロビジョンします。インスタンスを構成し、**「作成」**をクリックします。最初に**「アプリ」**フィールドで**「アンバインドのまま」**オプションを選択した場合でも、後でサービス・インスタンスを {{site.data.keyword.Bluemix_notm}} アプリにバインドすることができます。
2. サービス・インスタンス・ダッシュボードで、オブジェクトの保管を開始するためのコンテナーを作成します。
3. **「アクション」**ドロップダウン・メニューからコンテナーにファイルを追加します。
4. オブジェクトへのアクセスをテストするには、**「ダウンロード」**をクリックしてファイルを確認します。
5. インスタンスをアプリケーションに接続する準備ができたら、サービス資格情報をセットアップして[サービスをバインドします](/docs/services/reqnsi.html#add_service)。



# 関連リンク
{: #rellinks}

## API リファレンス 
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK 
{: #sdk}
* [OpenStack Software Development Kit (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## チュートリアルおよびサンプル 
{: #samples}
* [Java で IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} に接続する](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} へのアクセスに Python を使用する](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [{{site.data.keyword.objectstorageshort}} を活用するために PHP を使用する](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}
* [Object Storage for Bluemix へのアクセスに Node js を使用する](https://developer.ibm.com/recipes/tutorials/use-pkgcloud-to-access-ibm-object-storage-for-bluemix-with-node-js/){: new-window}

## 互換性のあるランタイム
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [コミュニティー・ビルドパック](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## 関連リンク
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} 料金シート](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} 前提条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
