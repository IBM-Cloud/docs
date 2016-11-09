---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 保障文件安全 {: #understanding-authentication}
*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

## OpenStack Identity (Keystone) V3 {: #keystone-authentication}

供应新的 {{site.data.keyword.objectstorageshort}} 实例将在 IBM 公共云中创建独立的 Keystone 项目。
{: shortdesc}

凭证结构包含一整组属性，允许您选择最适合您的应用程序的 OpenStack 令牌请求方法或 OpenStack SDK。将新应用程序绑定到实例时，将创建具有项目访问权的新 Keystone 用户。撤销供应实例后，将删除项目和用户。

有关使用 OpenStack Swift 和 Keystone 的更多信息，请查看 [OpenStack 文档站点](http://docs.openstack.org)。

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
						"password": "XXXXXXXXXX"
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
{: codeblock}

向 {{site.data.keyword.objectstorageshort}} 服务发起请求时，将响应头中 `X-Subject-Token` 字段的值用作 `X-Auth-Token` 字段。



示例响应如下所示。已对响应进行了修剪，以仅显示 {{site.data.keyword.objectstorageshort}} 相关信息。

```
	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

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
{: screen}

{{site.data.keyword.objectstorageshort}} URL 位于服务目录中。服务目录包含在令牌请求的响应主体中。响应是可用 OpenStack 服务的完整目录。从服务目录中选择类型为 `object-store` 的端点，以及与凭证中的区域字段相匹配的区域。

**注：**使用公共接口 (`publicURL`)。无法从 {{site.data.keyword.Bluemix_notm}} 访问内部接口 (`internalURL`)。


## 了解服务凭证 {: #understanding-credentials}

服务凭证用于为服务提供认证和安全性。供应实例时，会自动生成一组凭证。Swift 客户机通过下表中的环境变量获取认证信息：

<table>
  <tr>
    <th> 环境变量</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> `OS_USER_ID` </td>
    <td> 您的 {{site.data.keyword.objectstorageshort}} 用户标识。</td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> {{site.data.keyword.objectstorageshort}} 实例的密码。</td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> 项目标识。</td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> 存储对象的区域。{{site.data.keyword.objectstorageshort}} 可在达拉斯和伦敦区域中使用。</td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> 端点 URL。确保将 `/v3` 添加到 URL 末尾。</td>
  </tr>
</table>

*表 1：认证变量和描述*

####  在 UI 中添加服务凭证
1. 在服务实例仪表板上的**服务凭证**选项卡中，单击**新建凭证**并对其命名。
2. （*可选*）在**添加内联配置参数**文本字段中，输入要创建的角色的凭证信息。信息格式必须为 JSON 有效内容。有关 {{site.data.keyword.objectstorageshort}} 用户角色的更多信息，请参阅[访问权类型](../os_security.html#access-types)。
    - 创建管理用户：`{"role":"admin"}`
    - 创建非管理用户：`{"role":"member"}`
3. 单击**添加**。


## 访问权类型 {: #access-types}

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

*表 2：定义的用户角色*

您可以通过 {{site.data.keyword.Bluemix_notm}} 用户界面、Cloud Foundry API 或 Cloud Foundry CLI 来管理 {{site.data.keyword.objectstorageshort}} 用户。




## 授予读访问权 {: #read-access}

具有 admin 角色的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户对容器的读访问权，还可以控制读 ACL 组合。

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

*表 3：按选项列出的读访问许可权*



1. 对凭证进行认证。您可以使用在 UI 的“服务凭证”选项卡中找到的凭证，也可以生成新凭证。有关生成新凭证的更多信息，请参阅[生成服务凭证](insert link here)。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。Swift 命令：
    
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
    {: codeblock}
    
      cURL 命令：
  
    
    ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
    {: pre}
    
2. 通过运行以下命令，授予读访问权：
    Swift 命令：

    
    ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
    {: pre}
    
      cURL 命令：
  
    
    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}
    **注**：请使用逗号 (,) 来分隔访问控制表。


3. 验证读 ACL 值。Swift 命令：
    
    ```
  swift stat <container_name>
  ```
    {: pre}
  cURL 命令：
      
    ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
    {: pre}
    
    在以下示例输出中，可以看到已经授予了读访问权：
    
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
    {: screen}



## 授予写访问权 {: #write-access}

具有 admin 角色的 {{site.data.keyword.objectstorageshort}} 用户可以授予其他用户对容器的写访问权，还可以控制写 ACL 组合。

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

*表 4：按选项列出的写访问许可权*




1. 通过您所创建的服务凭证中的信息，认证您的凭证。您会在输出中收到 {{site.data.keyword.objectstorageshort}} URL 和认证令牌。Swift 命令：
    
    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
  ```
    {: codeblock}
    
      cURL 命令：
  
    
    ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
    {: pre}
    
2. 通过运行以下命令，授予写访问权：
    Swift 命令：
    
    ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
    {: pre}
    
      cURL 命令：
  
    
    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
    {: pre}
    
    **注**：请使用逗号 (,) 来分隔访问控制表。

3. 验证写 ACL 值。
Swift 命令：
    
    ```
  swift stat <container_name>
  ```
    {: pre}
    
    cURL 命令：
    
    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## 除去访问权 {: #removing-access}

要从容器除去读 ACL，请使用：
* Swift 命令：

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}
    
*  cURL 命令：
  

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

要从容器除去写 ACL，请使用：

* Swift 命令：

    ```
  swift post <container_name> --write-acl “”
  ```
    {: pre}
    
*    cURL 命令：
  

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

要验证是否已除去 ACL，请使用：

* Swift 命令：

    ```
  swift stat <container_name>
  ```
    {: pre}

  以下示例输出中显示的“读 ACL”和“写 ACL”均为空白，这表示访问权已除去。
  
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
  {: screen}

*   cURL 命令：
  
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
