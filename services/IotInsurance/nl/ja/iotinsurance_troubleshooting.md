---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# トラブルシューティング
{: #troubleshooting}

ここでは、{{site.data.keyword.Bluemix_notm}} での {{site.data.keyword.iotinsurance_full}} の使用に関する一般的なトラブルシューティングの問題を取り上げます。
{:shortdesc}

## アプリのデプロイに関する問題
{: #deployingapps}

{{site.data.keyword.Bluemix_notm}} 組織に十分な空きメモリーがないと、{{site.data.keyword.iotinsurance_short}} のアプリをデプロイできないことがあります。アプリで使用するメモリーを減らすか、アカウントのメモリー割り当て量を増やしてください。

### 現象

{{site.data.keyword.iotinsurance_short}} サービスを開いた時に、デプロイ機能が有効にならず、アプリをデプロイできません。

### 原因

組織でデプロイ機能を実行するには、少なくとも 2 GB の空きメモリーが必要です。トライアル・アカウントの最大のメモリー割り当て量は 2 GB です。{{site.data.keyword.iotinsurance_short}} 以外のサービスやアプリを作成した場合は、{{site.data.keyword.iotinsurance_short}} アプリのデプロイに必要なメモリーが組織にありません。

### 解決策

アカウントのメモリー割り当て量を増やすか、サービスやアプリで使用するメモリーを減らします。

  - アカウントのメモリー割り当て量を増やすには、[トライアル・アカウントを支払アカウントに変換](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)します。

  - 使用するメモリーをすぐに減らすには、{{site.data.keyword.iotinsurance_short}} 以外のサービスやアプリをすべて削除します。変更を有効にするために、{{site.data.keyword.iotinsurance_short}} サービスを再始動します。

  - メモリーの合計量が 2 GB を超えている支払アカウントの場合は、他のアプリやサービスで使用するメモリーを調整することによって、そのアプリやサービスを削除しないで済む可能性があります。詳しくは、[組織のメモリー制限値を超えた場合](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)を参照してください。
