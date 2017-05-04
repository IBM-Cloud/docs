---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 及開發工具
{: #cli}

使用 {{site.data.keyword.Bluemix_short}}，您可以存取各種功能強大的工具，例如統一指令行介面和 CLI 外掛程式。其中每個 CLI 下載都可用來支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。
{:shortdesc}

## ![](./images/CLI.svg) 指令行介面
{: #downloads}

下載及安裝指令行介面，以支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。

Cloud Foundry cf 指令行工具是所有 {{site.data.keyword.Bluemix_notm}} CLI 工具的必備項目。{{site.data.keyword.Bluemix_notm}} 指令行工具提供管理 {{site.data.keyword.Bluemix_notm}} 環境及 Cloud Foundry 應用程式的延伸體驗。

這兩個 CLI 工具依預設都會使用 443 埠。如果您在 CLI 工具與 {{site.data.keyword.Bluemix_notm}} 環境之間有 HTTP Proxy，則必須使用實際 HTTP Proxy URL 及埠（如果有的話）來配置 `http-proxy` 環境變數。如需詳細資料，請參閱 [Using the CLI with an HTTP Proxy Server ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}。


| *{{site.data.keyword.Bluemix_notm}}：bx* | *Cloud Foundry：cf* |
|---------------------|---------------|
| [下載 CLI](http://clis.ng.bluemix.net/)  <br> [檢視文件](/docs/cli/reference/bluemix_cli/index.html)|  [下載 CLI ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}  <br> [檢視文件](/docs/cli/reference/cfcommands/index.html) |
{: caption="表 1. CLI 下載" caption-side="top"}


## ![](./images/CLI_Plugin.svg) 指令行介面外掛程式

使用其他指令，輕鬆延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面。若要存取 {{site.data.keyword.Bluemix_notm}} 指令行介面外掛程式，請參閱 [CLI 外掛程式儲存庫 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/)。

### 延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面：bx
{: cli_bluemix_ext}

* 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式，請設定外掛程式登錄端點：


```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* 然後，執行下列指令，以安裝外掛程式：

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Bluemix Container Service*  |
|-----|-----|-----|
| 外掛程式名稱：active-deploy<br> [檢視文件](/docs/services/ActiveDeploy/cli.html#cli) | 外掛程式名稱：auto-scaling <br> [檢視文件](/docs/cli/plugins/auto-scaling/index.html) |  外掛程式名稱：container-service  <br> [檢視文件](/docs/containers/cs_cli_devtools.html) |
{: caption="表 2. 外掛程式" caption-side="top"}

|  *專用網路對等作業* | *VPN*  |
|-----|-----|
| 外掛程式名稱：private-network-peering  <br> [檢視文件](/docs/cli/plugins/pnp/index.html) |外掛程式名稱：VPN <br> [檢視文件](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="表 3. 外掛程式" caption-side="top"}


### 延伸 Cloud Foundry 指令行介面：cf
{: cli_cf_ext}

* 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 cf CLI 外掛程式，請設定外掛程式登錄端點：


```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* 然後，執行下列指令，以安裝外掛程式：

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| 外掛程式名稱：active-deploy<br>  [檢視文件](/docs/services/ActiveDeploy/cli.html#cli) |  外掛程式名稱：bluemix-admin<br> [檢視文件](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="表 4. 外掛程式" caption-side="top"}


| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 外掛程式名稱：ibm-containers<br> [檢視文件](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 外掛程式名稱：VPN <br> [檢視文件](/docs/cli/plugins/vpn/index.html) |
{: caption="表 5. 外掛程式" caption-side="top"}


## ![](./images/Integrated_Dev_Tools.svg) 整合式開發工具

下載並安裝外掛程式以整合您最愛的 {{site.data.keyword.Bluemix_notm}} 服務。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|
| [Egit Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](/docs/services/rules/index.html#rulov002) | [Bluemix Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){: new_window} |
{: caption="表 6. 外掛程式" caption-side="top"}
