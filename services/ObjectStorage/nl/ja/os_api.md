---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

## Swift REST API を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-restapi}
*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

コマンド・ライン・クライアント・インターフェース (cURL など) で Swift REST API を使用することも、アプリケーションから API を呼び出すこともできます。
{: shortdesc}

### {{site.data.keyword.objectstorageshort}} URL の構成 {: #access-points}

{{site.data.keyword.objectstorageshort}} API と相互作用するには、 {{site.data.keyword.objectstorageshort}} URL を次のように構成します。
  ```
https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL の構成要素  </th>
    <th> 定義 </th>
  </tr>
  <tr>
    <td> API のバージョン  </td>
    <td> バージョン 1: v1 </td>
  </tr>
  <tr>
    <td> アカウント情報  </td>
    <td> これは、お客様の ProjectID と接頭部の組み合わせです。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> コンテナー名前空間  </td>
    <td> コンテナーの名前。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> オブジェクト名前空間  </td>
    <td> ファイルまたはオブジェクトの名前。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> アクセス・ポイント</td>
    <td> ロンドン: https://lon.objectstorage.open.softlayer.com/
    <br> ダラス: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

*表 1. {{site.data.keyword.objectstorageshort}} URL 構成要素の説明*

例:

![{{site.data.keyword.objectstorageshort}} URL の構成要素が例のイメージで示されています](images/Swift_URL.png)


### {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

{{site.data.keyword.objectstorageshort}} REST API のオプションと例の包括的な一覧については、[OpenStack Swift API の詳細リファレンス](http://developer.openstack.org/api-ref-objectstorage-v1.html)を参照してください。
