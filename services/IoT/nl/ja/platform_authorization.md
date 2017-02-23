---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-14"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# アプリケーション接続

アプリケーションを {{site.data.keyword.iot_full}} に接続するには、API キーとトークンを使用することにより、または {{site.data.keyword.Bluemix_notm}} でアプリケーションを直接 {{site.data.keyword.iot_short_notm}} にバインドすることにより、接続する必要があります。アクセス・ダッシュボードを使用して、アクセス権限を付与します。
{:shortdesc}

## API キー接続
{: #api-key}
アプリケーションを {{site.data.keyword.iot_short_notm}} 組織に接続するときには、API キーが使用されます。アプリケーションでは、組織に接続するための API キー、そしてその API キーと共に使用する必要のある固有の認証トークンが必要です。  

アプリケーション接続について詳しくは、開発者用資料の [MQTT Connectivity for Applications](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html) を参照してください。

新しい API キーと認証トークンのペアを作成するには、以下のようにします。  
1.	{{site.data.keyword.iot_short_notm}} ダッシュボードで、**「アプリ」>「API キー」**に移動します。  
2.	**「API キーの生成」**をクリックします。
  
**重要:** API キーのノートとトークンのペアをメモします。認証トークンは復元できません。このトークンを紛失したり忘れたりした場合、新しい認証トークンを生成するために API キーの再登録が必要になります。
 - API キーの 1 つの例は `a-organization_id-a84ps90Ajs` です  
 - トークンの 1 つの例は `MP$08VKz!8rXwnR-Q*` です  
3.	ダッシュボードの中で API キーを特定するためのコメントを追加します。例: アプリケーション接続のためのキー。
4.	**「完了」**をクリックします。



## Bluemix バインディング接続
{: #bluemix-binding}
アプリケーションを、{{site.data.keyword.Bluemix_notm}} から {{site.data.keyword.iot_short_notm}} 組織にバインドすることができます。アプリケーションをバインドすることにより、同じスペースまたは組織内のサービス・インスタンスとのみ通信可能になります。アプリケーションがサービス・インスタンスと通信するために必要なすべてのデータが VCAP_SERVICES 環境変数に含まれます。ご使用のアプリケーションが複数のサービスにバインドされている場合、VCAP_SERVICES 変数には各サービス・インスタンスの接続情報が含まれます。  

しかし、外部アプリと同じ方法で、他のスペースや組織からのサービス・インスタンスを使用することもできます。バインディングを作成する代わりに、資格情報を使用して、アプリ・インスタンスを直接構成します。詳しくは、{{site.data.keyword.Bluemix_notm}} の資料の中の[新規サービス・インスタンスの要求](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)を参照してください。

自分の組織に関連付けられた Bluemix サービス・インスタンスにバインドされた Bluemix アプリケーションの詳細を確認するには、**「アプリ」>「Bluemix アプリ」**に移動してください。  
