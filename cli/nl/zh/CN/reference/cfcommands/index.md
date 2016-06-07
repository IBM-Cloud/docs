---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry (cf) 命令

*上次更新时间：2016 年 1 月 29 日*

您可以使用 Cloud Foundry (cf) 命令来管理应用程序。
{:shortdesc}

以下信息列出了管理应用程序最常用的 cf 命令。要列出所有 cf 命令及其帮助信息，请使用 `cf help`。使用 `cf command_name -h` 可查看特定命令的详细帮助信息。

*注：*如果您的网络中有 HTTP 代理服务器位于运行 cf 命令的主机和 Cloud Foundry API 端点之间，那么必须指定该代理服务器的主机名或 IP 地址，方法是设置 `HTTP_PROXY` 环境变量。有关详细信息，请参阅 [Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html)。

## cf api

显示或指定 {{site.data.keyword.Bluemix_notm}} API 端点的 URL。
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>Bluemix API 端点的 URL，必须指定该 URL 才能连接到 {{site.data.keyword.Bluemix_notm}}。通常，此 URL 为 https://api.{DomainName}。
如果您想显示当前正在使用的 API 端点的 URL，那么不需要为 cf api 命令指定此参数。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>禁用 SSL 验证过程。使用此参数可能会导致安全性问题。</dd>
<dt>*--unset*</dt>
<dd>除去所有 API 端点的连接信息。</dd>
</dl>

## cf apps

列出当前空间中部署的所有应用程序。还会显示每个应用程序的状态。

假定您有一个应用程序实例，那么在 cf apps 命令响应的实例列中，您会看到 1/1（如果应用程序启动）和 0/1（如果应用程序关闭）。如果您看到 ?/1，那么表明应用程序实例状态未知。您可以将应用程序 URL 复制到浏览器中来检查应用程序是否响应，也可以使用 `cf logs appname` 命令跟踪日志来查看应用程序是否在生成日志内容。

## cf bind-service

将现有服务实例绑定到应用程序。
```
cf bind-service appname service_instance
```

例如，如果您在当前组织和空间中有名为 `my_dataworks` 的服务实例，那么可以使用 `cf bind-service my_app
my_dataworks` 将此服务实例绑定到应用程序。

<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>service_instance</dt>
<dd>现有服务实例的名称。</dd>
</dl>

## cf create-service

创建服务实例。
```
cf create-service service_name service_plan service_instance
```
例如，您可以使用 `cf create-service DataWorks free my_dataworks` 来创建使用免费计划的 {{site.data.keyword.dataworks_short}} 服务的实例。

<dl>
<dt>service_name</dt>
<dd>服务的名称。</dd>
<dt>service_plan</dt>
<dd>服务套餐的名称。</dd>
<dt>service_instance</dt>
<dd>要用于您创建的新服务实例的名称。</dd>
</dl>

## cf create-space

创建空间。
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>空间的名称。</dd>
<dt>*-o*</dt>
<dd>要在其中创建空间的组织的名称。</dd>
<dt>*-q*</dt>
<dd>要分配给新创建的空间的配额。如果未指定，会自动分配缺省配额。</dd>
</dl>

## cf delete

删除现有应用程序。
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。<dd>
<dt>*-f*</dt>
<dd>在没有任何确认的情况下，强制删除应用程序。此参数是可选参数。</dd>
<dt>*-r*</dt>
<dd>删除与应用程序相关联的所有域名。此参数是可选参数。</dd>
</dl>

## cf delete-space

删除空间。
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>空间的名称。</dd>
<dt>*-f*</dt>
<dd>在没有任何确认的情况下，强制删除空间。此参数是可选参数。</dd>
*注：*删除空间的操作不可撤销。</dl>

## cf events

显示与应用程序有关的运行时事件。
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
</dl>

## cf help

显示所有 cf 命令的帮助信息。如果使用 command_name 参数，那么会显示特定 cf 命令的帮助信息。
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>命令的名称。如果想了解特定于某个命令的帮助信息，那么可以使用此参数。</dd>
<dd>如果不指定此参数，那么将显示所有 cf 命令的帮助信息。</dd>
</dl>


## cf login

登录到 {{site.data.keyword.Bluemix_notm}}。
```
cf login
```
发出 cf login 命令时，可以使用以下一个或多个参数：
<dl>
<dt>*-a* https://api.{DomainName}
	 </dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 端点的 URL。此参数是可选参数。</dd>
<dt>*-u* user_name</dt>
<dd>您的用户名。此参数是可选参数。</dd>
<dt>*-p* password</dt>
<dd>您的密码。</dd>
<dd>*重要信息：*如果在命令行界面上使用 *-p* 参数来提供密码，那么密码可能会记录在命令行历史记录中。出于安全考虑，请避免使用 -p 参数来提供密码。请改为在命令行界面提示您时输入密码。</dd>
<dt>*-o* organization_name</dt>
<dd>您要登录的组织的名称。</dd>
<dt>*-s* space_name</dt>
<dd>您要登录的空间的名称。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>禁用 SSL 验证过程。使用此参数可能会导致安全性问题。</dd>
</dl>

*注：*如果使用此命令的 *-p* 参数来提供密码，那么密码可能会记录在 shell 命令历史记录文件中，并且可能对本地操作系统的其他用户可见。


## cf logs

显示应用程序的 STDOUT 和 STDERR 日志流。
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>*--recent*</dt>
<dd>检索最新日志。</dd>
</dl>

## cf marketplace

列出 Marketplace 中可用的所有服务。此命令列出的服务还会显示在 {{site.data.keyword.Bluemix_notm}}“目录”中。
```
cf marketplace
```

## cf push

将新的应用程序部署到 Bluemix，或者更新 Bluemix 中现有的应用程序。
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>*-b* buildpack_name</dt>
<dd>buildpack 的名称。buildpack_name 可以是定制 buildpack 的名称，也可以是 Git URL，例如，`my-buildpack` 或 `https://github.com/heroku/heroku-buildpack-play.git`。</dd>
<dt>*-c* start_command</dt>
<dd>应用程序的启动命令。要使用缺省启动命令，请为此选项指定 null 值。例如：</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>您也可以使用此选项来运行脚本文件。例如：
```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>清单文件的路径。缺省清单文件为 manifest.yml，位于应用程序的根目录之下。</dd>
<dt>*-i* instance_number</dt>
<dd>实例数。</dd>
<dt>*-k* disk_limit</dt>
<dd>应用程序的磁盘限制，例如，*256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit</dt>
<dd>应用程序的内存限制，例如，*256M*、*1024M* 或 *1G*。</dd>
<dt>*-n* host_name</dt>
<dd>应用程序的主机名，例如，*my-subdomain*。</dd>
<dt>*-p* app_path</dt>
<dd>应用程序目录或应用程序归档文件的路径。</dd>
<dt>*-t* timeout</dt>
<dd>应用程序启动的最长时间（以秒为单位）。其他服务器端超时可能会覆盖此值。</dd>
<dt>*-s* stackname</dt>
<dd>要运行应用程序的堆栈。堆栈是预构建的文件系统，包括操作系统。使用 `cf stacks` 可查看 {{site.data.keyword.Bluemix_notm}} 中的可用堆栈。</dd>
<dt>*--no-hostname*</dt>
<dd>将 Bluemix 系统域映射到此应用程序。</dd>
<dt>*--no-manifest*</dt>
<dd>忽略缺省清单文件。</dd>
<dt>*--no-route*</dt>
<dd>不将路径映射到此应用程序。</dd>
<dt>*--no-start*</dt>
<dd>在应用程序部署后不启动该应用程序。</dd>
<dt>*--random-route*</dt>
<dd>为应用程序创建随机路径。</dd>
</dl>

## cf scale

显示或更改应用程序的实例编号、磁盘空间限制和内存限制。
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>*-i* instance_number</dt>
<dd>实例数</dd>
<dt>*-k* disk_limit</dt>
<dd>应用程序的磁盘限制，例如，*256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit</dt>
<dd>应用程序的内存限制，例如，*256M*、*1024M* 或 *1G*。</dd>
<dt>*-f*</dt>
<dd>在不提示的情况下，强制重新启动应用程序。</dd>
</dl>

## cf services

列出当前空间中可用的所有服务。
```
cf services
```

## cf set-env

设置应用程序的环境变量。
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>var_name</dt>
<dd>环境变量的名称。</dd>
<dt>var_value</dt>
<dd>环境变量的值。</dd>
</dl>

## cf stacks

列出所有堆栈。堆栈是预构建的文件系统，包括可运行应用程序的操作系统。
```
cf stacks
```

## cf stop

停止应用程序。
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
</dl>

## cf -v

显示 cf 命令行界面的版本。
```
cf -v
```

# 相关链接
{: #rellinks}
## 常规 
{: #general}
* [快速参考卡 - cf 命令](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
