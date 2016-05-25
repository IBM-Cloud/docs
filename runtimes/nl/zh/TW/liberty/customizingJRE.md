---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 自訂 JRE
{: #customizing_jre}

*前次更新：2016 年 3 月 23 日*

應用程式是在 Liberty 建置套件所提供及配置的 Java 執行時期環境 (JRE) 中執行。Liberty 建置套件也可以配置 JRE 版本或類型、自訂 JVM 選項，或重疊 JRE 功能。

## IBM JRE

依預設，應用程式會配置成使用輕量型版本的 IBM JRE 來執行。這個輕量型 JRE 經過拆解以提供核心的重要功能，並且大量減少磁碟和記憶體佔用量。如需輕量型 JRE 內容的相關資訊，請參閱 [Liberty for Java 執行時期](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html)。

依預設會使用 IBM JRE 第 8 版。請使用 JBP_CONFIG_IBMJDK 環境變數來指定 IBM JRE 的替代版本。例如，若要使用最新的 IBM JRE 7.1，請設定下列環境變數：
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

version 內容可以設成版本範圍。有兩個支援的版本範圍：1.7.+ 和 1.8.+。為求最佳結果，請使用 Java 8。

## OpenJDK
{: #openjdk}

應用程式可以選擇性地配置為使用 OpenJDK 作為 JRE 來執行。為了讓應用程式能使用 OpenJDK 執行，請將 JVM 環境變數設為 "openjdk"。例如，使用 cf 指令行工具，執行下列指令：
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

如果啟用的話，依預設會使用 OpenJDK 第 8 版。請使用 JBP_CONFIG_OPENJDK 環境變數來指定 OpenJDK 的替代版本。例如，若要使用最新的 OpenJDK 7，請設定下列環境變數：
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

version 內容可以設為 1.7.+ 之類的版本範圍，或[可用的 OpenJDK 版本清單](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml)所列出的任何特定版本。為求最佳結果，請使用 Java 8。

## 配置 JRE 選項
{: #configuring_jre}

### JVM 預設配置
{: #jvm_default_config}

Liberty 建置套件透過考慮下列項目來配置預設 JVM 選項：

* 應用程式的記憶體限制。已套用的 JVM 資料堆設定是根據下列項目計算而來：
  * 應用程式的記憶體限制，如[記憶體限制與 Liberty 建置套件](memoryLimits.html#memory_limits)中所述。
  * JRE 類型，因為 JVM 的資料堆相關選項會根據 JRE 的支援選項而不同。

* [Bluemix 中支援的 Liberty 特性](libertyFeatures.html#libertyfeatures)。
  * Bluemix 中不支援兩段式確定廣域資料庫交易，因此，透過設定 -Dcom.ibm.tx.jta.disable2PC=true 予以停用。

* Bluemix 環境。

    JVM 選項的配置是為了提供 Bluemix 環境中的最佳化，以及輔助記憶體相關錯誤狀況的診斷。
  * 透過停用 JVM 傾出選項，並在應用程式的記憶體耗盡時結束 (kill) 處理程序，以配置應用程式的快速失敗及回復。
  * 虛擬化調整（僅限 IBM JRE）。
  * 將失敗時的應用程式可用記憶體資源資訊遞送至 Loggregator。
  * 如果應用程式是配置為啟用 JVM 記憶體傾出，則會停用 Java 處理程序的結束 (kill) 功能，且 JVM 記憶體傾出會遞送至一個共同的應用程式 "dumps" 目錄。然後，即可從 Bluemix 儀表板或 CF CLI 檢視這些傾出。

以下是預設 JVM 配置的範例，它是建置套件針對以 512M 記憶體限制所部署的應用程式而產生的：
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### 自訂 JVM 配置
{: #customizing_jvm}

應用程式可以使用針對應用程式所配置之 JRE 定義的規格，來自訂 JVM 選項。請直接從 JRE 的文件參照如何指定選項及其用法的準則，因為選項會根據 JRE 而不同。

<table>
<tr>
<th align="left">JRE</th>
<th align="left">指令行選項格式</th>
<th align="left">參照</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>包括執行時期選項（字首為 -X）、任何 Java 系統內容（字首為 -D），而且不建議將 -XX 用於非正式用法（這些選項可能隨時變更）
</td>
<td>[第 8 版指令行選項](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html)、[第 7 版指令行選項](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)</td>
</tr>

<tr>
<td> OpenJDK</td>
<td>根據 HotSpot 執行時期，以 -X 表示非標準、-XX 表示開發人員選項，並使用布林旗標來啟用或停用選項</td>
<td>[HotSpot 執行時期概觀](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

需要自訂 JVM 選項的應用程式可以將此選項設為 Bluemix 中 IBM_JAVA_OPTIONS、JAVA_OPTS 或 JVM_ARGS 環境變數其中之一的值。請參閱「環境變數」小節，以瞭解如何設定應用程式的環境變數。包裝伺服器或伺服器目錄也可以包括含有指令行選項的 jvm.options 檔案，而不設定環境變數。

將 JVM 選項套用至 JRE 時，會先套用 Liberty 建置套件的預設選項，接著再套用自訂選項。自訂選項是依表格中所列的特定順序予以附加。已套用的 Java 選項的順序定義了哪些選項優先。最後套用之選項的優先順序高於先前套用的選項。


附註：部分選項可能不會生效，除非有代理程式觸發該選項。

<table>
<tr>
<th align="left">套用的順序</th>
<th align="left">應用程式 JVM 選項設定</th>
<th align="left">說明</th>
<th align="left">支援的應用程式類型</th>
<th align="left">更新已部署應用程式的 JVM 選項</th>
<th align="left">適用於 OpenJDK JRE</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>IBM JRE 所支援的環境變數</td>
<td>全部</td>
<td>重新啟動或重新編譯打包應用程式</td>
<td>否</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>透過 Liberty 建置套件「Java 選項」架構提供的環境變數</td>
<td>全部</td>
<td>重新編譯打包應用程式</td>
<td>是</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>Liberty 執行時期包裝伺服器或伺服器目錄所支援的 JVM 配置檔</td>
<td>伺服器套件</td>
<td>重新編譯打包應用程式</td>
<td>是</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>Liberty 執行時期所支援的環境變數</td>
<td>全部</td>
<td>重新啟動或重新編譯打包應用程式</td>
<td>是</td>
</tr>
</table>

### 決定執行中應用程式的已套用 JVM 選項
{: #determining_applied_jvm_options}

使用 JVM_ARGS 環境變數所指定的應用程式定義選項除外，其他產生的選項會以指令行選項形式（獨立式 Java 應用程式）或以 jvm.options 檔案（非獨立式 Java 應用程式）持續保存在執行時期環境中。您可以從「Bluemix 儀表板」或 CF CLI 檢視應用程式的已套用 JVM 選項。

獨立式 Java 應用程式的 JVM 選項會持續保存為指令行選項。您可以從 staging_info.yml 檔案檢視它們。
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

WAR、EAR、伺服器目錄及包裝伺服器部署的 JVM 選項會持續保存在 jvm.options 檔案中。

若要檢視 WAR、EAR 及伺服器目錄的 jvm.options 檔案，請執行下列指令：
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

若要檢視包裝伺服器的 jvm.options 檔案，請以您的伺服器名稱取代 &lt;serverName>，並執行下列指令：
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock}

#### 用法範例
{: #example_usage}

使用自訂的 JVM 選項部署應用程式，以啟用 IBM JRE JVM 詳細記憶體回收記載：
* 應用程式的 manifest.yml 檔案中包含的 JVM 選項：
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* 若要檢視產生的 JVM 詳細記憶體回收記載，請執行：
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* 更新已部署應用程式的 IBM JRE JVM 選項，以便在記憶體不足狀況中觸發 heap、snap 及 javacore：

使用 JVM 選項設定應用程式的環境變數，並重新啟動應用程式：
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* 若要在觸發記憶體不足狀況時檢視產生的 JVM 傾出，請執行：
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### 重疊 JRE
{: #overlaying_jre}

在部分情況中，檔案需要與 JRE 組合，才能公開其功能。應用程式開發者可以提供 JRE 檔案進行自訂作業。

要重疊的檔案可以與應用程式 WAR、EAR 或 JAR 包裝在一起，放在保存檔根目錄的 resources 資料夾。若為伺服器（壓縮檔或伺服器目錄），檔案可以包裝在伺服器目錄的 resources 資料夾中，與 server.xml 檔案在一起。

* WAR 檔
  * WEB-INF
  * resources
    * 其他檔案
    * .java-overlay


* EAR 檔
  * META-INF
  * resources
    * 其他檔案
    * .java-overlay


* JAR 檔
  * META-INF
  * resources
    * 其他檔案
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * resources
    * 其他檔案
    * .java-overlay

.java-overlay 目錄包含的特定檔案，位於要重疊之 Java JRE 所在的檔案階層（從 .java/jre 開始）。

例如，如果您要使用 AES 256 位元加密，則需要重疊這些 Java 原則檔案：
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

下載適當的未限定原則檔案，並將它們新增到您的應用程式，如：
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

當您推送應用程式時，這些 Jar 會重疊 Java 執行時期中的預設原則 Jar。這個處理程序會啟用 AES 256 位元加密。

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
