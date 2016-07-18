---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#系統存取
{: #system_access}
以下主題包括建立及管理服務實例的方法，以及如何存取系統以及如何設定存取系統的多種方法。
{: shortdesc}

*前次更新：2016 年 6 月 8 日*
{: .last-updated}

## WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 中的 REST API 使用
{: #restapi_usage}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} 中的實例會以下列其中一種方式建立、佈建、管理和刪除：

* 從 {{site.data.keyword.Bluemix_notm}} 使用者介面的 {{site.data.keyword.Bluemix_notm}}「型錄」及「服務儀表板」。
* 藉由建立使用 RESTful API 的應用程式或 Script。

透過使用遵循 Swagger 2.0 的 REST API，客戶能夠存取與透過入口網站和儀表板所提供功能的相同功能。如需所支援之 REST API 和資源的相關資訊，請參閱 WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} [REST API 文件](https://new-console.{DomainName}/apidocs/212){: new_window}。

**附註：**建立服務實例之後，根據所建立的 T 恤尺碼，您的服務可能無法立即供使用。建議您查詢所傳回 JSON 的**狀態**欄位，以判斷服務實例的現行狀態。

**附註：**依預設，API 基礎 URL 會指向[美國南部地區](https://wasaas-broker.ng.bluemix.net/wasaas-broker/api/v1){: new_window}中的端點。如果您使用英國或雪梨地區，請確定您的應用程式使用下列其中一個端點：

* [英國地區](https://wasaas-broker.eu-gb.bluemix.net/wasaas-broker/api/v1){: new_window}
* [雪梨地區](https://wasaas-broker.au-syd.bluemix.net/wasaas-broker/api/v1){: new_window}


## 服務儀表板
{: #service_dashboard}

在您建立服務實例之後，即會將您帶至服務儀表板。按一下組織儀表板中的「服務」圖示，一律可以回到服務儀表板。從服務儀表板，您可以存取：

*  此文件的鏈結
*  下載必要 OpenVPN 配置檔的鏈結。
*  啟動和停止虛擬機器的能力。一開始會啟動 VM。
*  主機名稱。
*  管理使用者及管理密碼。
*  專用 SSH 金鑰。
*  WebSphere® 管理使用者及管理密碼。
*  「管理中心」及「管理主控台」URL。

**附註**：由於特定量的運算、記憶體和 I/O 資源，客戶會因為處理停止狀態的累計 VM，被收取減價 5% 的費用。客戶會被控制在固定數量的已停止實例，最多不超過 10 個 IP 位址或 64 GB 的記憶體。


## 為 WebSphere Application Server for Bluemix 實例設定 openVPN
{: #setup_openvpn}

需要有 OpenVPN，才能存取 Bluemix 虛擬機器上的任何 WebSphere Application Server。您必須安裝它，而且必須使用管理者專用權來執行它。  

### 使用下列指示，在 Windows 中設定 openVPN：

1. 從 [openVPN Windows 下載](http://swupdate.openvpn.org/community/releases/)鏈結，下載
  * [openvpn-install-2.3.4-I001-x86_64.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-x86_64.exe){: new_window}（適用於 64 位元），或
  * [openvpn-install-2.3.4-I001-i686.exe](https://swupdate.openvpn.org/community/releases/openvpn-install-2.3.4-I001-i686.exe){: new_window}（適用於 32 位元）。
2. 確保[以 Windows 管理者身分執行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}，然後安裝 openVPN。
3. 在服務儀表板中，從 WebSphere Application Server for Bluemix 實例的 OpenVPN 下載鏈結下載 VPN 配置檔。將壓縮檔中的全部 4 個檔案解壓縮至 **{OpenVPN home}\config** 目錄。例如：

  <pre>  
C:\Program Files\OpenVPN\Config  </pre>
  {: codeblock}

4. 啟動 openVPN 用戶端程式 "OpenVPN GUI"。確保選取[以 Windows 管理者身分執行](https://technet.microsoft.com/en-us/magazine/ff431742.aspx){: new_window}來啟動程式。如果您沒有這麼做，則可能無法進行連接。

### 使用下列指示，在 Linux 中設定 openVPN：
1. 若要安裝 openVPN，請遵循以下[指示](https://openvpn.net/index.php/access-server/docs/admin-guides/182-how-to-connect-to-access-server-with-linux-clients.html){: new_window}。
  * 如果您需要手動下載及安裝 RPM 套件管理程式，請前往 [openVPN unix/linux 下載](https://openvpn.net/index.php/access-server/download-openvpn-as-sw.html){: new_window}。您可能需要 Linux 管理者的協助。
3. 在服務儀表板中，從 WebSphere Application Server for Bluemix 實例的 OpenVPN 下載鏈結下載 VPN 配置檔。請將檔案解壓縮至您要從中啟動 openVPN 用戶端的目錄。您需要相同目錄中的所有四個檔案。
3. 啟動 openVPN 用戶端程式。開啟終端機視窗，並移至包含配置檔案的目錄。以 root 身分執行下列指令：

  <pre>
$ openvpn --config vt-wasaas-wasaas.ovpn  </pre>
  {: codeblock}  

### 使用下列指示，在 Mac 中設定 openVPN：
1. 一種方法是安裝 [Tunnelblick](https://tunnelblick.net/){: new_window}（開放程式碼軟體產品）。
2. 從 WebSphere 服務解壓縮 VPN 配置檔。Tunnelblick 會提示您針對 Mac 輸入管理者密碼，以及將配置新增至您可用來連接的那組 VPN。
3. 連接至 VPN 網路，然後可以存取虛擬機器。在第一次存取後，Tunnelblick 會快取配置，並且您可以從 [Tunnelblick](https://tunnelblick.net/){: new_window} 連接。您可以將圖示放在頂端功能表列上，以方便進行存取。


## 使用 SSH 存取 WebSphere Application Server for Bluemix VM
{: #using_ssh}

這些指示假設您是使用 OpenSSH 作為用戶端。OpenSSH 通常適用於 Linux，也適用於在 Windows 上執行的 Cygwin。您還可以安裝 OpenSSH，以從 Windows 命令提示字元執行。

若要驗證 OpenSSH 的安裝，請輸入以下指令：
  ```
$ ssh -V
  ```
  {: codeblock}

您將收到與以下內容類似的回應：
  ```
OpenSSH_6.6p1, OpenSSL 1.0.1g 7 Apr 2014
  ```
  {: codeblock}

使用下列指示，設定 WebSphere Application Server for Bluemix VM 的 SSH 存取權：

1. 在您第一次連接時檢閱出現的警告訊息「無法確定主機 x.x.x.x 的真實性」。這是正常狀況。系統提示時，請選取 yes。現在會在 VM 上為使用者 virtuser 安裝公開金鑰。
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

當您按一下「管理中心」或「管理主控台」的鏈結時，可能會收到*未授信的連線*警告。確切的訊息文字會依瀏覽器而不同，而略過或刪除警告的確切步驟也會不同。

因為您是使用 {{site.data.keyword.IBM}} 所提供的鏈結，所以可以放心忽略該警告並進行連接。如果您的瀏覽器可以儲存安全異常狀況，則這麼做是防止未來發生警告的最簡單方式。

另一個選項是匯出送入的簽章者憑證，然後將它匯入至您的瀏覽器，以作為授信主要憑證。此選擇需要您在 *hosts* 檔案中建立項目，以將 VM 的 IP 位址對映至憑證發行方的通用名稱。此名稱採用下列格式：wl<pureapplication.ibmcloud.com。如果您現在於 URL 中使用主機名稱，而非 IP 位址，則應該會全新地進行連接。您接著需要在 URL 中使用該主機名稱而非 IP 位址來存取「管理中心」或「管理主控台」。

最後，客戶通常會針對他們設為外部的應用程式安裝自己的主要憑證。如需相關資訊，請參閱 [WebSphere Application Server](http://www.ibm.com/support/knowledgecenter/SSEQTP_8.5.5/com.ibm.websphere.base.doc/ae/tsec_securecomm.html?cp=SSEQTP_8.5.5%2F1-11-2-6&lang=en){: new_window} 或 [Liberty Core](http://www.ibm.com/support/knowledgecenter/SSD28V_8.5.5/com.ibm.websphere.wlp.core.doc/ae/twlp_sec_comm.html?lang=en){: new_window} Knowledge Center。

## 防火牆埠
{: #firewall_ports}

您可能會發現需要開啟防火牆上的埠，以容許存取應用程式及資料庫。
  * 在每一個 WebSphere Application Server for Bluemix 節點上，您會在 WAS_HOME/virtual/bin 目錄中找到 Script openFirewallPorts.sh。
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

**附註**：開啟埠的 sport 及 dport，已在防火牆的 INPUT 及 OUTPUT 區段中開啟。您必須使用 sudo，以 root 身分執行此 Script。您也可以直接修改 iptables。
