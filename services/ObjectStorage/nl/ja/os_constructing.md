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


# Swift REST API を使用するための {{site.data.keyword.objectstorageshort}} URL の作成

Swift REST API は、cURL などのコマンド・ライン・クライアント・インターフェースで使用するか、アプリケーションから呼び出すことができます。
{: shortdesc}


{{site.data.keyword.objectstorageshort}} REST API のオプションと例の総合リストについては、[OpenStack Swift API complete reference](http://developer.openstack.org/api-ref-objectstorage-v1.html) を参照してください。

URL を作成する前に、Keystone を使用してサービス・インスタンスを[認証](/docs/services/ObjectStorage/os_authenticate.html)する必要があります。カタログ応答を忘れずにメモしておいてください。以下に例を示します。

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

![{{site.data.keyword.objectstorageshort}} URL の構成要素が例のイメージで示されています](images/Swift_URL.png)

図 1. {{site.data.keyword.objectstorageshort}} URL 例
