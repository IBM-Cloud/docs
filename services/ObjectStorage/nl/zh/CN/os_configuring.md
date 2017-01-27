---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 配置 CLI 以使用 Swift 和 Cloud Foundry 命令

要使用 Swift 或 Cloud Foundry 命令与 {{site.data.keyword.objectstorageshort}} 服务进行交互，必须安装必备软件。
{: shortdesc}


## 安装 Swift 客户机 {: #install-swift-client}

如果尚未准备就绪，请安装以下必备软件。
* Python 2.7 或更高版本
* setuptools 软件包
* pip 软件包
* Cloud Foundry CLI


要安装 Python Swift 客户机，请运行以下命令：
```
pip install python-swiftclient
```
{: pre}

要安装 Python Keystone 客户机，请运行以下命令：
```
pip install python-keystoneclient
```
{: pre}

有关必备软件的更多信息，请参阅 [OpenStack 文档](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。


## 设置客户机 {: #setup-swift-client}

要配置 Swift 客户机，必须执行 `export` 命令以导出认证信息。您可以通过 CLI 使用 Cloud Foundry 或 cURL 命令，或通过 {{site.data.keyword.Bluemix_notm}} UI 来[生成凭证](/docs/services/ObjectStorage/os_credentials.html)。客户机将通过下表中的环境变量获取相关信息。

<table>
<caption> 表 1. 环境变量和描述</caption>
  <tr>
    <th> 环境变量</th>
    <th> 描述</th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> 您的 {{site.data.keyword.objectstorageshort}} 用户标识。</td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> {{site.data.keyword.objectstorageshort}} 实例的密码。</td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> 项目标识。</td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> 存储对象的区域。{{site.data.keyword.objectstorageshort}} 可在达拉斯和伦敦区域中使用。</td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> 端点 URL。确保将 <code>/v3</code> 添加到 URL 末尾。</td>
  </tr>
</table>



要导出认证信息，请输入您的凭证并运行以下命令：
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
  ```
{: codeblock}


示例：
```
  export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
{: screen}
