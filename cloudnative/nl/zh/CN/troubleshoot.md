---

copyright:
  years: 2017
lastupdated: "2017-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# 故障诊断
{: #ts}

{{site.data.keyword.dev_cli_notm}} 的一些已知问题已经记录在文档中，并且提供了变通方法。
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## 已知问题
{: #knownissues}

以下各部分介绍了已知问题以及可能的解决方案。


### 使用非移动模式创建项目时，发生主机名被占用错误
{: #hostname}

如果使用 {{site.data.keyword.dev_cli_short}} 从 Web 应用程序、BFF 或微服务模式创建项目，那么可能会看到以下错误：

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### 原因
{: #hostname-cause}
   
此错误是由于登录令牌到期导致的。


#### 解决方案
{: #hostname-resolution}

重新登录。

```
bx login
```
{: codeblock}


### {{site.data.keyword.dev_cli_short}} 发生一般故障
{: #general}

如果使用 {{site.data.keyword.dev_cli_short}} 创建、删除或列出命令或者对其进行编码，那么可能会看到以下错误：

```
Failed to <command> project.
```
{: codeblock}


#### 原因
{: #general-cause}
   
此错误是由于登录令牌到期导致的。


#### 解决方案
{: #general-resolution}

重新登录。

```
bx login
```
{: codeblock}


### 添加 {{site.data.keyword.objectstorageshort}} 功能时发生服务代理错误
{: #os}

如果使用 {{site.data.keyword.dev_cli_short}} 通过 {{site.data.keyword.objectstorageshort}} 功能创建两个项目，那么可能会看到以下错误：

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### 原因
{: #os-cause}
   
此错误是由于 {{site.data.keyword.objectstorageshort}} 服务仅提供免费 {{site.data.keyword.objectstorageshort}} 套餐的一个实例导致的。


#### 解决方案
{: #os-resolution}

系统将提示您选择其他套餐以避免此错误。


### 创建项目期间获取代码失败
{: #code}

如果使用 {{site.data.keyword.dev_cli_short}} 创建项目，那么可能会看到以下错误：
	
```
FAILED                            
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### 原因
{: #code-cause}

此错误是由于内部超时导致的。
	

#### 解决方案
{: #code-resolution}

可以通过以下任一方式获得代码：

* 使用 CLI 运行以下命令：

   ```
bx dev code <your-project-name>
	```
   {: codeblock}

   将 `<your-project-name>` 替换为创建项目期间指定的项目名称。

* 使用 {{site.data.keyword.dev_console}}。

	1. 在 {{site.data.keyword.dev_console}} 中选择您的[项目 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://console.{DomainName}/developer/projects)，并单击**获取代码**。

	2. 单击**生成代码**。

	3. 生成代码后，单击**下载代码**。


### 针对 Node.js 项目运行 `bx dev run` 时出错
{: #node}

如果使用 {{site.data.keyword.dev_cli_short}} 针对 Node.js Web 或 BFF 项目运行 `bx dev run`，那么可能会看到以下错误：

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### 原因
{: #node-cause}
   
此错误是由于将 `appmetrics` 模块安装到其他体系结构中导致的。在一个体系结构上安装的本机 npm 模块无法在其他体系结构上使用。包含的 Docker 映像基于 Linux 内核。


#### 解决方案
{: #node-resolution}

删除 `node_modules` 文件夹并再次运行 `bx dev run`。


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## 获取帮助与支持
{: #gettinghelp}

如果您对 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 或 {{site.data.keyword.dev_cli_notm}} 有任何问题或疑问，可通过搜索信息或在论坛中提问获取帮助。您还可以提交支持凭单。

在论坛中提问时，请对问题进行标记，以便 {{site.data.keyword.Bluemix_notm}} 开发团队能看到您的问题。

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

如果在使用 {{site.data.keyword.dev_console}} 或 {{site.data.keyword.dev_cli_notm}} 开发或部署应用程序时遇到技术问题：

* 请将问题发布到 [Stack Overflow ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix)，并以 `bluemix-dev-services` 和 `ibm-bluemix` 来标记问题。
* 请将问题发布到 `bluemix-dev-services` 通道中的 [Slack ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm-cloud-tech.slack.com/)。立即[注册 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://ibm.biz/IBMCloudNativeSlack)。


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

请参阅[获取帮助 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/support/index.html#getting-help)，以获取有关使用论坛的更多详细信息。

有关提交 {{site.data.keyword.IBM}} 支持凭单或者有关支持级别和凭单严重性的信息，请参阅[联系支持人员 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](/docs/support/index.html#contacting-support)。

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

