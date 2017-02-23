---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 產生服務認證 {: #credentials}

服務認證是用來提供服務的鑑別及安全。您可以使用 CLI 或 {{site.data.keyword.Bluemix_notm}} 使用者介面產生新建的認證。
{: shortdesc}


## 若要在使用者介面中新增認證，請執行下列動作：

1. 在服務實例儀表板的**服務認證**標籤中，按一下**新建認證**，並指定其名稱。
2. 選用項目：在**新增線型配置參數**文字欄位中，輸入角色的認證資訊，該角色要具有您想要提供的[存取權類型](/docs/services/ObjectStorage/os_access_types.html)。資訊必須格式化為 JSON 有效負載。
    - 若要建立管理使用者：`{"role":"admin"}`
    - 若要建立非管理使用者：`{"role":"member"}`
3. 按一下**新增**。


## 若要在 CLI 使用 Cloud Foundry 指令新增認證，請執行下列動作：

1. 如果您未登入 {{site.data.keyword.Bluemix_notm}}，請以具有開發人員角色的使用者身分登入。您必須位在您要管理之服務實例的空間內。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 產生服務認證。取代變數 `service-key-name` 來提供您的認證名稱。也可以選擇性地指派[使用者角色](/docs/services/ObjectStorage/os_access_types.html)。

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  範例：
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. 驗證您已建立之金鑰的認證。

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  針對具有成員角色之使用者的 Object-Storage-Acl-Test 實例的範例金鑰：

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
  {: screen}



#### 若要在 CLI 使用 cURL 指令新增認證，請執行下列動作：

1. 如果您未登入 {{site.data.keyword.Bluemix_notm}}，請以具有開發人員角色的使用者身分登入。您必須位在您要管理之服務實例的空間內。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 執行下列指令以產生服務認證。

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> 表 1. 說明的 cURL 服務認證變數</caption>
    <tr>
      <th> 變數</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td> ```https://api.ng.bluemix.net/v2/service_keys ``` </td>
      <td> 服務金鑰端點。</td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> 您可在 URL 中找到它。</td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> 服務實例的名稱。</td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> 將<a href= /docs/services/ObjectStorage/os_constructing.html>使用者的角色</a>指定為管理者或成員。</td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> 您使用 Keystone 鑑別實例時所收到的記號。</td>
    </tr>
  </table>

3. 執行下列指令，以驗證您的認證。

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
