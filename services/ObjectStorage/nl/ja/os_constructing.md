---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Swift REST API を使用するための {{site.data.keyword.objectstorageshort}} URL の作成

Swift REST API は、cURL などのコマンド・ライン・クライアント・インターフェースで使用するか、アプリケーションから呼び出すことができます。
{: shortdesc}


{{site.data.keyword.objectstorageshort}} REST API のオプションと例の総合リストについては、[OpenStack Swift API complete reference](http://developer.openstack.org/api-ref-objectstorage-v1.html) を参照してください。

Keystone を使用してサービス・インスタンスを認証した時に、カタログ応答をメモしました。その応答は、以下の例のようになっているはずです。

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


以下のイメージに示されているように、コンテナーおよびオブジェクトの名前空間を {{site.data.keyword.objectstorageshort}} URL の最後に追加します。

  ![例のイメージに示されている、{{site.data.keyword.objectstorageshort}} URL の断片。](images/swift_URL.png)
  図 1: {{site.data.keyword.objectstorageshort}} URL 例
