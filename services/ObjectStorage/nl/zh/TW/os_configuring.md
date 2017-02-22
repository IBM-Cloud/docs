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

# 配置 CLI 以使用 Swift 和 Cloud Foundry 指令

若要使用 Swift 或 Cloud Foundry 指令與 {{site.data.keyword.objectstorageshort}} 服務互動，您必須安裝必備軟體。
{: shortdesc}


## 安裝 Swift 用戶端 {: #install-swift-client}

如果您還沒有這麼做，請安裝下列必備軟體。
* Python 2.7 或更新版本
* setuptools 套件
* pip 套件
* Cloud Foundry CLI


若要安裝 Python Swift 用戶端，請執行下列指令：
```
pip install python-swiftclient
```
{: pre}

若要安裝 Python Keystone 用戶端，請執行下列指令：
```
pip install python-keystoneclient
```
{: pre}

如需必要條件的相關資訊，請參閱 [Openstack 文件](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。


## 設定用戶端 {: #setup-swift-client}

若要配置 Swift 用戶端，您必須`匯出`鑑別資訊。您可以使用 Cloud Foundry 或 cURL 指令，透過 CLI [產生認證](/docs/services/ObjectStorage/os_credentials.html)，或是透過 {{site.data.keyword.Bluemix_notm}} 使用者介面來進行。用戶端會從下表的環境變數中取得資訊。

<table>
<caption> 表 1. 環境變數與說明</caption>
  <tr>
    <th> 環境變數</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> 您的 {{site.data.keyword.objectstorageshort}} 使用者 ID。</td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> 您 {{site.data.keyword.objectstorageshort}} 實例的密碼。</td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> 您的專案 ID。</td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> 在其中儲存物件的地區。達拉斯及倫敦地區提供 {{site.data.keyword.objectstorageshort}}。</td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> 端點 URL。請確定 <code>/v3</code> 已加入 URL 尾端。</td>
  </tr>
</table>



若要匯出您的鑑別資訊，請輸入您的認證並執行下列指令：
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


範例：
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
