---

copyright:
  years: 2017
lastupdated: "2017-03-22"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}


# Node.js on Bluemix 入门

* {: download} 恭喜您，您已在 {{site.data.keyword.Bluemix}} 上部署了 Hello World 样本应用程序！要开始使用，请按照本逐步指南进行操作。或者，<a class="xref" href="http://bluemix.net" target="_blank" title="（下载样本代码）"><img class="hidden" src="../../images/btn_starter-code.svg" alt="下载应用程序代码" />下载样本代码</a>并自行探究。

通过遵循本指南，您将设置开发环境，在本地以及在 {{site.data.keyword.Bluemix}} 上部署应用程序，以及在应用程序中集成 {{site.data.keyword.Bluemix}} 数据库服务。

## 先决条件
{: #prereqs}

您将需要以下帐户和工具：
* [{{site.data.keyword.Bluemix_notm}} 帐户](https://console.ng.bluemix.net/registration/)
* [Cloud Foundry CLI ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Git ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://git-scm.com/downloads){: new_window}
* [Node ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://nodejs.org/en/){: new_window}


## 1. 克隆样本应用程序
{: #clone}

首先，克隆 Node.js *hello world* 样本应用程序 GitHub 存储库。
  ```
git clone https://github.com/IBM-Bluemix/get-started-node
  ```
  {: pre}

## 2. 在本地运行应用程序
{: #run_locally}

使用 npm 软件包管理器来安装依赖项并运行应用程序。

1. 在命令行上，切换到样本应用程序所在的目录。
  ```
cd get-started-node
```
  {: pre}

1. 安装 [package.json ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://docs.npmjs.com/files/package.json) 文件中列出的依赖项以在本地运行应用程序。  
  ```
npm install
```
  {: pre}

1. 运行应用程序。
  ```
npm start  
  ```
  {: pre}

可以查看应用程序：http://localhost:3000。

使用 [nodemon](https://nodemon.io/) 以在文件更改时自动重新启动应用程序。
{: tip}


## 3. 准备应用程序进行部署
{: #prepare}

如果要部署到 {{site.data.keyword.Bluemix_notm}}，设置 manifest.yml 文件会很有用。manifest.yml 包含有关应用程序的基本信息，例如名称、要为每个实例分配的内存量以及路径。我们在 `get-started-node` 目录中提供了样本 manifest.yml 文件。

打开 manifest.yml 文件，将 `name` 从 `GetStartedNode` 更改为您的应用程序名称 <var class="keyword varname" data-hd-keyref="app_name">app_name</var>。
{: download}

```
applications:
- name: GetStartedNode
  random-route: true
  memory: 128M
```
{: codeblock}

在此 manifest.yml 文件中，**random-route: true** 会为应用程序生成随机路径，以避免路径与其他路径冲突。如果您愿意，可以将 **random-route: true** 替换为 **host: myChosenHostName**，以提供您选择的主机名。[了解更多...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. 部署应用程序
{: #deploy}

您可以使用 Cloud Foundry CLI 将应用程序部署到 {{site.data.keyword.Bluemix_notm}}。

运行以下命令来设置 API 端点，将 *API-endpoint* 值替换为您区域的 API 端点。
   ```
cf api <API-endpoint>
   ```
   {: pre}

|API 端点                            |区域            |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | 美国南部       |
| https://api.eu-gb.bluemix.net  | 英国           |
| https://api.au-syd.bluemix.net | 悉尼           |

登录到 {{site.data.keyword.Bluemix_notm}} 帐户。

  ```
cf login
```
  {: pre}

从 *get-started-node* 目录中，将应用程序推送到 {{site.data.keyword.Bluemix_notm}}。
  ```
cf push
```
  {: pre}

部署应用程序可能需要几分钟时间。部署完成后，您将看到一条消息，指示应用程序正在运行。通过 push 命令输出中列出的 URL 查看应用程序，或者通过运行以下命令同时查看应用程序部署状态和 URL：
  ```
cf apps
  ```
  {: pre}

可以使用 `cf logs <Your-App-Name> --recent` 命令对部署过程中的错误进行故障诊断。
{: tip}

## 5. 添加数据库
{: #add_database}

接下来，我们要将 NoSQL 数据库添加到此应用程序并设置此应用程序，使其可以在本地以及在 {{site.data.keyword.Bluemix_notm}} 上运行。

1. 在浏览器中，登录到 {{site.data.keyword.Bluemix_notm}}，然后转至“仪表板”。通过在**名称**列中单击应用程序的名称以选择该应用程序。
2. 单击**连接**，然后单击**连接新项**。
2. 在**数据和分析**部分中，选择 `Cloudant NoSQL DB`，然后创建该服务。
3. 出现提示时，选择**重新编译打包**。{{site.data.keyword.Bluemix_notm}} 将重新启动应用程序，并使用 `VCAP_SERVICES` 环境变量为应用程序提供数据库凭证。此环境变量仅可用于在 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序。

通过环境变量，可以将部署设置与源代码分开。例如，可以将数据库密码存储在环境变量中，然后在源代码中引用此环境变量，而不是对密码进行硬编码。[了解更多...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. 使用数据库
{: #use_database}
现在，我们将更新本地代码以指向此数据库。我们将创建 JSON 文件，以用于存储应用程序将使用的服务的凭证。仅当应用程序在本地运行时，才会使用此文件。在 {{site.data.keyword.Bluemix_notm}} 中运行时，将从 `VCAP_SERVICES` 环境变量中读取凭证。

1. 在 `get-started-node` 目录中，创建名为 `vcap-local.json` 的文件并包含以下内容：
  ```
  {
    "services": {
      "cloudantNoSQLDB": [
        {
          "credentials": {
            "url":"CLOUDANT_DATABASE_URL"
          },
          "label": "cloudantNoSQLDB"
        }
      ]
    }
  }
  ```
  {: codeblock}

2. 在浏览器中，转至 {{site.data.keyword.Bluemix_notm}} 并选择**应用程序 > _your app_ > 连接 > Cloudant > 查看凭证**。

3. 仅将凭证中的 `url` 复制并粘贴到 `vcap-local.json` 文件的 `url` 字段，以替换 **CLOUDANT_DATABASE_URL**。

4. 在本地运行应用程序。
  ```
npm start  
  ```
  {: pre}

  查看本地应用程序：http://localhost:3000。现在，输入到应用程序中的所有名称都已添加到数据库。

  本地应用程序和 {{site.data.keyword.Bluemix_notm}} 应用程序共享该数据库。在刷新浏览器后，从任一应用程序添加的名称都将同时出现在这两个应用程序中。

请记住，如果无需应用程序在 {{site.data.keyword.Bluemix_notm}} 上继续运行，请停止该应用程序，这样就不会发生任何意外的费用。
{: tip}
