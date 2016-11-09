---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 複数地域にわたる {{site.data.keyword.objectstorageshort}} の管理 {: #multi-regions}
*最終更新日: 2016 年 10 月 19 日*
{: .last-updated}

{{site.data.keyword.objectstorageshort}} サービスは、ダラスとロンドンのストレージ地域をサポートします。これらのストレージ地域は、{{site.data.keyword.objectstorageshort}} サービス・インスタンスが作成される {{site.data.keyword.Bluemix_notm}} 地域 (「米国南部」や「英国」など) から独立しています。米国南部 {{site.data.keyword.Bluemix_notm}} 地域にインスタンスを作成した場合、「ダラス」または「ロンドン」のいずれかのストレージ地域に対してデータの読み取り/書き込みを行えます。
{: shortdesc}

米国南部 {{site.data.keyword.Bluemix_notm}} 地域では、「ダラス」ストレージ地域がデフォルトです。英国 {{site.data.keyword.Bluemix_notm}} 地域では、「ロンドン」ストレージ地域がデフォルトです。{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースは、常に {{site.data.keyword.Bluemix_notm}} 地域のデフォルトのストレージ地域を起動します。地域を切り替えるには、「{{site.data.keyword.objectstorageshort}} 地域」ドロップダウン・リストをクリックして、別の地域を選択します。

**注:** {{site.data.keyword.objectstorageshort}} サービスは、ストレージ地域間の複製をサポートしません。

### 複数地域アクセス

{{site.data.keyword.objectstorageshort}} サービスを使用するには、[OpenStack Keystone に対する認証](../ObjectStorage/os_security.html#keystone-authentication){: new_window}が必要です。正常に認証された後、`X-Subject-Token` および {{site.data.keyword.objectstorageshort}} エンドポイントが応答内で使用可能になります。各ストレージ地域で、[アクセス・ポイント](../ObjectStorage/os_api.html#access-points)が異なります。


例えば、「ダラス」ストレージ地域に `my_container` という名前のコンテナーを作成するには、curl コマンドで「ダラス」アクセス・ポイントを次のように指定します。

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
出力として以下を受け取ります。

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

「ロンドン」ストレージ地域に `my_container` という名前のコンテナーを作成するには、curl コマンドで「ロンドン」アクセス・ポイントを次のように指定します。

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
出力として以下を受け取ります。

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**注:** Keystone から獲得された `X-Subject-Token` (この例では `X-Trans-ID` とラベル付けされているもの) は、複数のストレージ地域にわたって機能します。
