---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# 開始使用 Git 撰寫程式碼
*前次更新：2016 年 3 月 2 日*  

您可以建立自動部署至 {{site.data.keyword.Bluemix}} 的受管理 Git 儲存庫。然後，您可以將變更推送至 Git 儲存庫，以修改在應用程式中執行的程式碼。
{:shortdesc}

1. 若要開始使用，請在應用程式的「概觀」頁面上按一下**新增 Git 儲存庫及管線**，或在「{{site.data.keyword.Bluemix_notm}} 一般經驗」中按一下**新增 GIT**。 
2. 在開啟的視窗中，確定已選取**將入門範本應用程式套件移入儲存庫並啟用「建置並部署」管線**勾選框。隨即建立 Git 儲存庫。如果有入門範本程式碼，就會將其載入儲存庫中。此外，在 {{site.data.keyword.jazzhub}} 中執行的 Delivery Pipeline 服務也會部署應用程式。  
3. 若要更新應用程式，您可以使用指令行或 Web IDE。
   **如果您使用指令行：**
   a. 在應用程式的「概觀」頁面上，從 Git URL 複製 Git 儲存庫。
   b. 在您偏好的編輯器中更新程式碼。
   c. 從 Git 指令行介面中，推送變更。  
	    
   **如果您使用 Web IDE：**  
   a. 在應用程式的「概觀」頁面上，按一下**編輯程式碼**。您的專案就會在 Web IDE 中開啟。  
   b. 視需要進行變更，然後使用內建 Git 支援來推送。  
		
已更新的應用程式即會重新部署至 {{site.data.keyword.Bluemix_notm}}。  

如需逐步指示，請參閱 [Set up Git integration and auto-deploy in DevOps Services](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment)。  

## 已新增 Git？請試用 {{site.data.keyword.Bluemix_notm}} Live Sync  

如果您要建置 Node.js 應用程式，可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync 來快速更新 {{site.data.keyword.Bluemix_notm}} 上的應用程式實例，並如同在桌面上一樣進行開發。  

若要進一步瞭解 {{site.data.keyword.Bluemix_notm}} Live Sync，請參閱 [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html)。如需指令的詳細資料，請參閱 [{{site.data.keyword.Bluemix_notm}} Live Sync CLI 文件](../cli/reference/bl/index.html)。若要使用 {{site.data.keyword.Bluemix_notm}} Live Sync 來搭配 Web IDE，請參閱[即時編輯](../develop/bluemixlive.html)。  

1. 下載並安裝 {{site.data.keyword.Bluemix_notm}} Live Sync bl 指令行。 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="下載 Windows bl 指令行按鈕" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="（在新分頁或視窗中開啟）"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="下載 Mac bl 指令行按鈕" /> </a>
</p>

**重要事項：**bl 指令行工具僅適用於 Windows 7 和 8，以及 Mac OS X 10.9 版或更新版本。 

2. 在指令行上，使用下列指令登入。系統會提示您輸入 IBM® ID 及密碼。
```
bl login
```

3. 輸入下列指令，以查看可用於 {{site.data.keyword.Bluemix_notm}} Live Sync 同步化的專案清單：
```
bl projects
```
在清單中尋找符合您應用程式的專案名稱。專案名稱的格式為 *your alias* | *your application name*。 

4. 輸入下列指令，將您的本端環境與您在 {{site.data.keyword.Bluemix_notm}} 上的專案同步化。如果您是專案的擁有者，只需要指定 your-application-name 作為 projectName。 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
此指令會繼續執行（而且同步化也會繼續進行），直到您輸入 "q" 為止。--verbose 選項會顯示記載及狀態資訊。如果有任何引數包含空格，則必須將名稱含括在引號中。

5. 使用另一個指令行視窗，在本端目錄中輸入下列指令，以在「即時編輯」模式下，將應用程式部署至 {{site.data.keyword.Bluemix_notm}}：
```
bl start
```  

當您變更本端目錄中的檔案時，變更會自動延伸到 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式，以及專案雲端工作區。如果您需要重新啟動 Node 應用程式，可以使用下列指令：
```
bl start --restart 
```
