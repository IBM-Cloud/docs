---

copyright:
  years: 2017
lastupdated: "2017-05-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 顯示來自 IBM UrbanCode Deploy 伺服器的資料
{: #connect_ucd}

若要在 Delivery Insights 中查看 IBM UrbanCode Deploy 伺服器中的資料，您必須設定 DevOps Connect 的實例、在伺服器上安裝修補程式，然後將該伺服器連接至 DevOps Connect。
{:shortdesc}

## 必要條件
{: #prereqs}

若要在 {{site.data.keyword.DRA_short}} 中查看 IBM UrbanCode Deploy 伺服器中的資訊，您必須在可以連接至 IBM UrbanCode Deploy 伺服器的系統上，管理 DevOps Connect 的實例。此系統可以是實體電腦或虛擬機器。
 

管理 DevOps Connect 的系統必須具備下列必要條件：
- 系統必須要有 Java Runtime Environment (JRE) 第 8 版或更新版本。
- 系統 `PATH` 變數必須包括 JRE 的位置。
- 系統必須容許 DevOps Connect 建立連往 IBM Bluemix 的送出連線。

此外，您的 IBM UrbanCode Deploy 伺服器必須是 6.2 版或更新版本。

## 配置 {{site.data.keyword.DRA_short}} 服務
{: #configure_service}

如果您沒有工具鏈或 {{site.data.keyword.DRA_short}}，則必須先設定 {{site.data.keyword.DRA_short}}：
1. 從 {{site.data.keyword.Bluemix}} 型錄中按一下 **{{site.data.keyword.DRA_short}}**、選取定價方案，然後按一下**建立**。
1. 按一下**管理**標籤，然後在**取得 UrbanCode 部署的見解**，按一下**從這裡開始**。Delivery Insights 會在背景中建立組織的工具鏈。工具鏈是工具整合的集合，在此情況下，IBM UrbanCode Deploy 和 {{site.data.keyword.DRA_short}} 是工具鏈的一部分。如需工具鏈的相關資訊，請參閱[使用工具鏈](../ContinuousDelivery/toolchains_working.html)。

如果您已經有工具鏈，請遵循下列步驟來新增 Delivery Insights：
1. 如果您還沒有 {{site.data.keyword.DRA_short}} 工具，請將它新增至工具鏈。
1. 在工具鏈上，按一下 {{site.data.keyword.DRA_short}} 工具。
1. 移至**設定 > Delivery Insights 設定**頁面。

現在您可以遵循 **Delivery Insights 設定**頁面上的指示，安裝 DevOps Connect 並將它連接至 {{site.data.keyword.DRA_short}}，如下一節所述。

## 安裝 DevOps Connect 並將它連接至 {{site.data.keyword.DRA_short}}
{: #install_connect}

1. 在 **Delivery Insights 設定**頁面中，遵循步驟來設定 DevOps Connect，並連接您的 IBM UrbanCode Deploy 伺服器。這些步驟包括：
{: #set_up_connect}
  1. 設定系統來執行 DevOps Connect，如[必要條件](uc_insights_connect_ucd.html#prereqs)中所述。
  1. 下載 DevOps Connect，這是以可執行的 JAR 檔提供。
  1. 從 **Delivery Insights 設定**頁面複製 Script 並執行它。這個指令會啟動 DevOps Connect，並且會有記號容許它連接至 {{site.data.keyword.Bluemix}} 上的組織。
  1. 將您的 IBM UrbanCode Deploy 伺服器連接至 DevOps Connect，如下一節所述。

## 將 IBM UrbanCode Deploy 伺服器連接至 DevOps Connect
{: #connect_ucd_to_connect}

1. 將修補程式安裝在 IBM UrbanCode Deploy 伺服器中。所有版本的 IBM UrbanCode Deploy 都需要修補程式，才能與 DevOps Connect 通訊。 
  1. 依照您的 IBM UrbanCode Deploy 版本，前往下列頁面下載正確的修補程式：[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. 將檔案解壓縮。其中包含一個以上您必須新增至伺服器的修補程式檔。

  1. 停止伺服器。請參閱[啟動及停止伺服器](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.install.doc/topics/run_server.html)。

  1. 將修補程式檔放在 <code><em>application_data</em>/patches</code> 資料夾中，其中 <code><em>application_data</em></code> 是伺服器應用程式資料的資料夾。在 Linux 上，預設應用程式資料的資料夾為 `/opt/ibm-ucd/server/appdata`，在 Windows 上，則為 `C:\Program Files\ibm-ucd\server\appdata`。在高可用性系統上，應用程式資料的資料夾一律在每一部伺服器都可以存取的共用網路磁碟機上。

  1. 選用項目：當伺服器停止時，若要提升從這部伺服器匯入資料的效能，請在資料庫上執行下列 SQL 指令：  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time);`  
  `create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);`  
  針對 `MyUCDDatabase`，請使用您的資料庫名稱。
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. 啟動伺服器。 

    **附註：**等待 IBM UrbanCode Deploy 伺服器啟動的時間可能會比平常久。如果伺服器最後未啟動，或是運作不正常，請刪除修補程式檔，然後重新啟動伺服器。修補程式檔不會永久影響伺服器。

1. 某些版本的 IBM UrbanCode Deploy 需要其他修補程式，才能讓伺服器連接至 DevOps Connect。如果您是使用 IBM UrbanCode Deploy 6.2 到 6.2.1.2 版，則必須在伺服器上安裝下列額外的修補程式：
  1. 下載修補程式：[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar)。
  1. 停止伺服器。
  1. 將修補程式檔放在 <code><em>application_data</em>/patches</code> 資料夾中。
  1. 啟動伺服器。

1. 建立 DevOps Connect 與 IBM UrbanCode Deploy 伺服器之間的整合：  

  **重要事項：**整合第一次執行時，DevOps Connect 會擷取過去 90 天的資料。如果您有大量部署資料，此程序可能需要很長的時間。若要擷取少於 90 天的資料，請參閱[疑難排解](uc_insights_connect_ucd.html#troubleshooting)。
  1. 在 IBM UrbanCode Deploy 中，建立鑑別記號。請參閱[記號](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.4/com.ibm.udeploy.admin.doc/topics/security_token.html)。
  1. 在 DevOps Connect 中，按一下**整合**，然後按一下**新增**。
  1. 指定整合的名稱和說明。DevOps Connect 的預設位置為 `https://hostname:8443/`，其中 `hostname` 是管理 DevOps Connect 之系統的主機名稱。
  1. 從**整合類型**清單中，選取 **IBM UrbanCode Deploy for Cloud 報告**。
  1. 在**伺服器 URI** 欄位中，輸入 IBM UrbanCode Deploy 伺服器的公用 URL，例如 `https://my_UCD.example.com:8447`。
  1. 在**鑑別記號**欄位中，輸入或貼上 IBM UrbanCode Deploy 所產生的鑑別記號。
  1. 在**管理使用者**欄位中，輸入以逗點區隔的 IBM ID 清單，以提供對 DevOps Connect 介面的存取權。
  1. 選用項目：按一下**執行整合**，以立即執行整合。依預設，整合每分鐘執行一次。
  1. 按一下**儲存**。

  ![在 DevOps Connect 中設定整合](images/uc_insights_dc_integration.gif)

現在您的資料已與 Delivery Insights 同步。您現在可以建立及檢視以此資料為基礎的報告。接下來，將 IBM UrbanCode Deploy 伺服器上的環境對映至 Delivery Insights 中的邏輯環境。

## 將環境對映至報告
{: #mapping}

### 邏輯環境

Delivery Insights 會將您的 IBM UrbanCode Deploy 環境（也稱為*實體環境*）分組成一個以上的邏輯環境。如此，您就可以將環境收集至對您和組織有意義的群組中。例如，如果您有用於多個應用程式的多個正式作業環境，您可以將所有這些環境分組在單一邏輯環境中，並將所有這些環境的度量值結合在單一正式作業環境儀表板中。對映是透過搜尋字串來進行，因此您可以用對 IBM UrbanCode Deploy 伺服器有意義的任何方式來對環境進行分組。

### 預設邏輯環境

依預設，您的報告包括使用字串來比對 IBM UrbanCode Deploy 環境的邏輯環境。例如，名稱中有 "dev" 的所有環境都會對映至 DEV 邏輯環境，而名稱中有 "prod" 的所有環境都會對映至 PROD 邏輯環境。

![預設邏輯環境](images/uc_insights_mapping.gif)

### 將環境對映至邏輯環境

您可以手動將實體環境對映至邏輯環境，或者您可以使用型樣，以動態方式建立實體環境與邏輯環境的關聯。

若要使用型樣將實體環境對映至邏輯環境，請遵循下列步驟：

1. 在 {{site.data.keyword.DRA_short}} 中，按一下 **Delivery Insights > 對映環境**。
1. 按一下現有邏輯環境，或按一下**新增邏輯環境**。
1. 在邏輯環境的設定中，按一下**型樣**下的**新增型樣**。
1. 指定環境名稱的型樣。您可以使用星號 (*) 作為萬用字元。例如，型樣 `env*` 符合環境 `env1`、`env2` 及 `env`。
1. 確認邏輯環境包含您想要的環境。

若要手動將環境對映至邏輯環境，請按一下**手動新增**，然後選取要新增或移除的環境。

![在 DevOps Connect 中設定整合](images/uc_insights_mapping_manually.gif)

現在您已經將環境對映至邏輯環境，您可以依據那些邏輯環境來聚集報告資訊。

## 建立報告

若要建立報告，請開啟 {{site.data.keyword.DRA_short}}、按一下 **Delivery Insights > 報告**，然後按一下**新增報告**。 

您可以從報告中，將卡片新增至**度量值**區段、過濾**最近的應用程式活動**下的活動，以及將圖表新增至**報告詳細資料**區段。**報告詳細資料**區段中的每一個圖表都可個別過濾及自訂。若要查看圖表背後的原始資料，請按一下圖表右上方的圖表「設定」按鈕，然後按一下**報告資料**。

若要變更圖表順序，請按一下頁面右上方的「設定」按鈕，然後按一下**編輯圖表佈置**。然後，您就可以在報告上拖放圖表來設定順序。

## 共用報告
依預設，只有您自己可以看到您的 Delivery Insights 報告。您可以將報告與 Bluemix 組織內的其他使用者共用。若要與 Bluemix 組織的內部人員共用報告，請開啟報告，按一下報告右上方的「設定」按鈕，然後再按一下**共用**。  

![共用報告](images/uc_insights_sharing.gif)。

## 建立審核報告

審核報告會以 PDF 格式顯示符合您設定之過濾器的所有活動完整清單。若要建立審核報告，請按一下 **Delivery Insights > 建立審核報告**。然後，指定報告的資訊，包括名稱。此外，也要設定報告的環境定義，例如針對應用程式、邏輯環境，或是 IBM UrbanCode Deploy 伺服器上的環境（一種實體環境）。從這裡選取要顯示在報告中的資料，然後按一下**建立**。 

## 疑難排解
{: #troubleshooting}

如果有很多應用程式和元件處理程序要求儲存在 IBM UrbanCode Deploy 伺服器資料庫中，在擷取程序期間可能會發生錯誤。伺服器輸出日誌中記錄類似於下列文字的訊息：

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

若要暫行解決此行為，請編輯外掛程式的 `plugin.properties` 檔案，以減少要擷取資料的天數。`plugin.properties` 檔案位於 DevOps Connect 安裝所在電腦上的 `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` 目錄中。請編輯下列這一行來移除 # 記號，並減少天數：

`#numDaysToRetrieve=90`

例如，將該行變更為下列文字，只擷取前 30 天的資料：

`numDaysToRetrieve=30`

儲存檔案，然後重新執行整合。檢查伺服器日誌，確定該錯誤不再發生。
