---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 範例：將 Cloud Foundry 應用程式日誌串流至 Splunk
{: #splunk}

在此範例中，名為 Jane 的開發人員會使用 IBM Virtual Servers 測試版及 Ubuntu 映像檔來建立虛擬伺服器。Jane 嘗試將 Cloud Foundry 應用程式日誌從 {{site.data.keyword.Bluemix_notm}} 串流至 Splunk。{:shortdesc}

  1. Jane 是從設定 Splunk 開始。

     a. Jane 從 [Download Splunk Light ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} 網站下載 Splunk Light，然後使用下列指令進行安裝。軟體會安裝在 */opt/splunk* 上。

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane 會安裝及修補 RFC5424 syslog 技術附加程式，以與 {{site.data.keyword.Bluemix_notm}} 整合。如需附加程式安裝指示的相關資訊，請參閱 [Cloud Foundry 準則 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}。

	    Jane 使用下列指令來安裝附加程式：

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        然後，Jane 會將 */opt/splunk/etc/apps/rfc5424/default/transforms.conf* 取代為包含下列文字的新 *transforms.conf* 檔案，以修補附加程式：

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. 設定 Splunk 之後，Jane 必須開啟 Ubuntu 機器上的一些埠來接受送入的 syslog 排除（埠 5140）及 Splunk Web 使用者介面（埠 8000），因為 {{site.data.keyword.Bluemix_notm}} 虛擬伺服器依預設會設定防火牆。

	    **附註：**在這裡完成 iptable 確認以供 Jane 進行評估，而且是暫時的。若要在正式作業環境中配置 Bluemix 虛擬伺服器中的防火牆設定，請參閱 [Network Security Groups ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 文件以取得詳細資料。

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   然後，Jane 會使用下列指令來執行 Splunk：

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane 會配置 Splunk 設定，以接受來自 {{site.data.keyword.Bluemix_notm}} 的 syslog 排除。她必須為 syslog 排除建立一個資料輸入。

     a. 從 Splunk Web 介面中，Jane 按一下**資料 > 資料輸入**。即會顯示 Splunk 所支援的輸入類型清單。

     b. 她選取 **TCP**，因為 syslog 排除使用 TCP 通訊協定。

     c. 在 **TCP** 窗格中，她在**埠**欄位中輸入 **5140**，並將其餘欄位空白，然後按**下一步**。

     d. 從**來源類型**清單中，她選取**未分類 > rfc5424_syslog**。

     e. 對於**方法**類型，她選取 **IP**。

     f. 在**索引**欄位中，Jane 按一下**建立新索引**。她將新索引命名為 "bluemix"，然後按一下**儲存**。

     g. 最後，在**檢閱**視窗中，Jane 確認設定正確，然後按一下**提交**來啟用此資料輸入。

  3. 在 {{site.data.keyword.Bluemix_notm}} 中，Jane 建立 syslog 排除服務，並將服務連結至應用程式。

     a. Jane 從 cf cli 使用下列指令來建立 syslog 排除服務：

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **附註：***dummyhost* 不是實際名稱。它用來隱藏實際主機名稱。

     b. Jane 會將 syslog 排除服務連結至她空間中的應用程式，然後重新編譯打包應用程式。

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane 試用她的應用程式，然後在 Splunk Web 介面中鍵入下列查詢字串：

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane 在她的 Splunk Web 介面中看到日誌串流。雖然 Jane 所安裝的 Splunk 是 Splunk Light，但一天還是可以保留 500MB 日誌。

