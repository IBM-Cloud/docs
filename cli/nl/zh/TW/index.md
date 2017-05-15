---



copyright:

  years: 2015, 2017

lastupdated: "2017-02-14"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 下載
{: #cli}

使用 {{site.data.keyword.Bluemix_short}}，您可以存取各種功能強大的工具，例如統一指令行介面和 CLI 外掛程式。其中每個 CLI 下載都可用來支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。
{:shortdesc}

## ![](./images/CLI.svg) 指令行介面
{: #downloads notoc}

下載及安裝指令行工具，以支援您的 {{site.data.keyword.Bluemix_notm}} 體驗。

{{site.data.keyword.Bluemix_notm}} CLI 提供指令行體驗來管理 {{site.data.keyword.Bluemix_notm}} 環境。它也會在其安裝中包括 Cloud Foundry 指令行介面 cf，用來管理 Cloud Foundry 應用程式及服務。 

這兩個 CLI 工具依預設都會使用 443 埠。如果您在 CLI 工具與 {{site.data.keyword.Bluemix_notm}} 環境之間有 HTTP Proxy，則必須使用實際 HTTP Proxy URL 及埠（如果有的話）來配置 `HTTP_PROXY` 環境變數。如需詳細資料，請參閱 [Using the CLI with an HTTP Proxy Server ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}。

[下載 {{site.data.keyword.Bluemix_notm}} CLI ![外部鏈結圖示](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window} <br> 
[檢視文件](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) 指令行介面外掛程式
{: #cliplugins notoc}

使用其他指令，輕鬆延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面。若要存取 {{site.data.keyword.Bluemix_notm}} 指令行介面外掛程式，請參閱 [CLI 外掛程式儲存庫 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}。

### 延伸您的 {{site.data.keyword.Bluemix_notm}} 指令行介面：bx
{: #cli_bluemix_ext notoc}


在您安裝 {{site.data.keyword.Bluemix_notm}} cli 工具之後，依預設會預先配置儲存庫別名為 `Bluemix` 的 [CLI 外掛程式儲存庫 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}。您可以直接安裝可用的外掛程式。

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Bluemix Container Service*  |
|-----|-----|-----|
| 外掛程式名稱：active-deploy<br> [檢視文件](/docs/services/ActiveDeploy/cli.html#cli) | 外掛程式名稱：auto-scaling <br> [檢視文件](/docs/cli/plugins/auto-scaling/index.html) | 外掛程式名稱：container-service  <br> [檢視文件](/docs/containers/cs_cli_devtools.html) |
{: caption="表 2. 外掛程式" caption-side="top"}

|  *專用網路對等作業* | *VPN*  |
|-----|-----|
| 外掛程式名稱：private-network-peering  <br> [檢視文件](/docs/cli/plugins/pnp/index.html) | 外掛程式名稱：VPN <br> [檢視文件](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="表 3. 外掛程式" caption-side="top"}

您也可以從符合 {{site.data.keyword.Bluemix_notm}} CLI 架構的其他儲存庫新增外掛程式。
1. 若要從另一個儲存庫安裝 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式，請設定外掛程式登錄端點：
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
其中 `repo_url` 是外掛程式儲存庫的 HTTPS URL。

2. 執行下列指令，以安裝外掛程式：
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### 延伸 Cloud Foundry 指令行介面：bx cf
{: #cli_cf_ext notoc}

在您安裝 {{site.data.keyword.Bluemix_notm}} 指令行工具之後，也會在 Bluemix CLI 目錄內安裝 Cloud Foundry 指令行介面。請使用 `bluemix cf` 執行 Cloud Foundry CLI 指令。

* 若要從 {{site.data.keyword.Bluemix_notm}} 登錄安裝 cf CLI 外掛程式，請設定外掛程式登錄端點：


```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* 然後，執行下列指令，以安裝外掛程式：

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *Active Deploy* | *Admin Console* |
|-----------------|-----------------|
| 外掛程式名稱：active-deploy<br>  [檢視文件](/docs/services/ActiveDeploy/cli.html#cli) |  外掛程式名稱：bluemix-admin<br> [檢視文件](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="表 4. 外掛程式" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 外掛程式名稱：ibm-containers<br> [檢視文件 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | 外掛程式名稱：VPN <br> [檢視文件](/docs/cli/plugins/vpn/index.html) |
{: caption="表 5. 外掛程式" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) 整合式開發工具
{: #ide notoc}

下載並安裝外掛程式以整合您最愛的 {{site.data.keyword.Bluemix_notm}} 服務。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|----------|
| [Egit Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 外掛程式](../services/rules/index.html#rulov002) | [Developer Toolkit ![外部鏈結圖示](../icons/launch-glyph.svg)](https://nextstage.torolab.ibm.com/apimanagement/getting-started/ ){: new_window} | [Bluemix Eclipse 外掛程式](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="表 6. 外掛程式" caption-side="top"}
