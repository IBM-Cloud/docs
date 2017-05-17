---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 收集容器中的非預設日誌資料
{: #logging_containers_collect_data}

若要擷取容器內非預設日誌位置中的資料，請在建立容器時，設定環境變數 **LOG_LOCATIONS**。
{:shortdesc}

* 在建立容器時，請新增 **LOG_LOCATIONS** 環境變數，並包含日誌檔的路徑。 
* 您可以新增多個日誌檔，以逗點將其隔開。 

## 透過 Bluemix 主控台收集非預設日誌資料
{: #logging_containers_collect_data_ui}

請完成下列步驟，以透過主控台收集非預設資料：

1. 從型錄中，選取**容器**，然後選擇映像檔。 

    所顯示的映像檔清單包括 {{site.data.keyword.IBM}} 所提供的映像檔，以及儲存在專用 {{site.data.keyword.Bluemix_notm}} 登錄中的映像檔。 

2. 定義您的容器。選擇類型、輸入容器的名稱、選取其大小，然後定義 IP 位址詳細資料和埠等其他屬性。如需相關資訊，請參閱[透過 {{site.data.keyword.Bluemix_notm}} 使用者介面來建立及部署單一容器](/docs/containers/container_single_ui.html#gui)。 

3. 展開**進階選項**區段，然後選取**新增環境變數**。

4. 新增 **LOG_LOCATIONS** 變數，並將其值設定為您要分析的日誌。

    例如，當您新增以最新 Liberty 映像檔為基礎的容器時，若要分析日誌檔 *dpkg.log*，請將環境值設定為下列值：
    
    <table>
      <caption>表 1. 日誌位置範例值</caption>
      <tbody>
        <tr>
          <th align="center">變數名稱</th>
          <th align="center">值</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. 按一下**建立**。

即會開啟容器儀表板。請檢查容器的狀態為*執行中*，然後檢查**監視及日誌**標籤中的日誌。


## 透過 CLI 收集非預設日誌資料
{: #logging_containers_collect_data_cli}

請完成下列步驟，以透過 CLI 收集非預設日誌資料：

1. 設定終端機來使用 {{site.data.keyword.containershort}} CLI。如需相關資訊，請參閱[設定 IBM Bluemix Container Service CLI](/docs/containers/container_cli_cfic_install.html)。

2. 使用下列指令來登入 Cloud Foundry CLI：`cf login`。依照系統提示，輸入您的 {{site.data.keyword.Bluemix_notm}} ID、密碼、組織及空間。 

    依預設，您會登入美國南部地區，或是您前次登入的地區。 
    
    您可以包含 **-a** 選項，以登入 {{site.data.keyword.Bluemix_notm}} 中的特定地區。例如，下表列出每個地區的指令：

    <table>
      <caption>表 2. 每個地區的指令</caption>
      <tbody>
        <tr>
          <th align="center">地區</th>
          <th align="center">指令</th>
        </tr>
        <tr>
          <td align="left">美國南部</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">英國</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">法蘭克福</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. 使用下列指令來登入 {{site.data.keyword.containershort}}：`cf ic login`

4. 從映像檔建立單一容器。包含 LOG_LOCATIONS 環境變數，以包含非預設日誌位置。  

    若要新增自訂位置，讓您能夠在 Kibana 中檢視該日誌資訊，請在建立容器時，新增 **LOG_LOCATIONS** 環境變數。請輸入下列指令：
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    其中
    
     <table>
      <caption>表 3. 指令選項</caption>
      <tbody>
        <tr>
          <th align="center">選項</th>
          <th align="center">說明</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> 如果您想要讓您的應用程式可從網際網路存取，您需要公開一個公用埠。包括 Dockerfile 中針對您要使用之映像檔所指定的任何埠。<br> 您可以選擇 UDP 與 TCP 其中一個，以指出您要使用的 IP 通訊協定。如果您未指定通訊協定，則會針對 TCP 資料流量自動公開您的埠。<br> 當您公開公用埠時，會建立容器的「公用網路安全群組」，讓您可以僅透過此公開埠傳送及接收公用資料。所有其他公用埠都會關閉，無法用來從網際網路存取應用程式。<br> 您可以利用多個 -p 選項來包括多個埠。</td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">設定環境變數。<br> 您可以個別列出多個索引鍵。請用引號括住環境變數名稱及值。<br> 若要新增要在容器中監視的日誌檔，請包含 LOG_LOCATIONS 環境變數與日誌檔路徑。</td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">定義容器的名稱。</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">公用地區中的登錄。例如，若為美國南部地區，預設網域名稱是：`ng.bluemix.net`，若為英國，則預設網域名稱是：`gb.bluemix.net`</td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">您要新增之映像檔的名稱。</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">您要新增之映像檔的標籤。</td>
        </tr>
      </tbody>
    </table>
    
    例如，若要建立以最新 Liberty 映像檔為基礎的容器，並包括日誌檔 `/var/log/dpkg.log`，請使用下列指令： 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    dpkg.log 檔案是標準 Ubuntu 日誌檔，通常會在建立容器期間產生，但不會自動推送至 Kibana。

若要檢查容器的狀態，請執行指令 `docker ps`。當狀態為*執行中* 時，請透過指令行或 Kibana，檢查 {{site.data.keyword.Bluemix_notm}} 主控台中的日誌。



