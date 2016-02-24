{:shortdesc: .shortdesc}

# 用于与 {{site.data.keyword.Bluemix_notm}} 进行交互的 bx 命令
{: #bluemix_cli}

*上次更新时间：*2016 年 1 月 5 日

{{site.data.keyword.Bluemix}} 命令行界面 (CLI) 提供了一组按名称空间分组的命令，供用户用于与 {{site.data.keyword.Bluemix_notm}} 进行交互。某些 {{site.data.keyword.Bluemix_notm}} CLI 命令称为 bx 命令，是现有 cf 命令的包装程序，另一些 CLI 命令是 {{site.data.keyword.Bluemix_notm}} 独有的。以下信息列出了 {{site.data.keyword.Bluemix_notm}} CLI 支持的所有命令，并包含命令名称、选项、用法、先决条件、描述和示例。{:shortdesc}
 
**注：***先决条件*列出使用命令前必须执行的操作。没有任何先决条件操作的命令会列出**无**。否则，先决条件可能会包含以下一个或多个操作：
<dl>
<dt>端点</dt>
<dd>使用命令前，必须通过 <code>bluemix api</code> 设置 API 端点。</dd>
<dt>登录</dt>
<dd>使用命令前，必须通过 <code>bluemix login</code> 命令登录。</dd>
<dt>目标</dt>
<dd>使用命令前，必须通过 <code>bluemix target</code> 命令设置组织和空间。</dd>
</dl>

## bluemix help
显示 {{site.data.keyword.Bluemix_notm}} CLI 第一级内置命令和受支持名称空间的一般帮助，或者显示特定内置命令或名称空间的帮助。

```
bluemix help [COMMAND|NAMESPACE]
```

**先决条件**：无

**命令选项**：

*命令*|*NAMESPACE*（可选）：显示其帮助信息的命令或名称空间。如果未指定，将显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助。

**示例**：

显示 {{site.data.keyword.Bluemix_notm}} CLI 的一般帮助：

```
bluemix help
```

显示 `catalog` 名称空间的帮助信息：

```
bluemix help catalog
```

```
bluemix catalog help
```

显示 `info` 命令的帮助信息：

```
bluemix help info
```

显示 `catalog` 名称空间下 `templates` 命令的帮助信息：

```
bluemix catalog help templates
```


## bluemix api
设置或查看 {{site.data.keyword.Bluemix_notm}} API 端点。此命令会对 `cf api` 命令打包。

```
bluemix api [API_ENDPOINT][--unset]
```

**先决条件**：无

**命令选项**：

*API_ENDPOINT*（可选）：作为目标的 API 端点，例如 https://api.ng.bluemix.net。如果未指定 *API_ENDPOINT* 和 `--unset` 选项，将显示当前 API 端点。

`--unset`（可选）：除去 API 端点设置。

**示例**：

将 API 端点设置为 api.ng.bluemix.net：

```
bluemix api api.ng.bluemix.net
```

查看当前 API 端点：

```
bluemix api
```

取消设置 API 端点：

```
bluemix api --unset
```


## bluemix login
用户登录。此命令会对 `cf login` 命令打包。命令选项与 `cf login` 命令选项相同。

```
bluemix login [OPTIONS...]
```

**先决条件**：端点

**命令选项**：
有关 `login` 命令支持的选项的信息，请参阅 `cf login` 命令用法信息，以了解用于管理应用程序的 cf 命令。


## bluemix logout
注销用户。此命令会对 `cf logout` 命令打包。

```
bluemix logout
```

**先决条件**：无


## bluemix target
设置或查看目标组织或空间。此命令会对 `cf target` 命令打包。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**先决条件**：端点和登录

**命令选项**：

-o *ORG_NAME*（可选）：要作为目标的组织的名称。

-s *SPACE_NAME*（可选）：要作为目标的空间的名称。

如果 -o *ORG_NAME* 或 -s *SPACE_NAME* 均未指定，那么将显示当前组织和空间。

**示例**：

将当前组织设置为 `MyOrg`，将空间设置为 `MySpace`：

```
bluemix target -o MyOrg -s MySpace
```

查看当前组织和空间：

```
bluemix target
```


## bluemix info
查看基本 {{site.data.keyword.Bluemix_notm}} 信息，包括当前区域、云控制器版本以及一些有用的端点，例如用于登录和交换访问令牌的端点。

```
bluemix info
```

**先决条件**：端点





## bluemix regions
查看 {{site.data.keyword.Bluemix_notm}} 上所有区域的信息。

```
bluemix regions
```

**先决条件**：端点


## bluemix region-set
切换到指定的区域。此命令会自动重定向到新区域中的相同组织和空间（如果可能）。如果用户已登录，该命令会提示用户选择新的组织和空间。API 端点会相应地更改。

```
bluemix region-set REGION_NAME
```

**先决条件**：端点

**命令选项**：

*REGION_NAME*（必需）：要切换到的区域的名称。可以使用 `bluemix regions` 命令来查看所有区域名称。

**示例**：

将当前区域设置为 `eu-gb`：

```
bluemix region-set eu-gb
```



## bluemix config
将缺省值写入配置文件。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**先决条件**：无

**命令选项**：

--http-timeout *TIMEOUT_IN_SECONDS*：HTTP 请求的超时值。缺省值为 60 秒。

--trace true|false|*path/to/file*：跟踪对终端或指定文件的 HTTP 请求。

--color true|false：启用或禁用颜色输出。缺省情况下，会启用颜色输出。

--locale *LOCALE*：设置缺省语言环境。如果 LOCALE 为 *CLEAR*，那么将删除先前的语言环境。

一次只能指定其中一个选项。

**示例**：

将 HTTP 请求超时设置为 30 秒：

```
bluemix config --http-timeout 30
```

启用 HTTP 请求的跟踪输出：

```
bluemix config --trace true
```

跟踪对指定文件 */home/usera/my_trace* 的 HTTP 请求：

```
bluemix config --trace /home/usera/my_trace
```

禁用颜色输出：

```
bluemix config --color false
```

将语言环境设置为 zh_Hans：

```
bluemix config --locale zh_Hans
```

清除语言环境设置：

```
bluemix config --locale CLEAR
```










## bluemix list
列出当前空间中的所有应用程序、容器、容器组和 VM 组。

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**先决条件**：端点、登录和目标

**命令选项**：

apps（可选）：仅显示应用程序信息。

containers（可选）：仅显示容器信息。

container-groups（可选）：仅显示容器组信息。

vm-groups（可选）：仅显示 VM 组信息。

一次只能指定 `apps`、`containers`、`container-groups` 或 `vm-groups` 中的一个选项。如果未指定其中任何选项，那么将列出所有 cf 应用程序、容器、容器组和 VM 组。

**示例**：

列出所有 cf 应用程序：

```
bluemix list apps
```

列出所有容器实例：

```
bluemix list containers
```

列出所有应用程序、容器、容器组和 VM 组：

```
bluemix list
```


## bluemix scale
将 cf 应用程序或容器组向内扩展或向外扩展到指定的实例计数、磁盘配额和内存大小。

**注：**扩展容器组时，只能指定实例数。如果未指定任何选项，此命令将列出容器组的当前实例计数，以及 cf 应用程序的磁盘配额和内存大小。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：要扩展的 cf 应用程序或容器组的名称。

-i *INSTANCE_COUNT*（可选）：要扩展的 cf 应用程序或容器组的新实例数。对于要扩展的容器组，此选项是唯一有效的选项。

-k *DISK_QUOTA*（可选）：cf 应用程序的新磁盘配额。对于扩展容器组无效。

-m *MEMORY_SIZE*（可选）：cf 应用程序的新内存大小。对于扩展容器组无效。

**示例**：

显示 `my-container-group` 的当前实例数：

```
bluemix scale my-container-group
```

将 `my-container-group` 扩展到 2 个实例：

```
bluemix scale my-container-group -i 2
```

将 `my-java-app` 扩展到 3 个实例、8G 磁盘配额和 1024M 内存大小：

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
执行针对 {{site.data.keyword.Bluemix_notm}} 的原始 HTTP 请求。缺省情况下，*Content-Type* 设置为 *application/json*。此命令会将请求发送到 {{site.data.keyword.Bluemix_notm}} 控制台服务器（例如 https://console.ng.bluemix.net），而不是发送到 cf API 端点（例如 https://api.ng.bluemix.net）。

```
bluemix curl PATH [OPTIONS...]
```

**先决条件**：端点和登录

**命令选项**：

*PATH*（必需）：资源的 URL 路径。例如，/rest/v2/apps。

*OPTIONS*（可选）：`bluemix curl` 命令支持的选项与 `cf curl` 命令支持的那些选项相同。

**示例**：

检索所有样板模板的信息：

```
bluemix curl /rest/templates
```


## bluemix iam orgs
此命令的功能和选项与 `cf orgs` 命令的相同。不同的是，该命令还会显示组织所在的区域。


## bluemix iam org
此命令的功能和选项与 `cf org` 命令的相同。不同的是，该命令还会显示组织所在的区域。


## bluemix iam org-create
此命令的功能和选项与 `cf create-org` 命令的相同。





## bluemix iam org-replicate
将组织从当前区域复制到其他区域。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**先决条件**：端点和登录

**命令选项**：

*ORG_NAME*（必需）：要复制的现有组织的名称。

*REGION_NAME*（必需）：托管所复制组织的区域的名称。

**示例**：

将组织 `OE_Runtimes_Scaling` 复制到区域 `eu-gb`：

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














## bluemix iam org-rename
此命令的功能和选项与 `cf rename-org` 命令的相同。


## bluemix iam org-delete
此命令的功能和选项与 `cf delete-org` 命令的相同。


## bluemix iam spaces
此命令的功能和选项与 `cf spaces` 命令的相同。


## bluemix iam space
此命令的功能和选项与 `cf space` 命令的相同。


## bluemix iam space-create
此命令的功能和选项与 `cf create-space` 命令的相同。


## bluemix iam space-rename
此命令的功能和选项与 `cf rename-space` 命令的相同。


## bluemix iam space-delete
此命令的功能和选项与 `cf delete-space` 命令的相同。


## bluemix iam user-create
此命令的功能和选项与 `cf create-user` 命令的相同。


## bluemix iam user-delete
此命令的功能和选项与 `cf delete-user` 命令的相同。


## bluemix iam org-users
此命令的功能和选项与 `cf org-users` 命令的相同。


## bluemix iam org-role-set
此命令的功能和选项与 `cf set-org-role` 命令的相同。


## bluemix iam org-role-unset
此命令的功能和选项与 `cf unset-org-role` 命令的相同。


## bluemix iam space-users
此命令的功能和选项与 `cf space-users` 命令的相同。


## bluemix iam space-role-set
此命令的功能和选项与 `cf set-space-role` 命令的相同。


## bluemix iam space-role-unset
此命令的功能和选项与 `cf unset-space-role` 命令的相同。


## bluemix catalog templates
查看 Bluemix 上的样板模板。

```
bluemix catalog templates [-d]
```

**先决条件**：端点和登录

**命令选项**：

-d（可选）：如果指定了 `-d` 选项，那么还会显示每个模板的描述。否则，只显示每个模板的标识和名称。


## bluemix catalog template-run
使用指定 URL 和描述基于指定模板创建 cf 应用程序。缺省情况下，新应用程序将自动启动。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**先决条件**：端点、登录和目标

**命令选项**：

*TEMPLATE_ID*（必需）：创建应用程序时所基于的模板。使用 `bluemix templates` 可查看所有模板的标识。

*CF_APP_NAME*（必需）：要创建的 cf 应用程序的名称。

-u *URL*（可选）：应用程序的路径。如果未指定，路径将由 {{site.data.keyword.Bluemix_notm}} 根据您的应用程序名称和缺省域自动设置。

-d *DESCRIPTION*（可选）：应用程序的描述。

--no-start（可选）：应用程序创建后不自动启动。如果未指定，应用程序创建后将自动启动。

**示例**：

基于 `javaHelloWorld` 模板创建 cf 应用程序 `my-app`：

```
bluemix catalog template-run javaHelloWorld my-app
```

基于 `rubyHelloWorld` 模板创建应用程序 `my-ruby-app`，路径为 `myrubyapp.ng.bluemix.net`，描述为 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.`：

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

基于 `pythonHelloWorld` 模板创建应用程序 `my-python-app`，不带自动启动：

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```




## bluemix catalog template-register

在 {{site.data.keyword.Bluemix_notm}} 上注册新的样板模板。

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**先决条件**：端点和登录

**命令选项**：

*TEMPLATE_ID*（必需）：新注册的模板的标识。

*TEMPLATE_URL*（必需）：托管新模板元数据的 URL。

**示例**：

创建名为 `javaHelloWorld` 的模板：

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

取消注册现有的样板模板。

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**先决条件**：端点和登录

**命令选项**：

*TEMPLATE_ID*（必需）：使用 `bluemix catalog templates` 可查看所有模板标识。

-f（可选）：强制取消注册，而不进行确认。

**示例**：

取消注册模板 `javaHelloWorld`，而不进行确认：

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
查看 {{site.data.keyword.Bluemix_notm}} 模板注册表。

```
bluemix catalog template-registry
```

**先决条件**：端点









## bluemix catalog service-broker

查看指定的服务代理程序信息。

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**先决条件**：端点和登录

**命令选项**：

*SERVICE_BROKER_NAME*（必需）：要访问的服务代理程序的名称。


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
创建服务代理程序。

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**先决条件**：端点和登录

**命令选项**：

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE*（必需）：用于描述要创建的新服务代理程序的 JSON。可以使用 JSON 文件名，也可以直接使用 JSON 文本。

--no-billing（可选）：如果指定了此选项，那么会禁止对服务代理程序进行记帐。 

**示例**：

使用 JSON 文件创建服务代理程序：

```
bluemix catalog service-broker-create ./broker.json
```

使用 JSON 文本创建新的服务代理程序，并且不对该服务代理程序进行记帐：

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

以下示例显示了服务代理程序 JSON 和所有必填字段：

```
{
    "name": "my_broker",  // 服务代理程序的名称
    "broker_url": "http://my_broker.ng.bluemix.net"  // 指向服务代理程序元数据的 URL
    "auth_username": "username",
	"auth_password": "password",  // 用于访问服务代理程序 URL 的用户名和密码。用户名和密码应通过 HTTP 基本授权进行发送。
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
更新现有服务代理程序。

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**先决条件**：端点和登录

**命令选项**：

*ORIGINAL_BROKER_NAME*（必需）：要更新的服务代理程序的名称。

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE*（必需）：用于描述服务代理程序的新 JSON。可以使用 JSON 文件名，也可以直接使用 JSON 文本。

**示例**：

更新现有服务代理程序 `auto-scaling`：

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

有关服务代理程序 JSON 格式的更多详细信息，请参阅 [bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create)。


## bluemix catalog service-broker-delete

删除指定的服务代理程序。

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**先决条件**：端点和登录

**命令选项**：

*SERVICE_BROKER_NAME*（必需）：要删除的服务代理程序的名称。

-f（可选）：强制删除，而不进行确认。

**示例**：

删除服务代理程序 `auto-scaling`，而不进行确认：

```
bluemix catalog service-broker-delete auto-scaling -f
```














## bluemix network routes
此命令的功能和选项与 `cf routes` 命令的相同。


## bluemix network route-check
此命令的功能和选项与 `cf check-route` 命令的相同。


## bluemix network route-map
将路径映射到具有指定域和主机名的现有 cf 应用程序或容器组。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：要与路径进行映射的 cf 应用程序或容器组的名称。

*DOMAIN*（必需）：路径的域。例如，mybluemix.net 或 ng.bluemix.net。 

-n *HOST_NAME*（可选）：路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。

**示例**：

使用指定的域将路径映射到 `my-app`：

```
bluemix network route-map my-app mybluemix.net
```

使用指定域和主机名将路径映射到“my-container-group”：

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
取消来自现有 cf 应用程序或容器组中的指定路径映射。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**先决条件**：端点、登录和目标

**命令选项**：

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*（必需）：cf 应用程序或容器组的名称。

*DOMAIN*（必需）：路径的域（例如，mybluemix.net 或 ng.bluemix.net）。 

-n *HOST_NAME*（可选）：路径的主机名。如果未提供，缺省情况下主机名将设置为应用程序名称或容器组名称。

**示例**：

从 `my-app` 取消 `my-app.mybluemix.net` 的映射：

```
bluemix network route-unmap my-app mybluemix.net
```

从 `my-container-group` 取消 `abc.ng.bluexmix.net` 的映射：

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
此命令的功能和选项与 `cf create-route` 命令的相同。


## bluemix network route-delete
此命令的功能和选项与 `cf delete-route` 命令的相同。


## bluemix network orphaned-routes-delete
此命令的功能和选项与 `cf delete-orphaned-routes` 命令的相同。


## bluemix network domains
此命令的功能和选项与 `cf domains` 命令的相同。


## bluemix network domain-create
此命令的功能和选项与 `cf create-domain` 命令的相同。


## bluemix network domain-delete
此命令的功能和选项与 `cf delete-domain` 命令的相同。


## bluemix network shared-domain-create
此命令的功能和选项与 `cf create-shared-domain` 命令的相同。


## bluemix network shared-domain-delete
此命令的功能和选项与 `cf delete-shared-domain` 命令的相同。




## bluemix security cert

列出指定主机的证书信息。

```
bluemix security cert HOST_NAME
```

**先决条件**：端点和登录

**命令选项**：

*HOST_NAME*（必需）：托管证书的服务器的名称。

**示例**：

查看主机 `ibmcxo-eventconnect.com` 上的证书：

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

将证书添加到当前组织中的指定域。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**先决条件**：端点、登录和目标

**命令选项**：

*DOMAIN*（必需）：将证书添加到其中的域。

-k *PRIVATE_KEY_FILE*（必需）：专用密钥文件路径。

-c *CERT_FILE*（必需）：证书文件路径。

-p *PASSWORD*（可选）：证书的密码。

-i *INTERMEDIATE_CERT_FILE*（可选）：中间证书文件路径。

--verify-client（可选）：是否启用客户机证书验证。

**示例**：

将证书添加到域 `ibmcxo-eventconnect.com`：

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
从当前组织中的指定域除去证书。

```
bluemix security cert-remove DOMAIN [-f]
```

**先决条件**：端点、登录和目标

**命令选项**：

*DOMAIN*（必需）：要从中除去证书的域。

-f（可选）：强制删除，而不进行确认。








## bluemix plugin repos
列出 {{site.data.keyword.Bluemix_notm}} CLI 中注册的所有插件存储库。

```
bluemix plugin repos
```

**先决条件**：无


## bluemix plugin repo-add
将新的插件存储库添加到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**先决条件**：无

**命令选项**：

*REPO_NAME*（必需）：要添加的存储库的名称。可以为每个存储库定义您自己的名称。

*REPO_URL*（必需）：要添加的存储库的 URL。存储库 URL 必须包含协议（例如，http://plugins.ng.bluemix.net，而不是 plugins.ng.bluemix.net）。http://plugins.ng.bluemix.net 是 {{site.data.keyword.Bluemix_notm}} CLI 的官方插件存储库。

**示例**：

将 Bluemix CLI 的官方插件存储库添加为 `bluemix-repo`：

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
从 {{site.data.keyword.Bluemix_notm}} CLI 中除去插件存储库。

```
bluemix plugin repo-remove REPO_NAME
```

**先决条件**：无

**命令选项**：

*REPO_NAME*（必需）：要除去的存储库的名称。

**示例**：

从 {{site.data.keyword.Bluemix_notm}} CLI 中除去 `bluemix-repo` 存储库：

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
列出所有添加的存储库或特定存储库中的所有可用插件。

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**先决条件**：无

**命令选项**：

-r *REPO_NAME*（可选）：仅列出指定存储库中的插件。

**示例**：

列出所有添加的存储库中的所有插件：

```
bluemix plugin repo-plugin-list
```

列出 `bluemix-repo` 存储库中的所有插件：

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
列出 {{site.data.keyword.Bluemix_notm}} CLI 中的所有已安装插件。

```
bluemix plugin list
```

**先决条件**：无


## bluemix plugin install
从指定的路径或存储库将特定版本的插件安装到 {{site.data.keyword.Bluemix_notm}} CLI 中。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**先决条件**：无

**命令选项**：

*PLUGIN_PATH*|*PLUGIN_NAME*（必需）：如果未指定 `-r *REPO_NAME*`，那么将从指定的本地路径或远程 URL 安装插件。

-r *REPO_NAME*（可选）：插件二进制文件所在的存储库的名称。-v *VERSION*（可选）：要安装的插件的版本。如果未提供，将安装插件的最新版本。此选项仅对从存储库安装插件有效。

**示例**：

从本地文件安装插件：

```
bluemix plugin install /downloads/new_plugin
```

从远程 URL 安装插件：

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

从 `bluemix-repo` 存储库安装最新版本的 `IBM-Containers` 插件：

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
从 `bluemix-repo` 存储库安装版本为 `0.5.800` 的 `IBM-Containers` 插件：

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```






## bluemix plugin uninstall
从 {{site.data.keyword.Bluemix_notm}} CLI 中卸载指定的插件。

```
bluemix plugin uninstall PLUGIN_NAME
```

**先决条件**：无

**命令选项**：

*PLUGIN_NAME*（必需）：要卸载的插件的名称。

**示例**：

卸载先前安装的 `IBM-Containers` 插件：

```
bluemix plugin uninstall IBM-Containers
```
