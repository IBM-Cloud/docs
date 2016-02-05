{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 和開發工具
{: #cli}

*前次更新：2016 年 1 月 19 日*

使用 {{site.data.keyword.Bluemix_short}}，您可以存取各種功能強大的工具，例如統一指令行介面和 CLI 外掛程式。其中每個 CLI 下載都可用來增強您的 {{site.data.keyword.Bluemix_notm}} 體驗。{:shortdesc}

## ![指令行介面](./images/CLI.png) 指令行介面
{: #downloads}

下載及安裝指令行介面，以支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。Cloud Foundry cf
指令行介面是所有其他 {{site.data.keyword.Bluemix_notm}} CLI 工具的必要條件。


| *Cloud Foundry：cf* |	*{{site.data.keyword.Bluemix_notm}}：bx* | 
|---------------------|---------------|
| [下載 CLI](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [檢視文件](./reference/cfcommands/index.html) | [下載 CLI](http://clis.{DomainName}/){: new_window}  <br> [檢視文件](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync：bl* |
|---------------|---------------|
| [Mac 安裝程式](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window} <br> [Windows 安裝程式](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window} <br> [檢視文件](./reference/bl/index.html) |


## ![指令行介面外掛程式](./images/CLI_Plugin.png) 指令行介面外掛程式

使用其他指令，輕鬆延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面。若要存取 {{site.data.keyword.Bluemix_notm}} 指令行介面外掛程式，請參閱 [{{site.data.keyword.Bluemix_notm}} CLI 外掛程式儲存庫](http://plugins.{DomainName}/){: new_window}。

1. 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 cf CLI 外掛程式，請設定外掛程式登錄端點：
```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. 執行下列指令，以安裝外掛程式：```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *Admin Console* | *Development Mode* | 
|-----------------|-----------------|-----------------|
| 外掛程式名稱：active-deploy<br>  [檢視文件](../services/ActiveDeploy/index.html#cli) |  外掛程式名稱：bluemix-admin<br> [檢視文件](../cli/plugins/bluemix_admin/index.html) | 外掛程式名稱：development-name <br> [檢視文件](./plugins/dev_mode/index.html) | 

### 延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面：bx
1. 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式，請設定外掛程式登錄端點：
```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. 執行下列指令，以安裝外掛程式：```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| 外掛程式名稱：ibm-containers<br> [檢視文件](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 外掛程式名稱：auto-scaling <br> [檢視文件](./plugins/auto-scaling/index.html) |外掛程式名稱：VPN <br> [檢視文件](./plugins/vpn/index.html) |

## ![整合式開發工具](./images/Integrated_Dev_Tools.png) 整合式開發工具


下載並安裝外掛程式以整合您最愛的 {{site.data.keyword.Bluemix_notm}} 服務。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 外掛程式](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 外掛程式](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 外掛程式](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 外掛程式](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 外掛程式](../services/rules/index.html#rulov002) |
