---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ネットワーク環境
{: #networkEnvironment}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のサービス・インスタンスがプロビジョンされた後、いくつかの方法で VM にアクセスできます。セキュアな VPN で接続し、SSH、従来の WebSphere 管理コンソール、およびアプリケーションから VM にアクセスすることができます。また、パブリック IP アドレスを使用して VM をインターネットに接続することも可能です。

以下の図は、これらのネットワーク・パスを示しています。

図 1. パブリック IP を使用したマルチテナント・ネットワーキングのクライアント・ビュー

![図 1. パブリック IP を使用したマルチテナント・ネットワーキングのクライアント・ビュー](images/wasaas_multi_tenantPublicIP.gif)

## VPN アクセス
{: #vpnAccess}

{{site.data.keyword.Bluemix_notm}} UI のサービス・ダッシュボードから WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} のサービス・インスタンスをプロビジョンすると、VPN 資格情報をダウンロードして OpenVPN 接続を確立できます。これにより、SSH で VM にアクセスできるようになります。また、Liberty 管理センター、従来の WebSphere 管理コンソール、およびアプリケーションへのアクセスも可能です。

## パブリック・インターネット・アクセス
{: #publicInternetAccess}

オプションで、{{site.data.keyword.Bluemix_notm}} UI のサービス・ダッシュボードで**「パブリック IP の管理 (Manage Public IP)」**をクリックしてパブリック IP を要求することで、WebSphere サーバーの VM 用のパブリック IP アドレスを要求することもできます。このプロセスにより、このサーバーの IP アドレスが予約されます。次に、**「IP を開く (Open IP)」**をクリックし、インターネットから WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} サービス・インスタンスへの接続を開きます。

## パブリック IP ポート
{: #publicIPports}

パブリック IP へのアクセスを開くと、その IP アドレスはご使用の VM と関連付けられ、ゲートウェイでポート 80 とポート 443 が開きます。ただし、デフォルトで、Liberty Core および従来の WebSphere Base サーバーは、ポート 80 とポート 443 を開きません。IBM HTTP Server では、デフォルトでポート 80 とポート 443 は開きます。このため、パブリック IP の使用時にポート 80/443 でアプリケーション・トラフィックを listen するよう Liberty Core および従来の WebSphere Base サーバーを構成する必要が生じる可能性があります。
* Liberty Core サーバーを構成するには、[パブリック・アクセス用に Liberty Core サーバーを構成する (Configure Liberty Core Server for public access)](networkEnvironment.html#configureLibertyForPublicAccess)を参照してください。
* 従来の WebSphere Base サーバーを構成するには、ポート 80/443 で listen する Web コンテナー・トランスポート・チェーンを追加します。この説明については、[Configuring transport chains](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5//com.ibm.websphere.nd.doc/ae/trun_chain_transport.html){: new_window} を参照してください。

## VPN のプライベート IP ポート
{: #privateIPports}

VM のプライベート IP アドレスには、VPN 接続を使用して接続します。図 1 に示すとおり、Liberty 管理センター (9080, 9443)、従来の WebSphere 管理コンソール (9060, 9043)、SSH (22)、および 80/443 以外のポートには、VPN 接続でのみアクセス可能です。Liberty 管理センターとアプリケーション・ポートの分離について詳しくは、サンプルの Liberty Core **server.xml** および **ibm-web-bnd.xml** を参照してください。

**問題の回避:** Liberty Core および従来の WebSphere Base サーバーの場合、VM がプロビジョンされる際にファイアウォール・ポートは事前構成されています。ただし、Deployment Manager または集合コントローラーが IBM HTTP Server と連結されている Network Deployment の構成においては、ファイアウォールでポートを開く必要がある可能性があります。詳細については、[ファイアウォール・ポート](systemAccess.html#firewall_ports)を参照してください。

## Liberty Core サーバーをパブリック IP アクセス用に構成する
{: #configureLibertyForPublicAccess}

パブリック IP の使用時にポート 80/443 でアプリケーション・トラフィックを listen するよう Liberty Core を構成する必要があります。

デフォルトで、Liberty は、Liberty 管理センター、およびポート 9080 および 9443 の **defaultHttpEndpoint** と関連付けられている **default_host** 仮想ホストで使用可能なアプリケーションで構成されます。Liberty 管理センターをアプリケーションの仮想ホストおよびエンドポイントと分離するようにご使用のサーバーを再構成し、それらを別のポートで使用可能にしてください。

以下のスニペットは、server.xml 構成の調整の例です。

```    
    <!-- open port 9080/9443 for incoming http connections -->
    <httpEndpoint id="defaultHttpEndpoint"
        host="*"
        httpPort="9080"
        httpsPort="9443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!-- define a new endpoint for public app traffic -->
    <httpEndpoint id="publicHttpEndpoint"
        host="*"
        httpPort="80"
        httpsPort="443">
        <tcpOptions soReuseAddr="true"/>
    </httpEndpoint>

    <!– restrict default_host to vpn so the Liberty Admin Center is not public -->
    <virtualHost id="default_host" allowFromEndpointRef="defaultHttpEndpoint">
      <hostAlias>*:9080</hostAlias>
      <hostAlias>*:9443</hostAlias>
    </virtualHost>

    <virtualHost id="external_host">
      <hostAlias>*:80</hostAlias>
      <hostAlias>*:443</hostAlias>
    </virtualHost>
```
{: codeblock}

次に、以下のスニペットをアプリケーションの **META-INF/ibm-web-bnd.xml** ファイルに含めることで、アプリケーションを **external_host** 仮想ホストと関連付けます。

```
    <?xml version="1.0" encoding="UTF-8"?>
    <web-bnd
        xmlns="http://websphere.ibm.com/xml/ns/javaee"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://websphere.ibm.com/xml/ns/javaee   
        http://websphere.ibm.com/xml/ns/javaee/ibm-web-bnd_1_0.xsd"
        version="1.0">

        <virtual-host name="external_host" />
    </web-bnd>
```
{: codeblock}
