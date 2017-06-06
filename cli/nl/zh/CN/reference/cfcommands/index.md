---



copyright:

  years: 2016, 2017

lastupdated: "2017-05-04"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Cloud Foundry (cf) 命令
{: #cf}

Cloud Foundry (cf) 命令行界面 (CLI) 提供了一组用于管理应用程序的命令。以下信息列出了管理应用程序最常用的 cf 命令，并包含命令名称、选项、用法、先决条件、描述和示例。要列出所有 cf 命令及其关联的帮助信息，请使用 `cf help`。使用 `cf command_name -h` 可查看特定命令的详细帮助信息。
{: shortdesc}

**注**：如果您的网络中有 HTTP 代理服务器位于运行 cf 命令的主机和 Cloud Foundry API 端点之间，那么必须通过设置 `HTTP_PROXY` 环境变量来指定该代理服务器的主机名或 IP 地址。有关详细信息，请参阅 [Using the cf CLI with an HTTP Proxy Server ![外部链接图标](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window}。


## Cloud Foundry CLI 命令索引
{: #CLIname_commands_index}

使用下表中的索引可查看常用 Cloud Foundry 命令：

<table summary="按字母顺序列出的常规 Cloud Foundry 命令（命令具有可获取命令更多信息的链接）">
 <caption>表 1. 常规 Cloud Foundry 命令</caption>
 <thead>
 <th colspan="6">常规 Cloud Foundry 命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="按字母顺序列出的用于管理应用程序、空间和服务的命令。每个命令都具有可获取命令更多信息的链接。">
 <caption>表 2. 用于管理应用程序、空间和服务的命令</caption>
 <thead>
 <th colspan="5">用于管理应用程序、空间和服务的命令</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[scale](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

使用此命令可显示或指定 {{site.data.keyword.Bluemix_notm}} API 端点的 URL。

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>先决条件</strong>：无。

<strong>命令选项</strong>：

   <dl>
   <dt>BluemixServerURL（可选）</dt>
   <dd>Bluemix API 端点的 URL，必须指定该 URL 才能连接到 {{site.data.keyword.Bluemix_notm}}。通常，此 URL 为 `https://api.{DomainName}`。
   如果您想显示当前正在使用的 API 端点的 URL，那么不需要为 cf api 命令指定此参数。</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>禁用 SSL 验证过程。使用此参数可能会导致安全性问题。</dd>
   <dt>* --unset</dt>
   <dd>除去所有 API 端点的连接信息。</dd>
    </dl>

<strong>示例</strong>：

查看当前 API 端点
```
cf api
```
{: codeblock}

除去与 api.ng.bluemix.net 的所有 API 端点的连接
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

禁用 api.ng.bluemix.network 的 SSL 验证过程
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

列出当前空间中部署的所有应用程序。还会显示每个应用程序的状态。

假定您有一个应用程序实例，那么在 cf apps 命令响应的实例列中，您会看到 1/1（如果应用程序启动）和 0/1（如果应用程序关闭）。如果您看到 ?/1（表明应用程序实例状态未知），您可以将应用程序 URL 复制到浏览器中来检查应用程序是否有响应，也可以使用 `cf logs appname` 命令跟踪日志来查看应用程序是否在生成日志内容。

```
cf apps
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`


## cf bind-service
{: #cf_bind-service}

将现有服务实例绑定到应用程序。


```
cf bind-service appname service_instance
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

   <dl>
   <dt>appname（必需）</dt>
   <dd>应用程序的名称。</dd>
   <dt>service_instance（必需）</dt>
   <dd>现有服务实例的名称。</dd>
    </dl>

<strong>示例</strong>：

将名为 `my_dataworks` 的服务实例绑定到名为 `my_app` 的应用程序。
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

创建服务实例

```
cf create-service service_name service_plan service_instance
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

   <dl>
   <dt>service_name（必需）</dt>
   <dd>服务的名称。</dd>
   <dt>service_plan（必需）</dt>
   <dd>服务套餐的名称。</dd>
   <dt>service_instance（必需）</dt>
   <dd>要用于您创建的新服务实例的名称。</dd>
    </dl>

<strong>示例</strong>：

创建使用`免费`套餐的 {{site.data.keyword.dataworks_short}} 服务实例。
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

创建空间。


```
cf create-space space_name [-o] [-q]
```

<strong>先决条件</strong>：`cf api` 和 `cf login`

<strong>命令选项</strong>：

   <dl>
   <dt>space_name（必需）</dt>
   <dd>空间的名称。</dd>
   <dt>*-o*（可选）</dt>
   <dd>要在其中创建空间的组织的名称。</dd>
   <dt>*-q*（可选）</dt>
   <dd>要分配给新创建的空间的配额。如果未指定，会自动分配缺省配额。</dd>
    </dl>

<strong>示例</strong>：

创建名为 new_space 的空间
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

删除现有应用程序。


```
cf delete appname [-f] [-r]
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

   <dl>
   <dt>appname（必需）</dt>
   <dd>应用程序的名称。</dd>
   <dt>*-f*（可选）</dt>
   <dd>在没有任何确认的情况下，强制删除应用程序。</dd>
   <dt>*-r*（可选）</dt>
   <dd>删除与应用程序相关联的所有域名。</dd>
    </dl>

<strong>示例</strong>：

删除名为 `my_app` 的应用程序（将需要确认）。
```
cf delete my_app
```
{: codeblock}

删除名为 `my_app` 的应用程序，而无需确认。
```
cf delete my_app -f
```
{: codeblock}

删除名为 `my_app` 的应用程序以及与 `my_app` 关联的所有域名。
```
cf delete my_app -r
```
{: codeblock}

删除名为 `my_app` 的应用程序以及与 `my_app` 关联的所有域名，而无需确认。
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

删除空间。

```
cf delete-space space_name [-f]
```

<strong>先决条件</strong>：`cf api` 和 `cf login`

<strong>命令选项</strong>：

   <dl>
   <dt>space_name（必需）</dt>
   <dd>空间的名称。</dd>
   <dt>*-f*（可选）</dt>
   <dd>在没有任何确认的情况下，强制删除空间。</dd>
   *注：*删除空间的操作不可撤销。
</dl>

<strong>示例</strong>：

删除名为 `my_app` 的应用程序（将需要确认）。
```
cf delete my_app
```
{: codeblock}

删除名为 `my_app` 的应用程序，而无需确认。
```
cf delete my_app -f
```
{: codeblock}

删除名为 `my_app` 的应用程序以及与 `my_app` 关联的所有域名。
```
cf delete my_app -r
```
{: codeblock}

删除名为 `my_app` 的应用程序以及与 `my_app` 关联的所有域名，而无需确认。
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

显示与应用程序有关的运行时事件。


```
cf events [appname]
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

   <dl>
   <dt>appname</dt>
   <dd>应用程序的名称。</dd>
   </dl>

<strong>示例</strong>：

显示名为 `my_app` 的应用程序的事件。
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

显示所有 cf 命令或特定 cf 命令的帮助信息。

```
cf help [command_name]
```

<strong>先决条件</strong>：无。

<strong>命令选项</strong>：

   <dl>
   <dt>command_name（可选）</dt>
   <dd>命令的名称。</dd>
    </dl>

<strong>示例</strong>：

显示所有 cf 命令的帮助信息。
```
cf help
```
{: codeblock}

显示 events 命令的帮助信息。
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}

登录到 {{site.data.keyword.Bluemix_notm}}。
如果您使用[联合标识](/docs/admin/account.html#signup)登录，那么必须使用单点登录 (SSO) 参数才能登录。 

**注**：您还可以使用 {{site.data.keyword.Bluemix_notm}} Platform API 密钥来登录。请使用用户名 `apikey` 并将 API 密钥值作为密码。有关创建 API 密钥的更多信息，请参阅[管理 API 密钥](/docs/iam/apikeys.html)。

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>先决条件</strong>：无。

<strong>命令选项</strong>：

<dl>
<dt>*-a* https://api.{DomainName}（可选）</dt>
<dd>{{site.data.keyword.Bluemix_notm}} API 端点的 URL。</dd>
<dt>*-u* user_name（可选）</dt>
<dd>您的用户名。</dd>
<dt>*-p* password（可选）</dt>
<dd>您的密码。</dd>
<dd>*重要信息：*如果在命令行界面上使用 *-p* 参数来提供密码，那么密码可能会记录在命令行历史记录中。出于安全考虑，请避免使用 -p 参数来提供密码。请改为在命令行界面提示您时输入密码。</dd>
<dt>*-sso*</dt>
<dd>使用联合标识登录时，必须使用单点登录选项 (SSO)。使用 IBM 标识登录时则无需如此。如果您尝试使用联合标识登录，但未指定 SSO 参数，系统将提示您使用该参数。使用 SSO 参数会在登录时提示您输入一次性密码。</dd>
<dt>*-o* organization_name</dt>
<dd>您要登录的组织的名称。</dd>
<dt>*-s* space_name</dt>
<dd>您要登录的空间的名称。</dd>
<dt>*--skip-ssl-validation*（可选）</dt>
<dd>禁用 SSL 验证过程。使用此参数可能会导致安全性问题。</dd>
</dl>

*注：*如果使用此命令的 *-p* 参数来提供密码，那么密码可能会记录在 shell 命令历史记录文件中，并且可能对本地操作系统的其他用户可见。

<strong>示例</strong>：

登录到 {{site.data.keyword.Bluemix_notm}}。
```
cf login
```
{: codeblock}

使用定义的端点 `https://api.ng.bluemix.net` 登录到 {{site.data.keyword.Bluemix_notm}}。
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

使用定义的端点 `https://api.ng.bluemix.net` 登录到 {{site.data.keyword.Bluemix_notm}}，用户名为 `user_name`，但出于安全原因，未指定密码。
```
cf login -a https://api.ng.bluemix.net -u user_name
```
{: codeblock}

使用定义的端点 `https://api.ng.bluemix.net` 登录到 {{site.data.keyword.Bluemix_notm}}，用户名为 `user_name`，组织名称为 `org_name`，空间名称为 `space_name`，但出于安全原因，未指定密码。
```
cf login -a https://api.ng.bluemix.net -u user_name -o org_name -s space_name
```
{: codeblock}

使用 API 密钥通过定义的端点 `https://api.ng.bluemix.net` 登录到 {{site.data.keyword.Bluemix_notm}}。请将 `apikey` 用作用户名，将实际 API 密钥用作密码。
```
cf login -a https://api.ng.bluemix.net -u apikey -p ThisValueIsYourAPIKey
```
{: codeblock}


## cf logs
{: #cf_logs}

显示应用程序的 STDOUT 和 STDERR 日志流。


```
cf logs appname [--recent]
```
<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>*--recent*（可选）</dt>
<dd>检索最新日志。</dd>
</dl>

<strong>示例</strong>：

显示名为 `my_app` 的应用程序的日志流。
```
cf logs my_app
```
{: codeblock}

显示名为 `my_app` 的应用程序的最近日志流。
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

列出 Marketplace 中可用的所有服务。此命令列出的服务还会显示在 {{site.data.keyword.Bluemix_notm}}“目录”中。


```
cf marketplace
```
<strong>先决条件</strong>：`cf api`

<strong>命令选项</strong>：无。

<strong>示例</strong>：

列出 marketplace 中的所有服务
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

将新的应用程序部署到 {{site.data.keyword.Bluemix_notm}}，或者更新 {{site.data.keyword.Bluemix_notm}} 中现有的应用程序。

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

<dl>
<dt>appname（必需）</dt>
<dd>应用程序的名称。</dd>
<dt>*-b* buildpack_name（可选）</dt>
<dd>buildpack 的名称。buildpack_name 可以是定制 buildpack 的名称（例如，liberty-for-java），也可以是 Git URL（例如，https://github.com/cloudfoundry/java-buildpack.git）或者带有分支或标记的 Git URL（例如，对于 v3.3.0 标记，URL 为 https://github.com/cloudfoundry/java-buildpack.git#v3.3.0）。</dd>
<dt>*-c* start_command（可选）</dt>
<dd>应用程序的启动命令。要使用缺省启动命令，请为此选项指定 null 值。</dd>
<dt>*-f* manifest_path（可选）</dt>
<dd>清单文件的路径。缺省清单文件为 manifest.yml，位于应用程序的根目录之下。</dd>
<dt>*-i* instance_number（可选）</dt>
<dd>实例数。</dd>
<dt>*-k* disk_limit（可选）</dt>
<dd>应用程序的磁盘限制。可能的值为 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-m* memory_limit（可选）</dt>
<dd>应用程序的内存限制。可能的值为 *256M*、*1024M* 或 *1G*。</dd>
<dt>*-n* host_name（可选）</dt>
<dd>应用程序的主机名，例如，*my-subdomain*。</dd>
<dt>*-p* app_path（可选）</dt>
<dd>应用程序目录或应用程序归档文件的路径。</dd>
<dt>*-s* stack_name（可选）</dt>
<dd>要运行应用程序的堆栈。堆栈是预构建的文件系统，包括操作系统。使用 `cf stacks` 可查看 {{site.data.keyword.Bluemix_notm}} 中的可用堆栈。</dd>
<dt>*-t* timeout（可选）</dt>
<dd>应用程序启动的最长时间（以秒为单位）。其他服务器端超时可能会覆盖此值。</dd>
<dt>*--no-hostname*（可选）</dt>
<dd>将 {{site.data.keyword.Bluemix_notm}} 系统域映射到此应用程序。</dd>
<dt>*--no-manifest*（可选）</dt>
<dd>忽略缺省清单文件。</dd>
<dt>*--no-route*（可选）</dt>
<dd>不将路径映射到此应用程序。</dd>
<dt>*--no-start*（可选）</dt>
<dd>在应用程序部署后不启动该应用程序。</dd>
<dt>*--random-route*（可选）</dt>
<dd>为应用程序创建随机路径。</dd>
</dl>

<strong>示例</strong>：

使用缺省启动命令启动名为 `my_app` 的应用程序。
```
cf push `my_app` -c null
```
{: codeblock}

使用用于运行名为 `run.sh` 的脚本文件的选项启动名为 `my_app` 的应用程序。
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

显示或更改应用程序的实例编号、磁盘空间限制和内存限制。


```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

<dl>
<dt>appname（必需）</dt>
<dd>应用程序的名称。</dd>
<dt>*-i* instance_number（可选）</dt>
<dd>实例数</dd>
<dt>*-k* disk_limit（可选）</dt>
<dd>应用程序的磁盘限制；可能的值为 `256M`、`1024M` 或 `1G`。</dd>
<dt>*-m* memory_limit（可选）</dt>
<dd>应用程序的内存限制；可能的值为 `256M`、`1024M` 或 `1G`。</dd>
<dt>*-f*（可选）</dt>
<dd>在不提示的情况下，强制重新启动应用程序。</dd>
</dl>

<strong>示例</strong>：

显示名为 `my_app` 的应用程序的实例编号、磁盘空间限制和内存限制。
```
cf scale my_app
```
{: codeblock}

对于名为 `my_app` 的应用程序，将实例编号修改为 `1234`，磁盘空间限制修改为 `1G`，内存限制修改为 `1G`。
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services

{: #cf_services}

列出当前空间中可用的所有服务。


```
cf services
```
<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：无。

<strong>示例</strong>：

列出当前空间中的所有服务。
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

设置应用程序的环境变量

```
cf set-env appname var_name var_value
```
<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

<dl>
<dt>appname（必需）</dt>
<dd>应用程序的名称。</dd>
<dt>var_name（必需）</dt>
<dd>环境变量的名称。</dd>
<dt>var_value（必需）</dt>
<dd>环境变量的值。</dd>
</dl>

<strong>示例</strong>：

对于名为 `my_app` 的应用程序，将名为 `variable_a` 的环境变量设置为值 `123`。
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

以安全方式访问应用程序容器。`cf ssh` 命令可以用于设置交互式 SSH 会话、运行远程命令、传输文件以及设置特定应用程序容器实例的端口转发。

```
cf ssh
```
<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

缺省情况下，Diego 应用程序已启用 SSH 访问。可以使用 `cf ssh-enabled` 命令来验证是否启用了 SSH 访问，或者使用 `cf enable-ssh` 命令来启用 SSH 访问（如果已禁用）。 

<strong>命令选项</strong>：

<dl>
<dt>appname</dt>
<dd>应用程序的名称。</dd>
<dt>-c</dt>
<dd>指定要运行的远程命令。</dd>
<dt>-i</dt>
<dd>将应用程序的特定实例设为目标。如果未指定，将使用应用程序的第一个实例（索引为 0 的实例）。</dd>
<dt>-L</dt>
<dd>启用本地端口转发，这会将计算机上的输出端口绑定到应用程序 VM 的输入端口。</dd>
<dt>-N</dt>
<dd>不运行远程命令。</dd>
<dt>-t、-tt 或 -T</dt>
<dd>支持在伪 tty 方式下运行 SSH 会话，而不生成终端行输出。<dd>
</dl>

<strong>示例</strong>：

启动与运行 `my_app` 应用程序的容器实例的交互式 SSH 会话。
```
$ cf ssh my_app
```
{: codeblock}

在 `my_app` 应用程序容器实例上运行单个命令。
```
$ cf ssh my_app -c "ls -l"
```

从 `my_app` 应用程序容器实例传输单个文件。
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

设置从本地计算机上 7777 端口到 `my_app` 应用程序容器实例上 8888 端口的端口转发。
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks

{: #cf_stacks}

列出所有堆栈。堆栈是预构建的文件系统，包括可运行应用程序的操作系统。


```
cf stacks
```
<strong>先决条件</strong>：`cf api` 和 `cf login`

<strong>命令选项</strong>：无。

<strong>示例</strong>：

列出所有堆栈。
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

停止应用程序

```
cf stop appname
```
<strong>先决条件</strong>：`cf api`、`cf login` 和 `cf target`

<strong>命令选项</strong>：

<dl>
<dt>appname（必需）</dt>
<dd>应用程序的名称。</dd>
</dl>

<strong>示例</strong>：

停止名为 `my_app` 的应用程序。
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

设置或查看目标组织或空间

```
cf target [-o org_name] [-s space_name]
```
<strong>先决条件</strong>：`cf api` 和 `cf login`

<strong>命令选项</strong>：

<dl>
<dt>-o *org_name*（可选）</dt>
<dd>空间所在的组织的名称。</dd>
<dt>-s *space_name*（可选）</dt>
<dd>空间的名称。</dd>
</dl>

<strong>示例</strong>：

将目标设置为名为“my_org”的组织和名为“my_space”的空间。
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

显示 cf 命令行界面的版本。


```
cf -v
```
<strong>先决条件</strong>：无。

<strong>命令选项</strong>：无。

<strong>示例</strong>：

显示 cf 命令行界面的版本。
```
cf -v
```
{: codeblock}



# 相关链接
{: #rellinks}

## 相关链接
{: #general}

* [下载 Cloud Foundry CLI ![外部链接图标](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases)
{: new_window}
* [Quick Reference Card - cf commands ![外部链接图标](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html)
{: new_window}
