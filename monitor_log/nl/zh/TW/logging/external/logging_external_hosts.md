---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 配置外部日誌主機
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} 在記憶體中保留了有限的日誌資訊量。
在記載資訊時，舊資訊會取代為較新的資訊。
若要保留所有日誌資訊，您可以將日誌儲存到外部日誌主機（例如協力廠商日誌管理服務或其他主機）。
{:shortdesc}

若要將日誌從您的應用程式及系統串流到外部日誌主機，請完成下列步驟：

  1. 決定記載端點。

	 您可以將日誌傳送給協力廠商日誌聚集器（例如 Papertrail、Splunk 或 Sumologic）。您也可以將日誌傳送給 syslog 主機、使用 TLS（傳輸層安全）加密的 syslog 主機，或 HTTPS POST 端點。不同日誌主機取得記載端點的方法會不同。

  2. 建立使用者提供的服務實例。

	 使用 `cf create-user-provided-service` 指令（或 `cups`，這是此指令的簡短版本），以建立使用者提供的服務實例：
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;

	 使用者提供的服務實例的名稱。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} 將日誌傳送至其中的記載端點。請參閱下表，以將 *logging_endpoint* 取代為您的值：

	 <table>
	 <caption>表 1. 記載端點值</caption>
     <thead>
     <tr>
     <th>記載端點</th>
     <th>指令</th>
	 <th>附註</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog 主機</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例如，若要啟用記載至 Papertrail 的功能，請鍵入 `cf cups my-logs -l syslog://<papertrail-url>`。請將 `<papertrail-url>` 取代為來自 Papertrail 的記載端點的 URL。</td>
     </tr>
	 <tr>
     <td>syslog-tls 主機</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>憑證必須受憑證管理中心信任。請不要使用自簽憑證。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>此端點必須位在公用網際網路上，並且可供 {{site.data.keyword.Bluemix_notm}} 存取</td>
     </tr>
     </tbody>
     </table>
  3. 將服務實例連結至您的應用程式。

	 使用下列指令，將服務實例連結至您的應用程式：

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 應用程式的名稱。

	 &lt;service_name&gt;

	 使用者提供的服務實例的名稱。

  4. 重新編譯打包應用程式。
     鍵入 `cf restage appname`，讓變更生效。

