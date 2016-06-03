---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#部署应用程序
{: #deployingapps}

*上次更新时间：2016 年 5 月 9 日*

您可以使用各种方法（例如，命令行界面和集成开发环境 (IDE)）将应用程序部署到 {{site.data.keyword.Bluemix}}。您还可以使用应用程序清单来部署应用程序。通过使用应用程序清单，可减少每次将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。
{:shortdesc}

##应用程序部署
{: #appdeploy}

将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 包含两个阶段：应用程序编译打包和应用程序启动。

###应用程序编译打包

在编译打包阶段，Droplet Execution Agent (DEA) 会使用在 cf 命令行界面或 `manifest.yml` 文件中提供的信息来确定要为应用程序编译打包创建的内容。DEA 会选择相应的 buildpack 来编译打包应用程序，并且编译打包过程的结果为 Droplet。有关将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 的更多信息，请参阅 [{{site.data.keyword.Bluemix_notm}} 体系结构，{{site.data.keyword.Bluemix_notm}} 的工作方式](../public/index.html#publicarch)。

在编译打包过程中，DEA 会检查 buildpack 是否与应用程序相匹配。例如，Liberty 运行时用于 .war 文件，或者 Node.js 运行时用于 .js 文件。然后，DEA 会创建包含 buildpack 和应用程序代码的独立容器。容器由 Warden 组件进行管理。有关更多信息，请参阅 [How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}。

###应用程序启动

启动应用程序时，将创建 Warden 容器的一个或多个实例。可以使用 **cf files** 命令来查看存储在 Warden 容器的文件系统中的文件，例如日志。如果应用程序无法启动，那么 DEA 将停止该应用程序，并除去 Warden 容器的整个内容。因此，如果应用程序停止，或者如果应用程序的编译打包过程失败，那么不会有日志文件可供您使用。

如果应用程序的日志不再可用，并因此导致 **cf files** 命令无法再用于查看编译打包错误的原因，那么可以改用 **cf logs** 命令。**cf logs** 使用 Cloud Foundry 日志聚集器来收集应用程序日志和系统日志的详细信息，并且可以查看在日志聚集器中缓冲的内容。有关日志聚集器的更多信息，请参阅[在 Cloud Foundry 中进行日志记录](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}。

**注：**缓冲区大小是有限制的。如果应用程序运行了很长时间且未重新启动，那么输入 `cf logs appname --recent` 后可能不会显示日志，原因是日志缓冲区可能已清除。因此，要调试大型应用程序的编译打包错误，可以在部署应用程序时，在 cf 命令行界面的单独命令行中输入 `cf logs appname` 来跟踪日志。

如果在 {{site.data.keyword.Bluemix_notm}} 上编译打包应用程序时遇到问题，那么可以执行[调试编译打包错误](../debug/index.html#debugging-staging-errors)中的步骤来解决问题。

##使用 cf 命令部署应用程序
{: #dep_apps}

通过命令行界面将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，必须根据应用程序语言和框架来提供 buildpack，以作为运行时环境。您还可以使用 Delivery Pipeline 服务将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。

{{site.data.keyword.Bluemix_notm}} 提供了支持 Java 和 Node.js 的内置 buildpack。如果要使用这些语言和框架，那么使用命令行界面部署应用程序时，无需指定 buildpack。由于 {{site.data.keyword.Bluemix_notm}} 是基于 Cloud Foundry 构建的，因此命令缺省为这些 buildpack。

如果使用外部 buildpack，那么在通过命令提示符将应用程序部署到 {{site.data.keyword.Bluemix_notm}} 时，必须使用 **-b** 选项来指定 buildpack 的 URL。

  * 要将 Liberty 服务器软件包部署到 {{site.data.keyword.Bluemix_notm}}，请从源目录使用以下命令：
  
  ```
  cf push
  ```
  
  有关 Liberty buildpack 的更多信息，请参阅 [Liberty for Java](../runtimes/liberty/index.html)。
  
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
    
  有关 `package.json` 文件的更多信息，请参阅 [package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window}。
  
  * 要将 PHP、Ruby 或 Python 应用程序部署到 {{site.data.keyword.Bluemix_notm}}，请从包含应用程序源的目录中使用以下命令：
  
  ```
  cf push appname 
```

###在多个空间中部署应用程序

应用程序特定于部署该应用程序的空间。不能在 {{site.data.keyword.Bluemix_notm}} 中的空间之间移动或复制应用程序。要在多个空间中部署应用程序，必须通过以下步骤将应用程序部署在要使用应用程序的每个空间中：

  1. 使用带 **-s** 选项的 **cf target** 命令，切换到要部署应用程序的空间：
  
  ```
  cf target -s <space_name>
  ```
  
  2. 转至应用程序目录，然后使用 **cf push** 命令部署应用程序，其中 appname 必须在域中唯一。
  
  ```
  cf push appname 
```
  
##应用程序清单
{: #appmanifest}

应用程序清单包含应用于 **cf push** 命令的选项。可以使用应用程序清单来减少每次将应用程序推送到 {{site.data.keyword.Bluemix_notm}} 时必须指定的部署详细信息的数量。

在应用程序清单中，可以指定多个选项，例如要创建的应用程序实例数、要分配给应用程序的内存量和磁盘配额，以及应用程序的其他环境变量。您还可以使用应用程序清单来自动执行应用程序部署。清单文件的缺省名称为 `manifest.yml`。

###清单文件中的受支持选项

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
*表 1. manifest.yml 文件中的受支持选项*

###样本 `manifest.yml` 文件

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

##环境变量
{: #app_env}

环境变量包含 {{site.data.keyword.Bluemix_notm}} 上已部署应用程序的环境信息。除了通过 *Droplet Execution Agent
(DEA)* 和 buildpack 设置的环境变量，还可为 {{site.data.keyword.Bluemix_notm}} 上的应用程序设置特定于应用程序的环境变量。

您可通过使用 **cf env** 命令或从 {{site.data.keyword.Bluemix_notm}} 用户界面查看正在运行的 {{site.data.keyword.Bluemix_notm}} 应用程序的以下环境变量：
	
  * 特定于应用程序的用户定义变量。有关如何向应用程序添加用户定义的变量的信息，请参阅[添加用户定义的环境变量](#ud_env){:new_window}。
	 
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
  <dd>JSON 字符串，其中包含有关部署的应用程序的信息。此信息包括应用程序名称、URI、内存限制、应用程序达到其当前状态时的时间戳记等。例如：<pre class="pre codeblock"><code>
  {
    "limits": {
"mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
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
            "tags": [
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

通过 buildpack 定义的变量对于每个 buildpack 是不同的。请参阅 [buildpack](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}，以了解任何其他兼容 buildpack。



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

有关每个环境变量的更多信息，请参阅 [Cloud Foundry 环境变量](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}。

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
	2. 在左侧导航窗格中，单击**环境变量**。
	3. 单击**用户定义**，然后单击**添加**。
	4. 填写必填字段，然后单击**保存**。
  * 使用命令行界面。使用 ``cf set-env`` 命令添加用户定义的变量。例如：```
    cf set-env appname env_var_name env_var_value
    ``
	
  * 使用 ``manifest.yml`` 文件。在该文件中添加值对。例如：```
	env:
      VAR1:value1
      VAR2:value2
    ``
	
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
{: #rellinks}

## 相关链接
{: #general}

* [使用应用程序清单进行部署](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF 清单生成器](http://cfmanigen.mybluemix.net/){:new_window}
* [cf V6 入门](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [IBM Continuous Delivery Pipeline for Bluemix 入门](../services/DeliveryPipeline/index.html#getstartwithCD)
