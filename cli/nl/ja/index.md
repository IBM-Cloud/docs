{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI と開発ツール
{: #cli}

*最終更新日: 2015 年 11 月 10 日*

{{site.data.keyword.Bluemix_short}} 用の強力なツールです。{:shortdesc}

## ![コマンド・ライン・インターフェース](./images/CLI.png) コマンド・ライン・インターフェース
{: #downloads}

{{site.data.keyword.Bluemix_notm}} の体験をサポートするコマンド・ライン・インターフェースをダウンロードしてインストールします。Cloud Foundry cf コマンド・ライン・インターフェースは、他のすべての {{site.data.keyword.Bluemix_notm}} CLI ツールの前提条件です。


| *Cloud Foundry: cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}: ice* | *{{site.data.keyword.Bluemix_notm}} Live Sync:
bl* |
|---------------------|---------------|---------------|
| [CLI のダウンロード](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [資料の表示](./reference/cfcommands/index.html) |[Docker のダウンロード](https://docs.docker.com/installation/){: new_window} <br> [ice Mac インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window} <br> [ice Windows インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window} <br> [ice Linux インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window} <br> [資料の表示](../containers/container_cli_ice_ov.html) | [Mac インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows インストーラー](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [資料の表示](./reference/bl/index.html) |


## ![コマンド・ライン・インターフェースのプラグイン](./images/CLI_Plugin.png) コマンド・ライン・インターフェースのプラグイン

ご使用の {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを、多くのコマンドで簡単に拡張します。{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースのプラグインにアクセスするには、『[{{site.data.keyword.Bluemix_notm}} CLI プラグイン・リポジトリー](http://plugins.{DomainName}/){: new_window}』を参照してください。

1. {{site.data.keyword.Bluemix_notm}} レジストリーから cf CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. プラグインをインストールするには、次のコマンドを実行します。```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* |  *開発モード* | 
|-----------------|-----------------|
| プラグイン名: active-deploy<br>  [資料の表示](../services/ActiveDeploy/index.html#cli) |  プラグイン名: development-name <br> [資料の表示](./plugins/dev_mode/index.html) | 

### {{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェースを拡張します: bx
1. {{site.data.keyword.Bluemix_notm}} レジストリーから {{site.data.keyword.Bluemix_notm}} CLI プラグインをインストールするには、プラグイン・レジストリーのエンドポイントを次のようにして設定します。
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. プラグインをインストールするには、次のコマンドを実行します。```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| プラグイン名: ibm-containers<br> [資料の表示](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![統合開発ツール](./images/Integrated_Dev_Tools.png) 統合開発ツール


お気に入りの {{site.data.keyword.Bluemix_notm}} サービスを統合するためのプラグインをダウンロードしてインストールします。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse プラグイン](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse プラグイン](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse プラグイン](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer
Eclipse プラグイン](../services/rules/index.html#rulov002) |
