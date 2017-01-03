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


# 使用 Swift CLI 存取 {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}


{{site.data.keyword.objectstorageshort}} 服務是以 OpenStack Swift 為基礎，並且可以使用任何相容的用戶端應用程式加以存取。本節說明如何使用 Python Swift 用戶端（其為 {{site.data.keyword.objectstorageshort}} API 及其延伸的指令行介面 (CLI)）來處理容器及檔案。
{: shortdesc}




## 安裝 Swift 用戶端 {: #install-swift-client}

如果您還沒有這麼做，請安裝下列[必備軟體](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。
* Python 2.7 或更新版本
* setuptools 套件
* pip 套件


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




## 設定用戶端 {: #setup-swift-client}

若要設定 Swift 用戶端，您必須`匯出`鑑別資訊。您可以[透過使用者介面](../ObjectStorage/os_security.html#understanding-credentials)或[透過 CLI](../ObjectStorage/os_cli.html#generating-cli)產生認證。

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




## 產生 {{site.data.keyword.objectstorageshort}} 服務認證 {: #generating-cli}

若要使用 Swift CLI 產生服務認證，您可以使用下列步驟。

1. 如果您未登入 {{site.data.keyword.Bluemix_notm}}，請以具有開發人員角色的使用者身分登入。您必須位在您要管理之服務實例的空間內。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 產生服務認證。`service-key-name` 是您指定的認證名稱。您可以使用 Cloud Foundry 指令或 cURL 指令。Cloud Foundry 指令：
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```
  {: pre}

  範例 Cloud Foundry 指令：
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

  cURL 指令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```
  {: pre}

3. 驗證您已建立的「服務金鑰」認證。Cloud Foundry 指令：
  ```
  cf service-keys <service_instance>
  ```
  {: pre}

  Object-Storage-Acl-Test 實例的範例成員服務金鑰：

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

  cURL 指令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: pre}




## 透過 CLI 將物件儲存至容器 {: #storing-cli}

1. 如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. 執行下列指令，以建立新的 {{site.data.keyword.objectstorageshort}} 容器。您目前可以設定 *container_name* 變數。
  ```
  swift post <container_name>
  ```
  {: pre}

**附註**：您收到錯誤訊息，請確認您已安裝[必備軟體](../ObjectStorage/os_cli.html##install-swift-client)。

3. （選用）若要驗證已建立容器，請執行下列指令來列出容器。
  ```
  swift list
  ```
  {: pre}

4. 為了避免意外覆寫所造成的資料毀損，請[設定物件版本化](../ObjectStorage/os_versioning.html#work-with-object-versioning)。若不想要物件版本化，請列出儲存庫中的現有檔案，並視需要重新命名目錄或檔案，然後才進行上傳。

4. 執行下列指令，以將檔案上傳至容器。
  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

**附註**：若要上傳超過 5 GB 的檔案，[需要額外的步驟](../ObjectStorage/os_large_files.html#large-files)。


5. （選用）若要驗證上傳成功，請執行下列指令來檢視容器內容：
  ```
  swift list <container_name>
  ```
  {: pre}




## 使用 Swift CLI 下載物件 {: #downloading-cli}


1.  如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. 為了避免意外覆寫所造成的資料毀損，請[設定物件版本化](../ObjectStorage/os_versioning.html#work-with-object-versioning)。若不想要物件版本化，請列出儲存庫中的現有檔案，並視需要重新命名目錄或檔案，然後才進行下載。

3. 執行下列指令來下載檔案：

```
swift download <container_name> <file_name>
```
{: pre}




## 透過 CLI 刪除物件及容器 {: #deleting-cli}

**注意**：如果您刪除容器，則會刪除容器內所儲存的所有物件。







1.  如果您未登入 {{site.data.keyword.Bluemix_notm}}，請登入包含 {{site.data.keyword.objectstorageshort}} 實例的組織和空間。
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. （選用）確認您已備份物件，然後才刪除檔案及容器。

3. 執行下列指令，以刪除檔案：
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

3. 若要刪除容器，請執行下列指令：
  ```
  swift delete <container_name>
  ```
  {: pre}

**附註**：您可以排定[特定時間來刪除物件](../ObjectStorage/os_deletion.html#schedule-object-deletion)。





## 使用目錄 {: #directory-cli}

#### 使用 Swift CLI 將目錄新增至容器

Swift 沒有真正的目錄結構，但會使用命名來代表目錄佈置。如果您指定目錄名稱，則會將它附加至所有檔名，作為相對路徑的一部分。

1. 在本端建立目錄，並將您的檔案儲存在其中。
2. 執行下列指令，以將目錄上傳至容器：
  ```
  swift upload <container_name> <directory_name>
  ```
  {: pre}

#### 下載目錄
若要下載目錄結構，請使用 `-prefix` 參數來表示您要下載的目錄或目錄結構。

1. 執行下列指令，以下載目錄：
  ```
  swift download <container_name> --prefix <directory>
  ```
  {: pre}
