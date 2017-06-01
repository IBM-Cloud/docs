---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#系統存取
{: #system_access}


本節討論建立及管理服務實例的方法，以及如何存取系統以及如何設定存取系統的多種方法。
{: shortdesc}


## WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的 REST API 使用
{: #restapi_usage}

WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 中的實例會以下列其中一種方式建立、佈建、管理和刪除：

* 從 {{site.data.keyword.Bluemix_notm}} 使用者介面的 {{site.data.keyword.Bluemix_notm}}「型錄」及「服務儀表板」。
* 藉由建立使用 RESTful API 的應用程式或 Script。

透過使用遵循 Swagger 2.0 的 REST API，客戶能夠存取與透過入口網站和儀表板所提供功能的相同功能。如需所支援 REST API 及資源的相關資訊，請參閱 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 文件](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api#/){: new_window}。如需示範 REST API 用法的範例程式碼，請下載由 Git 管理的 WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} [REST API 範例](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}。

**附註：**建立服務實例之後，根據所建立的 T 恤尺碼，您的服務可能無法立即供使用。建議您查詢所傳回 JSON 的**狀態**欄位，以判斷服務實例的現行狀態。

**附註：**[REST API 範例](https://github.com/IBM-Bluemix/WebSphere-for-Bluemix-API-Usage){: new_window}中所參照的 **apiEndpoint** URL 指向「美國南部地區」。如果您是使用其他地區，請確定您的應用程式參照適當的 **apiEndpoint**。

*表 1. Rest API 的 API 端點 URL 實作*

| **地區名稱** | **地理位置** | **地區字首** | **API 端點 URL** |       
|:-------------:|:----------:|:--------------:|:-------------:|
| 美國南部 | 美國德州達拉斯 | ng | https://wasaas-broker.ng.bluemix.net/wasaas-broker/api  |
| 英國 | 英國倫敦 | eu-gb | https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api  |
| 雪梨 | 澳洲雪梨 | au-syd | https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api  |
| 法蘭克福 | 德國法蘭克福 | eu-de | https://wasaas-broker.eu-de.bluemix.net/wasaas-broker/api  |



## 服務儀表板
{: #service_dashboard}

在您建立服務實例之後，即會將您帶至服務儀表板。按一下組織儀表板中的「服務」圖示，一律可以回到服務儀表板。從服務儀表板，您可以存取：

* 此文件的鏈結
* 下載必要 OpenVPN 配置檔的鏈結
* 啟動和停止虛擬機器的能力。一開始會啟動 VM
* 主機名稱
* 管理使用者及管理密碼
* 專用 SSH 金鑰
* WebSphere® 管理使用者及管理密碼
* 「管理中心」及「管理主控台」URL

**附註**：由於特定量的運算、記憶體和 I/O 資源，客戶會因為處理停止狀態的累計 VM，被收取減價 5% 的費用。客戶會被控制在固定數量的已停止實例，最多不超過 10 個 IP 位址或 64 GB 的記憶體。


## 為 WebSphere Application Server in Bluemix 實例設定 openVPN
{: #setup_openvpn}

需要有 OpenVPN，才能存取任何 WebSphere Application Server in Bluemix 虛擬機器。必須使用管理者專用權來安裝及執行它。

### 使用下列指示，在 Windows 中設定 openVPN：

1. 從 [openVPN Windows 下載](http://swupdate.openvpn.org/community/releases/)鏈結，下載
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window}（適用於 64 位元），或
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}（適用於 32 位元）。
2. 確定您[以 Windows 管理者身分執行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}且已安裝 openVPN。
3. 在服務儀表板中，從 WebSphere Application Server in Bluemix 實例的 OpenVPN 下載鏈結下載 VPN 配置檔。將壓縮檔中的全部 4 個檔案解壓縮至 **{OpenVPN home}\config** 目錄。例如：

  <pre>  
C:\Program Files\OpenVPN\Config  </pre>
  {: codeblock}

4. 啟動 openVPN 用戶端程式 "OpenVPN GUI"。確保選取[以 Windows 管理者身分執行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}來啟動程式。如果您沒有這麼做，則可能無法進行連接。

### 使用下列指示，在 Linux 中設定 openVPN：
1. 若要安裝 openVPN，請遵循[指示](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}。
  * 如果您需要手動下載及安裝 RPM 套件管理程式，請前往 [openVPN unix/linux 下載](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}。您可能需要 Linux 管理者的協助。
3. 在服務儀表板中，從 WebSphere Application Server in Bluemix 實例的 OpenVPN 下載鏈結下載 VPN 配置檔。請將檔案解壓縮至您要從中啟動 openVPN 用戶端的目錄。您需要相同目錄中的所有四個檔案。
3. 啟動 openVPN 用戶端程式。開啟終端機視窗，並移至包含配置檔案的目錄。以 root 身分執行下列指令：

  <pre>
$ openvpn --config vt-wasaas-wasaas.ovpn  </pre>
  {: codeblock}  

### 使用下列指示，在 Mac 中設定 openVPN：
1. 一種方法是安裝 [Tunnelblick](https://tunnelblick.net/){: new_window}（開放程式碼軟體產品）。
2. 從 WebSphere 服務解壓縮 VPN 配置檔。Tunnelblick 會提示您針對 Mac 輸入管理者密碼，以及將配置新增至您可用來連接的那組 VPN。
3. 連接至 VPN 網路，然後可以存取虛擬機器。在第一次存取後，Tunnelblick 會快取配置，並且您可以從 [Tunnelblick](https://tunnelblick.net/){: new_window} 連接。您可以將圖示放在頂端功能表列上，以方便進行存取。


## 使用 SSH 存取 WebSphere Application Server in Bluemix VM
{: #using_ssh}

這些指示假設您是使用 OpenSSH 作為用戶端。OpenSSH 通常適用於 Linux，也適用於在 Windows 上執行的 Cygwin。您還可以安裝 OpenSSH，以從 Windows 命令提示字元執行。

若要驗證 OpenSSH 的安裝，請輸入以下指令：
  
  ```
$ ssh -V
  ```
  {: codeblock}

下列訊息是回應的範例：
  ```
OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

使用下列指示，設定 WebSphere Application Server in Bluemix VM 的 SSH 存取權：

1. 在您第一次連接時檢閱出現的警告訊息「無法確定主機 x.x.x.x 的真實性」。這是正常訊息。系統提示時，請選取 yes。現在會在 VM 上為使用者 virtuser 安裝公開金鑰。
2. 使用私密金鑰登入 virtuser。為獲取最佳結果，請使用私密金鑰鑑別方法。
3. 將私密金鑰內容複製至檔案。
4. 執行以下指令：

  <pre>
$ ssh virtuser@169.53.246.xxx -i /path/privateKeyFileName  </pre>
  {: codeblock}

5. 使用以下指令，將 virtuser 切換為 root 使用者，以獲取完整的 sysadmin 權限：

  <pre>
$ sudo su root  </pre>
  {: codeblock}

6. 如果您在使用專用 SSH 金鑰存取系統時遇到問題，請使用提供的 root 密碼。執行以下指令，以 root 身分登入，並提供密碼。

 <pre>
$ ssh root@169.53.246.x  </pre>
  {: codeblock}

7. 不論使用私密 ssh 金鑰還是 root 密碼來存取系統，都請立即變更 root 密碼。
8. 要簡化 SSH 指令，請在 %HOME%/.ssh 目錄中建立名為 "config" 的檔案。例如：

  <pre>
   Host VM1
Hostname 169.53.246.xxx
User virtuser
IdentityFile /path/privateKeyFileName  </pre>
  {: codeblock}

9. 執行 "ssh VM1"，以 virtuser 進行連接。

## 系統路徑
{: #system_paths}

* 可以從 */opt/IBM/WebSphere/Liberty/bin* 發出 Liberty Profile 指令。
* Liberty Profile 伺服器設定檔位置是 */opt/IBM/WebSphere/Profiles/Liberty/servers/server1*。
* 可以從 */opt/IBM/WebSphere/AppServer/bin* 發出傳統 WebSphere Application Server 指令。
* 伺服器的傳統 WebSphere Application Server 設定檔位置是 */opt/IBM/WebSphere/Profiles/DefaultAppSrv01/servers/server1*。

## 使用管理中心及管理主控台鏈結
{: #console_links}

當您按一下「管理中心」或「管理主控台」的鏈結時，可能會收到*未授信的連線* 警告。確切的訊息文字會依瀏覽器而不同，而略過或刪除警告的確切步驟也會不同。

因為您是使用 {{site.data.keyword.IBM}} 所提供的鏈結，所以可以放心忽略該警告並進行連接。如果您的瀏覽器可以儲存安全異常狀況，則這麼做是防止未來發生警告的最簡單方式。

另一個選項是匯出送入的簽章者憑證，然後將它匯入至您的瀏覽器，以作為授信主要憑證。此選擇需要您在 *hosts* 檔案中建立項目，以將 VM 的 IP 位址對映至憑證發行方的通用名稱。此名稱採用下列格式：wl<pureapplication.ibmcloud.com。如果您現在於 URL 中使用主機名稱，而非 IP 位址，則可以全新地進行連接。您接著必須在 URL 中使用該主機名稱而非 IP 位址來存取「管理中心」或「管理主控台」。

最後，客戶通常會針對他們設為外部的應用程式安裝自己的主要憑證。如需相關資訊，請參閱 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 或 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} IBM Knowledge Center。

## 防火牆埠
{: #firewall_ports}

您可能會發現需要開啟防火牆上的埠，以容許存取應用程式及資料庫。
  * 在每一個 WebSphere Application Server in Bluemix 節點上，您會在 WAS_HOME/virtual/bin 目錄中找到 Script openFirewallPorts.sh。
  * 在每一個 Liberty Collective 主機上，您會在 WAS_HOME/virtual/bin 目錄中找到 Script openFirewallPorts.sh。

用法：

  ```
      $ openFirewallPorts.sh -ports <PORT>:<PROTOCOL>,... -persist true|false
  ```
  {: codeblock}

* PORT 是埠號
* PROTOCOL 是 TCP 或 UDP
* -persist 是 true 或 false

若要指定多個埠，請用逗點 "," 予以區隔。

**附註**：已開啟之埠的 sport 與 dport，已在防火牆的 INPUT 與 OUTPUT 區段開啟。您必須使用 sudo，以 root 身分執行此 Script。您也可以直接修改 iptables。

## 配置 Web 伺服器
{: #configure_webserver}

當您佈建 Cell 或群體時，會得到預先配置的環境。具體而言，對於傳統的 Network Deployment Cell，您會收到下列環境：

* 與 IBM HTTP Server 並置的部署管理程式，用於開發及測試用途。

* 聯合至部署管理程式的自訂節點。

* 部署管理程式、IHS 伺服器以及節點代理程式，全都在一開始時佈建為 STARTED 狀態。

如果您需要 Web 伺服器處理所有使用者要求，則在部署應用程式之後，可能需要產生並傳播外掛程式。

**避免麻煩：**在產生並傳播外掛程式之前，請確定已完成下列必要作業：

* 在本端 Windows、Linux 或 Mac 環境中，確保已配置、啟動 [openVPN](systemAccess.html#setup_openvpn)，且您已連接到適當的的地區。

* 從「WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服務儀表板」中，按一下**開啟管理主控台**，並使用 wsadmin 及「服務儀表板」中所提供的「管理密碼」來登入。

* 從管理主控台中，建立應用程式伺服器（例如，***server1***)，因為部署管理程式已與空的自訂節點聯合。

* 啟動您建立的伺服器。

* 在應用程式安裝期間，確保您的應用程式模組已對映到您剛啟動的伺服器，以及對映到 Web 伺服器（例如，***webserver1***）。

下列高階步驟假設已完成必要作業：

1. 從「管理主控台」的「環境」選項產生外掛程式：
   1. 選擇「環境」>「更新廣域 Web 伺服器外掛程式配置」
   2. 按一下**確定**或**改寫以產生新的外掛程式配置檔**
2. 從「部署管理程式」，將外掛程式複製到 Web 伺服器配置：

  ```
   cp /opt/IBM/WebSphere/Profiles/DefaultDmgr01/config/cells/plugin-cfg.xml /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
  ```
  {: codeblock}
3. 編輯 **IHS_HOME/conf**（例如，*/opt/IBM/WebSphere/HTTPServer/conf*）中的 **httpd.conf**)，並確保下列兩行存在：

    ```
    LoadModule was_ap22_module /opt/IBM/WebSphere/Plugins/bin/64bits/mod_was_ap22_http.so
    WebSpherePluginConfig /opt/IBM/WebSphere/Plugins/config/webserver1/plugin-cfg.xml
    ```
    {: codeblock}  
4. 使用這兩個指令開啟埠：

  ```
   export serverPorts=2810:TCP,2810:UDP,8880:TCP,8880:UDP,9101:TCP,9101:UDP,9061:TCP,9061:UDP,9080:TCP,9080:UDP,9354:TCP,9354:UDP,9044:TCP,9044:UDP,9443:TCP,9443:UDP,5060:TCP,5060:UDP,5061:TCP,5061:UDP,11005:TCP,11005:UDP,11007:TCP,11007:UDP,9633:TCP,9633:UDP,7276:TCP,7276:UDP,7286:TCP,7286:UDP,5558:TCP,5558:UDP,5578:TCP,5578:UDP

   sudo /opt/IBM/WebSphere/AppServer/virtual/bin/openFirewallPorts.sh -ports $serverPorts -persist true
  ```
    {: codeblock}
5. 使用下列兩個指令停止並啟動 Web 伺服器：
    ```
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k stop
    sudo /opt/IBM/WebSphere/HTTPServer/bin/apachectl -k start
    ```
    {: codeblock}
8. 透過外掛程式存取應用程式：
  ```
   http://169.53.246.xxx/contextRoot/
  ```
  {: codeblock}

**附註：**所提供的步驟，代表當您試圖配置 Web 伺服器時的許多路徑之一。如需進一步的協助，請參閱 [IBM Knowledge Center](https://www.ibm.com/support/knowledgecenter/search/configure%20web%20server?scope=SSAW57_9.0.0){: new_window}。

**附註：**如果您無法存取應用程式，則可能面臨防火牆上的埠存取問題。因此，您可能需要重新啟動下列任何伺服器：應用程式伺服器、節點代理程式、Web 伺服器和部署管理程式。另外，您也可能需要存取「WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} 服務儀表板」，然後重新啟動每部虛擬機器。

## SSL 配置
{: #ssl_configuration}

傳統 WebSphere Application Server 及 Liberty 設定檔已配置 [SSL_TLSv2](https://www.ibm.com/support/knowledgecenter/en/SSYKE2_8.0.0/com.ibm.java.security.component.80.doc/security-component/jsse2Docs/protocols.html){: new_window} 通訊協定。若要變更通訊協定，請修改下列檔案：

針對傳統 WebSphere Application Server：

1. 編輯 /opt/IBM/WebSphere/Profiles/*profile_name*/config/cell/*cell_name* 中的 **security.xml**，並修改下行：

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}

2. 編輯 /opt/IBM/WebSphere/Profiles/*profile_name*/properties 中的 **ssl.client.props**，並修改下行：

  ```
  com.ibm.ssl.protocol=SSL_TLSv2
  ```
{: codeblock}

針對 Liberty 設定檔：

1. 編輯 /opt/IBM/WebSphere/Profiles/Liberty/servers/server1 中的 **server.xml**，並修改 defaultSSLConfig ssl 配置元素中的下行：

  ```
  sslProtocol="SSL_TLSv2"
  ```
{: codeblock}
