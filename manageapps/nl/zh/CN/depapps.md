---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 部署应用程序
{: #deployingapps}

您可以使用各种方法（例如，命令行界面和集成开发环境 (IDE)）将应用程序部署到 {{site.data.keyword.Bluemix}}。您还可以使用应用程序清单来部署应用程序。通过使用应用程序清单，可减少每次将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。
{:shortdesc}

## 应用程序部署
{: #appdeploy}

将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 包含两个阶段：应用程序编译打包和应用程序启动。

Cloud Foundry 支持 Diego，这是全新的缺省运行时体系结构，它提供了一组功能，用于增强托管和构造云平台的应用程序开发体验。此体系结构更新改进了 Cloud Foundry 平台的总体运行情况和性能。新体系结构支持多种应用程序容器技术，包括 Garden 和 Windows，也支持允许直接登录到应用程序容器的 SSH 包以及其他创新性更改。有关近期体系结构升级的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![外部链接图标](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}。


您创建的所有新应用程序都将在 Diego 上运行，因此您必须开始将 DEA 上运行的现有应用程序迁移到新的 Diego 体系结构。

**注**：Cloud Foundry Diego 体系结构会影响所有 {{site.data.keyword.Bluemix_notm}} Public 区域环境。{{site.data.keyword.Bluemix_notm}} Dedicated 和 {{site.data.keyword.Bluemix_notm}} Local 环境将在日后更新。

### 应用程序编译打包
{: #diego}

在编译打包阶段，Diego 将处理与应用程序容器编排相关的所有方面。推送应用程序时，云控制器将向 Diego 发送编译打包请求，随后 Diego 将接管分配应用程序实例的任务。Diego 后端会以确保容错和长期一致性的方式对应用程序容器进行编排，并在一系列虚拟机（称为“单元”）之间均衡负载。此外，Diego 会确保用户可以访问其应用程序的日志。所有 Diego 组件都设计为进行集群，这意味着您可以创建不同的可用性区域。

为了验证应用程序的运行状况，Diego 支持用于 DEA 的基于端口的相同检查。但是，Diego 还设计为能够具备更通用的选项，如基于 URL 的运行状况检查，未来可能会启用这些选项。

#### 新应用程序编译打包
{: #stageapp}

所有新应用程序都会部署到 Diego 体系结构。要对新应用程序编译打包，请使用 **cf push** 命令部署应用程序：

  1. 部署应用程序：
  ```
  $ cf push APPLICATION_NAME
  ```

有关 **cf push** 命令的更多详细信息，请参阅 [cf push](/docs/cli/reference/cfcommands/index.html#cf_push)。

### 将现有应用程序迁移到 Diego
{: #migrateapp}

Diego 是 {{site.data.keyword.Bluemix_notm}} 的缺省 Cloud Foundry 体系结构，将除去对 DEA 的支持，所以您必须通过更新每个现有应用程序来迁移所有这些应用程序。通过使用 Diego 标志更新应用程序，开始将应用程序迁移到 Diego。应用程序将立即尝试开始在 Diego 上运行，并最终停止在 DEA 上运行。

在应用程序从 DEA 体系结构更新到 Diego 的过程中，您可能会遇到较短时间的停机，或者如果应用程序与 Diego 不兼容，那么可能会遇到较长时间的停机。为了缩短停机时间，请通过将应用程序的副本部署到 Diego，然后交换路径并向下扩展 DEA 应用程序，从而执行[蓝绿部署](/docs/manageapps/updapps.html#blue_green)。

要将应用程序迁移到 Diego，请执行以下步骤：

 1.  安装 [cf CLI ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 和 [Diego-Enabler CLI 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}。
 2. 查看[已知问题列表](depapps.html#knownissues)。
 3. 设置 Diego 标志以将应用程序更改为在 Diego 上运行：
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

更新应用程序后，验证应用程序是否已启动。如果迁移的应用程序无法启动，那么该应用程序会保持脱机状态，直到您确定并解决了问题，然后重新启动应用程序为止。

在将除去 DEA 体系结构支持时，IBM 将向您提醒即将到来的必需迁移时间段；如果您一直未迁移应用程序，操作团队将为您迁移所有应用程序。

要验证应用程序正在哪个后端上运行，请使用以下命令：

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Diego 迁移已知问题
{: #knownissues}

将应用程序迁移到 Diego 时，您可能需要解决以下已知问题：

  * 使用 `--no-route` 选项部署的工作程序应用程序未报告为“正常运行”。为了避免此问题，请使用 `cf set-health-check APP_NAME none` 命令禁用基于端口的运行状况检查。
  * 不再支持 **cf files** 命令。替代命令为 **cf ssh**。有关 **cf ssh** 命令的更多详细信息，请参阅 [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)。
  * 有些应用程序可能会使用大量文件描述符 (inode)。如果遇到此问题，必须使用 `cf scale APP_NAME [-k DISK]` 命令增大用于应用程序的磁盘限额。

有关已知问题的完整列表，请参阅 Cloud Foundry 文档页面中的 [Migrating to Diego ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}。

在除去对旧 DEA 体系结构的支持之前，可以运行以下命令转换回 DEA：`cf disable-diego APPLICATION_NAME`。此外，在除去该支持之前，您仍然可以将新应用程序部署到 DEA 体系结构：

**注**：您必须安装 [cf CLI ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 和 [Diego-Enabler CLI 插件 ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} 才可使用 `disable-diego` 命令。

1. 在不启动应用程序的情况下，对应用程序进行部署：
```
  $ cf push APPLICATION_NAME --no-start
  ```
2. 运行 disable-diego 命令：
```
  $ cf disable-diego APPLICATION_NAME
  ```
3. 启动应用程序：
```
  $ cf start APPLICATION_NAME
  ```

### 应用程序启动
{: #startapp}

启动应用程序时，将创建应用程序容器的一个或多个实例。对于在 Diego 上运行的应用程序，可以使用 **cf ssh** 或 **cf scp** 命令来访问包含日志的应用程序容器的文件系统。**cf files** 命令不适用于在 Diego 体系结构上运行的应用程序。

**注**：如果您仍有应用程序在 DEA 上运行，那么在除去对 DEA 的支持之前，您仍可以使用 **cf files** 命令来查看应用程序容器中的文件。

如果应用程序无法启动，那么该应用程序会停止，并会除去应用程序容器的整个内容。因此，如果应用程序停止，或者如果应用程序的编译打包过程失败，那么不会有日志文件可供您使用。

如果应用程序的日志不再可用，并因此导致 **cf ssh**、**cf scp** 或 **cf files** 命令无法再用于查看应用程序容器内编译打包错误的原因，那么可以改用 **cf logs** 命令。**cf logs** 使用 Cloud Foundry 日志聚集器来收集应用程序日志和系统日志的详细信息，并且可以查看在日志聚集器中缓冲的内容。有关日志聚集器的更多信息，请参阅 [Logging in Cloud Foundry ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}。

**注：**缓冲区大小是有限制的。如果应用程序运行了很长时间仍未重新启动，那么输入 `cf logs appname --recent` 命令后可能不会显示日志，原因是日志缓冲区可能已清除。因此，要调试大型应用程序的编译打包错误，可以在部署应用程序时，在 cf 命令行界面的单独命令行中输入 `cf logs appname` 命令来跟踪日志。

如果在 {{site.data.keyword.Bluemix_notm}} 上编译打包应用程序时遇到问题，那么可以执行[调试编译打包错误](/docs/debug/index.html#debugging-staging-errors)中的步骤来解决问题。


## 使用 cf 命令部署应用程序
{: #dep_apps}

通过命令行界面将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，必须根据应用程序语言和框架来提供 buildpack，以作为运行时环境。您还可以使用 Delivery Pipeline 服务将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。

{{site.data.keyword.Bluemix_notm}} 提供了支持 Java 和 Node.js 的内置 buildpack。如果要使用这些语言和框架，那么使用命令行界面部署应用程序时，无需指定 buildpack。由于 {{site.data.keyword.Bluemix_notm}} 是基于 Cloud Foundry 构建的，因此命令缺省为这些 buildpack。

如果使用外部 buildpack，那么在通过命令提示符将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，必须使用 **-b** 选项来指定 buildpack 的 URL。

  * 要将 Liberty 服务器软件包部署到 {{site.data.keyword.Bluemix_notm}}，请从源目录使用以下命令：

  ```
cf push
  ```

  有关 Liberty buildpack 的更多信息，请参阅 [Liberty for Java](/docs/runtimes/liberty/index.html)。

  * 要将 Java Tomcat 应用程序部署到 {{site.data.keyword.Bluemix_notm}}，请使用以下命令：

  ```
cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * 要将 WAR 包部署到 {{site.data.keyword.Bluemix_notm}}，请使用以下命令：

  ```
  cf push appname -p app.war
  ```
  或者，可通过使用以下命令指定包含应用程序文件的目录：

  ```
  cf push appname -p "./app"
  ```

  * 要将 Node.js 应用程序部署到 {{site.data.keyword.Bluemix_notm}}，请使用以下命令：

  ```
  cf push appname -p app_path
  ```

Node.js 应用程序中必须具有 `package.json` 文件，Node.js buildpack 才可识别此应用程序。`app.js` 文件是应用程序的入口脚本，可在 `package.json` 文件中指定该文件。以下示例显示简单的 `package.json` 文件：  
	

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  有关 `package.json` 文件的更多信息，请参阅 [package.json ![外部链接图标](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}。

  * 要将 PHP、Ruby 或 Python 应用程序部署到 {{site.data.keyword.Bluemix_notm}}，请从包含应用程序源的目录中使用以下命令：

  ```
  cf push appname
  ```

### 在多个空间中部署应用程序

应用程序特定于部署该应用程序的空间。不能在 {{site.data.keyword.Bluemix_notm}} 中的空间之间移动或复制应用程序。要在多个空间中部署应用程序，必须通过以下步骤将应用程序部署在要使用应用程序的每个空间中：

  1. 使用带 **-s** 选项的 **cf target** 命令，切换到要部署应用程序的空间：

  ```
  cf target -s <space_name>
  ```

  2. 转至应用程序目录，然后使用 **cf push** 命令部署应用程序，其中 appname 必须在域中唯一。

  ```
  cf push appname
  ```

## 应用程序清单
{: #appmanifest}

应用程序清单包含应用于 **cf push** 命令的选项。可以使用应用程序清单来减少每次将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。

在应用程序清单中，可以指定多个选项，例如要创建的应用程序实例数、要分配给应用程序的内存量和磁盘配额，以及应用程序的其他环境变量。您还可以使用应用程序清单来自动执行应用程序部署。清单文件的缺省名称为 `manifest.yml`。

### 清单文件中的受支持选项

下表显示了可在应用程序清单文件中使用的受支持选项。如果选择使用除 `manifest.yml` 以外的其他文件名，那么必须将 **-f** 选项用于 **cf push** 命令。在以下示例中，`appManifest.yml` 是文件名：

```
cf push -f appManifest.yml
```

<p>  </p>


|选项	|描述	|用法或示例|
|:----------|:--------------|:---------------|
|**buildpack**	|定制 buildpack 的 URL 或名称。	|`buildpack: ` *buildpack_URL*|
|**disk_quota**	|为应用程序分配的磁盘配额。缺省值为 1G。	|`disk_quota: 500M`|
|**domain**	|{{site.data.keyword.Bluemix_notm}} 中应用程序的域名。	|`domain:` ng.bluemix.net|
|**host**	|{{site.data.keyword.Bluemix_notm}} 中应用程序的主机名。此值在 {{site.data.keyword.Bluemix_notm}} 环境中必须唯一。	|`host: ` *host_name*|
|**name**	|{{site.data.keyword.Bluemix_notm}} 中的应用程序名称。此值在 {{site.data.keyword.Bluemix_notm}} 环境中必须唯一。	|`name: ` *appname*|
|**path**	|应用程序的位置。此值可以是相对路径，也可以是绝对路径。	|`path: ` *path_to_application*|
|**command**	|应用程序的定制启动命令，或用于运行脚本文件的命令。	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|为应用程序分配的内存量。缺省值为 1G。	|`memory: 512M`|
|**instances**	|要为应用程序创建的实例数。	|`instances: 2`|
|**timeout**	|用于启动应用程序的最大时间量（以秒为单位）。缺省值为 60 秒。	|`timeout: 80`|
|**no-route**	|布尔值，用于阻止将路径分配给仅在后台运行的应用程序。缺省值为 **false**。	|`no-route: true`|
|**random-route**	|布尔值，用于将随机路径分配给应用程序。缺省值为 **false**。	|`random-route: true`|
|**services**	|要绑定到应用程序的服务。	|`services: - mysql_maptest`|
|**env**	|应用程序的定制环境变量。|`env: DEV_ENV: production`|
{: caption="表 1. 清单 YAML 文件中的受支持选项" caption-side="top"}

### 样本 manifest.yml 文件

以下示例显示了在 {{site.data.keyword.Bluemix_notm}} 中使用内置社区 Node.js buildpack 的 Node.js 应用程序的清单文件。

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## 环境变量
{: #app_env}

环境变量包含 {{site.data.keyword.Bluemix_notm}} 上已部署应用程序的环境信息。除了通过 *Droplet Execution Agent
(DEA)* 和 buildpack 设置的环境变量，还可为 {{site.data.keyword.Bluemix_notm}} 上的应用程序设置特定于应用程序的环境变量。

您可通过使用 **cf env** 命令或从 {{site.data.keyword.Bluemix_notm}} 用户界面查看正在运行的 {{site.data.keyword.Bluemix_notm}} 应用程序的以下环境变量：

  * 特定于应用程序的用户定义变量。有关如何向应用程序添加用户定义的变量的信息，请参阅[添加用户定义的环境变量 ![外部链接图标](../icons/launch-glyph.svg)](#ud_env){:new_window}。

  * VCAP_SERVICES 变量，其中包含用于访问服务实例的连接信息。如果应用程序与多个服务绑定，那么 VCAP_SERVICES 变量会包含每个服务实例的连接信息。例如：

  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

您还有权访问通过 DEA 和 buildpack 设置的环境变量。

以下变量通过 DEA 定义：

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>已部署应用程序的根目录。</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>应用程序的每个实例可以使用的最大内存量。可以在应用程序 <span class="ph filepath">manifest.yml</span> 文件中指定此值，或者在推送应用程序时通过命令行指定。</dd>
  <dt><strong>PORT</strong></dt>
  <dd>DEA 上用于与应用程序进行通信的端口。DEA 在编译打包时会为应用程序分配端口。</dd>
  <dt><strong>PWD</strong></dt>
  <dd>运行 buildpack 的当前工作目录。</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>存储临时和编译打包文件的目录。</dd>
  <dt><strong>USER</strong></dt>
  <dd>运行 DEA 的用户标识。</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>DEA 主机的 IP 地址。</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>JSON 字符串，其中包含有关部署的应用程序的信息。此信息包括应用程序名称、URI、内存限制、应用程序达到其当前状态时的时间戳记等。例如：
<pre class="pre codeblock"><code>
  {
"limits": {
"mem": 512,
        "disk": 1024,
        "fds": 16384
        },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>JSON 字符串，包含与已部署应用程序绑定的服务的信息。例如：
<pre class="pre codeblock"><code>
  {
"mysql-5.5": [
        {
                        "name": "mysql-ix",
            "label": "mysql-5.5",
      "tags":[
"mysql",
                "relational",
                "data_management",
                "ibm_experimental"
                        ],
            "plan": "300",
"credentials": {
"name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
                }
    ]
}
</code></pre></dd>

</dl>

通过 buildpack 定义的变量对于每个 buildpack 是不同的。请参阅 [Buildpack ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}，以了解任何其他兼容 buildpack。


<ul>
    <li>以下变量通过 Liberty buildpack 定义：<dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>运行应用程序的 Java SDK 的位置。</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>运行应用程序时要使用的 Java SDK 选项。</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>用于在 DEA 中启动 Liberty 概要文件服务器实例的 Java 命令。</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>在 DEA 中启动 Liberty 概要文件服务器实例时共享资源和服务器定义的位置。</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>生成的输出（例如，日志文件）的位置以及正在运行的 Liberty 概要文件服务器实例的工作目录。</dd>
	  </dl>
</li>
<li>以下变量通过 Node.js buildpack 定义：
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Node.js 运行时环境的目录。</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Node.js 运行时环境用于高速缓存的目录。</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Node.js 运行时环境使用的系统路径。</dd>
	</dl>
</li>
</li>
</ul>

您可以使用以下样本 Node.js 代码来获取 VCAP_SERVICES 环境变量的值：

```
if (process.env.VCAP_SERVICES) {
var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

有关每个环境变量的更多信息，请参阅 [Cloud Foundry Environment Variables ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}。

## 定制应用程序部署
{: #customize_dep}

您可以为应用程序定制部署任务。例如，可以为应用程序指定启动命令，并可以配置应用程序启动环境。
{:shortdesc}

### 指定启动命令

要为应用程序指定启动命令，可以使用下列其中一种方式。指定的启动命令将覆盖 buildpack 提供的缺省启动命令。

**注：**如果希望 buildpack 的启动命令优先，请将 **null** 指定为启动命令。

  * 使用 **cf push** 命令并指定 -c 参数。例如，部署 Node.js 应用程序时，可以通过 -c 参数指定 **node app.js** 启动命令：

  ```
cf push appname -p app_path -c "node app.js"
  ```

  * 在 `manifest.yml` 文件中使用 command 参数。例如，部署 Node.js 应用程序时，可以在清单文件中指定 **node app.js** 启动命令：


  ```
command: node app.js
```


### 添加用户定义的环境变量
{: #ud_env}

用户定义的环境变量是特定于应用程序的。要向运行中应用程序添加用户定义的环境变量，可以使用以下选项：

  * 使用 {{site.data.keyword.Bluemix_notm}} 用户界面。请完成以下步骤：
    1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”上，单击应用程序磁贴。这将显示应用程序详细信息页面。
	2. 单击**环境变量**。
	3. 单击**用户定义**，然后单击**添加**。
	4. 填写必填字段，然后单击**保存**。
  * 使用命令行界面。使用 `cf set-env` 命令添加用户定义的变量。例如：
    ```
cf set-env appname env_var_name env_var_value
    ```

  * 使用 `manifest.yml` 文件。在该文件中添加值对。例如：
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```

添加了用户定义的环境变量后，可以使用以下样本 Node.js 代码来获取所定义变量的值：

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```

### 配置启动环境

要为应用程序配置启动环境，可以将 shell 脚本添加到 `/.profile.d` 目录中。`/.profile.d` 目录位于应用程序的构建目录下。`/.profile.d` 目录中的脚本由 {{site.data.keyword.Bluemix_notm}} 在应用程序运行之前运行。例如，可以将 NODE_ENV 环境变量设置为 **production**，方法是将包含以下内容的 `node_env.sh` 文件放入 `/.profile.d` 目录下：

```
export NODE_ENV=production;
```

###防止上传文件和目录

在使用 cf 命令行界面来部署应用程序时，通过忽略 {{site.data.keyword.Bluemix_notm}} 可在其他位置获得的某些文件和目录来节省上传时间。要防止这些文件和目录上传到 {{site.data.keyword.Bluemix_notm}}，您可以在应用程序的根目录中创建 `.cfignore` 文件。

**注：**`.cfignore` 文件必须为 UTF-8 格式。

`.cfignore` 文件包含您要忽略的文件和目录名称，每行一个名称。可以使用星号 (*) 作为通配符。指定目录时，该目录下的所有文件和子目录同时忽略。例如，`.cfignore` 文件中的以下内容指示所有 `.swp` 文件以及 `tmp/` 目录下的所有文件和子目录不会上传到 {{site.data.keyword.Bluemix_notm}}。

```
*.swp
tmp/
```

# 相关链接
{: #rellinks notoc}

## 相关链接
{: #general}

* [Deploying with Application Manifests ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![外部链接图标](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6 ![外部链接图标](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [IBM Continuous Delivery Pipeline for Bluemix 入门](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
