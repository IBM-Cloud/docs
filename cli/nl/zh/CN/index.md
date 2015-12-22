{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# CLI 和开发工具
{: #cli}

*上次更新时间：2015 年 11 月 10 日*

{{site.data.keyword.Bluemix_short}} 的强大工具。{:shortdesc}

## ![命令行界面](./images/CLI.png) 命令行界面
{: #downloads}

下载并安装命令行界面以便为您的 {{site.data.keyword.Bluemix_notm}} 体验提供支持。Cloud Foundry cf 命令行界面是所有其他 {{site.data.keyword.Bluemix_notm}} CLI 工具的先决条件。


| *Cloud Foundry：cf* |	*{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}：ice* | *{{site.data.keyword.Bluemix_notm}} Live Sync：bl* |
|---------------------|---------------|---------------|
| [下载 CLI](https://github.com/cloudfoundry/cli/releases){: new_window}<br> [查看文档](./reference/cfcommands/index.html) |[下载 Docker](https://docs.docker.com/installation/){: new_window}<br> [ice Mac 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.pkg){: new_window}<br> [ice Windows 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.exe){: new_window}<br> [ice Linux 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_ice.tar.gz){: new_window}<br> [查看文档](../containers/container_cli_ice_ov.html) | [Mac 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.pkg){: new_window}<br> [Windows 安装程序](ftp://public.dhe.ibm.com/cloud/bluemix/cli/Bluemix_bl.exe){: new_window}<br> [查看文档](./reference/bl/index.html) |


## ![命令行界面插件](./images/CLI_Plugin.png) 命令行界面插件

使用更多命令轻松扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面。要访问 {{site.data.keyword.Bluemix_notm}} 命令行界面插件，请参阅 [{{site.data.keyword.Bluemix_notm}} CLI 插件存储库](http://plugins.{DomainName}/){: new_window}。

1. 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 cf CLI 插件，请设置插件注册表端点：```
cf add-plugin-repo bluemix-cf-staging http://plugins.ng.bluemix.net
```
2. 运行以下命令来安装插件：```
cf install-plugin plugin_name -r bluemix-cf-staging
```

| *Active Deploy* |  *开发方式* | 
|-----------------|-----------------|
| 插件名称：active-deploy<br>  [查看文档](../services/ActiveDeploy/index.html#cli) |  插件名称：development-name<br> [查看文档](./plugins/dev_mode/index.html) | 

### 扩展 {{site.data.keyword.Bluemix_notm}} 命令行界面：bx
1. 要从 {{site.data.keyword.Bluemix_notm}} 注册表安装 {{site.data.keyword.Bluemix_notm}} CLI 插件，请设置插件注册表端点：```
bluemix plugin repo-add bluemix-bx-staging http://plugins.ng.bluemix.net
```
2. 运行以下命令来安装插件：```
bluemix plugin install plugin_name -r bluemix-bx-staging
```

| *{{site.data.keyword.IBM}} Containers for {{site.data.keyword.Bluemix_notm}}* |
|-----|
| 插件名称：ibm-containers<br> [查看文档](https://www.{{DomainName}}/docs/containers/container_cli_cfic.html#container_cli_cfic) |

## ![集成开发工具](./images/Integrated_Dev_Tools.png) 集成开发工具


下载并安装插件，以集成首选的 {{site.data.keyword.Bluemix_notm}} 服务。

| *{{site.data.keyword.jazzhub_short}}* | *Liberty for Java* | *MobileFirst* | *{{site.data.keyword.rules_short}}* |
|-------------|----------|----------|----------|
| [Egit Eclipse 插件](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_egit){: new_window}<br> [RTC Eclipse 插件](https://hub.jazz.net/docs/reference/gitclient/#eclipse_using_rtc){: new_window} | [Liberty Eclipse 插件](https://developer.ibm.com/wasdev/downloads/liberty-profile-using-eclipse/){: new_window} | [Eclipse 插件](https://marketplace.eclipse.org/content/ibm-mobilefirst-platform-studio){: new_window} | [Rules Designer Eclipse 插件](../services/rules/index.html#rulov002) |
