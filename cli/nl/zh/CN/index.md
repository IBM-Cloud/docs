{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 和开发工具
{: #cli}

*上次更新时间：2016 年 1 月 19 日*

通过 {{site.data.keyword.Bluemix_short}}，您可以访问各种功能强大的工具，例如统一命令行界面和 CLI 插件。其中每个 CLI 下载都可用于增强您的 {{site.data.keyword.Bluemix_notm}} 体验。{:shortdesc}

## ![命令行界面](./images/CLI.png) 命令行界面
{: #downloads}

下载并安装命令行界面以便为您的 {{site.data.keyword.Bluemix_notm}} 体验提供支持。Cloud Foundry cf 命令行界面是所有其他 {{site.data.keyword.Bluemix_notm}} CLI 工具的先决条件。


| *Cloud Foundry：cf* |	*{{site.data.keyword.Bluemix_notm}}：bx* | 
|---------------------|---------------|
| [下载 CLI](https://github.com/cloudfoundry/cli/releases){: new_window}<br> [查看文档](./reference/cfcommands/index.html) | [下载 CLI](http://clis.{DomainName}/){: new_window}<br> [查看文档](./reference/bluemix_cli/index.html)| 

| *{{site.data.keyword.Bluemix_notm}} Live Sync：bl* |
|---------------|---------------|
| [Mac 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window}<br> [Windows 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window}<br> [查看文档](./reference/bl/index.html) |


## ![命令行界面插件](./images/CLI_Plugin.png) 命令行界面插件

使用更多命令轻松扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面。要访问 {{site.data.keyword.Bluemix_notm}} 命令行界面插件，请参阅 [{{site.data.keyword.Bluemix_notm}} CLI 插件存储库](http://plugins.{DomainName}/){: new_window}。

1. 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 cf CLI 插件，请设置插件注册表端点：```
cf add-plugin-repo bluemix-cf http://plugins.ng.bluemix.net
```
2. 运行以下命令来安装插件：```
cf install-plugin plugin_name -r bluemix-cf
```

| *Active Deploy* | *管理控制台* | *开发方式* | 
|-----------------|-----------------|-----------------|
| 插件名称：active-deploy<br>  [查看文档](../services/ActiveDeploy/index.html#cli) |  插件名称：bluemix-admin<br> [查看文档](../cli/plugins/bluemix_admin/index.html) | 插件名称：development-name<br> [查看文档](./plugins/dev_mode/index.html) | 

### 扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面：bx
1. 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 {{site.data.keyword.Bluemix_notm}} CLI 插件，请设置插件注册表端点：```
bluemix plugin repo-add bluemix-bx http://plugins.ng.bluemix.net
```
2. 运行以下命令来安装插件：```
bluemix plugin install plugin_name -r bluemix-bx
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* | *{{site.data.keyword.autoscaling}} CLI* | *VPN* |
|-----|----|----|
| 插件名称：ibm-containers<br> [查看文档](https://www.{DomainName}/docs/containers/container_cli_cfic.html#container_cli_cfic) | 插件名称：auto-scaling<br> [查看文档](./plugins/auto-scaling/index.html) |插件名称：VPN<br> [查看文档](./plugins/vpn/index.html) |

## ![集成开发工具](./images/Integrated_Dev_Tools.png) 集成开发工具


下载并安装插件，以集成首选的 {{site.data.keyword.Bluemix_notm}} 服务。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 插件](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}<br> [RTC Eclipse 插件](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 插件](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 插件](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 插件](../services/rules/index.html#rulov002) |
