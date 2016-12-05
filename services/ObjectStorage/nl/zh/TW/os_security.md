---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 保護檔案安全 {: #understanding-authentication}


## 瞭解服務認證 {: #understanding-credentials}

服務認證是用來提供服務的鑑別及安全。佈建實例時，會自動產生一組認證。Swift 用戶端會從下表的環境變數中取得鑑別資訊。

<table>
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
    <td> 端點 URL。請確定 `/v3` 已加入 URL 尾端。</td>
  </tr>
</table>

表 1：鑑別變數及說明

####  在使用者介面中新增服務認證
1. 在服務實例儀表板的**服務認證**標籤中，按一下**新建認證**，並指定其名稱。
2. （*選用*）在**新增線型配置參數**文字欄位中，輸入您要建立之角色的認證資訊。資訊必須格式化為 JSON 有效負載。如需 {{site.data.keyword.objectstorageshort}} 使用者角色的相關資訊，請參閱[存取類型](../os_security.html#access-types)。
    - 若要建立管理使用者：`{"role":"admin"}`
    - 若要建立非管理使用者：`{"role":"member"}`
3. 按一下**新增**。


## 存取類型 {: #access-types}

存取服務是由使用者角色及容器存取控制清單所控制。{{site.data.keyword.objectstorageshort}} 使用者可以是管理使用者或非管理使用者。存取控制清單是由管理使用者在容器層次上啟用，因此不適用於服務實例、儲存空間帳戶，或無法在專案層次上使用。

<table>
  <tr>
    <th> 管理使用者（管理者）</th>
    <th> 非管理使用者（成員）</th>
  </tr>
  <tr>
    <td> 管理存取控制</td>
    <td> 依預設，對服務及其容器沒有存取權</td>
  </tr>
  <tr>
    <td> 可以建立及刪除容器</td>
    <td> 可以根據容器的讀寫 ACL 執行動作</td>
  </tr>
  <tr>
    <td> 可以讀取容器並寫入其中</td>
    <td> 可以執行由管理者決定的動作</td>
  </tr>
</table>

表 2：定義的使用者角色

您可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面、Cloud Foundry API 或 Cloud Foundry CLI 管理 {{site.data.keyword.objectstorageshort}} 使用者。




## 授與讀取權 {: #read-access}

具有管理者角色的 {{site.data.keyword.objectstorageshort}} 使用者可以授與另一位使用者對容器的讀取權，以及操作讀取 ACL 組合。

<table>
  <tr>
    <th> 許可權</th>
    <th> 讀取 ACL 選項</th>
  </tr>
  <tr>
    <td> 無論帳戶連結為何，所有參照者皆可讀取</td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> 所有參照者及清單皆可讀取及列出</td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以讀取及列出</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以讀取及列出</td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可讀取及列出</td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可讀取及列出</td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

表 3：依選項列出的讀取權



1. 鑑別您的認證。您可以使用在使用者介面的服務認證標籤中找到的認證，也可以產生新的認證。如需產生新認證的相關資訊，請參閱[產生服務認證](insert link here)。您會收到 {{site.data.keyword.objectstorageshort}} URL 及鑑別記號作為輸出。Swift 指令：

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

    cURL 指令：

    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}

2. 執行下列指令來授與讀取權。Swift 指令：

    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **附註**：使用逗點 (,) 來區隔存取控制清單。


3. 驗證「讀取 ACL」值。Swift 指令：

    ```
    swift stat <container_name>
    ```
    {: pre}
    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    在下列範例輸出中，您可以看到已授與讀取權：

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



## 授與寫入權 {: #write-access}

具有管理者角色的 {{site.data.keyword.objectstorageshort}} 使用者可以授與另一位使用者對容器的寫入權，以及操作寫入 ACL 組合。

<table>
  <tr>
    <th> 許可權</th>
    <th> 寫入 ACL 選項</th>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以寫入</td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以寫入</td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可寫入</td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可寫入</td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

表 4：依選項列出的寫入權



1. 使用您所建立之服務認證中的資訊來鑑別您的認證。您會收到 {{site.data.keyword.objectstorageshort}} URL 及鑑別記號作為輸出。Swift 指令：

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

    cURL 指令：

    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}

2. 執行下列指令來授與寫入權。Swift 指令：

    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}

    **附註**：使用逗點 (,) 來區隔存取控制清單。

3. 驗證寫入 ACL 值。Swift 指令：

    ```
    swift stat <container_name>
    ```
    {: pre}

    cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## 移除存取權 {: #removing-access}

若要從容器中移除讀取 ACL，請執行下列指令：
* Swift 指令：

    ```
    swift post <container_name> --read-acl “”
    ```
    {: pre}

*  cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

若要從容器中移除寫入 ACL，請執行下列指令：

* Swift 指令：

    ```
    swift post <container_name> --write-acl ""
    ```
    {: pre}

*  cURL 指令：

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

若要驗證您已移除 ACL，請執行下列指令：

* Swift 指令：

    ```
    swift stat <container_name>
    ```
    {: pre}

  下列範例輸出將「讀取 ACL」及「寫入 ACL」顯示為空白，這表示已移除存取權。

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

* cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
