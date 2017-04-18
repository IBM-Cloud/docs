---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# 开始使用 {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}

*上次更新时间：2016 年 8 月 13 日*
{: .last-updated}


## 使用 {{site.data.keyword.objectstorageshort}} 用户界面 {: #using-object-storage-ui}

### UI 元素和导航
供应 {{site.data.keyword.objectstorageshort}} 后，可以在 {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务实例仪表板中查看实例信息。在仪表板中，选择 {{site.data.keyword.objectstorageshort}} 实例以查看包含更详细信息的面板。  
#### 使用情况数据
在应用程序主页上，将显示实例的存储器使用情况信息。还将显示所有容器中的当前**存储容器**数和**对象**总数。还会列出内存使用情况（以兆字节为单位）。**使用的存储空间**是指使用的当前空间量。
#### 操作
要检索最新的使用情况数据，请单击**刷新**按钮。   
#### 对象浏览器
使用对象浏览器可管理对象存储容器和对象。可以执行创建容器、上传文件、删除容器和删除文件等操作。


## 从 {{site.data.keyword.Bluemix_notm}} 应用程序使用 {{site.data.keyword.objectstorageshort}} {: #using-object-storage-from-bluemix-app}

### 如何在创建后将 {{site.data.keyword.objectstorageshort}} 服务绑定到应用程序 {: #bind-object-storage-to-application}
1.	在 {{site.data.keyword.Bluemix_notm}} 仪表板中，选择要绑定的应用程序。
2.	在应用程序概述中，单击**绑定服务或 API**。
3.	从服务列表中，选择 {{site.data.keyword.objectstorageshort}} 实例，然后单击**添加**。
4.	系统提示时，单击**重新编译打包**。应用程序必须重新编译打包后，才可使用新服务。

### 绑定上下文

如果要在绑定上下文中使用 {{site.data.keyword.objectstorageshort}}，那么将通过应用程序绑定进程间接提供云凭证。将服务实例成功绑定到应用程序后，类似于以下示例的配置将添加到 `VCAP_SERVICES` 环境变量。

```
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
```

## 使用 Swift CLI 访问 {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

您可以通过因特网以及 IBM {{site.data.keyword.Bluemix_notm}} 中的应用程序和虚拟服务器访问 {{site.data.keyword.objectstorageshort}} 服务。{{site.data.keyword.objectstorageshort}} 服务的常见用例如下所示：

* 备份实例中的卷数据
* 传输大量数据时用作中间位置
* 在未直接连接的环境之间传输数据
* 充当中心存储库

{{site.data.keyword.objectstorageshort}} 服务基于 OpenStack Swift，可以使用任何兼容的客户机应用程序进行访问。本部分描述如何利用 Python Swift 客户机来使用容器和文件；Python Swift 客户机是 {{site.data.keyword.objectstorageshort}} API 及其扩展的命令行界面。

### 安装 Swift 客户机 {: #install-swift-client}

如果尚未安装以下必备软件，请进行安装。有关更多信息，请参阅 [OpenStack 文档](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。
* Python 2.7 或更高版本
* setuptools 软件包
* pip 软件包

使用 Python pip 安装 Python Swift 客户机：

```
	sudo pip install python-swiftclient
```

通过运行以下命令，安装 Python Keystone 客户机：

```
	sudo pip install python-keystoneclient
```

### 设置客户机 {: #setup-swift-client}

Swift 客户机通过以下环境变量获取认证信息：
* `OS_AUTH_URL` 是端点 URL
* `OS_USER_ID` 是用户名
* `OS_PASSWORD` 是密码

如下所示，设置认证信息。

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

可以在 {{site.data.keyword.objectstorageshort}} 用户界面的**服务凭证**页面中查找 {{site.data.keyword.objectstorageshort}} 服务的凭证值。

**注：**请确保为 Swift 客户机配置环境变量 `OS_AUTH_URL` 时，在 {{site.data.keyword.objectstorageshort}} 用户界面的凭证中，将 `/v3` 添加到 `auth_url`。


### 使用容器 {: #work-with-containers}

列出容器：
```
	swift list
```
创建容器：
```
	swift post <container_name>
```
列出容器的内容：
```
	swift list <container_name>
```
### 使用对象 {: #work-with-objects}

#### 向容器添加文件
```
	swift upload <container_name> <file_name>
```
#### 向容器添加大于 5 GB 的文件

如果要上传大于 5 GB 的文件，必须将其拆分成较小的区块。可以通过提供 `-segment-size` 参数，指示 Swift 客户机来处理此类上传：
```
	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
各个分段会并行上传到名为 `<container_name>_segments` 的独立容器中。上传完所有分段后，Swift 会创建清单文件，以便可以从包含名为 `<file_name>` 的原始文件的原始容器 `<container_name>` 中将这些分段下载到单个文件中。

例如，以下命令将从名为 `test_container` 的容器中上传名为 `large_file` 的文件，文件的分段大小为 `1073741824`。
```
	swift upload test_container -S 1073741824 large_file
```
可以运行以下命令来下载该文件：
```
	swift download test_container large_file
```
#### 下载文件
```
	swift download <container_name> <file_name>
```
#### 向容器添加目录

Swift 没有真正的目录结构，而是使用命名来表示目录布局。要向容器添加目录，请运行以下命令：
```
	swift upload <container_name> <directory_name>
```
此命令会将完整目录结构作为相对路径上传。例如，如果指定 `/mnt/volume1`，那么目录结构 mnt/volume1 将附加到所有文件名，以指示目录结构。


#### 下载目录

要下载目录结构，请使用 `-prefix` 参数来指示要下载的目录或目录结构。
```
	swift download <container_name> --prefix <directory>
```
#### 删除文件
```
	swift delete <container_name> <file_name>
```
### 使用对象版本控制 {: #work-with-object-versioning}

通过使用 `X-Versions-Location` 标记，您可以设置容器中每一个对象的版本。要执行此操作，请创建附加容器，以保留较旧版本的对象，如下所示。

如果您使用 Swift 客户机，那么您可以如下对其进行设置：
```
	swift post container_one -H "X-Versions-Location:container_two"
```
如果您使用 curl，那么您可以对其进行如下设置：
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
在该示例中，已设置 `container_two` 包含存储在 `container_one` 中的较旧版本的对象。因此，`container_one` 将具有对象的最新版本，而 `container_two` 将具有对象的较旧版本。请确保存在 `container_two`，以便可以进行版本控制。

在已设置版本控制的情况下，当您将对象上传至 `container_one` 时，如果存在对象的现有版本，那么当在 `container_one` 中创建新版本时，现有版本会移至 `container_two`。如果您从 `container_one` 删除对象，那么对象的较旧版本会从 `container_two` 移回 `container_one`。

`container_two` 中的对象将会自动以下列格式命名：`<Length><Object_name>/<Timestamp>`。

`Length` 指的是对象名称的长度；其为 3 个字符的零填充的十六进制数字。`Object_name` 是对象的名称。`Timestamp` 是最初上传此特定版本对象的时间戳记。

要禁用版本控制，请使用 `X-Remove-Versions-Location` 标记：
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
或者
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
以下是使用版本控制的完整示例：

1. 创建容器：
```
		$ swift post container_one
		$
```
2. 设置 container_one 的版本控制：
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. 创建 container_two：
```
		$ swift post container_two
		$
```
4. 第一次将对象上传至 container_one：
```
		$ swift upload container_one object
		object
		$
```
5. 列出 container_one 中的对象：
```
		$ swift list container_one
		object
		$
```
6. 列出 container_two 中的对象：
```
		$ swift list container_two
		$
```
7. 将新版本的对象上传至 container_one：
```
		$ swift upload container_one object
		object
		$
```
8. 列出 container_one 中的对象：
```
		$ swift list container_one
		object
		$
```
9. 列出 container_two 中的对象：
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. 删除 container_one 中的对象：
```
		$ swift delete container_one object
		object
		$
```
11. 列出这两个容器：
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### 安排对象删除 {: #schedule-object-deletion}

您可以设置对象在给定时间量到期。换句话说，您可以安排删除对象。通过使用 `X-Delete-At` 或 `X-Delete-After` 标头，可以完成此操作。`X-Delete-At` 标头采用整数代表删除对象的戳记时间。`X-Delete_After` 标头采用整数代表在该秒数之后删除对象。

如果您使用 Swift 客户机对容器内的对象执行发布操作，请参阅以下示例。

* 要将对象设置为在“2016/04/01 08:00:00”删除，请使用以下命令：
```
		swift post -H "X-Delete-At:1459515600" container object
```
* 要将对象设置为在此后一小时删除，请使用以下命令：
```
		swift post -H "X-Delete-After:3600" container object
```
执行此操作之后，`swift stat container object` 命令将会在戳记时间中显示 `X-Delete-At` 标头与适当的到期时间。

* 要从对象除去到期时间，请使用以下命令：
```
		swift post -H "X-Remove-Delete-After:" container object
```
如果您使用 cURL，那么命令如下所示：

* 要将对象设置为在“2016/04/01 08:00:00”删除，请使用以下命令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* 要将对象设置为在此后一小时删除，请使用以下命令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* 要检查对象是否有标头，请使用以下命令：
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* 要除去到期时间，请使用以下命令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**注：**对象的实际删除可能不会在所指示的确切时间发生。但是，对象确实会在指定的时间到期，这表示将无法再使用该对象。实际删除操作将会在下一次 Swift 集群中配置的 swift-object-expirer 守护程序运行时发生。





### 创建临时 URL {: #create-temporary-url}

临时 URL 较长且难以猜中，可用于在指定时间段内下载对象，而不必请求进一步认证 。使用以下步骤可生成临时 URL：

1. 确定认证帐户。
2. 设置密钥。
3. 创建临时 URL。

#### 确定认证帐户

Swift `stat` 命令将显示有关帐户的信息：
```
	swift stat
```
找到“帐户”字段，并记录*帐户：*后面的完整字符串，包括 `AUTH_`。

#### 设置密钥

此密钥可以是所选的任何内容，但最佳做法是选择难以猜中的随机长字符串。
```
	swift post -m "Temp-URL-Key:<key>"
```
运行 Swift `stat` 命令，以验证成功设置 `Temp-URL-Key`。
```
	swift stat
```

#### 创建临时 URL

Swift `tempurl` 命令将采用以下位置参数：

* [method] GET 用于允许下载。PUT 用于允许上传。
* [seconds] 临时 URL 将可用的时间（以秒为单位）。
* [path] 表示为 `/v1/<auth_account>/<container_name>/<object_name>` 的对象的完整路径。有关更多信息，请参阅 [{{site.data.keyword.objectstorageshort}} URL](#access-points)。
* [key] 在步骤 2 中设置的密钥。

```
swift tempurl GET <seconds> <path> <key>
```

此命令将返回 URL，可以将此 URL 附加到集群名称以获得完整 URL。使用该完整 URL 可通过任何兼容的 HTTP 客户机（例如，curl、wget 或 Firefox）来下载对象。

## 使用 Swift REST CLI 访问 {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

可以通过命令行客户机接口（例如，cURL）来使用 Swift REST API，也可以通过应用程序来调用该 API。  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

要与 {{site.data.keyword.objectstorageshort}} API 进行交互，请如下所示构造 {{site.data.keyword.objectstorageshort}} URL：
```
	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
```


URL 由 5 个部分组成。`<API version>` 是 v1。您可以从 {{site.data.keyword.objectstorageshort}} 用户界面查找 {{site.data.keyword.objectstorageshort}} 的 `<project ID>`、`<container namespace>` 和 `<object namespace>`。对于 `<access point>`，请参阅下表：


| **区域**  |   **公共访问点**                     |
|-------------|-----------------------------------------------|
| 达拉斯      | https://dal.objectstorage.open.softlayer.com/ |
| 伦敦      | https://lon.objectstorage.open.softlayer.com/ |


*表 1. {{site.data.keyword.objectstorageshort}} 访问点*


### {{site.data.keyword.objectstorageshort}} API

请参阅 [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}，以获取 {{site.data.keyword.objectstorageshort}} REST API 选项和示例的整套列表。

## 跨多区域使用 {{site.data.keyword.objectstorageshort}} {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务支持“达拉斯”和“伦敦”存储区域。这两个存储区域独立于 {{site.data.keyword.Bluemix_notm}} 区域（例如，美国南部区域和英国），而 {{site.data.keyword.objectstorageshort}} 服务实例创建于该区域。例如，如果在美国南部的 {{site.data.keyword.Bluemix_notm}} 区域中创建 {{site.data.keyword.objectstorageshort}} 实例，那么可以读写“达拉斯”或“伦敦”存储区域的数据。  

对于美国南部的 {{site.data.keyword.Bluemix_notm}} 区域，“达拉斯”存储区域是缺省值。对于英国的 {{site.data.keyword.Bluemix_notm}} 区域，“伦敦”存储区域是缺省值。{{site.data.keyword.objectstorageshort}} 用户界面启动后始终会进入 {{site.data.keyword.Bluemix_notm}} 区域的缺省存储区域。要切换区域，请单击“{{site.data.keyword.objectstorageshort}} 区域”下拉列表，然后选择其他区域。

**注：**{{site.data.keyword.objectstorageshort}} 服务不支持跨存储区域复制。

### 多区域访问

要使用 {{site.data.keyword.objectstorageshort}} 服务，必须[向 OpenStack Keystone 认证](#keystone-authentication)。认证成功后，响应中将可以使用 `X-Subject-Token` 和 {{site.data.keyword.objectstorageshort}} 端点。

例如，要在“达拉斯”存储区域中创建名为 `my_container` 的容器，请在 curl 命令中指定达拉斯访问点，如下所示：
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

要在“伦敦”存储区域中创建名为 `my_container` 的容器，请在 curl 命令中指定伦敦访问点，如下所示：
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**注：**从 Keystone 获取的 `X-Subject-Token` 在所有存储区域中都有效。

有关不同区域的访问点的更多信息，请参阅 [Object Storage 访问点](#access-points)表。


## 了解认证和凭证 {: #understanding-authentication-credentials}

### 生成 {{site.data.keyword.objectstorageshort}} 凭证而不绑定应用程序

要生成在 {{site.data.keyword.Bluemix_notm}} 应用程序外部使用的 {{site.data.keyword.objectstorageshort}} 云凭证，必须为 {{site.data.keyword.objectstorageshort}} 实例生成服务密钥。可以通过从用户界面的侧边栏中选择**服务凭证**或使用 Cloud Foundry CLI（V6.11.3 或更高版本）来生成新密钥。为 {{site.data.keyword.objectstorageshort}} 实例生成服务密钥并检索到该服务密钥后，可以使用 Cloud Integration 信息通过 OpenStack SDK 或 OpenStack Identity API 来请求 Keystone 令牌，并开始使用 Swift 帐户来管理对象。

要使用 Cloud Foundry CLI 创建密钥，请登录并运行以下命令：
 ```
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>
```
要从 Cloud Foundry CLI 中检索服务凭证，请运行以下命令：
```
	cf service-key <object_storage_instance_name> <unique_name_for_this_key>
```

### 云项目和用户
供应新的 {{site.data.keyword.objectstorageshort}} 实例将在 IBM 公共云中创建独立的 Keystone 项目。将新应用程序绑定到 {{site.data.keyword.objectstorageshort}} 实例时，将创建具有项目访问权的新 Keystone 用户。撤销供应实例后，将删除项目和用户。

### OpenStack Identity (Keystone) V3 {: #keystone-authentication}
凭证结构包含一整组属性，允许您选择最适合您的应用程序的 OpenStack 令牌请求方法或 OpenStack SDK。

建议使用的 V3 令牌请求是对 https://identity.open.softlayer.com/v3/auth/tokens 的 POST 请求，如以下 curl 命令中所示：
```
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
```
向 {{site.data.keyword.objectstorageshort}} 服务发起请求时，将响应头中 `X-Subject-Token` 字段的值用作 `X-Auth-Token` 字段。

示例响应如下所示。已对响应进行了修剪，以仅显示 {{site.data.keyword.objectstorageshort}} 相关信息。

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```

{{site.data.keyword.objectstorageshort}} URL 位于服务目录中。服务目录包含在令牌请求的响应主体中。响应是可用 OpenStack 服务的完整目录。从服务目录中选择类型为 `object-store` 的端点，以及与凭证中的区域字段相匹配的区域。

**注：**使用公共接口 (`publicURL`)。无法从 {{site.data.keyword.Bluemix_notm}} 访问内部接口 (`internalURL`)。



## 使用细颗粒度访问控制保护文件 {: #fine-grained-access-control}

如果您有多个用户将文件存储在同一容器中，那么可以使用细颗粒度访问控制表来保护文件。

注：本文档中概述的过程需要使用 Swift CLI。有关更多信息，请参阅[将 {{site.data.keyword.objectstorageshort}} 与 Swift CLI 配合使用](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli)。


### 访问权类型 {: #access-types}

对服务的访问权是通过用户角色和容器访问控制表进行控制的。{{site.data.keyword.objectstorageshort}} 用户可以是管理用户，也可以是非管理用户。访问控制表由管理用户在容器级别启用，其在服务实例、存储帐户或项目级别不可用。

<table>
  <tr>
    <th> 管理用户 (admin)</th>
    <th> 非管理用户 (member)</th>
  </tr>
  <tr>
    <td> 管理访问控制</td>
    <td> 缺省情况下，无权访问服务或其容器</td>
  </tr>
  <tr>
    <td> 可以创建和删除容器</td>
    <td> 可以基于容器读/写 ACL 执行操作</td>
  </tr>
  <tr>
    <td> 可以读取和写入容器</td>
    <td> 可以执行由 admin 确定的操作</td>
  </tr>
</table>

*表 1：定义的用户角色*

您可以通过 {{site.data.keyword.Bluemix_notm}} 用户界面、Cloud Foundry API 或 Cloud Foundry CLI 来管理 {{site.data.keyword.objectstorageshort}} 用户。



### 生成 {{site.data.keyword.objectstorageshort}} 服务凭证 {: #generating}

从新的 {{site.data.keyword.Bluemix_notm}} 控制台，可以为 {{site.data.keyword.objectstorageshort}} 用户生成新的服务凭证。要查看新的控制台，请单击**尝试新 {{site.data.keyword.Bluemix_notm}}**。

1.  以开发者角色的用户身份登录到 {{site.data.keyword.Bluemix_notm}}。您必须位于要管理的服务实例的空间内。
2. 单击**服务凭证**选项卡。
3. 单击**新建凭证**。
4. 提供凭证名称。
5. 在**添加内联配置参数**文本字段中，输入您想要创建的角色的凭证信息。信息格式必须为 JSON 有效内容。
  - 创建管理用户：`{"role":"admin"}`
  - 创建非管理用户：`{"role":"member"}`
5. 单击**添加**。

要使用 cURL 命令或 Swift CLI 来生成服务凭证，可以使用以下步骤。

1. 以开发者角色的用户身份登录到 {{site.data.keyword.Bluemix_notm}}。您必须位于要管理的服务实例的空间内。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. 生成服务凭证。`service-key-name` 将是凭证的名称。您可以使用 Cloud Foundry 命令或 cURL 命令。

  Cloud Foundry 命令：
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```

  示例：

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  cURL 命令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```

3. 为您所创建的服务密钥验证凭证。

  Cloud Foundry 命令：
  ```
  cf service-key <service_key_name> <member_name>
  ```
  示例：
  为名为 Object-Storage-Acl-Test 的服务实例创建成员服务密钥。
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  cURL 命令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```



### 分配访问权 {: #assigning-access}  

只有 admin 角色的 {{site.data.keyword.objectstorageshort}} 用户才能授予其他用户读取或写入容器的访问权。

要在 CLI 中授予读访问权，请使用 `--read-acl` 或 `-r` 选项。

1. 通过您所创建的服务凭证中的信息，认证您的凭证。您会在输出中收到 Object Storage URL 和认证令牌。

  Swift 命令：
  ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL 命令：
  ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
3. 通过运行以下命令，授予读访问权：

  Swift 命令：
  ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. 验证读 ACL 值。

  Swift 命令：
  ```
  swift stat <container_name>
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  示例输出：
  ```
  HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
  ```

您可以控制读 ACL 组合。

<table>
  <tr>
    <th> 许可权</th>
    <th> 读 ACL 选项</th>
  </tr>
  <tr>
    <td> 读取（针对所有引用方，而不论帐户亲缘关系为何）</td>
    <td> `.r,*`</td>
  </tr>
  <tr>
    <td> 读取和列示（针对所有引用方和列表）</td>
    <td> `.r:*,.rlistings`</td>
  </tr>
  <tr>
    <td> 读取和列示（针对特定项目中的指定用户）</td>
    <td> `< project_id>:< user_id>`</td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的指定用户）</td>
    <td> `<*>:< user_id>`</td>
  </tr>
  <tr>
    <td> 读取和列示（针对指定项目中的每个用户）</td>
    <td> `< project_id>:<*>`</td>
  </tr>
  <tr>
    <td> 读取和列示（针对每个项目中的每个用户）</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 2：按选项列出的读访问许可权*

注：请使用逗号 (,) 来分隔访问控制表。例如，`-read-acl project id:user_id1, project_id2:user_id2`。


要授予写访问权，请通过 Swift CLI 使用 `--write-acl` 或 `-w` 选项。

1. 通过您所创建的服务凭证中的信息，认证您的凭证。您会在输出中收到 Object Storage URL 和认证令牌。

  Swift 命令：
  ```
  export OS_USER_ID="<user_id>"
  export OS_PASSWORD="<password>"
  export OS_TENANT_ID=<tenant_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL 命令：
  ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
2. 通过运行以下命令，授予写访问权：

  Swift 命令：
  ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. 验证写 ACL 值。

  Swift 命令：
  ```
  swift stat <container_name>
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


您可以控制写 ACL 组合。

<table>
  <tr>
    <th> 许可权</th>
    <th> 写 ACL 选项</th>
  </tr>
  <tr>
    <td> 写入（针对特定项目中的指定用户）</td>
    <td> `<project_id>:<user_id>`</td>
  </tr>
  <tr>
    <td> 写入（针对每个项目中的指定用户）</td>  
    <td> `*:<user_id>`</td>
  </tr>
  <tr>
    <td> 写入（针对指定项目中的每个用户）</td>
    <td> `<project_id>:<*>`</td>
  </tr>
  <tr>
    <td> 写入（针对每个项目中的每个用户）</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 3：按选项列出的写访问许可权*

注：请使用逗号 (,) 来分隔访问控制表。例如，`-write-acl project id:user_id1, project_id2:user_id2`。




### 除去访问权 {: #removing-access}

要从容器除去读 ACL，请使用：

  Swift 命令：
  ```
  swift post <container_name> --read-acl “”
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

要从容器除去写 ACL，请使用：

  Swift 命令：
  ```
  swift post <container_name> --write-acl “”
  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

要验证是否已除去 ACL，请使用：

  Swift 命令：
  ```
  swift stat <container_name>
  ```

  示例输出：
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  cURL 命令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## 取消绑定和撤销供应 {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### 如何撤销供应 {{site.data.keyword.objectstorageshort}} 服务
1.	从 {{site.data.keyword.Bluemix_notm}} 仪表板中选择服务。  
2.	单击齿轮图标，并选择**删除服务**。

**注意：**如果撤销供应 IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服务实例，将删除云项目和 Swift 帐户。撤销供应的实例中的所有容器和对象也将从 Swift 中删除，并且无法复原。

### 取消绑定应用程序或删除服务密钥

如果取消应用程序与 {{site.data.keyword.objectstorageshort}} 实例的绑定或删除服务密钥，那么将删除凭证。{{site.data.keyword.objectstorageshort}} 帐户要到撤销供应 {{site.data.keyword.objectstorageshort}} 实例后才会删除。通过[重新绑定或创建新的服务密钥](#bind-object-storage-to-application)，可以生成新的云凭证。
