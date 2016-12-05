---

copyright:
  years: 2016
lastupdated:  "2016-08-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilefoundation_short}} サーバーのカスタム・ドメインの構成
{: #configcustomdomain}

{{site.data.keyword.mobilefoundation_short}} は、{{site.data.keyword.Bluemix_notm}} **地域**に基づいたドメイン名を含む URL を使用してアクセス可能な、{{site.data.keyword.mfserver_short_notm}} をプロビジョンします。<!--on {{site.data.keyword.containerlong}} as a container group. The container group will be mapped to-->独自のカスタム・ドメインを構成することも可能です。
{:shortdesc}

この <!--container group is created with a-->URL や経路は、{{site.data.keyword.Bluemix_notm}} `地域`に基づいたデフォルト・ドメイン名を使用して作成されます。

*表 1. {{site.data.keyword.Bluemix_notm}}* の「地域」に基づいたアプリケーション・ドメイン名

  |ドメイン |  地域  |    
  |:----- | :----- |    
  |`mybluemix.net` | 米国南部 |    
  |`eu-gb.mybluemix.net` | 英国  |
  |`au-syd.mybluemix.net` | シドニー  |      

独自ドメインを使用できるようにするには、以下のステップを実行してカスタム・ドメインを構成する必要があります。

1.	いずれかのサポートされるプランを選択して、{{site.data.keyword.mobilefoundation_short}} サービス・インスタンスを作成することで、{{site.data.keyword.mfserver_short_notm}} インスタンスを作成します。

+ 使用するカスタム・ドメインを {{site.data.keyword.Bluemix_notm}} `組織` に追加します。**「組織の管理」>「ドメイン」>「ドメインの追加」**と進み、独自のドメインを追加します。

+ サーバーがカスタム・ドメインを使用するように<!--container group-->経路をセットアップします。

+ ドメインの DNS プロバイダーに進み、サーバーが実行されているデフォルトの {{site.data.keyword.Bluemix_notm}} の経路にドメインからトラフィックをルーティングする CNAME エントリーを追加します。<!--container group-->

+ カスタム・ドメインに `https` を構成する場合は、{{site.data.keyword.Bluemix_notm}} でドメインの SSL 証明書をアップロードします。これを行うには、**「組織の管理」>「ドメイン」**と進み、SSL 証明書を構成するカスタム・ドメインを選択し、**「証明書のアップロード」**をクリックしてドメインの SSL 証明書をアップロードします。詳しくは、[SSL Certificates and Bluemix Custom Domains](https://developer.ibm.com/bluemix/2014/09/28/ssl-certificates-bluemix-custom-domains/) を参照してください。
