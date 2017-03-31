---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iotinsurance_short}} 疑難排解
{: #ts}

以下是關於在 {{site.data.keyword.Bluemix_notm}} 上使用 {{site.data.keyword.iotinsurance_full}} 的常見疑難排解問題解答。
{:shortdesc}

## 部署應用程式時的問題
{: #deployingapps}
如果在 {{site.data.keyword.Bluemix_notm}} 組織中沒有足夠的記憶體，您可能無法部署 {{site.data.keyword.iotinsurance_short}} 的應用程式。您可以減少應用程式使用的記憶體，或是增加帳戶的記憶體配額。
{:shortdesc}

當您開啟 {{site.data.keyword.iotinsurance_short}} 服務時，未啟用「部署」功能，且您無法部署任何應用程式。
{: tsSymptoms}

您的組織必須有至少 2 GB 的可用記憶體，才能啟用「部署」功能。試用帳戶的記憶體配額上限為 2 GB。如果您建立了非 {{site.data.keyword.iotinsurance_short}} 的服務或應用程式，您的組織便沒有足夠的記憶體可部署 {{site.data.keyword.iotinsurance_short}} 應用程式。
{: tsCauses}

您可以增加帳戶的記憶體配額，或是減少服務及應用程式使用的記憶體。
- 若要增加帳戶的記憶體配額，您可以[將試用帳戶轉換為付費帳戶](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)。
- 若要快速減少使用中的記憶體，請移除非 {{site.data.keyword.iotinsurance_short}} 的所有服務及應用程式。重新啟動 {{site.data.keyword.iotinsurance_short}} 服務，讓變更生效。
- 針對具有超過 2 GB 總記憶體的付費帳戶，您可能可以藉由調整其他應用程式或服務使用的記憶體量而避免移除它們。如需相關資訊，請參閱[已超出組織的記憶體限制](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory)。
{: tsResolve}

## 效能問題
{: #performance_issues}

在尖峰活動期間，您可能會發現效能變慢。
{:shortdesc}

進行頻繁 API 呼叫的忙碌系統的回應時間可能會延遲。
{: tsSymptoms}

{{site.data.keyword.iotinsurance_short}} 預設會部署 {{site.data.keyword.cloudantfull}} 試用版。此版本限制每秒可進行的 API 呼叫數目。
{: tsCauses}

升級至 {{site.data.keyword.cloudant}} 標準版本。
{: tsResolve}

## 取得 {{site.data.keyword.iotinsurance_short}} 的協助及支援
{: #gettinghelp}

如果您在使用 {{site.data.keyword.iotinsurance_full}} 時有問題或疑問，請檢查 {{site.data.keyword.Bluemix_notm}}，或者透過搜尋資訊或透過討論區提出問題來取得協助。您也可以開啟支援問題單。

- 您可以移至 [Bluemix 狀態頁面 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/support/#status){:new_window} 來檢查 {{site.data.keyword.Bluemix_notm}} 是否可用。

- 您可以檢閱討論區，以查看其他使用者是否發生相同的問題。使用討論區提出問題時，請標記您的問題，讓 {{site.data.keyword.Bluemix_notm}} 開發團隊可以看到它。
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
- 如果您有使用 {{site.data.keyword.iotinsurance_short}} 開發或部署應用程式的相關技術問題，請將問題張貼在 [Stack Overflow ![外部鏈結圖示](../../icons/launch-glyph.svg)](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window}，並使用 "ibm-bluemix" 及 "iot-for-insurance" 來標記您的問題。
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
- 若是服務及開始使用指示的相關問題，請使用 [IBM developerWorks dW Answers ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window} 討論區。請加上 "iot-for-insurance" 及 "bluemix" 標籤。

如需使用討論區的詳細資料，請參閱[取得協助](https://www.{DomainName}/docs/support/index.html#getting-help)。

- 如果您仍然無法解決問題，則可以開啟 IBM 支援問題單。如需開啟 IBM 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](../support/index.html#contacting-support)。
