
{:shortdesc: .shortdesc}

# VCAP 服务

*上次更新时间：2015 年 11 月 9 日*


VCAP_SERVICES 环境变量是一个 JSON 对象，包含可用于与 {{site.data.keyword.Bluemix_notm}} 中的服务实例进行交互的信息。{:shortdesc}


## 检索 VCAP_SERVICES 环境变量的值
{:retrieving}

VCAP_SERVICES 环境变量是一个 JSON 对象，包含可用于与 {{site.data.keyword.Bluemix_notm}} 中的服务实例进行交互的信息。这些信息包括服务实例名称、凭证以及服务实例的连接 URL。这些值会在应用程序绑定到 {{site.data.keyword.Bluemix_notm}} 中的服务实例时填充到 VCAP_SERVICES 环境变量中。

只有在将服务实例绑定到应用程序时，VCAP_SERVICES 环境变量的值才可用。您可以通过使用 WebSocket 控制台驱动程序查看应用程序环境变量。以下示例显示了如何使用 WebSocket 控制台驱动程序来查看 Node.js 应用程序的环境变量。

首先，运行命令以重新推送 Node.js 应用程序。```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp```
接着，输入以下 URL：```
https://yourapp.{APPDomain}/bash.sh
```
在显示的页面中，单击复选标记以连接工具，然后发出 env 命令以查看应用程序的环境变量。有关 cf-debug-tools 的更多信息，请参阅 [Cloud Foundry 的调试工具](https://github.com/dmikusa-pivotal/cf-debug-tools)。


## 查看 Bluemix 基础架构层
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} 抽象化并隐藏操作系统和基础架构层，这样您就无需对这些内容进行管理。但是，有时您可能希望了解有关应用程序的操作系统和中间件的更多信息。

可以运行 cf stacks 命令来显示要将应用程序部署到其中的可用堆栈或根文件系统。还可以指定堆栈，方法是在运行 cf push 命令时使用 *-s* 选项和 *stack_name*，其中 stack_name 是根文件系统，例如 `lucid64` 或 `cflinuxfs2`：
```
cf push appName -s stack_name
```
可以使用 `cf buildpacks` 命令来显示作为运行时提供的供应用程序在其中运行的中间件组件，例如 WebSphere Liberty 概要文件和 SDK for Node.js。此外，可以使用以下命令来指定应用程序的运行时环境：
```
cf push appName -b buildpackname
```
