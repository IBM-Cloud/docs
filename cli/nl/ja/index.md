---



copyright:

  years: 2015，2016

lastupdated: "2016-10-24"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI と開発ツール
{: #cli}

{{site.data.keyword.Bluemix_short}} では、統合コマンド・ライン・インターフェースおよび CLI プラグインなどの強力なツールにアクセスできます。これらの各 CLI のダウンロードは、ユーザーの {{site.data.keyword.Bluemix_notm}} 体験をサポートするためにすべて使用可能です。
{:shortdesc}

## ![](./images/CLI.svg) コマンド・ライン・インターフェース
{: #downloads}

{{site.data.keyword.Bluemix_notm}} の体験をサポートするコマンド・ライン・インターフェースをダウンロードしてインストールします。

Cloud Foundry cf コマンド・ライン・ツールは、すべての {{site.data.keyword.Bluemix_notm}} CLI ツールの前提条件です。{{site.data.keyword.Bluemix_notm}} コマンド・ライン・ツールでは、Cloud Foundry アプリケーションの他に、{{site.data.keyword.Bluemix_notm}} 環境を管理するための拡張機能も体験できます。

デフォルトでは、CLI ツールは両方とも 443 ポートを使用します。CLI ツールと {{site.data.keyword.Bluemix_notm}} 環境の間に HTTP プロキシーがある場合、実際の HTTP プロキシーの URL とポート (ある場合) を使用して、`http-proxy` 環境変数を構成する必要があります。詳しくは、『[Using the CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}』を参照してください。


| *{{site.data.keyword.Bluemix_notm}}: bx* | *Cloud Foundry: cf* |
|---------------------|---------------|
| [CLI のダウンロード](http://clis.ng.bluemix.net/)  <br> [資料の表示](./reference/bluemix_cli/index.html)|  [CLI のダウンロード](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [資料の表示](./reference/cfcommands/index.html) |


## ![](./images/CLI_Plugin.svg) コマンド・ライン・インターフェースのプラグイン

ご使用の {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを、多くのコマンドで簡単に拡張します。{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースのプラグインにアクセスするには、『[ CLI プラグイン・リポジトリー](https://plugins.ng.bluemix.net/)』を参照してください。

### {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースの拡張: bx
{: cli_bluemix_ext}

* {{site.data.keyword.Bluemix_notm}} レジストリーから {{site.data.keyword.Bluemix_notm}} CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* 次に、以下のコマンドを実行してプラグインをインストールします。

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *ネットワーク・セキュリティー・グループ* |
|-----|-----|-----|
| プラグイン名: active-deploy<br> [資料の表示](/docs/services/ActiveDeploy/cli.html#cli) | プラグイン名: auto-scaling <br> [資料の表示](./plugins/auto-scaling/index.html) |  プラグイン名: nsg <br> [資料の表示](./plugins/networksecuritygroups/index.html)  |


### Cloud Foundry コマンド・ライン・インターフェースの拡張: cf
{: cli_cf_ext}

* {{site.data.keyword.Bluemix_notm}} レジストリーから cf CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* 次に、以下のコマンドを実行してプラグインをインストールします。

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *管理コンソール* |
|-----------------|-----------------|
| プラグイン名: active-deploy<br>  [資料の表示](/docs/services/ActiveDeploy/cli.html#cli) |  プラグイン名: bluemix-admin<br> [資料の表示](/docs/cli/plugins/bluemix_admin/index.html) |

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| プラグイン名: ibm-containers<br> [資料の表示](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | プラグイン名: VPN <br> [資料の表示](./plugins/vpn/index.html) |


## ![](./images/Integrated_Dev_Tools.svg) 統合開発ツール

お気に入りの {{site.data.keyword.Bluemix_notm}} サービスを統合するためのプラグインをダウンロードしてインストールします。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse プラグイン](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse プラグイン](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse プラグイン](/docs/services/rules/index.html#rulov002) |
