---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} のトラブルシューティング
{: #ts}

ここでは、{{site.data.keyword.Bluemix_notm}} での {{site.data.keyword.iotinsurance_full}} の使用に関する一般的なトラブルシューティングの問題を取り上げます。
{:shortdesc}

## アプリのデプロイに関する問題
{: #deployingapps}
{{site.data.keyword.Bluemix_notm}} 組織に十分な空きメモリーがないと、{{site.data.keyword.iotinsurance_short}} のアプリをデプロイできないことがあります。アプリで使用するメモリーを減らすか、アカウントのメモリー割り当て量を増やしてください。
{:shortdesc}

{{site.data.keyword.iotinsurance_short}} サービスを開いた時に、デプロイ機能が有効にならず、アプリをデプロイできません。
{: tsSymptoms}

組織でデプロイ機能を実行するには、少なくとも 2 GB の空きメモリーが必要です。トライアル・アカウントの最大のメモリー割り当て量は 2 GB です。{{site.data.keyword.iotinsurance_short}} 以外のサービスやアプリを作成した場合は、{{site.data.keyword.iotinsurance_short}} アプリのデプロイに必要なメモリーが組織にありません。
{: tsCauses}

アカウントのメモリー割り当て量を増やすか、サービスやアプリで使用するメモリーを減らします。
- アカウントのメモリー割り当て量を増やすには、[トライアル・アカウントを支払アカウントに変換](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)します。
- 使用するメモリーをすぐに減らすには、{{site.data.keyword.iotinsurance_short}} 以外のサービスやアプリをすべて削除します。変更を有効にするために、{{site.data.keyword.iotinsurance_short}} サービスを再始動します。
- メモリーの合計量が 2 GB を超えている支払アカウントの場合は、他のアプリやサービスで使用するメモリーを調整することによって、そのアプリやサービスを削除しないで済む可能性があります。詳しくは、[組織のメモリー制限値を超えた場合](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)を参照してください。
{: tsResolve}

## パフォーマンスの問題
{: #performance_issues}

ピーク・アクティビティーの期間に、パフォーマンスが遅くなることがあります。
{:shortdesc}

システムがビジー状態になり、頻繁に実行される API 呼び出しで応答時間の遅延が発生することがあります。
{: tsSymptoms}

デフォルトでは、{{site.data.keyword.iotinsurance_short}} は {{site.data.keyword.cloudantfull}} の試用版をデプロイします。このバージョンでは、1 秒間に実行可能な API 呼び出しの数が制限されます。
{: tsCauses}

{{site.data.keyword.cloudant}} の標準バージョンにアップグレードしてください。
{: tsResolve}

## {{site.data.keyword.iotinsurance_short}} のヘルプとサポートの入手
{: #gettinghelp}

{{site.data.keyword.iotinsurance_full}} を使用していて問題や質問がある場合は、{{site.data.keyword.Bluemix_notm}} を調べることができます。さらに、フォーラムで情報を検索したり質問を投稿したりして役立つ情報を得ることができます。また、サポート・チケットを開くこともできます。

- [Bluemix ステータス・ページ ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window} にアクセスすると、{{site.data.keyword.Bluemix_notm}} が利用可能かどうかを確認することができます。

- フォーラムの情報を見て、他のユーザーも同じ問題を経験しているかどうかを調べることができます。フォーラムを使用して質問するときは、{{site.data.keyword.Bluemix_notm}} 開発チームの目に止まるように、質問にタグを付けてください。
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- {{site.data.keyword.iotinsurance_short}} を使用したアプリの開発またはデプロイに関する技術的な質問がある場合は、[Stack Overflow ![外部リンク・アイコン](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} に質問を投稿し、質問には「ibm-bluemix」と「iot-for-insurance」のタグを付けてください。
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- サービスや概説に関する質問は、[IBM developerWorks dW Answers ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window} フォーラムを使用してください。「iot-for-insurance」と「bluemix」のタグを含めてください。

フォーラムの使用について詳しくは、[ヘルプの取得](https://www.{DomainName}/docs/support/index.html#getting-help)を参照してください。

- それでも問題を解決できない場合は、IBM サポート・チケットを開くことができます。IBM サポート・チケットを開く方法や、サポート・レベルとチケットの重大度については、[サポートへのお問い合わせ](../support/index.html#contacting-support)を参照してください。
