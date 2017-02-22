---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 和开发工具
{: #cli}

通过 {{site.data.keyword.Bluemix_short}}，您可以访问各种功能强大的工具，例如统一命令行界面和 CLI 插件。其中每个 CLI 下载都可用于支持您的 {{site.data.keyword.Bluemix_notm}} 体验。
{:shortdesc}

## ![](./images/CLI.svg) 命令行界面
{: #downloads}

下载并安装命令行界面以便为您的 {{site.data.keyword.Bluemix_notm}} 体验提供支持。

Cloud Foundry cf 命令行工具是所有 {{site.data.keyword.Bluemix_notm}} CLI 工具的必备软件。{{site.data.keyword.Bluemix_notm}} 命令行工具提供了管理 {{site.data.keyword.Bluemix_notm}} 环境以及 Cloud Foundry 应用程序的延伸体验。


缺省情况下，这两种 CLI 工具均使用 443 端口。如果在 CLI 工具与 {{site.data.keyword.Bluemix_notm}} 环境之间有 HTTP 代理，那么必须使用实际 HTTP 代理 URL 和端口（如有）来配置 `http-proxy` 环境变量。有关更多详细信息，请参阅 [Using the CLI with an HTTP Proxy Server ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}。


| *{{site.data.keyword.Bluemix_notm}}：bx* | *Cloud Foundry：cf* |
|---------------------|---------------|
| [下载 CLI](http://clis.ng.bluemix.net/)<br> [查看文档](/docs/cli/reference/bluemix_cli/index.html)|  [下载 CLI ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}<br> [查看文档](/docs/cli/reference/cfcommands/index.html) |
{: caption="Table 1. CLI download" caption-side="top"}


## ![](./images/CLI_Plugin.svg) 命令行界面插件

使用更多命令轻松扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面。要访问 {{site.data.keyword.Bluemix_notm}} 命令行界面插件，请参阅 [CLI 插件存储库 ![外部链接图标](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/)。

### 扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面：bx
{: cli_bluemix_ext}

* 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 {{site.data.keyword.Bluemix_notm}} CLI 插件，请设置插件注册表端点：

```
bluemix plugin repo-add bluemix-bx https://plugins.ng.bluemix.net
```
{: codeblock}

* 然后，运行以下命令来安装插件：

```
bluemix plugin install plugin_name -r bluemix-bx
```
{: codeblock}


| *{{site.data.keyword.activedeployshort}} CLI* | *{{site.data.keyword.autoscaling}} CLI* | *IBM Containers*  |
|-----|-----|-----|
| 插件名称：active-deploy<br> [查看文档](/docs/services/ActiveDeploy/cli.html#cli) | 插件名称：auto-scaling<br> [查看文档](/docs/cli/plugins/auto-scaling/index.html) |  插件名称：IBM-Containers<br> [查看文档](/docs/cli/plugins/containers/index.html) |
{: caption="Table 2. Plug-ins" caption-side="top"}

|  *专用网络对等* | *VPN*  |
|-----|-----|
| 插件名称：private-network-peering<br> [查看文档](/docs/cli/plugins/pnp/index.html) |插件名称：VPN<br> [查看文档](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="Table 3. Plug-ins" caption-side="top"}


### 扩展 Cloud Foundry 命令行界面：cf
{: cli_cf_ext}

* 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 cf CLI 插件，请设置插件注册表端点：

```
cf add-plugin-repo bluemix-cf https://plugins.ng.bluemix.net
```
{: codeblock}

* 然后，运行以下命令来安装插件：

```
cf install-plugin plugin_name -r bluemix-cf
```
{: codeblock}


| *Active Deploy* | *管理控制台* |
|-----------------|-----------------|
| 插件名称：active-deploy<br>  [查看文档](/docs/services/ActiveDeploy/cli.html#cli) |  插件名称：bluemix-admin<br> [查看文档](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="Table 4. Plug-ins" caption-side="top"}


| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 插件名称：ibm-containers<br> [查看文档](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 插件名称：VPN<br> [查看文档](/docs/cli/plugins/vpn/index.html) |
{: caption="Table 5. Plug-ins" caption-side="top"}


## ![](./images/Integrated_Dev_Tools.svg) 集成开发工具

下载并安装插件，以集成首选的 {{site.data.keyword.Bluemix_notm}} 服务。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *Eclipse Tools for Bluemix* |
|-------------|----------|----------|----------|----------|
| [Egit Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window} <br> [RTC Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](/docs/services/rules/index.html#rulov002) | [Bluemix Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){: new_window} |
{: caption="Table 6. Plug-ins" caption-side="top"}
