{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 及開發工具
{: #cli}

*前次更新：2015 年 11 月 10 日*

{{site.data.keyword.Bluemix_short}} 的強大工具。{:shortdesc}

## ![指令行介面](./images/CLI.png) 指令行介面
{: #downloads}

下載及安裝指令行介面，以支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。Cloud Foundry cf
指令行介面是所有其他 {{site.data.keyword.Bluemix_notm}} CLI 工具的必要條件。


| *Cloud Foundry：cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}：ice* | *{{site.data.keyword.Bluemix_notm}} Live Sync：bl* |
|---------------------|---------------|---------------|
| [下載 CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [檢視文件](./reference/cfcommands/index.html) |[下載 Docker](https://docs.docker.com/installation/){: new_window} <br> [ice Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window} <br> [ice Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window} <br> [ice Linux Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window} <br> [檢視文件](../containers/container_cli_ice_ov.html) | [Mac Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows Installer](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [檢視文件](./reference/bl/index.html) |


## ![指令行介面外掛程式](./images/CLI_Plugin.png) 指令行介面外掛程式

使用其他指令，輕鬆延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面。若要存取 {{site.data.keyword.Bluemix_notm}} 指令行介面外掛程式，請參閱 [{{site.data.keyword.Bluemix_notm}} CLI 外掛程式儲存庫](http://plugins.{DomainName}/){: new_window}。

1. 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 cf CLI 外掛程式，請設定外掛程式登錄端點：
```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. 執行下列指令，以安裝外掛程式：```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* |  *Development Mode* | 
|-----------------|-----------------|
| 外掛程式名稱：active-deploy<br>  [檢視文件](../services/ActiveDeploy/index.html#cli) |  外掛程式名稱：development-name <br> [檢視文件](./plugins/dev_mode/index.html) | 

### 延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面：bx
1. 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式，請設定外掛程式登錄端點：
```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. 執行下列指令，以安裝外掛程式：```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| 外掛程式名稱：ibm-containers<br> [檢視文件](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![整合式開發工具](./images/Integrated_Dev_Tools.png) 整合式開發工具


下載並安裝外掛程式以整合您最愛的 {{site.data.keyword.Bluemix_notm}} 服務。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 外掛程式](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 外掛程式](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 外掛程式](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 外掛程式](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 外掛程式](../services/rules/index.html#rulov002) |
