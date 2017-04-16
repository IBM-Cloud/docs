---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Liberty for Java 疑難排解
{: #ts}


以下是有關在 {{site.data.keyword.Bluemix_notm}} 上使用 Liberty for Java 的常見疑難排解問題的答案。
{:shortdesc}

## 應用程式無法開始接受連線
{: #health_check_timeout}

### 發生的狀況

Liberty 應用程式無法啟動，錯誤為「無法開始接受連線」。例如，日誌中的錯誤可能類似下列內容：

```
   2016-11-14T14:44:58.45+0000 [API/0]      OUT App instance exited with guid 21ac63eb-9595-428a-94c7-b0b02aaf77cc payload: {"cc_partition"=>"default", "droplet"=>"21ac63eb-9595-428a-94c7-b0b02aaf77cc", "version"=>"b2772438-92de-4d47-b680-ea772ac2288a", "instance"=>"f4799c8c89214bbd8067883c3ffe23e0", "index"=>0, "reason"=>"CRASHED", "exit_status"=>255, "exit_description"=>"failed to accept connections within health check timeout", "crash_timestamp"=>1479134698} 2016-11-14T14:45:07.50+0000 [DEA/4]      ERR Instance (index 0) failed to start accepting connections
```

{: tsSymptoms}

### 發生的原因

Bluemix 會對應用程式執行性能檢查，以查看它是否已順利啟動。性能檢查會測試應用程式是否正在接聽指派給應用程式的埠。此檢查的預設逾時是 60 秒，而部分應用程式可能需要 60 秒以上的時間才能啟動。
{: tsCauses}

### 修正方式

請先檢查日誌，以尋找任何可能導致 Liberty 應用程式失敗的明顯錯誤。如果未發現任何明顯錯誤，請嘗試下列動作：

* 增加性能檢查逾時。使用 "cf push" 指令來部署應用程式時，請使用 "-t" 選項來指定較長的應用程式啟動逾時。例如：

```
    $ cf push myApp -t 180
```

性能檢查逾時也可以指定於 manifest.yml 檔案中。例如：

```
   ---
     ...
     timeout: 180
```

* 停用 appstate 特性。appstate 特性會與 Bluemix 性能檢查處理程序整合，以確定 Liberty 應用程式已完整起始設定，然後應用程式才能收到 HTTP 要求。此特性的負面影響是部分應用程式可能需要較長的時間才能啟動。若要停用 appstate 特性，請在應用程式上設定下列環境內容，並重新編譯打包應用程式：

```
   $ cf set-env myApp JBP_CONFIG_LIBERTY “app_state: false”
```

* 考慮重構應用程式。如果您的應用程式需要很長的時間才能起始設定，您可能需要重構應用程式才能執行延遲及（或）非同步起始設定。

* 使用 "no-route" 選項進行部署。使用 "--no-route" 選項來部署應用程式。這樣會停用埠性能檢查。例如：

```
   $ cf push myApp –no-route
```

在起始設定應用程式之後，請將路徑對映至應用程式。例如：

```
   $ cf map-route myApp mybluemix.net
```

{: tsResolve}

## IBM 閘道的 SSL 錯誤
{: #ssl_handshake_failure}

### 發生的狀況

下列錯誤顯示於日誌中，而且應用程式可能無法啟動：

```
   2016-11-03T12:32:44.82-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error 2016-11-03T12:32:44.83-0200 [App/0]      ERR [ERROR   ] CWPKI0022E: SSL HANDSHAKE FAILURE:  A signer with SubjectDN CN=*.gateway.prd.na.ca.ibmserviceengage.com, O=International Business Machines Corp., L=Armonk, ST=New York, C=US was sent from the target host.  The signer might need to be added to local trust store /home/vcap/app/wlp/usr/servers/defaultServer/resources/security/key.jks, located in SSL configuration alias defaultSSLConfig.  The extended error message from the SSL handshake exception is: PKIX path building failed: java.security.cert.CertPathBuilderException: PKIXCertPathBuilderImpl could not build a valid CertPath.; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: The certificate issued by CN=DigiCert Global Root CA, OU=www.digicert.com, O=DigiCert Inc, C=US is not trusted; internal cause is: 2016-11-03T12:32:44.83-0200 [App/0]      ERR java.security.cert.CertPathValidatorException: Certificate chaining error
```
{: tsSymptoms}


## 發生的原因

下列情況可能會產生錯誤：Monitoring & Analytics 服務已連結至 Liberty 應用程式，而且 Liberty 應用程式已部署為包含可配置 Liberty ssl-1.0 特性的 server.xml 的伺服器目錄或包裝伺服器。將 Monitoring & Analytics 服務連結至 Liberty 應用程式，可讓運行環境透過安全連線來連接至服務。該安全連線是使用預設 SSL 設定所建立。由於預設 SSL 設定指定於 Liberty 的 server.xml 中，所以已配置的信任儲存庫可能不信任 Monitoring & Analytics 服務所使用的憑證。
{: tsCauses}

## 修正方式

* 修改配置，以使用 JVM 的信任儲存庫。更新 Liberty 的 server.xml，以使用 JVM 的 cacerts 檔案作為信任儲存庫。將下列內容新增至 server.xml：
```
   <ssl id="defaultSSLConfig" trustStoreRef="defaultTrustStore"/> <keyStore id="defaultTrustStoretore" location="${java.home}/lib/security/cacerts"/>
```

* 更新已配置的信任儲存庫，以信任「DigitCert 主要 CA」。

  * 從 https://www.digicert.com/CACerts/DigiCertGlobalRootCA.crt 下載「DigiCert 主要 CA」
  * 假設使用 resources/security/key.jks 作為信任儲存庫，請使用 Java 的 keytool 公用程式將 CA 匯入至金鑰：

```
   $ keytool -importcert --storepass <keyStorePassword> -keystore <path>/resources/security/key.jks -file DigiCertGlobalRootCA.crt
```

進行這些變更之後，請不要忘記重新編譯打包應用程式。
{: tsResolve}
