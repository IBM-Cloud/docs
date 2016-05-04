---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 JConsole 在 Bluemix 中監視 Liberty
{: #jconsole}

*前次更新：2016 年 3 月 23 日*

## 使用 JConsole 監視 Bluemix Liberty 執行時期的步驟如下：
{: #steps_to_monitor}

1. 在包含適當 server.xml 的伺服器套件內推送您的應用程式。
2. 在指令行上使用適當的系統內容啟動 JConsole 應用程式。
3. 對 JConsole 提供適當的遠端處理程序 URL、使用者名稱和密碼。

### 推送伺服器套件
{: #push_server_package}

推送包含您應用程式的伺服器套件，並將它限制在單一實例。您的 server.xml 檔案必須包含 `monitor-1.0` 及 `restConnector-1.0` 特性。它也必須包含 basicRegistry 元素及 administrator-role 元素。
```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * 附註：密碼應該使用 Liberty 提供的 securityUtility 工具加以編碼。

### 啟動 JConsole 應用程式
{: #start_jconsole_app}

JConsole 包含在您的 Java 安裝中。若要啟動 JConsole 應用程式，請移至 &lt;java-home&gt;/bin，並執行下列指令：
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

您可能必須傳遞其他參數才能配置 Java 信任儲存庫。下列參數在大部分情況下應該都適用：
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### 完成連線
{: #start_jconsole_app}
  * 在 Remote Process 欄位中填寫下列 URL：
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST。
  *  同時也在 Username 及 Password 欄位中填寫來自 server.xml 檔案的 administrator-role 角色的使用者和密碼。
  * 按一下 Connect。

連線成功時，JConsole 便開始監視。

如果連線失敗，您可以產生日誌來協助診斷問題。首先，嘗試在 jconsole 指令加上 ** -J-Djava.util.logging.config.file=c:/tmp/logging.properties**，以收集用戶端追蹤。以下是記載內容檔範例：
```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
```
{: #codeblock}

您也可以將 <b>&dash;J&dash;Djavax.net.debug=ssl</b> 新增至 jconsole 指令。這會在個別 JConsole 輸出視窗中產生 SSL 診斷追蹤。最後，您可以在 server.xml 檔案中新增下列內容，以便在伺服器端啟用追蹤功能：
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
