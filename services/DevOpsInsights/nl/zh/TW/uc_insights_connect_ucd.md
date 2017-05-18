---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 將 IBM UrbanCode Deploy 伺服器連接至 Delivery Insights
{: #connect_ucd}

若要在 Delivery Insights 中查看 IBM UrbanCode Deploy 伺服器中的資料，您必須在伺服器上安裝修補程式，然後將該伺服器連接至 DevOps Connect。
{:shortdesc}

## 開始之前

- 請參閱[必要條件](uc_insights_prereqs.html)，包括設定 DevOps Connect 的實例。
- 您的 IBM UrbanCode Deploy 伺服器必須是 6.2 版或更新版本。

## 程序

1. 將修補程式安裝在 IBM UrbanCode Deploy 伺服器中。所有版本的 IBM UrbanCode Deploy 都需要修補程式，才能與 DevOps Connect 通訊。 
  1. 依照您的 IBM UrbanCode Deploy 版本，前往下列頁面下載正確的修補程式：[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. 將檔案解壓縮。其中包含一個以上您必須新增至伺服器的修補程式檔。

  1. 停止伺服器。請參閱[啟動及停止伺服器](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html)。

  1. 將修補程式檔放在 <code><em>application_data</em>/patches</code> 資料夾中，其中 <code><em>application_data</em></code> 是伺服器應用程式資料的資料夾。在 Linux 上，預設應用程式資料的資料夾為 `/opt/ibm-ucd/server/appdata`，在 Windows 上，則為 `C:\Program Files\ibm-ucd\server\appdata`。在高可用性系統上，應用程式資料的資料夾一律在每一部伺服器都可以存取的共用網路磁碟機上。

  1. 選用項目：當伺服器停止時，若要增加從這部伺服器匯入資料的效能，請在資料庫上執行下列 SQL 指令：  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  針對 `MyUCDDatabase`，請使用您的資料庫名稱。
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. 啟動伺服器。 

    **附註：**等待 IBM UrbanCode Deploy 伺服器啟動的時間可能會比平常久。如果伺服器最後未啟動，或是運作不正常，請刪除修補程式檔，並重新啟動伺服器。修補程式檔不會永久影響伺服器。

1. 某些版本的 IBM UrbanCode Deploy 需要其他修補程式，才能讓伺服器連接至 DevOps Connect。如果您是使用 IBM UrbanCode Deploy 6.2 到 6.2.1.2 版，則必須在伺服器上安裝下列其他修補程式：
  1. 下載修補程式：[http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar)。
  1. 停止伺服器。
  1. 將修補程式檔放在 <code><em>application_data</em>/patches</code> 資料夾中。
  1. 啟動伺服器。

1. 建立 DevOps Connect 與 IBM UrbanCode Deploy 伺服器之間的整合：  
  **重要事項：**整合第一次執行時，DevOps Connect 會擷取過去 90 天的資料。如果您有大量部署資料，此程序可能需要很長的時間。若要擷取少於 90 天的資料，請參閱[疑難排解](uc_insights_connect_ucd.html#troubleshooting)。
  1. 在 IBM UrbanCode Deploy 中，建立鑑別記號。請參閱[記號](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html)。
  1. 在 DevOps Connect 中，按一下**整合**，然後按一下**新增**。
  1. 指定整合的名稱和說明。DevOps Connect 的預設位置為 `https://hostname:8443/`，其中 `hostname` 是管理 DevOps Connect 之系統的主機名稱。
  1. 從**整合類型**清單中，選取 **IBM UrbanCode Deploy for Cloud 報告**。
  1. 在**伺服器 URI** 欄位中，輸入 IBM UrbanCode Deploy 伺服器的公用 URL，例如 `https://my_UCD.example.com:8447`。
  1. 在**鑑別記號**欄位中，輸入或貼上 IBM UrbanCode Deploy 所產生的鑑別記號。
  1. 在**管理使用者**欄位中，輸入以逗點區隔的 IBM ID 清單，以提供對 DevOps Connect 介面的存取權。
  1. 選用項目：按一下**執行整合**，以立即執行整合。依預設，整合每分鐘執行一次。
  1. 按一下**儲存**。

  ![在 DevOps Connect 中設定整合](images/uc_insights_dc_integration.gif)

現在您的資料已與 Delivery Insights 同步。您現在可以建立及檢視以此資料為基礎的報告。

## 疑難排解
{: #troubleshooting}

如果有很多應用程式和元件處理程序要求儲存在 IBM UrbanCode Deploy 伺服器資料庫中，在擷取程序期間可能會發生錯誤。伺服器輸出日誌中記錄類似於下列文字的訊息：

`ORA-01652: unable to extend temp segment by 128 in tablespace TEMP`

若要暫行解決此行為，請編輯外掛程式的 `plugin.properties` 檔案，以減少要擷取資料的天數。`plugin.properties` 檔案位於 DevOps Connect 安裝所在電腦上的 `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` 目錄中。請編輯下列這一行來移除 # 記號，並減少天數：

`#numDaysToRetrieve=90`

例如，將該行變更為下列文字，只擷取前 30 天的資料：

`numDaysToRetrieve=30`

儲存檔案，然後重新執行整合。檢查伺服器日誌，確定該錯誤不再發生。
