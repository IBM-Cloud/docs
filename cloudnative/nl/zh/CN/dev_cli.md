---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

{{site.data.keyword.dev_cli_long}} 提供了可扩展的命令驱动方法，通过使用 `dev` 插件创建、开发和部署 Web 项目。对于想要在开发端到端微服务应用程序时使用命令行控件的开发者来说是理想的选择。

{: shortdesc}

{{site.data.keyword.dev_cli_notm}} 使用两个容器，便于构建和测试应用程序。第一个容器是工具容器，包含用于构建和测试应用程序所必需的实用程序。此容器的 Docker 文件通过 [dockerfile-tools](#command-parameters) 参数定义。您可以将其视为一个开发容器，因为它包含通常用于开发特定运行时的工具。

第二个容器是运行容器。此容器的形式适合部署在如 {{site.data.keyword.Bluemix}} 等产品中使用。因此，此容器一般会定义一个入口点，用于启动应用程序。选择通过 {{site.data.keyword.dev_cli_short}} 运行应用程序时，会使用此容器。此容器的 Docker 文件通过 [dockerfile-run](#run-parameters) 参数定义。


## 添加 {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### 先决条件
{: #prereq}

因为 {{site.data.keyword.dev_cli_short}} 不但可扩展性高，而且支持利用其他补充技术，所以必须满足一些先决条件，才能充分开发并正确利用其功能。

1. 安装 [Cloud Foundry CLI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/cli#getting-started)。

2. 安装 [{{site.data.keyword.Bluemix}} CLI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html)。

3. 获取 [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net) 标识。

4. 可选：如果计划在本地运行和调试应用程序，那么还必须安装 [Docker ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.docker.com/get-docker)。只有非移动项目需要执行此操作。


### 安装
{: #installation}

1. 通过运行以下命令安装 [{{site.data.keyword.dev_cli_short}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window}：
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	通过运行以下命令验证安装是否成功：  
 
	```
	bx dev
	```
	{: codeblock}
	

### 开始之前
{: #before-install}
	
1. 登录到 {{site.data.keyword.Bluemix_notm}}。

	```
	bx login
	```
	{: codeblock}
	
	**注：**如果凭证被拒绝，那么使用的可能是联合标识。执行下列步骤以使用联合标识进行认证。
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. 登录到 [{{site.data.keyword.iamshort}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.bluemix.net/iam/#/apikeys){: new_window}。
	2. 选择**创建 API 键**。
		* 输入 apiKey 名称和描述
	3. 下载 apiKey。
	4. 打开文件并从 `apiKey` 字段复制值。
	5. 使用以下命令登录：
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## 命令
{: #commands}

使用以下命令创建、部署、调试和测试项目。

### Build
{: #build}

您可以使用 `build` 命令构建应用程序。`build-cmd-run` 配置元素用于构建应用程序。`test`、`debug` 和 `run` 命令都会将构建作为正常操作的一部分来运行，其运行方式与 build 命令相同，因此不需要在执行这些命令之前执行 build 命令。

在当前项目目录中运行以下命令以构建应用程序：  

```
bx dev build
```
{: codeblock}


[Build 命令参数](#command-parameters)


### Code
{: #code}

`code` 命令用于在部署后下载应用程序代码，以便可在本地查看或执行其他更改。

运行以下命令以从指定项目下载代码。

```
bx dev code <projectName>
```
{: codeblock}


### Create
{: #create}

创建新项目，提示所有必需信息，包括语言、项目名称和应用程序模式类型。将在当前目录中创建项目。 

要在当前项目目录中创建新项目并将服务与其关联，请运行以下命令：

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

您可以通过 `debug` 命令调试应用程序。通过将 `build-cmd-debug` 配置元素用作构建指令，先针对项目完成构建。然后，容器开始公开 `container-port-map-debug` 中定义的调试端口。将偏好的调试工具连接到端口，可照常调试应用程序。

**限制：**：目前 Swift 项目不可用于调试。

在当前项目目录中运行以下命令以调试应用程序：

```
bx dev debug
```
{: codeblock}	

要退出调试会话，请使用 `CTRL-C`。


#### Debug 命令参数
{: #debug-parameters}

以下参数专用于 `debug` 命令，可帮助调试应用程序。

##### `container-port-map-debug`
{: #port-map-debug}

* 调试端口的端口映射。第一个值为要在主机操作系统中使用的端口，第二个值为容器中的端口 (host:container)。
* 用法：`bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* 用于为 DEBUG 构建代码。
* 用法：`bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* 用于在工具容器中调试代码。如果 `build-cmd-debug` 将以调试方式启动应用程序，那么这是可选的。
* 用法：`bx dev debug debug-cmd /the/debug/command`

#### 本地应用程序调试：
{: #local-app-dev}

有关本地应用程序调试的更多信息，请参阅[本地应用程序调试](docs/cloudnative/dev_cli_local_debug.html#local-debug)。


### Delete
{: #delete}

此命令用于从 {{site.data.keyword.Bluemix}} 空间除去项目。

运行以下命令可从 {{site.data.keyword.Bluemix}} 删除项目：

```
bx dev delete <projectName>
```
{: codeblock}
 

**注** **不会**除去 {{site.data.keyword.Bluemix}} 服务。


### Help
{: #help}

缺省情况下，如果未传入任何操作或自变量，或者，如果提供了“help”操作，那么此命令会显示常规“帮助”文本。显示的常规帮助包含基本自变量的描述以及可用操作的列表。  

运行以下命令以显示常规帮助信息：

```
bx dev help
```
{: codeblock}


### 列表
{: #list}

您可以列出空间中所有 {{site.data.keyword.Bluemix_notm}} 项目。

运行以下命令以列出项目：

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Run
{: #run}

您可以通过 `run` 命令运行应用程序。通过将 `build-cmd-run` 配置元素用作构建指令，先针对项目完成构建。然后，会启动运行容器，并公开 `container-port-map` 中定义的端口。如果运行容器不包含完成此步骤的入口点，那么可以使用 `run-cmd` 调用应用程序。 

在当前项目目录中运行以下命令以启动应用程序：

```
bx dev run
```
{: codeblock}

要退出会话，请使用 `CTRL-C`。


#### 运行参数
{: #run-parameters}

以下参数专用于 `run` 命令，可帮助管理运行容器中的应用程序。

##### `container-name-run`
{: #container-name-run}
	
* 运行容器的容器名称。
* 用法：`bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* 容器中要在运行时共享的位置。
* 用法：`bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* 容器中要针对运行共享的主机系统上的位置。
* 用法：`bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* 运行容器的 Docker 文件。
* 用法：`bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* 要从 dockerfile-run 创建的映像。
* 用法：`bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* 用于在运行容器中运行代码的可选参数。如果您的映像将启动应用程序，那么这是可选的。
* 用法：`bx dev run run-cmd [/the/run/command]`
	
### Status
{: #status}

您可以查询 `container-name-run` 和 `container-name-tools` 所定义的 {{site.data.keyword.dev_cli_short}} 使用的容器的状态。 

在当前项目目录中运行以下命令以检查容器状态：

```
bx dev status
```
{: codeblock}


[Status 命令参数](#command-parameters)


### Stop
{: #stop}

您可以通过 `stop` 命令停止容器。使用 `container-name` 参数可指定要停止的容器。如果未指定此参数，那么 stop 命令将停止 `container-name-run` 所定义的运行容器。 

在当前项目目录中运行以下命令以停止容器：

```
bx dev stop
```
{: codeblock}


#### 其他 stop 参数： 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* 工具容器的容器名称。
* 用法：`bx dev stop container-name <demo-tools>` 

### Test
{: #test}

您可以通过 `test` 命令测试应用程序。通过将 `build-cmd-run` 配置元素用作构建指令，先针对项目完成构建。然后，使用工具容器针对应用程序调用 `test-cmd`。

运行以下命令以测试应用程序： 

```
bx dev test
```
{: codeblock}


[Test 命令参数](#command-parameters)


## Build、debug、run 和 test 的参数
{: #command-parameters}

既可以将以下参数与 `build|debug|run|test` 命令配合使用，也可以通过命令行和/或直接更新项目的 `cli-config.yml` 文件来指定这些参数。其他参数可用于 [`debug`](#debug-parameters) 和 [`run`](#run-parameters) 命令，并且会记录在其各自的部分中。

**注**：在命令行上输入的命令参数优先于 `cli-config.yml` 配置。

##### `container-name-tools`  
{: #container-name-tools}

* 工具容器的容器名称。
* 用法：`bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* 主机上要针对 build、debug 和 test 共享的位置。
* 用法：`bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* 容器中要针对 build、debug 和 test 共享的位置。
* 用法：`bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* 容器的端口映射。第一个值为要在主机操作系统中使用的端口，第二个值为容器中的端口 (host:container)。
* 用法：`bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* 工具容器的 Docker 文件。
* 用法：`bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* 要从 dockerfile-tools 创建的映像。
* 用法：`bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* 用于针对除 DEBUG 之外的所有用法构建代码的命令。
* 用法：`bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* 用于在工具容器中测试代码的命令。
* 用法：`bx dev <build|debug|run|test> test-cmd [/the/test/command]`

