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

# SDK Generator 插件
{: #sdk-cli}

{{site.data.keyword.IBM}} SDK Generator 插件可安装在 [{{site.data.keyword.Bluemix_notm}} CLI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/cli/reference/bluemix_cli/index.html) 中。

作为 {{site.data.keyword.Bluemix_notm}} 上的开发者，您可以使用此插件，从符合[开放 API 规范 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.openapis.org/) 的 REST API 定义中生成 SDK。当您对 REST API 定义进行更改时，可以使用此插件，仅重新生成 SDK 而非重新生成整个项目。

您还可以查看给定空间中的 Cloud Foundry 应用程序是否具有对生成 SDK 有效的 REST API 定义。最后，您可以使用 {{site.data.keyword.IBM_notm}} SDK Generator 插件，来验证任何 REST API 定义，以确保它们符合 SDK 生成器需求。

通过此 {{site.data.keyword.IBM_notm}} SDK Generator 插件，您可以轻松地将应用程序的后端服务与所生成的 SDK 相集成。当 REST API 发生更改时，可以重新生成 SDK 并替换旧的 SDK 以进行无缝 SDK 升级。您还可以将 CLI 集成到 DevOps 管道，并确保每次构建应用程序时，SDK 始终与 API 规范保持一致。

REST API 定义必须有效，或者在活动服务器端点上托管，或者是您系统上的本地文件。如果托管 REST API 定义，则必须在 `OPENAPI_SPEC` 环境变量中定义相对 URL。


## 需求
{: #prereqs}

确保满足以下需求。

* 具有 [{{site.data.keyword.Bluemix_notm}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://bluemix.net) 帐户
* 具有符合[开放 API ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.openapis.org/) 规范的有效 API 定义


## 安装
{: #installation}

1. [安装 {{site.data.keyword.Bluemix}} CLI ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html)。

2. [安装插件 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in)。

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## 命令
{: #commands}

使用以下命令，生成 SDK、验证开放 API 定义文件或列出 Cloud Foundry 应用程序。


### 生成 SDK
{: #gen}

使用 `bluemix sdk generate [arguments...][command options]`。


#### 自变量
{: #gen-args}

* `APP_NAME` - 当前空间中 Cloud Foundry 应用程序的名称
* `OPENAPI_DOC_LOCATION` - 原始 REST API 定义 JSON 或 Yaml 的 URL 或相对文件路径
* `GENERATED_SDK_NAME`（可选）- 所生成 SDK 的名称


#### 选项
{: #gen-options}

* `PLATFORM`（必要）
   * `--android` - 生成 Android SDK
   * `--ios` - 生成 iOS Swift SDK
   * `--swift` - 生成 Swift 服务器 SDK
* `--output "YOUR_RELATIVE_PATH"`（可选）- 将所生成的 SDK 置于 `YOUR_RELATIVE_PATH` 所指定的目录中（如果存在现有的 SDK 则覆盖）
* `--unzip`（可选）- 解压缩所生成的 SDK（如果存在现有的 SDK 工件则覆盖）


#### 用法
{: #gen-usage}

要通过在 {{site.data.keyword.Bluemix_notm}} 中运行的 Cloud Foundry 应用程序生成 SDK，可以使用应用程序的名称作为 CLI 的参数。以下命令使用应用程序的名称作为 `SDK_Name`。

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

要从开放 API 定义文件或本地 JSON 或 Yaml 文件的 URL 生成 SDK，请使用以下命令。

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### 验证开放 API 定义
{: #validating}

使用 `bluemix sdk validate [argument]`。


#### 自变量
{: #val-args}

* `APP_NAME` - 当前空间中 Cloud Foundry 应用程序的名称
* `OPENAPI_DOC_LOCATION` - 原始 REST API 定义 JSON 或 Yaml 的 URL 或相对文件路径


#### 用法
{: #val-usage}

要验证在 {{site.data.keyword.Bluemix_notm}} 中运行的 Cloud Foundry 应用程序 API 规范，可以使用应用程序的名称作为 CLI 的参数。

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

要从 API 规范文档或本地 JSON 或 Yaml 文件的 URL 验证 SDK，请使用以下命令。

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### 列出应用程序 (Cloud Foundry)
{: #list-apps}

使用 `bluemix sdk list [argument][option]` 可以列出应用程序并验证 API 规范。您必须已将 `OPENAPI_SPEC` 环境变量设置为托管规范的相对 URL 路径。


#### 自变量
{: #list-args}

* `SPACE_NAME`（可选）当前组织中您要搜索应用程序的 Cloud Foundry 空间的名称。如果未提供，则会搜索当前空间。


#### 选项
{: #list-options}

* `--url`（可选）- 为列表中的每个应用程序，显示开放 API 定义的完整 URL


#### 用法
{: #list-usage}

要列出当前空间中的应用程序，请使用以下命令。

```
bluemix sdk list
```
{: codeblock}

要列出当前空间中的应用程序并显示 API 规范 URL，请使用以下命令。

```
bluemix sdk list --url
```
{: codeblock}

要列出特定空间中的应用程序，请使用以下命令。

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

要列出特定空间中的应用程序并显示 API 规范 URL，请使用以下命令。

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
