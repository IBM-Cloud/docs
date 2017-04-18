---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}

*前次更新：2016 年 8 月 13 日*
{: .last-updated}


## 使用 {{site.data.keyword.objectstorageshort}} 使用者介面 {: #using-object-storage-ui}

### 使用者介面元素及導覽
若您的 {{site.data.keyword.objectstorageshort}} 已佈建，可以在 {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服務實例儀表板中看到您的實例資訊。從儀表板中，選取 {{site.data.keyword.objectstorageshort}} 實例，以檢視含有其他詳細資訊的畫面。  
#### 用量資料
在應用程式的首頁上，您會看到實例的儲存空間用量資訊。它也會顯示**儲存空間容器**的現行數目，以及所有容器中的**物件**總數。它會以 MB 為單位列出記憶體用量。**耗用的儲存空間**是指已使用的現行空間數量。
#### 動作
若要擷取最新的用量資料，請按一下**重新整理**按鈕。   
#### 物件瀏覽器
使用物件瀏覽器來管理物件儲存空間容器及物件。您可以建立容器、上傳檔案、刪除容器、刪除檔案，以及執行其他動作。


## 從 {{site.data.keyword.Bluemix_notm}} 應用程式使用 {{site.data.keyword.objectstorageshort}} {: #using-object-storage-from-bluemix-app}

### 如何在建立之後將 {{site.data.keyword.objectstorageshort}} 服務連結至應用程式 {: #bind-object-storage-to-application}
1.	在 {{site.data.keyword.Bluemix_notm}} 儀表板中，選取您要連結的應用程式。
2.	在應用程式概觀中，按一下**連結服務或 API**。
3.	從服務清單中選取您的 {{site.data.keyword.objectstorageshort}} 實例，然後按一下**新增**。
4.	系統提示時，按一下**重新編譯打包**。您的應用程式必須重新編譯打包，才能使用新的服務。

### 連結環境定義

如果您要在連結環境定義中使用 {{site.data.keyword.objectstorageshort}}，雲端認證會間接透過應用程式連結程序來提供。在您順利將服務實例連結至應用程式之後，會在 `VCAP_SERVICES` 環境變數中新增一個類似於下列範例的配置。

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

## 使用 Swift CLI 來存取 {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

您可以透過網際網路及 IBM {{site.data.keyword.Bluemix_notm}} 內的應用程式和虛擬伺服器來存取 {{site.data.keyword.objectstorageshort}} 服務。{{site.data.keyword.objectstorageshort}} 服務的常見使用案例如下：

* 從您的實例備份磁區資料
* 用來作為傳送大量資料時的媒介位置
* 在未直接連接的環境之間傳送資料
* 充當中央儲存庫

{{site.data.keyword.objectstorageshort}} 服務是以 OpenStack Swift 為基礎，並且可以使用任何相容的用戶端應用程式加以存取。本節說明如何使用 Python Swift 用戶端（其為 {{site.data.keyword.objectstorageshort}} API 及其延伸的指令行介面 (CLI)）來處理容器及檔案。

### 安裝 Swift 用戶端 {: #install-swift-client}

安裝下列必備軟體（如果尚未安裝的話）。如需相關資訊，請參閱 [OpenStack 文件](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}。
* Python 2.7 或更新版本
* setuptools 套件
* pip 套件

使用 Python pip 來安裝 Python Swif 用戶端：

```
	sudo pip install python-swiftclient
```

執行下列指令安裝 Python Keystone 用戶端：

```
	sudo pip install python-keystoneclient
```

### 設定用戶端 {: #setup-swift-client}

Swift 用戶端從下列環境變數取得鑑別資訊：
* `OS_AUTH_URL` 是端點 URL
* `OS_USER_ID` 是使用者名稱
* `OS_PASSWORD` 是密碼

如下所示設定鑑別資訊。

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

您可以從 {{site.data.keyword.objectstorageshort}} 使用者介面的**服務認證**頁面中找到 {{site.data.keyword.objectstorageshort}} 服務的認證值。

**附註：**請確定當您為 Swift 用戶端配置環境變數 `OS_AUTH_URL` 時，已從 {{site.data.keyword.objectstorageshort}} 使用者介面的認證中，將 `/v3` 新增至 `auth_url`。


### 使用容器 {: #work-with-containers}

列出容器：
```
	swift list
```
建立容器：
```
	swift post <container_name>
```
列出容器的內容：
```
	swift list <container_name>
```
### 使用物件 {: #work-with-objects}

#### 將檔案新增至容器
```
	swift upload <container_name> <file_name>
```
#### 將大於 5 GB 的檔案新增至容器

如果您要上傳的檔案大於 5 GB，則必須將其分割為較小的片段。藉由提供 `-segment-size` 參數，即可指示 Swift 用戶端來處理這類上傳作業：
```
	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
每一個區段都會平行上傳到名為 `<container_name>_segments` 的個別容器。上傳所有區段之後，Swift 會建立資訊清單檔，讓這些區段可以從原始檔名為 `<file_name>` 的原始容器 `<container_name>` 中下載為單一檔案。例如，下列指令會從名為 `test_container` 的容器中上傳名為 `large_file` 的檔案，區段大小為 `1073741824`。
```
	swift upload test_container -S 1073741824 large_file
```
您可以執行下列指令來下載檔案：
```
	swift download test_container large_file
```
#### 下載檔案
```
	swift download <container_name> <file_name>
```
#### 將目錄新增至容器

Swift 沒有真正的目錄結構，但會使用命名來代表目錄階層。若要將目錄新增至容器，請執行下列指令：
```
	swift upload <container_name> <directory_name>
```
這個指令將上傳完整目錄結構作為相對路徑。例如，如果指定 `/mnt/volume1`，目錄結構 mnt/volume1 將會附加至所有檔名以指出該目錄結構。


#### 下載目錄

若要下載目錄結構，請使用 `-prefix` 參數來表示您要下載的目錄或目錄結構。
```
	swift download <container_name> --prefix <directory>
```
#### 刪除檔案
```
	swift delete <container_name> <file_name>
```
### 使用物件版本化 {: #work-with-object-versioning}

您可以使用 `X-Versions-Location` 旗標來設定容器中每個物件的版本。如果要這麼做，請另外建立一個容器，以存放舊版本的物件，如下所示。

如果您使用 swift 用戶端，您可以如下所示設定它：
```
	swift post container_one -H "X-Versions-Location:container_two"
```
如果您使用 curl，您可以如下所示設定它：
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
在範例中，`container_two` 已設定為包含您儲存在 `container_one` 的舊版本物件。因此，`container_one` 將具有最新版本的物件，而 `container_two` 將具有舊版本的物件。請確定 `container_two` 存在，版本化才能運作。設定版本化之後，當您上傳物件至 `container_one` 時，如果有該物件的現有版本，當新版本在 `container_one` 中建立時，現有版本會移至 `container_two`。如果您從 `container_one` 刪除物件，舊版物件會從 `container_two` 移回 `container_one`。

`container_two` 中的物件將自動使用下列格式命名：`<Length><Object_name>/<Timestamp>`。

`Length` 是指物件的名稱長度；這是 3 個字元並以零填補的十六進位數。`Object_name` 是物件的名稱。`Timestamp` 是物件的這個特定版本最初上傳時的時間戳記。

若要停用版本化，請使用 `X-Remove-Versions-Location` 旗標：
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
或
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
以下是版本化的完整使用範例：
1. 建立容器：
```
		$ swift post container_one
		$
```
2. 設定 container_one 的版本化：
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. 建立 container_two：
```
		$ swift post container_two
		$
```
4. 第一次將物件上傳到 container_one：
```
		$ swift upload container_one object
		object
		$
```
5. 列出 container_one 中的物件：
```
		$ swift list container_one
		object
		$
```
6. 列出 container_two 中的物件：
```
		$ swift list container_two
		$
```
7. 將物件的新版本上傳到 container_one：
```
		$ swift upload container_one object
		object
		$
```
8. 列出 container_one 中的物件：
```
		$ swift list container_one
		object
		$
```
9. 列出 container_two 中的物件：
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. 刪除 container_one 中的物件：
```
		$ swift delete container_one object
		object
		$
```
11. 列出這兩個容器：
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### 排定物件刪除 {: #schedule-object-deletion}

您可以設定物件，在給定的時間量內到期。換句話說，您可以排定物件刪除。若要這樣做，您可以利用 `X-Delete-At` 或 `X-Delete-After` 標頭。`X-Delete-At` 標頭會接受一個代表新紀元時間的整數，將會在該時間刪除物件。`X-Delete_After` 標頭會接受一個代表秒數的整數，在該秒數之後將會刪除物件。

如果您使用 swift 用戶端，請對容器中的物件進行 post，如下列範例所示。

* 若要設定將在 "2016/04/01 08:00:00" 刪除物件，請使用下列指令：
```
		swift post -H "X-Delete-At:1459515600" container object
```
* 若要設定將在現在起的一小時後刪除物件，請使用下列指令：
```
		swift post -H "X-Delete-After:3600" container object
```
  這樣做之後，`swift stat container object` 指令將以新紀元時間顯示 `X-Delete-At` 標頭與適當的有效期限。

* 若要移除物件的有效期限，請使用下列指令：
```
		swift post -H "X-Remove-Delete-After:" container object
```
如果您使用 cURL，則指令如下。

* 若要設定將在 "2016/04/01 08:00:00" 刪除物件，請使用下列指令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* 若要設定將在現在起的一小時後刪除物件，請使用下列指令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* 若要檢查物件是否有標頭，請使用下列指令：
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* 若要移除有效期限，請使用下列指令：
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**附註：**物件實際刪除可能不會按照指出的確切時間發生。然而，物件實際上會在指定的時間到期，也就是說，無法再呼叫到它。實際的刪除將在 swift 叢集中配置的 swift-object-expirer 常駐程式下次執行時發生。





### 建立暫時 URL {: #create-temporary-url}

暫時 URL 是一個很長、難以猜測的 URL，可用來在指定的時段下載物件，而無需進一步鑑別。請使用下列步驟產生暫時 URL：

1. 識別您的鑑別帳戶。
2. 設定秘密金鑰。
3. 建立暫時 URL。

#### 識別您的鑑別帳戶

Swift `stat` 指令可列印您帳戶的相關資訊：
```
	swift stat
```
找到「帳戶」欄位並記下*帳戶*：之後的完整字串，包括 `AUTH_`。

#### 設定秘密金鑰

此金鑰可以是您選取的任何項目，但最佳做法是選取一個很長、隨機且難以猜測的字串。
```
	swift post -m "Temp-URL-Key:<key>"
```
執行 Swift `stat` 指令，來驗證是否已順利設定 `Temp-URL-Key`。
```
	swift stat
```

#### 建立暫時 URL

Swift `tempurl` 指令採用下列位置引數：

* [method] GET 可容許下載。PUT 可容許上傳。
* [seconds] 暫時 URL 可供使用的時間（以秒為單位）。
* [path] 物件的完整路徑（以 `/v1/<auth_account>/<container_name>/<object_name>` 表示）。如需相關資訊，請參閱 [{{site.data.keyword.objectstorageshort}} URL](#access-points)。
* [key] 您在步驟 2 中設定的金鑰。

```
swift tempurl GET <seconds> <path> <key>
```

這個指令將傳回 URL，您可以將其附加至叢集名稱以取得完整 URL。請使用完整 URL 與任何相容的 HTTP 用戶端（例如 curl、wget 或 Firefox）搭配來下載物件。

## 使用 Swift REST API 來存取 {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

您可以搭配使用 Swift REST API 與指令行用戶端介面（例如 cURL），或是從應用程式中呼叫 API。  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

若要與 {{site.data.keyword.objectstorageshort}} API 進行互動，請如下所示建構 {{site.data.keyword.objectstorageshort}} URL：
```
	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
```


URL 包含五個部分。`<API version>` 為 v1。您可以從 {{site.data.keyword.objectstorageshort}} 使用者介面中找到 {{site.data.keyword.objectstorageshort}} 的 `<project ID>`、`<container namespace>` 及 `<object namespace>`。如需 `<access point>`，請參閱下表：


| **地區**    |   **公用存取點**                              |
|-------------|-----------------------------------------------|
| 達拉斯      | https://dal.objectstorage.open.softlayer.com/ |
| 倫敦        | https://lon.objectstorage.open.softlayer.com/ |


*表 1. {{site.data.keyword.objectstorageshort}} 存取點*


### {{site.data.keyword.objectstorageshort}} API

如需 {{site.data.keyword.objectstorageshort}} REST API 選項及範例的綜合性清單，請參閱 [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}。

## 跨多個地區使用 {{site.data.keyword.objectstorageshort}} {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服務支援達拉斯和倫敦儲存空間地區。這些儲存空間地區與在其中建立 {{site.data.keyword.objectstorageshort}} 服務實例的 {{site.data.keyword.Bluemix_notm}} 地區（例如美國南部及英國）無關。例如，如果在美國南部的 {{site.data.keyword.Bluemix_notm}} 地區中建立 {{site.data.keyword.objectstorageshort}} 實例，便可以在達拉斯或倫敦儲存空間地區中讀取及寫入資料。  

對於美國南部的 {{site.data.keyword.Bluemix_notm}} 地區，達拉斯儲存空間地區是預設值。對於英國的 {{site.data.keyword.Bluemix_notm}} 地區，倫敦儲存空間地區是預設值。{{site.data.keyword.objectstorageshort}} 使用者介面一律會啟動至 {{site.data.keyword.Bluemix_notm}} 地區的預設儲存空間地區。若要切換地區，請按一下「{{site.data.keyword.objectstorageshort}} 地區」下拉清單，然後選擇其他地區。

**附註：**{{site.data.keyword.objectstorageshort}} 服務不支援跨儲存空間地區抄寫。

### 多個地區存取

若要使用 {{site.data.keyword.objectstorageshort}} 服務，您必須[鑑別 OpenStack Keystone](#keystone-authentication)。順利鑑別之後，將在回應中提供 `X-Subject-Token` 及 {{site.data.keyword.objectstorageshort}} 端點。

例如，若要在達拉斯儲存空間地區建立名為 `my_container` 的容器，請在 curl 指令中指定達拉斯存取點，如下所示：
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

若要在倫敦儲存空間地區建立名為 `my_container` 的容器，請在 curl 指令中指定倫敦存取點，如下所示：
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**附註：**從 Keystone 獲得的 `X-Subject-Token` 適用於各個儲存空間地區。如需不同地區存取點的相關資訊，請參閱 [Object Storage 存取點](#access-points)表格。


## 瞭解鑑別及認證 {: #understanding-authentication-credentials}

### 產生 {{site.data.keyword.objectstorageshort}} 認證，而無需連結應用程式

若要產生用於 {{site.data.keyword.Bluemix_notm}} 應用程式外部的 {{site.data.keyword.objectstorageshort}} 雲端認證，您必須產生 {{site.data.keyword.objectstorageshort}} 實例的服務金鑰。您可以從使用者介面的資訊看板選取**服務認證**或使用 Cloud Foundry CLI（6.11.3 版或更新版本）來產生新的金鑰。在產生並擷取 {{site.data.keyword.objectstorageshort}} 實例的服務金鑰之後，您可以使用 Cloud Integration 資訊來要求 Keystone 記號，其作法是使用 OpenStack SDK 或 OpenStack Identity API，並開始使用 Swift 帳戶來管理物件。

若要利用 Cloud Foundry CLI 來建立金鑰，請登入並執行下列指令：
 ```
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>
```
若要從 Cloud Foundry CLI 中擷取服務認證，請執行下列指令：
```
	cf service-key <object_storage_instance_name> <unique_name_for_this_key>
```

### 雲端專案及使用者
佈建新的 {{site.data.keyword.objectstorageshort}} 實例會在 IBM Public Cloud 中建立隔離的 Keystone 專案。當您將新的應用程式連結至 {{site.data.keyword.objectstorageshort}} 實例時，會建立具有專案存取權的新 Keystone 使用者。當您取消佈建實例時，會刪除專案及使用者。

### OpenStack Identity (Keystone) 第 3 版 {: #keystone-authentication}
認證結構包含一組完整的屬性，可讓您選擇最符合您應用程式的 OpenStack 記號要求方法或 OpenStack SDK。

建議的第 3 版記號要求是 https://identity.open.softlayer.com/v3/auth/tokens 的 POST 要求，如下列 curl 指令中所示：
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
當您對 {{site.data.keyword.objectstorageshort}} 服務發出要求時，請使用回應標頭中 `X-Subject-Token` 欄位的值作為 `X-Auth-Token` 欄位。範例回應如下。回應會縮減為只顯示 {{site.data.keyword.objectstorageshort}} 相關資訊。

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
	    "extras" : {},
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

{{site.data.keyword.objectstorageshort}} URL 位在「服務型錄」中。「服務型錄」包含在記號要求的回應主體中。回應是可用的 OpenStack 服務的完整型錄。從「服務型錄」中選取類型為 `object-store` 的端點，以及符合認證中之地區欄位的地區。

**附註：**請使用公用介面（`publicURL`)。無法從 {{site.data.keyword.Bluemix_notm}} 存取內部介面 (`internalURL`)。



## 利用精細存取控制來保護檔案的安全 {: #fine-grained-access-control}

當您有多個使用者將檔案儲存在相同的容器中時，精細存取控制清單可協助保護檔案的安全。

附註：本文件中概述的程序需要 Swift CLI。如需相關資訊，請參閱[使用 {{site.data.keyword.objectstorageshort}} 與 Swift CLI 搭配](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli)。


### 存取類型 {: #access-types}

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

*表 1：定義的使用者角色*

您可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面、Cloud Foundry API 或 Cloud Foundry CLI 管理 {{site.data.keyword.objectstorageshort}} 使用者。



### 產生 {{site.data.keyword.objectstorageshort}} 服務認證 {: #generating}

從新的 {{site.data.keyword.Bluemix_notm}} 主控台中，您可以為 {{site.data.keyword.objectstorageshort}} 使用者產生新的服務認證。若要查看新的主控台，請按一下**嘗試新的 {{site.data.keyword.Bluemix_notm}}**。

1.  以具有開發人員角色的使用者身分登入 {{site.data.keyword.Bluemix_notm}}。您必須位在您要管理之服務實例的空間內。
2. 按一下**服務認證**標籤。
3. 按一下**新建認證**。
4. 提供認證的名稱。
5. 在**新增線型配置參數**文字欄位中，輸入您要建立之角色的認證資訊。資訊必須格式化為 JSON 有效負載。
  - 若要建立管理使用者：`{"role":"admin"}`
  - 若要建立非管理使用者：`{"role":"member"}`
5. 按一下**新增**。

若要使用 cURL 指令或 Swift CLI 產生服務認證，您可以使用下列步驟。

1. 以具有開發人員角色的使用者身分登入 {{site.data.keyword.Bluemix_notm}}。您必須位在您要管理之服務實例的空間內。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. 產生服務認證。`service-key-name` 將是認證的名稱。您可以使用 Cloud Foundry 指令或 cURL 指令。

  Cloud Foundry 指令：
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```

  範例：

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  cURL 指令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```

3. 驗證您已建立之「服務金鑰」的認證。

  Cloud Foundry 指令：
  ```
  cf service-key <service_key_name> <member_name>
  ```
  範例：
  為名為 Object-Storage-Acl-Test 的服務實例建立成員服務金鑰。
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
  cURL 指令：
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```



### 指派存取權 {: #assigning-access}  

只有具有管理者角色的 {{site.data.keyword.objectstorageshort}} 使用者，才能授與另一個使用者對容器的讀取權或寫入權。

若要在 CLI 授與讀取權，請使用 `--read-acl` 或 `-r` 選項。

1. 使用您所建立之服務認證中的資訊來鑑別您的認證。您會收到 Object Storage URL 及鑑別記號作為輸出。

  Swift 指令：
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
  cURL 指令：
  ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
3. 執行下列指令來授與讀取權：

  Swift 指令：
  ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. 驗證「讀取 ACL」值。

  Swift 指令：
  ```
  swift stat <container_name>
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  輸出範例：
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

您可以操作讀取 ACL 組合。

<table>
  <tr>
    <th> 許可權</th>
    <th> 讀取 ACL 選項</th>
  </tr>
  <tr>
    <td> 無論帳戶連結為何，所有參照者皆可讀取</td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> 所有參照者及清單皆可讀取及列出</td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以讀取及列出</td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以讀取及列出</td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可讀取及列出</td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可讀取及列出</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 2：依選項列出的讀取權*

附註：使用逗點 (,) 來區隔存取控制清單。例如，`-read-acl project id:user_id1, project_id2:user_id2`。


若要授與寫入權，請透過 Swift CLI 使用 `--write-acl` 或 `-w` 選項。

1. 使用您所建立之服務認證中的資訊來鑑別您的認證。您會收到 Object Storage URL 及鑑別記號作為輸出。

  Swift 指令：
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
  cURL 指令：
  ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
2. 執行下列指令來授與寫入權：

  Swift 指令：
  ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. 驗證寫入 ACL 值。

  Swift 指令：
  ```
  swift stat <container_name>
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


您可以操作寫入 ACL 組合。

<table>
  <tr>
    <th> 許可權</th>
    <th> 寫入 ACL 選項</th>
  </tr>
  <tr>
    <td> 特定專案中指定的使用者可以寫入</td>
    <td> `<project_id>:<user_id>` </td>
  </tr>
  <tr>
    <td> 每個專案中指定的使用者可以寫入</td>  
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> 指定專案中的每個使用者皆可寫入</td>
    <td> `<project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 每個專案中的每個使用者皆可寫入</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 3：依選項列出的寫入權*

附註：使用逗點 (,) 來區隔存取控制清單。例如，`-write-acl project id:user_id1, project_id2:user_id2`。




### 移除存取權 {: #removing-access}

若要從容器中移除讀取 ACL，請執行下列指令：

  Swift 指令：
  ```
  swift post <container_name> --read-acl ""
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

若要從容器中移除寫入 ACL，請執行下列指令：

  Swift 指令：
  ```
  swift post <container_name> --write-acl ""
  ```
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

若要驗證您已移除 ACL，請執行下列指令：

  Swift 指令：
  ```
  swift stat <container_name>
  ```

  輸出範例：
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
  cURL 指令：
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## 取消連結及取消佈建 {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### 如何取消佈建 {{site.data.keyword.objectstorageshort}} 服務
1.	從 {{site.data.keyword.Bluemix_notm}} 儀表板中選取您的服務。  
2.	按一下齒輪圖示，然後選取**刪除服務**。

**注意：**如果您取消佈建 IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} 服務實例，則會刪除雲端專案及 Swift 帳戶。已取消佈建實例中的所有容器及物件會從 Swift 中刪除，而且無法還原。

### 取消連結應用程式或刪除服務金鑰

如果您從 {{site.data.keyword.objectstorageshort}} 實例取消連結應用程式，或是刪除服務金鑰，則會刪除認證。在取消佈建 {{site.data.keyword.objectstorageshort}} 實例之前，不會刪除 {{site.data.keyword.objectstorageshort}} 帳戶。[重新連結或建立新的服務金鑰](#bind-object-storage-to-application)，即可產生新的雲端認證。
