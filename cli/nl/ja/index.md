---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-15"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# ダウンロード
{: #cli}

{{site.data.keyword.Bluemix_short}} では、統合コマンド・ライン・インターフェースおよび CLI プラグインなどの強力なツールにアクセスできます。これらの各 CLI のダウンロードは、ユーザーの {{site.data.keyword.Bluemix_notm}} 体験をサポートするためにすべて使用可能です。
{:shortdesc}

## ![](./images/CLI.svg) コマンド・ライン・インターフェース
{: #downloads notoc}

{{site.data.keyword.Bluemix_notm}} の体験をサポートするコマンド・ライン・ツールをダウンロードしてインストールします。

{{site.data.keyword.Bluemix_notm}} CLI は、ご使用の {{site.data.keyword.Bluemix_notm}} 環境を管理するためのコマンド・ラインを利用できるようにします。また、Cloud Foundry アプリケーションとサービスを管理するための Cloud Foundry コマンド・ライン・インターフェースである cf が、そのインストール済み環境に組み込まれています。 

デフォルトでは、CLI ツールは両方とも 443 ポートを使用します。CLI ツールと {{site.data.keyword.Bluemix_notm}} 環境の間に HTTP プロキシーがある場合、実際の HTTP プロキシーの URL とポート (ある場合) を使用して、`HTTP_PROXY` 環境変数を構成する必要があります。詳しくは、[Using the CLI with an HTTP Proxy Server ![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window} を参照してください。

[{{site.data.keyword.Bluemix_notm}} CLI のダウンロード![「外部リンク」アイコン](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[資料の表示](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) コマンド・ライン・インターフェースのプラグイン
{: #cliplugins notoc}

ご使用の {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを、多くのコマンドで簡単に拡張します。{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェース・プラグインにアクセスするには、[CLI プラグイン・リポジトリー ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} を参照してください。

### {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースの拡張: bx
{: #cli_bluemix_ext notoc}


{{site.data.keyword.Bluemix_notm}} cli ツールのインストール後、[CLI プラグイン・リポジトリー ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} は、デフォルトでリポジトリー別名 `Bluemix` で事前構成されます。使用可能なプラグインを直接インストールできます。

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.autoscaling}} CLI* |  *IBM Bluemix Container Service*  |
|-----|-----|-----|
| プラグイン名: auto-scaling <br> [資料の表示](/docs/cli/plugins/auto-scaling/index.html) |  プラグイン名: container-service  <br> [資料の表示](/docs/containers/cs_cli_devtools.html) |
{: caption="表 2. プラグイン" caption-side="top"}

|  *プライベート・ネットワーク・ピアリング* | *VPN*  |
|-----|-----|
| プラグイン名: private-network-peering  <br> [資料の表示](/docs/cli/plugins/pnp/index.html) | プラグイン名: VPN <br> [資料の表示](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="表 3. プラグイン" caption-side="top"}

また、{{site.data.keyword.Bluemix_notm}} cli アーキテクチャーに準拠した他のリポジトリーからプラグインを追加することもできます。
1. 別のリポジトリーから {{site.data.keyword.Bluemix_notm}} CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
ここで、`repo_url` は、プラグイン・リポジトリーの https URL です。

2. プラグインをインストールするには、次のコマンドを実行します。
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### Cloud Foundry コマンド・ライン・インターフェースの拡張: bx cf
{: #cli_cf_ext notoc}

{{site.data.keyword.Bluemix_notm}} コマンド・ライン・ツールをインストールすると、Cloud Foundry コマンド・ライン・インターフェースも Bluemix CLI ディレクトリー内にインストールされます。`bluemix cf` を使用して Cloud Foundry CLI コマンドを実行します。

* {{site.data.keyword.Bluemix_notm}} レジストリーから cf CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* 次に、以下のコマンドを実行してプラグインをインストールします。

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *管理コンソール* |
-----------------|
|  プラグイン名: bluemix-admin<br> [資料の表示](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="表 4. プラグイン" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| プラグイン名: ibm-containers<br> [資料の表示 ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | プラグイン名: VPN <br> [資料の表示](/docs/cli/plugins/vpn/index.html) |
{: caption="表 5. プラグイン" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) 統合開発ツール
{: #ide notoc}

お気に入りの {{site.data.keyword.Bluemix_notm}} サービスを統合するためのプラグインをダウンロードしてインストールします。

| *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|----------|----------|----------|----------|----------|
| [Liberty Eclipse プラグイン ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse プラグイン ![「外部リンク」アイコン](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse プラグイン](../services/rules/index.html#rulov002) | [デベロッパーズ・ツールキット](/docs/services/apiconnect/apic_003.html#apic_001 ) | [Bluemix Eclipse プラグイン](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="表 6. プラグイン" caption-side="top"}
