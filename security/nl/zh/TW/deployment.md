---

 

copyright:

  years: 2014, 2017

lastupdated: "2017-01-10" 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} 安全部署
{: #security-deployment}

{{site.data.keyword.Bluemix_notm}} 安全部署架構包含適用於應用程式使用者及開發人員的不同資訊流程，以確保安全存取。

![Bluemix 安全部署架構](images/sec_deployment.svg)

圖 3. Bluemix 安全部署架構

針對 {{site.data.keyword.Bluemix_notm}} *應用程式使用者*，**應用程式使用者流程**如下所示：
 1. 透過防火牆，並實施侵入防禦及網路安全。
 2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
 3. 透過網路路由器。
 4. 在 Droplet Execution Agent (DEA) 中呼叫應用程式運行環境。

{{site.data.keyword.Bluemix_notm}} *開發人員* 遵循兩個主要流程：一個適用於登入，一個適用於開發及部署。
 * **開發人員登入流程**包括下列項目：
    * 若為登入「{{site.data.keyword.Bluemix_notm}} 公用」的開發人員，流程如下所示：
      1. 透過 IBM Single Sign On 服務。
      2. 透過 IBM Web 身分。
    * 若為登入「{{site.data.keyword.Bluemix_notm}} 專用」或「Bluemix 本端」的開發人員，流程會透過企業 LDAP。
 * **開發及部署流程**如下所示：
    1. 透過防火牆，並實施侵入防禦及網路安全。這僅適用於「{{site.data.keyword.Bluemix_notm}} 專用」。
    2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
    3. 透過網路路由器。
    4. 透過利用 Cloud Foundry 雲端控制器所進行的授權，以確保僅能存取開發人員所建立的應用程式及服務實例。

針對「{{site.data.keyword.Bluemix_notm}} 專用」及「{{site.data.keyword.Bluemix_notm}} 本端」*管理者*，**管理者流程**如下所示：
 1. 透過防火牆，並實施侵入防禦及網路安全。
 2. 透過 IBM DataPower Gateway，並具有反向 Proxy 及 SSL 終止 Proxy。
 3. 透過網路路由器。
 4. 到達 {{site.data.keyword.Bluemix_notm}} 使用者介面中的「管理」頁面。

除了這些路徑中所述的使用者之外，經過授權的 IBM 安全作業團隊也會執行各種作業安全作業，例如下列作業：
 * 漏洞掃描。若為「{{site.data.keyword.Bluemix_notm}} 本端」，您掌控了防火牆內的實體安全以及任何掃描。
 * 使用者存取管理。
 * 利用 IBM Endpoint Manager 定期套用修正程式，來強化作業系統。
 * 風險管理與侵入防禦。
 * 使用 QRadar 進行安全監視。
 * 可在「管理」頁面上取得安全報告。
