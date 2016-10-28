---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} 疑難排解
{: #ts}
前次更新：2016 年 8 月 1 日
{: .last-updated}

這裡會回答有關在 {{site.data.keyword.Bluemix_notm}} 上使用 {{site.data.keyword.iot_full}} 的常見疑難排解問題。
{:shortdesc}

## 連接至 {{site.data.keyword.iot_short_notm}} 時發生問題
{: #connection_problem}

連線至 {{site.data.keyword.iot_short_notm}} 突然中斷。
{:shortdesc}

當您嘗試連接至 {{site.data.keyword.iot_short_notm}} 時，裝置或應用程式收到錯誤。
{: tsSymptoms}

您可能有兩個裝置嘗試以相同的用戶端 ID 和認證進行連線。每個用戶端 ID 僅限用於一個唯一連線。您不能有兩個使用相同 ID 的並行連線。應用程式可以共用相同的 API 金鑰，但 MQTT 需要用戶端 ID 一律是唯一的。
{: tsCauses}

若要解決此問題，請確認沒有兩個裝置嘗試使用相同的認證進行連接。
{: tsResolve}

## 裝置與 {{site.data.keyword.iot_short_notm}} 間歇性中斷連線
{: #disconnection_problem}

裝置與 {{site.data.keyword.iot_short_notm}} 的連線間歇性突然中斷。
{:shortdesc}

連接至 {{site.data.keyword.iot_short_notm}} 服務的裝置間歇性中斷連線。裝置會重新連線，但過沒多久又突然斷線。
{: tsSymptoms}

這可能是因為當您連接時，用於 MQTT ping 選項的值太低，讓它看起來像是連線逾時。例如，如果用戶端 MQTT 設定不正確，導致無法及時收到 ping，連線就會關閉。
{: tsCauses}

若要修正此問題，請確認已為連線設定適當的 ping 和 KeepAlive 參數。   
{: tsResolve}


## 取得 {{site.data.keyword.iot_short_notm}} 的協助和支援
{: #gettinghelp}

如果您在使用 {{site.data.keyword.iot_short_notm}} 時，有任何問題或疑問，您可以搜尋資訊來取得協助，或是透過討論區來提出問題。您也可以開啟支援問題單。

使用討論區來提出問題時，請標記您的問題，讓 {{site.data.keyword.Bluemix_notm}} 開發團隊能看到您的問題。

* 如果您有關於使用 {{site.data.keyword.iot_short_notm}} 來開發或部署應用程式的技術問題，請將您的問題張貼在 [Stack Overflow](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window}，並且在問題上加上 "ibm-bluemix" 和 "watson-iot" 標籤。
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* 若有關於服務和開始使用指示的問題，請使用 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window} 討論區。加上 "watson-iot" 和 "bluemix" 標籤。

如需有關使用討論區的詳細資訊，請參閱[取得協助](https://www.{DomainName}/docs/support/index.html#getting-help)。

如需開啟 IBM 支援問題單，或是支援層次和問題單嚴重性的相關資訊，請參閱[聯絡支援中心](https://www.{DomainName}/docs/support/index.html#contacting-support)。
