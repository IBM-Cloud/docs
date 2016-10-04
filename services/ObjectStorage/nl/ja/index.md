---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 入門 {: #getting-started-with-object-storage}

最終更新日: 2016 年 8 月 25 日
{: .last-updated}

{{site.data.keyword.objectstoragefull}} を利用すると、完全にプロビジョンされた Swift {{site.data.keyword.objectstorageshort}} アカウントにアクセスしてデータを管理することができます。Swift は、完全分散型の、API によるアクセスが可能なストレージ・プラットフォームを提供します。
アプリケーションで直接使用することも、バックアップに使用することも可能で、コスト効率の高いスケールアウト・ストレージに理想的です。

**注:** プロバイダー・サイドの暗号化は提供されていません。アップロードの前にデータを暗号化するのは、クライアント・アプリケーションの責任です。


{{site.data.keyword.objectstorageshort}} の使用を開始するには、以下のようにします。

1.	{{site.data.keyword.Bluemix_notm}} カタログから {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョンします。
2.	{{site.data.keyword.objectstorageshort}} インスタンスを構成し、**「作成」**をクリックします。最初に**「アプリ」**フィールドで**「アンバインドのまま」**オプションを選択した場合、構成完了後もサービス・インスタンスを {{site.data.keyword.Bluemix_notm}} アプリケーションにバインドすることができます。手順については、[アプリのバインド](../ObjectStorage/objectstorge_usingobjectstorage.html#using-object-storage-from-bluemix-app)に関する資料を参照してください。



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
* [Java による {{site.data.keyword.objectstoragefull}} への接続](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} へのアクセスに Python を使用する](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [{{site.data.keyword.objectstorageshort}} を活用するために PHP を使用する](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}
* [Node.js による {{site.data.keyword.objectstoragefull}} へのアクセスに pkgcloud を使用する](https://developer.ibm.com/recipes/tutorials/use-pkgcloud-to-access-ibm-object-storage-for-bluemix-with-node-js/){: new_window}

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
