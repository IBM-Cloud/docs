---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Swift on Bluemix 入门

* {: download} 恭喜您，您已在 {{site.data.keyword.Bluemix}} 上部署了 Hello World 样本应用程序！要开始使用，请按照本逐步指南进行操作。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下载样本代码）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下载应用程序代码" />下载样本代码</a>并自行探究。

通过遵循本指南，您将设置开发环境，在本地以及在 {{site.data.keyword.Bluemix}} 上部署应用程序，以及在应用程序中集成 {{site.data.keyword.Bluemix}} 数据库服务。

## 先决条件
{: #prereqs}
* [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}
* [Cloud Foundry CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* 适用于您平台的 [Swift 编译器 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://swift.org/download/)。

## 1. 克隆样本应用程序
{: #clone}

现在，您可以开始使用简单的 Swift 应用程序。克隆存储库，并切换到样本应用程序所在的目录。
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  仔细阅读 *get-started-swift* 目录中的文件，以熟悉其内容。

## 2. 在本地运行应用程序
{: #run_locally}

一旦安装了 Swift 编译器并克隆了此 Git 存储库，就可以立即编译并运行应用程序。转至系统上此存储库的根目录，并发出以下命令：
```
swift build
```
{: pre}

运行此命令可能需要几分钟时间。

一旦成功编译了应用程序，就可以运行 Swift 编译器生成的可执行文件：
```
.build/debug/kitura-helloworld
```
{: pre}

您应该会看到类似于以下内容的输出：

```
Server is listening on port: 8080
```
{: screen}

在 http://localhost:8080 中查看您的应用程序

## 3. 准备应用程序进行部署
{: #prepare}

如果要部署到 {{site.data.keyword.Bluemix_notm}}，设置 manifest.yml 文件会很有用。manifest.yml 包含有关应用程序的基本信息，例如名称、要为每个实例分配的内存量以及路径。我们在 `get-started-swift` 目录中提供了样本 manifest.yml 文件。

打开 manifest.yml 文件，将 `name` 从 `GetStartedSwift` 更改为您的应用程序名称 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
  ```
  {: codeblock}

在此 manifest.yml 文件中，**random-route: true** 会为应用程序生成随机路径，以避免路径与其他路径冲突。如果您愿意，可以将 **random-route: true** 替换为 **host: myChosenHostName**，以提供您选择的主机名。[了解更多...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. 部署应用程序
{: #deploy}

您可以使用 Cloud Foundry CLI 来部署应用程序。

选择 API 端点
  ```
cf api <API-endpoint>
  ```
  {: pre}

将命令中的 *API-endpoint* 替换为以下列表中的 API 端点。

|URL                             |区域            |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 美国南部       |
| https://api.eu-gb.bluemix.net  | 英国           |
| https://api.au-syd.bluemix.net | 悉尼           |

登录到您的 {{site.data.keyword.Bluemix_notm}} 帐户

   ```
cf login
```
   {: pre}

从 *get-started-swift* 目录中，将应用程序推送到 {{site.data.keyword.Bluemix_notm}}
   ```
cf push
```
   {: pre}

这可能需要一分钟。如果部署过程中发生错误，您可以使用命令 `cf logs <Your-App-Name> --recent` 进行故障诊断。

部署完成后，您应该会看到一条消息，指示应用程序正在运行。通过 push 命令输出中列出的 URL 查看应用程序。您还可以发出 `cf apps` 命令来查看应用程序状态和 URL。

## 5. 添加数据库
{: #add_database}

接下来，我们要将 NoSQL 数据库添加到此应用程序并设置此应用程序，使其可以在本地以及在 {{site.data.keyword.Bluemix_notm}} 上运行。

1. 在浏览器中登录到 {{site.data.keyword.Bluemix_notm}}。浏览至`仪表板`。通过在`名称`列中单击应用程序的名称以选择该应用程序。
2. 单击`连接`，然后单击`连接新项`。
3. 在`数据和分析`部分中，选择 `Cloudant NoSQL DB`
4. 选择定价套餐。Bluemix 提供了免费的 `Lite` 套餐，其中包含精选的一组云服务，并提供了入门所需的足够容量
5. 出现提示时，选择`重新编译打包`。{{site.data.keyword.Bluemix_notm}} 将重新启动应用程序，并使用 `VCAP_SERVICES` 环境变量为应用程序提供数据库凭证。此环境变量仅可用于在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序。

通过环境变量，可以将部署设置与源代码分开。例如，可以将数据库密码存储在环境变量中，然后在源代码中引用此环境变量，而不是对密码进行硬编码。[了解更多...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. 使用数据库
{: #use_database}

现在，我们将更新本地代码以指向此数据库。创建 JSON 文件，以用于存储应用程序将使用的服务的凭证。仅当应用程序在本地运行时，才会使用此文件。在 {{site.data.keyword.Bluemix_notm}} 中运行时，将从 VCAP_SERVICES 环境变量中读取凭证。

在 `Sources` 目录中，创建名为 `config.json` 的文件并包含以下内容（请参阅 config.json.example）：
 ```
 {
    "vcap":{
       "services":{
          "cloudantNoSQLDB":[
             {
                "credentials":{
                   "host":"<host>",
                   "password":"<password>",
                   "port":443,
                   "url":"<url>",
                   "username":"<username>"
                },
                "label":"cloudantNoSQLDB",
                "name": "CloudantService"
             }
          ]
       }
    }
 }
 ```
{: pre}

此样本应用程序使用 Swift-cfenv 软件包与 Bluemix 进行交互，以解析环境变量。[了解更多...](https://packagecatalog.com/package/IBM-Swift/Swift-cfenv)
返回到 {{site.data.keyword.Bluemix_notm}} UI，选择“应用程序”->“连接”-> Cloudant ->“查看凭证”

仅将凭证复制并粘贴到本地 config.json 文件的相应字段中。

在本地构建并运行应用程序。
 ```
swift build  
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

查看应用程序：http://localhost:8080。现在，输入到应用程序中的所有名称都已添加到数据库。

此样本应用程序使用 Kitura-CouchDB 软件包与 Cloudant 进行交互。[了解更多...](https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)
{: tip}

本地应用程序和 {{site.data.keyword.Bluemix_notm}} 应用程序共享该数据库。通过上面 push 命令输出中列出的 URL 查看 {{site.data.keyword.Bluemix_notm}} 应用程序。在刷新浏览器后，从任一应用程序添加的名称都应该会同时出现在这两个应用程序中。


请记住，如果无需应用程序继续运行，请将其停止，这样就不会发生任何意外的费用。
{: tip}
