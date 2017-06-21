---



copyright:

  years: 2015, 2017

lastupdated: "2017-05-15"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# 下载
{: #cli}

通过 {{site.data.keyword.Bluemix_short}}，您可以访问各种功能强大的工具，例如统一命令行界面和 CLI 插件。其中每个 CLI 下载都可用于支持您的 {{site.data.keyword.Bluemix_notm}} 体验。
{:shortdesc}

## ![](./images/CLI.svg) 命令行界面
{: #downloads notoc}

下载并安装命令行工具以便为您的 {{site.data.keyword.Bluemix_notm}} 体验提供支持。

{{site.data.keyword.Bluemix_notm}} CLI 提供了管理 {{site.data.keyword.Bluemix_notm}} 环境的命令行体验。它还在其安装中包含 Cloud Foundry 命令行界面 (cf)，用于管理 Cloud Foundry 应用程序和服务。 

缺省情况下，这两种 CLI 工具均使用 443 端口。如果在 CLI 工具与 {{site.data.keyword.Bluemix_notm}} 环境之间有 HTTP 代理，那么必须使用实际 HTTP 代理 URL 和端口（如有）来配置 `HTTP_PROXY` 环境变量。有关更多详细信息，请参阅 [Using the CLI with an HTTP Proxy Server ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/cf-cli/http-proxy.html){: new_window}。

[下载 {{site.data.keyword.Bluemix_notm}} CLI ![外部链接图标](../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/){: new_window}<br> 
[查看文档](/docs/cli/reference/bluemix_cli/index.html)

## ![](./images/CLI_Plugin.svg) 命令行界面插件
{: #cliplugins notoc}

使用更多命令轻松扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面。要访问 {{site.data.keyword.Bluemix_notm}} 命令行界面插件，请参阅 [CLI 插件存储库 ![外部链接图标](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window}。

### 扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面：bx
{: #cli_bluemix_ext notoc}


安装 {{site.data.keyword.Bluemix_notm}} CLI 工具后，缺省情况下，[CLI 插件存储库 ![外部链接图标](../icons/launch-glyph.svg)](https://plugins.ng.bluemix.net/){: new_window} 预配置了存储库别名 `Bluemix`。您可以直接安装可用的插件。

```
bluemix plugin install plugin_name -r Bluemix
```

| *{{site.data.keyword.autoscaling}} CLI* |  *IBM Bluemix Container Service*  |
|-----|-----|-----|
| 插件名称：auto-scaling<br> [查看文档](/docs/cli/plugins/auto-scaling/index.html) |  插件名称：container-service<br> [查看文档](/docs/containers/cs_cli_devtools.html) |
{: caption="表 2. 插件" caption-side="top"}

|  *专用网络对等连接* | *VPN*  |
|-----|-----|
| 插件名称：private-network-peering<br> [查看文档](/docs/cli/plugins/pnp/index.html) | 插件名称：VPN<br> [查看文档](/docs/cli/plugins/bx_vpn/index.html) |
{: caption="表 3. 插件" caption-side="top"}

您还可以从符合 {{site.data.keyword.Bluemix_notm}} CLI 体系结构的其他存储库添加插件。
1. 要从其他存储库安装 {{site.data.keyword.Bluemix_notm}} CLI 插件，请设置插件注册表端点：
```
bluemix plugin repo-add bluemix-other-repo [repo_url]
```
其中，`repo_url` 是插件存储库的 HTTPS URL。

2. 运行以下命令来安装插件：
```
bluemix plugin install plugin_name -r bluemix-other-repo
```


### 扩展 Cloud Foundry 命令行界面：bx cf
{: #cli_cf_ext notoc}

安装 {{site.data.keyword.Bluemix_notm}} 命令行工具后，还会在 Bluemix CLI 目录内安装 Cloud Foundry 命令行界面。使用 `bluemix cf` 运行 Cloud Foundry CLI 命令。

* 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 cf CLI 插件，请设置插件注册表端点：

```
bluemix cf add-plugin-repo bluemix-cf-repo https://plugins.ng.bluemix.net
```
{: codeblock}

* 然后，运行以下命令来安装插件：

```
bluemix cf install-plugin plugin_name -r bluemix-cf-repo
```
{: codeblock}

| *管理控制台* |
-----------------|
|  插件名称：bluemix-admin<br> [查看文档](/docs/cli/plugins/bluemix_admin/index.html) |
{: caption="表 4. 插件" caption-side="top"}

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *VPN* |
|-----------------|-----------------|
| 插件名称：ibm-containers<br> [查看文档 ![外部链接图标](../icons/launch-glyph.svg)](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic){: new_window} | 插件名称：VPN<br> [查看文档](/docs/cli/plugins/vpn/index.html) |
{: caption="表 5. 插件" caption-side="top"}

## ![](./images/Integrated_Dev_Tools.svg) 集成开发工具
{: #ide notoc}

下载并安装插件，以集成首选的 {{site.data.keyword.Bluemix_notm}} 服务。

| *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* | *API Connect* | *Eclipse Tools for Bluemix* |
|----------|----------|----------|----------|----------|
| [Liberty Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 插件](../services/rules/index.html#rulov002) | [开发者工具箱](/docs/services/apiconnect/apic_003.html#apic_001 ) | [Bluemix Eclipse 插件](/docs/manageapps/eclipsetools/eclipsetools.html) |
{: caption="表 6. 插件" caption-side="top"}
