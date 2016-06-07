---

 

copyright:

  years: 2015，2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 场景：端到端开发
{: #ee}

*上次更新时间：2016 年 4 月 18 日*

构建、运行和部署应用程序时，可以使用 {{site.data.keyword.Bluemix}} 用户界面、平台和一组工具。首次操作时，请遵循此端到端开发场景。
{:shortdesc}

## 注册
{: #ee_start}

开始之前，需要通过以下链接注册 IBM 标识：[https://console.ng.bluemix.net/](https://console.ng.bluemix.net/)。注册后，登录到 {{site.data.keyword.Bluemix_notm}}，即可开始 30 天免费试用。{{site.data.keyword.Bluemix_notm}} 提供了 2 GB 运行时内存和 10 个服务实例供您免费试用。

## 使用 {{site.data.keyword.Bluemix_notm}} 用户界面创建 Web 应用程序
{: #ee_appui}

注册后，可使用 {{site.data.keyword.Bluemix_notm}} 用户界面开始构建您的第一个应用程序。

在 {{site.data.keyword.Bluemix_notm}} 中，应用程序与组织和空间相关联。一个组织可由多个合作者拥有并使用。最初，您将获得根据您的用户名命名的缺省组织，并且您是唯一的合作者。您还将获得该组织内的一个空间。空间是运行应用程序的环境；例如，您可以拥有 dev 空间、test 空间和 production 空间，分别用作开发环境、测试环境和生产环境。此外，每个环境都属于一个区域。通过 {{site.data.keyword.Bluemix_notm}}，您可以将应用程序部署到特定地理区域，以减少网络等待时间，增强数据隐私性，提高可用性。有关详细信息，请参阅“区域”。

对于此场景，应使用 Node.js 来开发 Web 应用程序。假定您在美国，并且您的大部分应用程序用户也在美国。您决定在靠近您用户群的位置构建并运行应用程序，以便能够减少网络等待时间。登录到 {{site.data.keyword.Bluemix_notm}} 后，单击右上方您的帐户名称，然后选择**美国南部**区域。然后，可以执行以下步骤来创建应用程序：

  1. 单击加号按钮。
  2. 选择**计算** > **CF 应用程序** > **SDK for Node.js**。
  3. 键入应用程序的唯一名称（例如 TestNode），然后单击**创建**。应用程序名称必须在整个 {{site.data.keyword.Bluemix_notm}} 环境中唯一。
  
现在，可以看到**开始编码**指示信息。您可以遵循指示信息来下载、修改和部署 TestNode 入门模板代码。

缺省情况下，会为应用程序分配 1 个实例和 512 MB 内存配额。您可以增大内存，或者添加更多实例来获取应用程序的高可用性，例如 3 个实例，每个实例 1 GB 内存。单击**查看应用程序概述**，可指定应用程序实例数和内存配额。例如，在实例数中键入 3，在内存配额中键入 1 GB，然后单击**保存**。您还可以查看文件、日志和环境变量以对问题进行故障诊断。

## 使用 {{site.data.keyword.Bluemix_notm}} 用户界面绑定服务
{: #ee_bindui}

创建应用程序后，您希望将应用程序与数据库相连接。这样，您就可以通过数据库查询语言来存储和观察应用程序数据。在此场景中，您决定使用 {{site.data.keyword.Bluemix_notm}} 提供的 {{site.data.keyword.cloudant}} 服务。

要在应用程序内使用服务，您需要通过执行以下步骤来创建服务实例，并将应用程序绑定到该服务实例。
  1. 单击应用程序“概述”页面上的**添加服务或 API**。
  2. 在 {{site.data.keyword.Bluemix_notm}}“目录”中，选择 {{site.data.keyword.cloudant}} 服务。
  3. 为服务实例键入唯一名称，或使用 {{site.data.keyword.Bluemix_notm}} 生成的缺省名称，然后单击**创建**。
  4. 这将显示“重新编译打包应用程序”窗口。单击**重新编译打包**以对应用程序重新编译打包。
  
现在，您的应用程序已绑定到 {{site.data.keyword.cloudant}} 服务。您可以在 VCAP_SERVICES 环境变量中找到应用程序与服务实例进行通信时所需的所有数据。例如，{{site.data.keyword.Bluemix_notm}} 会在同一虚拟机上托管多个应用程序，而这些应用程序不能使用同一 HTTP 端口号来接收入局请求。为了避免冲突，会为每个应用程序提供唯一端口号。此端口号在 VCAP_APP_PORT 变量下提供。

单击应用程序“概述”页面上的**环境变量**，可查看 VCAP_SERVICES 的整个列表来了解更多信息：
```
{
   "cloudantNoSQLDB": [

      {
         "name": "Cloudant NoSQL DB-tx",
         "label": "cloudantNoSQLDB",
         "plan": "Shared",
         "credentials": {
            "username": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix",
            "password": "b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424",
            "host": "d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com",
            "port": 443,
            "url": "https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com"
         }
      }
   ]
}
```

**注：**此环境变量是序列化 JSON 对象。其中，一个条目对应一个与应用程序绑定的服务实例。每个服务实例提供的数据量和数据类型都是特定于服务的。如果应用程序未使用任何服务，那么 VCAP_SERVICES 为空 JSON 对象。仅当将服务添加到应用程序后，才会使用此环境变量。

## 使用 cf cli 构建应用程序
{: #ee_cf}

{{site.data.keyword.Bluemix_notm}} 提供了多个工具，供您在开始对应用程序进行编码时使用，例如 cf 命令行界面和 Eclipse 工具。您可以选择从 cf 命令行界面开始对应用程序 TestNode 进行编码。

  1. 首先，下载并开发应用程序的代码。
  
    1. 转至应用程序的“开始编码”页面。单击**下载入门模板代码**按钮以下载应用程序代码。
    2. 将下载的文件解压缩到目录，例如 `C:\test`。
    3. 使用本地集成开发环境开发代码。
	
  2. 安装 **cf** 命令行界面 (CLI)。
  
    1. 下载适用于您的操作系统的 cf 命令行工具安装程序。
    2. 遵循工具向导来完成安装。
    3. 使用 **cf -v** 命令来验证 cf 命令行界面的版本。例如：
	
	```
	cf -v
	```
	
    **要求：**确保始终使用最新版本的 cf 命令行工具。
  3. 安装 **cf** 命令行界面后，必须使用 **cf api** 命令来指定要使用的 {{site.data.keyword.Bluemix_notm}} 区域。**cf** 命令行界面使用 *https://api.Bluemix_URL*，其中 *Bluemix_URL* 是区域的 URL。美国南部区域的 URL 为 {{Domain}}。输入以下命令，以连接到 {{site.data.keyword.Bluemix_notm}}：
  
  ```
  cf api https://api.ng.bluemix.net
	 ```
  
  有关连接到其他 {{site.data.keyword.Bluemix_notm}} 区域的更多信息，请参阅 {{site.data.keyword.Bluemix_notm}} 区域。指定 {{site.data.keyword.Bluemix_notm}} 区域后，您所指定的位置信息会得到保存。
  
  4. 接下来，可以使用 cf login 命令登录到 {{site.data.keyword.Bluemix_notm}}。
  
  ```
  cf login -u your_user_ID -p ***** -o your_org_name -s your_space_name
  ```
  
  5. 登录到 {{site.data.keyword.Bluemix_notm}} 后，即准备就绪，可以将应用程序重新部署到 {{site.data.keyword.Bluemix_notm}}。从应用程序目录 `C:\test`，输入以下命令：
  
  ```
  cf push TestNode```
  
  有关 **cf push** 命令的更多信息，请参阅“上传应用程序”。
  
  6. 现在，可以通过在浏览器中输入以下应用程序 URL 来访问应用程序：```
  http://TestNode.mybluemix.net
  ```

您还可以选择使用其他工具来构建应用程序，例如 Eclipse 工具。有关更多信息，请参阅 {{site.data.keyword.Bluemix_notm}} 用户界面上应用程序的“开始编码”页面。

## 使用 cf cli 绑定服务
{: #ee_cfbind}

通过 {{site.data.keyword.Bluemix_notm}}，您可以使用 Bluemix 用户界面添加服务，如本场景的较早部分中所述。此外，还可以使用 **cf** 命令行界面来绑定服务。假定要使用 cf 命令行界面将 {{site.data.keyword.cloudant}} 服务添加到应用程序 TestNode 中。

要在应用程序内使用 {{site.data.keyword.cloudant}} 服务，您需要创建 Cloudant 服务实例，将应用程序绑定到该服务实例，然后使用该服务实例。相同的过程对所有其他服务均适用。

  1. 创建 Cloudant NoSQL DB 服务实例。
  
  使用 cf create-service 命令创建新的服务实例。例如：
  
  ```
  cf create-service cloudantNoSQLDB Shared cloudant100```
  
  您还可以使用 cf services 命令来查看所创建的服务实例的列表。
  
  ```
  cf services```
  
  服务实例创建后，任何应用程序都可绑定和使用该服务实例。
  
  2. 将服务实例与应用程序绑定。
  
  要使用服务实例，必须将其绑定到应用程序。使用 cf bind-service 命令并指定应用程序名称和所创建的服务实例，可将服务实例绑定到应用程序。
  
  ```
  cf bind-service TestNode cloudant100```
  
  将服务实例绑定到应用程序后，{{site.data.keyword.Bluemix_notm}} 就能够与服务进行通信，还能让新应用程序与该服务实例进行通信。对于不同的服务，在绑定期间，{{site.data.keyword.Bluemix_notm}} 处理应用程序和服务实例的方式可能会不同。例如，某些服务可能会为每个与服务实例进行通信的应用程序创建一个新租户。服务会使用凭证等信息来响应 {{site.data.keyword.Bluemix_notm}}，这些信息必须传递到应用程序，应用程序才能与服务进行通信。

  **注：**在将应用程序绑定到服务实例时，如果应用程序正在运行，那么只有在重新启动应用程序后，才会更新 VCAP_SERVICES 环境变量。要重新启动应用程序，请使用 cf restart 命令。
  
  3. 使用服务实例。
  
  在此场景中，VCAP_SERVICES 环境变量包含应用程序连接到此 {{site.data.keyword.cloudant}} 实例时可使用的信息，例如以下各项：
  
  <dl><dt>username</dt>
  <dd>d72837bb-b341-4038-9c8e-7f7232916197-bluemix</dd>
  <dt>password</dt>
  <dd>b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424</dd>
  <dt>url</dt>
  <dd>https://d72837bb-b341-4038-9c8e-7f7232916197-bluemix:b6fc4708942b70a88853177ee52a528d07a43fa8575a69abeb8e044a7b0a7424@d72837bb-b341-4038-9c8e-7f7232916197-bluemix.cloudant.com</dd></dt></dl>
  
  例如，Node.js 应用程序可能会按如下方式访问这些信息：```
  if (process.env.VCAP_SERVICES) {

        var env = JSON.parse(process.env.VCAP_SERVICES);
        var cloudant = env['"cloudantNoSQLDB'][0].credentials;
  } else {
        var cloudant = {
"username" : "user1",
                "password" : "secret",
                "url" : "https://user1:secret@localhost:25002"
                }
        };
  ```
  
  **注：**如样本代码所示，要连接到 {{site.data.keyword.cloudant}} 服务实例，首先可以检查 VCAP_SERVICES 环境变量是否存在。如果存在，那么应用程序可以使用 cloudant 变量的属性来访问数据库。但是，如果 VCAP_SERVICES 环境变量不存在，那么将使用本地 {{site.data.keyword.cloudant}} 服务实例以及所提供的缺省值。
  
  4. 与服务实例进行交互。
  
  可以使用凭证信息来与服务实例进行交互。可执行的操作包括读取、写入和更新。以下示例演示了如何将 JSON 对象插入到 {{site.data.keyword.cloudant}} 服务实例：```
  // create a new message
var create_message = function(req, res) {
  require('cloudantdb').connect(cloudant.url, function(err, conn) {

    var collection = conn.collection('messages');


    // create message record
    var parsedUrl = require('url').parse(req.url, true);
    var queryObject = parsedUrl.query;
    var name = (queryObject["name"] || 'Bluemix');
    var message = { 'message': 'Hello, ' + name, 'ts': new Date()
};
    collection.insert(message, {safe:true}, function(err){
      if (err) { console.log(err.stack); }
      res.writeHead(200, {'Content-Type': 'text/plain'});
      res.write(JSON.stringify(message));
      res.end('\n');
    });
  });
}
  ```
  
  5. **可选：**取消绑定或删除服务实例。
  
  不再使用服务实例或需要释放一些空间时，您可能希望撤销绑定或删除服务实例。要取消服务实例与应用程序的绑定，请使用 **cf unbind-service** 命令；要删除服务实例，请使用 **cf delete-service** 命令。

  有关服务的更多信息，请参阅“服务”。有关哪些 **cf** 选项可用于在 {{site.data.keyword.Bluemix_notm}} 环境中管理应用程序的更多信息，请在 **cf** 命令行界面中发出 **cf --help**。

  **注：**请在确保不再需要服务实例后，再将其删除。删除服务实例会擦除与该服务实例关联的所有数据。如果应用程序所绑定到的服务已删除，那么只有在重新启动该应用程序后，其 VCAP_SERVICES 环境变量才能得到更新。

## 计算应用程序成本
{: #ee_billing}

30 天免费试用到期，但您希望继续使用 {{site.data.keyword.Bluemix_notm}}。您必须向“现买现付”帐户或“预订”帐户添加自己的信用卡信息，才可继续使用 {{site.data.keyword.Bluemix_notm}}。但是，{{site.data.keyword.Bluemix_notm}} 仍会为大多数运行时框架和服务提供免费限额，即使您转换为付费帐户，也是如此。除非使用量超过免费限额，否则 {{site.data.keyword.Bluemix_notm}} 不会对您进行收费。

{{site.data.keyword.Bluemix_notm}} 提供了估算工具和计算器，供您查看自己的应用程序成本。您可以通过以下方式来查看 TestNode 的成本：

  * 在仪表板中，单击 TestNode。然后，在“概述”页面中，单击**估算此应用程序的成本**，以查看 **SDK for Node.js** 运行时和支持的价格，以及应用程序的每月总价格。
  
  * 或者，在“价格表”页面中，键入应用程序的每月运行时和服务使用量。例如，3 个 **SDK for Node.js** 实例，每个实例使用 1 GB 内存。这将计算并显示每月的价格。

您还可以手动计算应用程序成本，方法是累加运行时和服务的价格，然后减去免费限额。有关更多信息，请参阅“手动计算成本”。

## 除去应用程序
{: #ee_removing}

当构建的应用程序越来越多时，就可能会越来越接近配额限制。有一些应用程序，您可能不再使用，但它们仍占用着配额。在 {{site.data.keyword.Bluemix_notm}} 中，随时都可以轻松地删除应用程序来释放一些空间。

在 {{site.data.keyword.Bluemix_notm}} 用户界面中，转至应用程序“概述”页面，单击**菜单**图标，然后删除不再使用的应用程序。还可以使用 **cf delete** 命令来删除应用程序。
