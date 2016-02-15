{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI と開発ツール
{: #cli}

*最終更新日: 2016 年 1 月 19 日*

{{site.data.keyword.Bluemix_short}} では、統合コマンド・ライン・インターフェースおよび CLI プラグインなどの強力なツールにアクセスできます。これらの各 CLI のダウンロードは、ユーザーの {{site.data.keyword.Bluemix_notm}} 体験をサポートするためにすべて使用可能です。
{:shortdesc}

## ![コマンド・ライン・インターフェース](./images/CLI.png) コマンド・ライン・インターフェース
{: #downloads}

{{site.data.keyword.Bluemix_notm}} の体験をサポートするコマンド・ライン・インターフェースをダウンロードしてインストールします。Cloud Foundry cf コマンド・ライン・インターフェースは、他のすべての {{site.data.keyword.Bluemix_notm}} CLI ツールの前提条件です。


| *Cloud Foundry: cf* |	*{{site.data.keyword.Bluemix_notm}}: bx* | 
|---------------------|---------------|
| [CLI のダウンロード](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [資料の表示](./reference/cfcommands/index.html) | [CLI のダウンロード](http://clis.{DomainName}/){: new_window}  <br> [資料の表示](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------|---------------|
| [Mac インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [資料の表示](./reference/bl/index.html) |


## ![コマンド・ライン・インターフェースのプラグイン](./images/CLI_Plugin.png) コマンド・ライン・インターフェースのプラグイン

ご使用の {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを、多くのコマンドで簡単に拡張します。{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースのプラグインにアクセスするには、『[{{site.data.keyword.Bluemix_notm}} CLI プラグイン・リポジトリー](http://plugins.{DomainName}/){: new_window}』を参照してください。

1. {{site.data.keyword.Bluemix_notm}} レジストリーから cf CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. プラグインをインストールするには、次のコマンドを実行します。```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *管理コンソール* | *開発モード* | 
|-----------------|-----------------|-----------------|
| プラグイン名: active-deploy<br>  [資料の表示](../services/ActiveDeploy/index.html#cli) |  プラグイン名: bluemix-admin<br> [資料の表示](../cli/plugins/bluemix_admin/index.html) | プラグイン名: development-name <br> [資料の表示](./plugins/dev_mode/index.html) | 

### {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースの拡張: bx
1. {{site.data.keyword.Bluemix_notm}} レジストリーから {{site.data.keyword.Bluemix_notm}} CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. プラグインをインストールするには、次のコマンドを実行します。```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| プラグイン名: ibm-containers<br> [資料の表示](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | プラグイン名: auto-scaling <br> [資料の表示](./plugins/auto-scaling/index.html) |プラグイン名: VPN <br> [資料の表示](./plugins/vpn/index.html) |

## ![統合開発ツール](./images/Integrated_Dev_Tools.png) 統合開発ツール


お気に入りの {{site.data.keyword.Bluemix_notm}} サービスを統合するためのプラグインをダウンロードしてインストールします。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse プラグイン](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse プラグイン](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse プラグイン](../services/rules/index.html#rulov002) |
