---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 更新應用程式
{: #updatingapps}


您可以使用 cf push 指令或 {{site.data.keyword.Bluemix}} DevOps Services，來更新 {{site.data.keyword.Bluemix_notm}} 中的應用程式。在許多情況下，即使是內建建置套件（例如 Node.js），您還是必須提供 -c 參數來指定用來啟動應用程式的指令。
{:shortdesc}

## 建立及使用自訂網域
{: #domain}

對於 CF 應用程式及容器群組，您可以在應用程式的 URL 中使用自訂網域，而不使用預設的 {{site.data.keyword.Bluemix_notm}} 系統網域（即 mybluemix.net）。

網域提供在 {{site.data.keyword.Bluemix_notm}} 中配置給組織的 URL 路徑。若要使用自訂網域，必須在公用 DNS 伺服器上登錄自訂網域，在 {{site.data.keyword.Bluemix_notm}} 中配置自訂網域，然後將自訂網域對映至公用 DNS 伺服器上的 {{site.data.keyword.Bluemix_notm}} 系統網域。將自訂網域對映至 {{site.data.keyword.Bluemix_notm}} 系統網域之後，該自訂網域的要求即會遞送至 {{site.data.keyword.Bluemix_notm}} 中的應用程式。

您可以使用 {{site.data.keyword.Bluemix_notm}} 使用者介面或 cf 指令行介面，在 {{site.data.keyword.Bluemix_notm}} 中建立及使用自訂網域。

* 使用 {{site.data.keyword.Bluemix_notm}} 使用者介面：

  1. 建立組織的自訂網域。

	1. 移至**管理** &gt; **帳戶** &gt; **組織** &gt; **檢視詳細資料**（針對您的組織）。然後，按一下**編輯組織** &gt; **網域**。

	2. 在**網域**標籤上，按一下**新增網域**，輸入自訂網域名稱，然後按一下**儲存**。

	**附註**：例如，您可以使用 `mycompany.com` 來建立路徑 `www.mycompany.com` 與您應用程式的關聯。您也可以使用 `example.mycompany.com` 來建立路徑 `www.example.mycompany.com` 與您應用程式的關聯。

  2. 新增含有自訂網域的路徑至應用程式。

    1. 按一下**功能表**圖示 ![「功能表」圖示](../icons/icon_hamburger.svg) &gt; **儀表板**，然後按一下您要新增路徑的應用程式列。即會顯示**概觀**頁面。

	2. 從**路徑**功能表中，選取**編輯路徑**。

	3. 按一下**新增路徑**，然後指定您要用於應用程式的路徑。
	4. 按一下**儲存**。

* 使用 cf 指令行介面：

  1. 鍵入下列指令以建立組織的自訂網域：

    ```
cf create-domain <your org name> mydomain
    ```

    *organization_name*

        組織的名稱。

    *mydomain*

        您要使用的自訂網域名稱。

  2. 新增含有自訂網域的路徑至應用程式。若為 CF 應用程式，請鍵入下列指令：

    ```
cf map-route myapp mydomain -n host_name
    ```
    若為容器群組，請鍵入下列指令：
     ```
     cf ic route map -n host_name -d mydomain mycontainergroup
     ```
    *myapp*

    	若為 CF 應用程式，則是應用程式的名稱。

    *mydomain*

    	自訂網域的名稱，例如 `www.mydomain.mybluemix.net`。

    *host_name*

        您要用於應用程式的路徑中的主機名稱。

    *mycontainergroup*

        若為容器群組，則是容器群組的名稱。


在 {{site.data.keyword.Bluemix_notm}} 中配置自訂網域之後，您必須將自訂網域對映至已登錄 DNS 伺服器上的 {{site.data.keyword.Bluemix_notm}} 系統網域：

  1. 在 DNS 伺服器上，設定自訂網域名稱的 'CNAME' 記錄。視您的 DNS 提供者而定，設定 CNAME 記錄的步驟有所不同。例如，如果您是使用 GoDaddy，請遵循 GoDaddy 的[網域說明 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://www.godaddy.com/help/add-a-cname-record-19236){: new_window} 指引。
  2. 將自訂網域名稱對映至應用程式執行所在的 {{site.data.keyword.Bluemix_notm}} 地區的安全端點。使用下列地區端點，提供在 {{site.data.keyword.Bluemix_notm}} 中配置給組織的 URL 路徑：

    * US-SOUTH：`secure.us-south.bluemix.net`
    * EU-GB：`secure.eu-gb.bluemix.net`
    * AU-SYD：`secure.au-syd.bluemix.net`
    * EU-DE：`secure.eu-de.bluemix.net`

在瀏覽器或指令行介面中，輸入下列 URL 以存取 myapp 應用程式：

```
http://host_name.mydomain
```

**附註：**若要移除遺留的路徑，請使用下列指令：

```
cf delete-route domain -n hostname -f
```

*domain* 是網域名稱，而 *hostname* 是應用程式路徑的主機名稱。如需 **cf delete-route** 指令的相關資訊，請鍵入 `cf delete-route -h`。

##藍綠部署
{: #blue_green}

{{site.data.keyword.Bluemix_notm}} 支援使用藍綠部署技術來啟用持續交付並使中斷時間事件減到最少。

*藍綠部署* 是一種零中斷時間的部署技術，由兩個幾乎相同的正式作業環境（稱為 Blue 及 Green）組成。它們的差別在於開發人員有意變更的構件，通常是應用程式的版本。在任何給定時間，至少會有一個環境是作用中。使用藍綠部署技術，可以有下列好處：

* 快速地讓軟體從測試的最終階段進入實際正式作業。
* 部署新版本的應用程式時不會中斷應用程式的資料流量。
* 快速回復。如果其中一個環境有問題，您可以快速切換至其他環境。

如果已經將應用程式部署至 {{site.data.keyword.Bluemix_notm}}，且想要將應用程式更新成新版本，您可以使用下列兩種方法其中之一來確保藍綠部署。

### 範例：使用 cf rename 指令

在此範例中，應用程式的名稱為 Blue。此範例示範如何使用 **cf rename** 指令來更新 *Blue* 的版本，而不用中斷應用程式的資料流量。更新版本安裝完成時，即可選擇性地刪除舊版的 *Blue*。

1. 將 *Blue* 應用程式推送至 {{site.data.keyword.Bluemix_notm}}。

  ```
cf push Blue
  ```

  **結果：** *Blue* 應用程式執行中，且正在回應 URL `Blue.mybluemix.net`。

2. 使用 **cf rename** 指令，將 *Blue* 應用程式重新命名為 *Green*：

  ```
cf rename Blue Green
  ```

  使用 **cf apps** 指令，列出現行空間中的應用程式：

  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```

  **結果：** *Green* 應用程式執行中，且正在回應 URL `Blue.mybluemix.net`。

3. 進行必要變更，並備妥已更新的 *Blue* 版本。將已更新的 *Blue* 應用程式推送至 {{site.data.keyword.Bluemix_notm}}：

  ```
cf push Blue
  ```

  使用 **cf apps** 指令，列出現行空間中的應用程式：

  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```

  **結果：**
    * 已部署兩個應用程式實例：*Blue* 及 *Green*。
	* 該 *Green* 應用程式執行中，且正在回應 URL `Blue.mybluemix.net`。

4. 選用項目：如果您要刪除舊版 (*Green*) 的應用程式，請使用 **cf delete** 指令。

  ```
cf delete Green -f
  ```

  使用 **cf route** 指令，列出空間中的路徑：

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```

  **結果：** *Blue* 應用程式正在回應 URL `Blue.mybluemix.net`。

### 範例：使用 cf map-route 指令

在此範例中，*Blue* 是先前部署的應用程式，而 *Green* 是更新後的版本。此範例示範如何使用 **cf map-route** 指令更新 *Blue* 的版本，而不用中斷應用程式的資料流量。更新版本安裝完成時，即可選擇性地刪除舊版的 *Blue*。

1. 將 *Blue* 應用程式推送至 {{site.data.keyword.Bluemix_notm}}。

  ```
cf push Blue
  ```

  **結果：** *Blue* 應用程式執行中，且正在回應 URL `Blue.mybluemix.net`。

2. 進行必要變更，並備妥 *Green* 版本。將 *Green* 應用程式推送至 {{site.data.keyword.Bluemix_notm}}：

  ```
cf push Green
  ```

  使用 **cf route** 指令，列出現行空間中的應用程式：

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```

  **結果：**

    * 已部署兩個應用程式實例：*Blue* 及 *Green*。
	* 該 *Blue* 應用程式正在回應 URL `Blue.mybluemix.net`。且 *Green* 應用程式正在回應 URL `Green.mybluemix.net`。

3. 將 *Blue* 應用程式對映至 *Green* 應用程式，讓 `Blue.mybluemix.net` 的所有資料流量同時遞送至 *Blue* 應用程式及 *Green* 應用程式。

  ```
cf map-route Green mybluemix.net -n Blue
  ```

  使用 cf routes 指令，列出空間中的路徑：

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```

  **結果：**

    * 「CF 路由器」現在會將 Blue.mybluemix.net 的資料流量同時傳送給 Blue 應用程式及 Green 應用程式。
	* 「CF 路由器」會繼續將 Green.mybluemix.net 的資料流量傳送給 Green 應用程式。

4. 驗證 *Green* 如預期執行時，請從 *Blue* 應用程式移除 `Blue.mybluemix.net` 路徑：

  ```
cf unmap-route Blue mybluemix.net -n Blue
  ```

  使用 cf routes 指令，列出空間中的路徑：

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```

  **結果：**「CF 路由器」停止將資料流量傳送至 *Blue* 應用程式。*Green* 應用程式正在同時回應 URL：`Green.mybluemix.net` 及 `Blue.mybluemix.net`。

5. 移除 *Green* 應用程式的 `Green.mybluemix.net` 路徑。

  ```
cf unmap-route Green mybluemix.net -n Green
  ```

  **結果：**「CF 路由器」停止將資料流量傳送至 *Blue* 應用程式。*Green* 應用程式正在回應 URL `Blue.mybluemix.net`。

6. 選用項目：如果您要刪除舊版 (*Blue*) 的應用程式，請使用 `cf delete` 指令。

  ```
cf delete Blue -f
  ```

  使用 cf route 指令，列出空間中的路徑：

  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```

  **結果：** *Green* 應用程式正在回應 URL `Blue.mybluemix.net`。


# 相關鏈結
{: #rellinks notoc}

## 相關鏈結
{: #general}

* [BlueGreenDeployment ![外部鏈結圖示](../icons/launch-glyph.svg)](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services ![外部鏈結圖示](../icons/launch-glyph.svg)](https://hub.jazz.net/){:new_window}
