{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} (BETA) 入门{: #getting-started-with-object-storage} 

{{site.data.keyword.objectstoragefull}} 为您提供了对完整供应的 Swift {{site.data.keyword.objectstorageshort}} 帐户的访问权，以用于管理您的数据。Swift 提供了一个可通过 API 访问的全分布式存储平台。您可以直接在应用程序中使用 Swift，或将其用于备份，因此最适合用于高性价比的向外扩展存储。

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 使用 OpenStack Identity (Keystone) 进行认证，并可以使用 OpenStack Object Storage (Swift) API V1 调用对其直接进行访问。IBM {{site.data.keyword.objectstorageshort}} 可以绑定到 {{site.data.keyword.Bluemix_notm}} 应用程序，或者可以从 {{site.data.keyword.Bluemix_notm}} 应用程序外部对其进行访问。 

有关使用 OpenStack Swift 和 Keystone 的更多信息和文档，请访问 [OpenStack 文档站点](http://docs.openstack.org){: new_window}。

{{site.data.keyword.objectstorageshort}} 体系结构图如下所示：

[![{{site.data.keyword.objectstorageshort}} 体系结构图](images/object_storage_solution_archectiture_small.png)](http://www.stage1.ng.bluemix.net/docs/api/content/services/ObjectStorage/images/object_storage_solution_archectiture.png){: new_window}

*图 1. {{site.data.keyword.objectstorageshort}} 体系结构图*

**注：**提供者端加密并未提供。由客户机应用程序负责在上传数据之前对数据进行加密。

**注：**{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} 服务的一般可用性发行版发布后，会将 {{site.data.keyword.objectstorageshort}} 服务 Beta 套餐从目录中除去。宽限期过后，将除去使用 Beta 套餐的服务实例。[更新定价套餐](#changeplan)以继续使用 {{site.data.keyword.objectstorageshort}} 服务。 




## 在 {{site.data.keyword.Bluemix_notm}} 中创建 {{site.data.keyword.objectstorageshort}} 实例{: #creating-object-storage-instance} 

### 如何创建 {{site.data.keyword.objectstorageshort}} 服务实例
1.	转至 {{site.data.keyword.Bluemix_notm}} **目录**选项卡，然后在搜索框中输入 **{{site.data.keyword.objectstorageshort}}**，或者转至**服务**，然后选择**存储**。单击 **{{site.data.keyword.objectstorageshort}}** 服务。 
2.	选择空间、应用程序、服务名称和套餐，然后单击**创建**。
**注：**如果对于**应用程序**字段，初始选择的是**保持未绑定**选项，那么在完成配置后仍可以将服务实例绑定到 {{site.data.keyword.Bluemix_notm}} 应用程序。请参阅以下指示信息。

## 从 {{site.data.keyword.Bluemix_notm}} 应用程序使用 {{site.data.keyword.objectstorageshort}}{: #using-object-storage-from-bluemix-app} 

### 如何在创建后将 {{site.data.keyword.objectstorageshort}} 服务绑定到应用程序{: #bind-object-storage-to-application} 
1.	在 {{site.data.keyword.Bluemix_notm}} 仪表板中，选择要绑定的应用程序。
2.	在应用程序概述中，单击**绑定服务或 API**。
3.	从服务列表中，选择 {{site.data.keyword.objectstorageshort}} 实例，然后单击**添加**。
4.	系统提示时，单击**重新编译打包**。应用程序必须重新编译打包后，才可使用新服务。

### 绑定上下文

如果要在绑定上下文中使用 {{site.data.keyword.objectstorageshort}}，那么将通过应用程序绑定进程间接提供云凭证。将服务实例成功绑定到应用程序后，类似于以下示例的配置将添加到 `VCAP_SERVICES` 环境变量。

    {
    "Object-Storage": [
    {
      "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
         "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
       }
      ]
    }

## 使用 {{site.data.keyword.objectstorageshort}} 用户界面{: #using-object-storage-ui}

### UI 元素和导航
供应 {{site.data.keyword.objectstorageshort}} 后，可以在 {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务实例仪表板中查看实例信息。在仪表板中，选择 {{site.data.keyword.objectstorageshort}} 实例以查看包含更详细信息的面板。  
#### 使用情况数据
在面板顶部，将显示实例的存储器使用情况信息。还将显示所有容器中的当前**存储容器**数和**对象**总数。还会列出内存使用情况（以兆字节为单位）。**使用的存储空间**是指使用的当前空间量。 
#### 操作
要检索最新的使用情况数据，请单击**刷新**按钮。   
####对象浏览器 
面板的底部部分包含对象浏览器。使用对象浏览器可管理对象存储容器和对象。可以执行创建容器、上传文件、删除容器和删除文件等操作。

## 使用 Swift CLI 访问 {{site.data.keyword.objectstorageshort}}{: #using-swift-cli}

您可以通过因特网以及 IBM {{site.data.keyword.Bluemix_notm}} 中的应用程序和虚拟机访问 {{site.data.keyword.objectstorageshort}} 服务。{{site.data.keyword.objectstorageshort}} 服务的常见用例如下所示：

* 备份实例中的卷数据
* 传输大量数据时用作中间位置
* 在未直接连接的环境之间传输数据
* 充当中心存储库

{{site.data.keyword.objectstorageshort}} 服务基于 OpenStack Swift，可以使用任何兼容的客户机应用程序进行访问。本部分描述如何利用 Python Swift 客户机来使用容器和文件；Python Swift 客户机是 {{site.data.keyword.objectstorageshort}} API 及其扩展的命令行界面。

### 安装 Swift 客户机

如果尚未安装以下必备软件，请进行安装。有关更多信息，请参阅 [OpenStack 文档](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。 
* Python 2.7 或更高版本
* setuptools 软件包
* pip 软件包

使用 Python pip 安装 Python Swift 客户机：

	sudo pip install python-swiftclient

### 设置客户机

Swift 客户机通过以下环境变量获取认证信息：
* “`OS_AUTH_URL`”是端点 URL
* “`OS_USER_ID`”是用户名
* “`OS_PASSWORD`”是密码

如下所示，设置认证信息。 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

可以在 {{site.data.keyword.objectstorageshort}} 用户界面的**服务凭证**页面中查找 {{site.data.keyword.objectstorageshort}} 服务的凭证值。 

**注：**请确保为 Swift 客户机配置环境变量“`OS_AUTH_URL`”时，在 {{site.data.keyword.objectstorageshort}} 用户界面的凭证中，将“`/v3`”添加到“`auth_url`”。


![{{site.data.keyword.objectstorageshort}} 服务凭证](images/service_credentials.jpg)

*图 2. {{site.data.keyword.objectstorageshort}} 服务凭证*

### 使用容器

列出容器：

	swift list
	
创建容器：

	swift post <container_name>
	
列出容器的内容：

	swift list <container_name>

### 使用对象

#### 向容器添加文件

	swift upload <container_name> <file_name>

#### 向容器添加大于 5 GB 的文件

如果要上传大于 5 GB 的文件，必须将其拆分成较小的区块。可以通过提供“`-segment-size`”参数，指示 Swift 客户机来处理此类上传：

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
各个分段会并行上传到名为“``<container_name>_segments``”的独立容器中。上传完所有分段后，Swift 会创建清单文件，以便可以从包含名为“```<file_name>`”的原始文件的原始容器“`<container_name>`”中将这些分段下载到单个文件中。

例如，以下命令将从名为“`test_container`”的容器中上传名为“`large_file`”的文件，文件的分段大小为“`1073741824`”。

	swift upload test_container -S 1073741824 large_file

可以运行以下命令来下载该文件：

	swift download test_container large_file

#### 下载文件

	swift download <container_name> <file_name>
	
#### 向容器添加目录

Swift 没有真正的目录结构，而是使用命名来表示目录布局。要向容器添加目录，请运行以下命令：

	swift upload <container_name> <directory_name>
	
此命令会将完整目录结构作为相对路径上传。例如，如果指定“`/mnt/volume1`”，那么目录结构 mnt/volume1 将附加到所有文件名，以指示目录结构。

	
#### 下载目录

要下载目录结构，请使用“`-prefix`”参数来指示要下载的目录或目录结构。

	swift download <container_name> --prefix <directory>
	
#### 删除文件

	swift delete <container_name> <file_name>

### 创建临时 URL

临时 URL 较长且难以猜中，可用于在指定时间段内下载对象，而不必请求进一步认证 。使用以下步骤可生成临时 URL：

1. 确定认证帐户。
2. 设置密钥。
3. 创建临时 URL。

#### 确定认证帐户

Swift 的“`stat`”命令将显示有关帐户的信息：

	swift stat

找到“帐户”字段，并记录“*帐户：*”后面的完整字符串，包括“`AUTH_`”。

#### 设置密钥

此密钥可以是所选的任何内容，但最佳做法是选择难以猜中的随机长字符串。

	swift post -m "Temp-URL-Key:<key>"

#### 创建临时 URL

Swift 的“`tempurl`”命令将采用以下位置参数：

* [method] GET 用于允许下载，PUT 用于允许上传
* [seconds] 临时 URL 将可用的时间（以秒为单位）
* [path] 表示为 /v1/<auth_account>/<container_name>/<object_name> 的对象的完整路径
* [key] 在步骤 2 中设置的密钥

```
swift tempurl GET <seconds> <path> <key>
```

此命令将返回 URL，可以将此 URL 附加到集群名称以获得完整 URL。使用该完整 URL 可通过任何兼容的 HTTP 客户机（例如，curl、wget 或 Firefox）来下载对象。

## 使用 Swift REST CLI 访问 {{site.data.keyword.objectstorageshort}}{: #using-swift-restapi}

可以通过命令行客户机接口（例如，cURL）来使用 Swift REST API，也可以通过应用程序来调用该 API。  

### {{site.data.keyword.objectstorageshort}} URL{: #access-points}

要与 {{site.data.keyword.objectstorageshort}} API 进行交互，请如下所示构造 {{site.data.keyword.objectstorageshort}} URL：

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>

例如：

![{{site.data.keyword.objectstorageshort}} URL](images/Swift_URL.png)

*图 3. {{site.data.keyword.objectstorageshort}} URL*

URL 由 5 个部分组成。`“<API version>”`为 V1。您可以在 {{site.data.keyword.objectstorageshort}} 用户界面中找到 {{site.data.keyword.objectstorageshort}} 的`“<project ID>”`、`“<container namespace>”`和`“<object namespace>”`。对于“`<access point>`”，请参阅下表： 


| **区域**  |     **内部访问点**                             |     **公共访问点**                   |
|-------------|-----------------------------------------------------------|-----------------------------------------------|
| 达拉斯      | https://dal.objectstorage.service.open.networklayer.com/  | https://dal.objectstorage.open.softlayer.com/ | 
| 伦敦      | https://lon.objectstorage.service.open.networklayer.com/  | https://lon.objectstorage.open.softlayer.com/ |


*表 1. {{site.data.keyword.objectstorageshort}} 访问点*

从 {{site.data.keyword.Bluemix_notm}} 内部访问 {{site.data.keyword.objectstorageshort}} 服务时，请使用内部访问点；从 {{site.data.keyword.Bluemix_notm}} 外部访问 {{site.data.keyword.objectstorageshort}} 服务时，请使用公共访问点。

### {{site.data.keyword.objectstorageshort}} API

请参阅 [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}，以获取 {{site.data.keyword.objectstorageshort}} REST API 选项和示例的整套列表。

## 跨多区域使用 {{site.data.keyword.objectstorageshort}}{: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务支持“达拉斯”和“伦敦”存储区域。这两个存储区域独立于 {{site.data.keyword.Bluemix_notm}} 区域（例如，美国南部区域和英国），而 {{site.data.keyword.objectstorageshort}} 服务实例创建于该区域。例如，如果在美国南部的 {{site.data.keyword.Bluemix_notm}} 区域中创建 {{site.data.keyword.objectstorageshort}} 实例，那么可以读写“达拉斯”或“伦敦”存储区域的数据。  

对于美国南部的 {{site.data.keyword.Bluemix_notm}} 区域，“达拉斯”存储区域是缺省值。对于英国的 {{site.data.keyword.Bluemix_notm}} 区域，“伦敦”存储区域是缺省值。{{site.data.keyword.objectstorageshort}} 用户界面启动后始终会进入 {{site.data.keyword.Bluemix_notm}} 区域的缺省存储区域。要切换区域，请单击“{{site.data.keyword.objectstorageshort}} 区域”下拉列表，然后选择其他区域。

![{{site.data.keyword.objectstorageshort}} 更改区域](images/change_region.png)

*图 4. {{site.data.keyword.objectstorageshort}} 更改区域*

**注：**{{site.data.keyword.objectstorageshort}} 服务不支持跨存储区域复制。

### 多区域访问

要使用 {{site.data.keyword.objectstorageshort}} 服务，必须[向 OpenStack Keystone 认证](#keystone-authentication)。认证成功后，响应中将可以使用“`X-Subject-Token`”和 {{site.data.keyword.objectstorageshort}} 端点。

例如，要在“达拉斯”存储区域中创建名为“`my_container`”的容器，请在 curl 命令中指定达拉斯访问点，如下所示：

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


要在“伦敦”存储区域中创建名为“`my_container`”的容器，请在 curl 命令中指定伦敦访问点，如下所示：

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**注：**从 Keystone 获取的“`X-Subject-Token`”在所有存储区域中都有效。 

有关不同区域的访问点的更多信息，请参阅 [Object Storage 访问点](#access-points)表。


## 了解认证和凭证{: #understanding-authentication-credentials}

### 生成 {{site.data.keyword.objectstorageshort}} 凭证而不绑定应用程序

要生成在 {{site.data.keyword.Bluemix_notm}} 应用程序外部使用的 {{site.data.keyword.objectstorageshort}} 云凭证，必须为 {{site.data.keyword.objectstorageshort}} 实例生成服务密钥。可以通过从用户界面的侧边栏中选择**服务凭证**或使用 Cloud Foundry CLI（V6.11.3 或更高版本）来生成新密钥。为 {{site.data.keyword.objectstorageshort}} 实例生成服务密钥并检索到该服务密钥后，可以使用 Cloud Integration 信息通过 OpenStack SDK 或 OpenStack Identity API 来请求 Keystone 令牌，并开始使用 Swift 帐户来管理对象。
   
要使用 Cloud Foundry CLI 创建密钥，请登录并运行以下命令：
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

要从 Cloud Foundry CLI 中检索服务凭证，请运行以下命令：

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


### 云项目和用户
供应新的 {{site.data.keyword.objectstorageshort}} 实例将在 IBM 公共云中创建独立的 Keystone 项目。将新应用程序绑定到 {{site.data.keyword.objectstorageshort}} 实例时，将创建具有项目访问权的新 Keystone 用户。撤销供应实例后，将删除项目和用户。

### OpenStack Identity (Keystone) V3 {: #keystone-authentication}
凭证结构包含一整组属性，允许您选择最适合您的应用程序的 OpenStack 令牌请求方法或 OpenStack SDK。 
 
建议使用的 V3 令牌请求是对 https://identity.open.softlayer.com/v3/auth/tokens 的 POST 请求，如以下 curl 命令中所示：

	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo

向 {{site.data.keyword.objectstorageshort}} 服务发起请求时，将响应头中“`X-Subject-Token`”字段的值用作“`X-Auth-Token`”字段。

示例响应如下所示：

	HTTP/1.1 201 Created
	X-Subject-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9
	Vary: X-Auth-Token
	Content-Type: application/json
	Content-Length: 960
	Date: Tue, 10 Jun 2014 20:40:14 GMT
	
	{"token": 
	{"audit_ids": ["ECwrVNWbSCqmEgPnu0YCRw"], "methods": ["password"],
	 "roles": [{"id": "c703057be878458588961ce9a0ce686b", "name": "admin"}],
	 "expires_at": "2014-06-10T21:40:14.360795Z", 
	 "project": {"domain": {"id": "default", "name": "Default"}, "id": "3d4c2c82bd5948f0bcab0cf3a7c9b48c", "name": "demo"}, 
	 "catalog": [
	 {
		"endpoints": [
			{
			"adminURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "20cbfa6ff22b4a67a1484d30235bfc80",
			"internalURL": "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://lon.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "london"
			},
			{
			"adminURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"id": "4207049680fa4effbecd044c7448a8cb",
			"internalURL": "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"publicURL": "https://dal.objectstorage.open.softlayer.com/v1/AUTH_35a68d1d115b4a0f8c7975d4f96f256b",
			"region": "dallas"
			}
			],
		"endpoints_links": [],
		"name": "swift",
		"type": "object-store"
		},
	 ], 
	 "extras": {},
	 "user": {"domain": {"id": "default", "name": "Default"}, "id": "3ec3164f750146be97f21559ee4d9c51", "name": "admin"},  "issued_at": "2014-06-10T20:40:14.360822Z"}}


{{site.data.keyword.objectstorageshort}} URL 位于服务目录中。服务目录包含在令牌请求的响应主体中。响应是可用 OpenStack 服务的完整目录。从服务目录中选择端点，类型为“`object-store`”、区域与凭证中的区域字段相匹配，接口为内部接口 (`internalURL`) 或公共接口 (`publicURL`)；其中，从 {{site.data.keyword.Bluemix_notm}} 内部访问 {{site.data.keyword.objectstorageshort}} 服务时使用内部接口，从 {{site.data.keyword.Bluemix_notm}} 外部访问 {{site.data.keyword.objectstorageshort}} 服务时使用公共接口。



## 取消绑定和撤销供应 {{site.data.keyword.objectstorageshort}}{: #deprovisioning-object-storage}

### 如何撤销供应 {{site.data.keyword.objectstorageshort}} 服务
1.	从 {{site.data.keyword.Bluemix_notm}} 仪表板中选择服务。  
2.	单击右上角的齿轮图标，并选择**删除服务**。
	
**警告：**如果撤销供应 IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务实例，将删除云项目和 Swift 帐户。撤销供应的实例中的所有容器和对象也将从 Swift 中删除，并且无法复原。

### 取消绑定应用程序或删除服务密钥

如果取消应用程序与 {{site.data.keyword.objectstorageshort}} 实例的绑定或删除服务密钥，那么将删除凭证。{{site.data.keyword.objectstorageshort}} 帐户要到撤销供应 {{site.data.keyword.objectstorageshort}} 实例后才会删除。通过[重新绑定或创建新的服务密钥](#bind-object-storage-to-application)，可以生成新的云凭证。

## 常见问题{: #FAQ} 

### 价格是如何根据所选套餐变化的？
定价根据所选套餐而变化。有关更多定价信息，请参阅 [IBM Bluemix 价格表](https://console.ng.bluemix.net/pricing/){: new_window}或使用[计算器](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet){: new_window}，以获取更详细的估算。

### 如何将 Beta 套餐更改为标准套餐？{: #changeplan}  
{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}} 服务的一般可用性发行版发布后，会将 {{site.data.keyword.objectstorageshort}} 服务 Beta 套餐从目录中除去。客户服务实例不会自动从 Beta 套餐迁移到标准套餐。需要执行以下步骤来更新套餐：

1.	在 {{site.data.keyword.objectstorageshort}} 用户界面的左侧导航栏中，单击**套餐**。
2.	选择**标准**作为新套餐，然后单击**保存**。

![{{site.data.keyword.objectstorageshort}} 更改定价套餐](images/Change_plan.png)

*图 5. {{site.data.keyword.objectstorageshort}} 更改定价套餐*

服务实例和客户数据将迁移到新套餐。

还可以使用命令行界面来更改付款套餐。有关更多信息，请参阅[如何更改套餐](../../pricing/index.html#changing)  

**注：**Beta 套餐服务实例无法迁移到免费套餐。将禁用未迁移的所有服务实例，并且在 60 天后删除这些实例。 

### 对于 {{site.data.keyword.objectstorageshort}}，我可以使用哪些帐户和付款套餐？
{{site.data.keyword.objectstorageshort}} 服务随附多个套餐选项。自一般可用性发行版以来，目前提供两种套餐：标准套餐和免费套餐。标准套餐只适用于 {{site.data.keyword.Bluemix_notm}} 付费帐户（即现买现付或预订帐户）和 IBM 内部用户。

仍有效的试用帐户可以使用免费套餐，免费套餐只允许 {{site.data.keyword.Bluemix_notm}} 组织中存在一个实例。在 {{site.data.keyword.Bluemix_notm}} 试用时间到期后，将禁用关联的 {{site.data.keyword.objectstorageshort}} 服务实例，即无法通过 {{site.data.keyword.Bluemix_notm}} 用户界面或命令行来访问存储帐户。在 30 天宽限期后，将清除 {{site.data.keyword.Bluemix_notm}} 帐户，并且删除所有数据。要避免数据丢失，建议尽快升级到 {{site.data.keyword.Bluemix_notm}} 付费帐户。要升级帐户，请单击右上角的用户管理菜单，然后选择**帐户**，这将提供有关升级过程的指示信息。

在免费套餐中创建的实例可以升级到标准套餐，步骤如[如何将 Beta 套餐更改为标准套餐？](#changeplan)中所述。要升级到标准套餐，关联的组织必须为 {{site.data.keyword.Bluemix_notm}} 付费帐户。具有 {{site.data.keyword.objectstorageshort}} 实例的试用帐户无法升级到标准套餐，而标准套餐上的实例也无法降级到其他套餐。

### 使用 {{site.data.keyword.objectstorageshort}} 如何计费和收费？

{{site.data.keyword.objectstorageshort}} 服务仅按使用内容收费。要开始使用此服务，无需支付最低费用、设置费或保证金。无需为 API 请求或入站数据网络流量付费。

按 {{site.data.keyword.objectstorageshort}} 使用量计费的依据是在整个计费周期内平均每天的存储使用量。包括在 {{site.data.keyword.Bluemix_notm}} 组织帐户下创建的容器中的所有对象数据。 

出站数据传输收费适用于通过公用网络从您的任何对象容器中读取数据的情况。此项计费的依据是在整个计费周期内平均每天的公共出站数据传输。

{{site.data.keyword.objectstorageshort}} 定价的度量组件如下所示：
* 存储使用量  - $0.04/GB/月
* 公共出站数据传输  - $0.09/GB/月 

在计费周期结束后，{{site.data.keyword.Bluemix_notm}} 将对当前计费周期的使用量进行自动计费。您可以通过 {{site.data.keyword.Bluemix_notm}} 报告查看当前计费周期的费用。

为伦敦和达拉斯发布的标准服务套餐定价相同。

### 在 {{site.data.keyword.objectstorageshort}} 中如何执行数据复制？
{{site.data.keyword.objectstorageshort}} 服务从多个存储节点复制数据并维护这些数据的三个副本。有关更多信息，请参阅 [OpenStack Swift 复制](http://docs.openstack.org/developer/swift/overview_replication.html){: new_window}文档。

># 相关链接{:class="linklist"}
>## API 参考{:id="api"}
>* [OpenStack Object Storage (Swift) API V1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
>* [OpenStack Identity (Keystone) API V3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}
>
># 相关链接{:class="linklist"}
>## SDK{:id="sdk"}
>* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}
>
># 相关链接{:class="linklist"}
>## 教程和样本{:id="samples"}
>* [Connecting to IBM Object Storage for Bluemix with Java](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
>* [Use Python to access your Bluemix Object Storage](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
>* [Bluemix Object Storage Community](https://www.ibm.com/developerworks/community/groups/service/html/communityoverview?communityUuid=1b48459f-4091-43cb-bca4-37863606d989){: new_window}
>
># 相关链接{:class="linklist"}
>## 兼容运行时{:id="buildpacks"}
>* [Liberty for Java](https://www.ng.bluemix.net/docs/starters/liberty/index.html){: new_window}
>* [SDK for Node.js](https://www.ng.bluemix.net/docs/starters/nodejs/index.html){: new_window}
>* [Go](https://www.ng.bluemix.net/docs/starters/go/index.html){: new_window}
>* [PHP](https://www.ng.bluemix.net/docs/starters/php/index.html){: new_window}
>* [Python](https://www.ng.bluemix.net/docs/starters/python/index.html){: new_window}
>* [Ruby](https://www.ng.bluemix.net/docs/starters/rails/index.html){: new_window}
>* [社区 buildpack](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}
>
># 相关链接{:class="linklist"}
>## 相关链接{:id="general"}
>* [IBM Bluemix 价格表](https://www.ng.bluemix.net/#/pricing){: new_window}
>* [IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
>
>{:elementKind="article" id="rellinks"}
