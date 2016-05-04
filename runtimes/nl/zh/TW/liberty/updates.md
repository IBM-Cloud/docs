---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty 建置套件的最新更新項目
{: #latest_updates}

## Liberty 建置套件中的最新更新項目清單。

*前次更新：2016 年 3 月 23 日*

### 2016 年 3 月 25 日：已更新 Liberty 建置套件 v2.7-20160321-1358
* 建置套件包含根據 [3 月的測試版](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/)之 WebSphere Liberty 的更新版本。Liberty 的更新版本讓 cloudant-1.0 測試版特性可在 Bluemix 中使用。
* 建置套件也包含 IBM JRE 的更新版本：8 SR2 FP12 及 7.1 SR3 FP32。 
* 建置套件提供用於 [Auto-Scaling 服務](../../services/Auto-Scaling/index.html)之代理程式的更新版本。 
* 現在，建置套件隨附了 [Monitoring and Analytics 服務](../../services/monana/index.html#monana_oview)的新資料收集器。新的收集器可讓您配置監視臨界值，且包含許多錯誤修正程式。
* 建置套件提供已更新的 DB2® JDBC 驅動程式 4.19.49 版。 
* [devconsole 和 shell 應用程式管理公用程式](../../manageapps/app_mng.html#app_management)所使用的 Node.js 執行時期已更新至最新的 0.12.12 版。

### 2016 年 3 月 7 日：已更新 Liberty 建置套件 v2.6-20160225-1649
* 建置套件新增了 Dynatrace 應用程式監視的支援。如需詳細資料，請參閱[使用 Dynatrace](dynatrace.html)。
* 建置套件新增了對 [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/) 的支援。

### 2016 年 2 月 10 日：已更新 Liberty 建置套件 v2.5-20160209-1336
* 建置套件包含根據 [2 月的測試版](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/)之 WebSphere Liberty 的更新版本。Liberty 設定檔的更新版本讓 apiDiscovery-1.0 GA 特性可在 Bluemix 中使用。

### 2016 年 2 月 4 日：已更新 Liberty 建置套件 v2.4-20160127-1437
* 建置套件包含根據 1 月的測試版之 WebSphere Liberty 的更新版本。在此更新中，先前以測試版特性提供的 scim-1.0 Liberty 特性，現在提供為可用於正式作業的特性。Liberty 的更新版本也讓 passwordUtilities-1.0 測試版特性可在 Bluemix 中使用。
* 建置套件也包含已更新的 IBM JRE 7.1 SF3 FP20 和 IBM JRE 8 SR2 FP10。
* 建置套件已更新，會在[自動配置 MySQL 類型的服務](autoConfig.html)時，下載最新的 1.x [MariaDB Connector/J JDBC 驅動程式](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)。

### 2015 年 12 月 16 日：已更新 Liberty 建置套件 v2.3-20151208-1311
* 建置套件包含根據 [12 月的測試版](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/)之 Liberty 設定檔的更新版本。Liberty 設定檔的更新版本讓 spnego-1.0 和 wsSecuritySaml-1.1 GA 特性以及 scim-1.0 測試版特性可在 Bluemix 中使用。
* 建置套件也包含已更新的 IBM JRE 8 SR2。
* 建置套件也已更新，會在[自動配置](autoConfig.html) PostgreSQL 或 MySQL 類型的服務時，下載最新的 [9.4.x PostgreSQL JDBC 驅動程式](https://jdbc.postgresql.org/)和 1.2.x [MariaDB Connector/J JDBC 驅動程式](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/)。

### 2015 年 11 月 23 日：已更新 Liberty 建置套件 v2.2-20151119-1720
* 建置套件包含更新版本的 Liberty 設定檔執行時期和 WebSphere eXtreme
Scale Client，以及 [Apache Commons Collection 漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21971426)的安全修正程式。
* 建置套件也包含更新版本的 [Java MongoDB
Driver](https://docs.mongodb.org/ecosystem/drivers/java/) 2.13.3 版。新的驅動程式與 MongoDB 2.4、2.6 和 3.0 版相容。
* 建置套件也提供用於 [Monitoring and Analytics 服務](../../services/monana/index.html)之資料收集器的更新版本。已更新的資料收集器已針對方法追蹤功能加以改良。


### 2015 年 10 月 16 日：已更新 Liberty 建置套件 v2.1-20151006-0912
* 建置套件包含根據 [10 月的測試版](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/)之 Liberty 設定檔的更新版本。在此更新中，先前以測試版特性提供的 bells-1.0、rtcomm-1.0、rtcommGateway-1.0、samlWeb-2.0、sipServlet-1.1 Liberty 特性，現在提供為可用於正式作業的特性。
* 建置套件也包含已更新的 IBM JRE 8 SR1 FP11。
* 建置套件也提供許多效能改良和最佳化：
  * 部署 WAR 或 EAR 檔時，依預設已停用 [CDI 1.2](optionsForPushing.html)
隱含 Bean 保存檔掃描特性。
  * 若要減少 Droplet 大小，[應用程式管理公用程式](../../manageapps/app_mng.html) devconsole 和 shell 需要重新編譯打包作業，而非重新啟動。
  * IBM JRE 的共用類別快取已停用，因為它未重複用於 Bluemix 環境。

### 2015 年 9 月 18 日：已更新 Liberty 建置套件 v2.0-20150914-1535
* 建置套件引進了兩項重大變更：
  * WAR 及 EAR 檔案的預設配置會啟用 Java EE 7 Web 設定檔特性，而非 Java EE 6 Web 設定檔特性。
  * 預設 Java 版本是第 8 版，而非第 7 版。
* 如需這些變更及其如何影響應用程式的詳細資料，請參閱 [Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/) 部落格文章。
* 建置套件也引進了 app_state 配置選項，以透過 JBP_CONFIG_LIBERTY 環境變數停用 appstate 特性。appstate 特性會與 Cloud Foundry 性能檢查處理程序整合，以確定 Liberty 應用程式已完整起始設定，然後應用程式才能收到 HTTP 要求。若要停用 appstate 特性，您可以將 JBP_CONFIG_LIBERTY 環境變數設為 "app_state: false"。

### 2015 年 9 月 4 日：已更新 Liberty 建置套件 v1.22-20150824-1104
* 建置套件支援 [HTTP_PROXY 及 HTTPS_PROXY 環境變數](environmentVariables.html)。如果設定的話，建置套件將在下載各種建置套件元件時，使用這些環境變數所指定的 Proxy 伺服器。


### 2015 年 8 月 19 日：已更新 Liberty 建置套件 v1.21-20150811-1342
* 建置套件包含根據 [8 月的測試版](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/)之 Liberty 設定檔的更新版本。Liberty 設定檔的更新版本讓下列新的[測試版特性](usingBetaFeatures.html)可在 Bluemix 中使用：bells-1.0、rtcommGateway-1.0、samlWebSso-2.0。

### 2015 年 7 月 31 日：已更新 Liberty 建置套件 v1.20.1-20150729-1255
* 建置套件包含更新版本的 IBM JRE：7.1 SR1 FP10 及 8 SR1 FP10。已更新的 JRE 包含[最新的安全修正程式](http://www-01.ibm.com/support/docview.wss?uid=swg21964161)及其他改良功能。
* 對 [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant) 服務提供[自動配置支援](autoConfig.html)的服務外掛程式已更新，可確保該服務的連線是透過安全通道建立。

### 2015 年 7 月 21 日：已更新 Liberty 建置套件 v1.20-20150713-1450
* 建置套件包含根據 [8.5.5.6 版](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/)之 Liberty 設定檔的更新版本。在此版本中，先前以測試版特性提供的所有 Java EE 7 Liberty 特性，現在提供為可用於正式作業的特性。由於 Bluemix 中的埠及其他限制，部分特性（例如遠端 EJB）在平台中未完全受到支援。
* 建置套件會辨識並執行包裝成 [distZip 樣式](https://docs.gradle.org/current/userguide/application_plugin.html)的應用程式。
* 建置套件包含 [Monitoring and Analytics 服務](../../services/monana/index.html)和
WebSphere eXtreme Scale Client 的已更新資料收集器，它們可支援新的 Liberty 執行時期版本。

### 2015 年 6 月 30 日：已更新 Liberty 建置套件 v1.19.1-20150622-1509
* 此版本的建置套件包含已更新的 IBM JRE，以及 [LogJam 漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21961390)的安全修正程式。
* [New Relic](newRelic.html) 代理程式已更新為 3.17 版。新版本提供與
Liberty 設定檔執行時期的改良整合。

### 2015 年 6 月 14 日：已更新 Liberty 建置套件 v1.19-20150608-1717
* 建置套件包含許多應用程式管理加強功能，包括對開發主控台及 Web 型 Shell 存取的支援。如需詳細資料，請參閱[應用程式管理文件](../../manageapps/app_mng.html)。
* 建置套件也包含關於找不到 [Monitoring and Analytics 服務](../../services/monana/index.html)之 Liberty 特性的問題修正程式。

### 2015 年 5 月 27 日：已更新 Liberty 建置套件 v1.18-20150519-1642
* 建置套件包含根據 [5 月的測試版](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/)之 Liberty 設定檔的更新版本。

### 2015 年 5 月 5 日：已更新 Liberty 建置套件 v1.17-20150501-1729
* 建置套件包含根據 [4 月的測試版](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/)之 Liberty 設定檔的更新版本。在此更新中，先前以測試版特性提供的 jsp-2.3、el-3.0 和 jdbc-4.1 Liberty 特性，現在提供為可用於正式作業的特性。此外，其他的 Java EE 7 特性如 jsf-2.2、javaMail-1.5、webProfile-7.0 和 javaee-7.0，現在都提供為[測試版特性](usingBetaFeatures.html)。
* 建置套件也提供對 Java 8 的起始支援。IBM JRE 7.1 仍是預設 JRE，但可以藉由設定 JBP_CONFIG_IBMJDK 環境變數為應用程式啟用 IBM JRE 8。同時也支援配置 OpenJDK 的版本。如需所有詳細資料，請參閱[自訂 JRE](customizingJRE.html)。
* 建置套件提供新的 JBP_CONFIG_LIBERTY 環境變數，它可以用來置換在部署 WAR 或 EAR 檔時為應用程啟用的預設 Liberty 特性集。
如需相關資訊，請參閱[獨立式應用程式](optionsForPushing.html#stand_alone_apps)。
* [Monitoring and Analytics 服務](../../services/monana/index.html)的服務外掛程式已更新，以減少針對服務產生的日誌大小。
* 在此版本的建置套件中，Droplet 的應用程式檔案佈置方式已變更。檔案結構的變更避免了與維護符號鏈結相關的複雜性，且應該對應用程式沒有影響。

### 2015 年 4 月 15 日：已更新 Liberty 建置套件 v1.16-20150407-1737
* 此版本的建置套件包含已更新的 IBM JRE 7.1-2.11，以及 [Bar Mitzvah 漏洞的安全修正程式](http://www-01.ibm.com/support/docview.wss?uid=swg21882777)。
* 部署獨立式 WAR 檔時，如果提供的話，建置套件現在使用內嵌 **ibm-web-ext.xml** 檔中指定的環境定義根目錄，來作為應用程式的環境定義根目錄。在此變更中，先前部署在根環境定義下的應用程式，可能會部署到不同的環境定義下，視 **ibm-web-ext.xml** 檔中的設定而定。

### 2015 年 4 月 3 日：已更新 Liberty 建置套件 v1.15-20150402-1422
* 建置套件包含根據 [3 月的測試版](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/)之 Liberty 設定檔的更新版本。Liberty 設定檔的更新版本讓 jsf-2.2 測試版特性可在 Bluemix 中使用。
* 建置套件也包含用於 [Monitoring and Analytics 服務](../../services/monana/index.html)之資料收集器的更新版本。

### 2015 年 3 月 20 日：已更新 Liberty 建置套件 v1.14-20150319-1159
* 這個版本的建置套件包含已更新的 IBM JRE 7.1.2.11 以及 [FREAK 漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21699864)安全修正程式。
* [SQL Database](services/SQLDB/index.html#SQLDB) 服務提供付費方案，這些方案提供選項來透過 SSL
通訊協定連接資料庫伺服器。建置套件對 SQL Database 服務的自動配置支援已更新，會將執行時期配置為在有 SSL 連線資訊可用時，透過 SSL 與資料庫進行連線。
* 建置套件已更新，部署獨立式 WAR 或 EAR 檔時，如果應用程式保存檔的根目錄包含 **server.xml** 配置檔，便會報告錯誤。
* 建置套件包含 MongoDB 自動配置服務外掛程式的修正程式，此外掛程式在某些情況下會產生無效的 **server.xml** 配置。

### 2015 年 2 月 10 日：已更新 Liberty 建置套件 v1.13-20150209-1122
* 建置套件包含 [Apache HttpComponents 和 Java 重疊特性漏洞](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us)的安全修正程式。
* 建置套件包含根據 [2 月的測試版](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/)之 Liberty 設定檔的更新版本。Liberty 設定檔的更新版本提供 WebSocket GA 特性 websocket-1.1 的更新版本。它也讓下列 Java EE 7 測試版特性可在 Bluemix 中使用：
  * cdi-1.2、el-3.0、jsp-2.3、jca-1.7、jacc-1.5 及 jaspic-1.1 
* 建置套件提供與 [ZeroTrunaround 的 JRebel 工具](http://zeroturnaround.com/software/jrebel/)的整合。此整合可讓您輕鬆使用 JRebel 搭配 Bluemix 應用程式，以及執行立即的應用程式更新，而不必重新部署或重新編譯打包應用程式。只支援獨立式 Web 應用程式。

### 2015 年 2 月 6 日：已更新 Liberty 建置套件 v1.12-20150130-1016
* 建置套件包含根據 [1 月的測試版](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/)之 Liberty 設定檔的更新版本。
* 建置套件包含用於 [Monitoring and Analytics 服務](../../services/monana/index.html#gettingstartedtemplate)之資料收集器的修整版本。

### 2015 年 1 月 23 日：已更新 Liberty 建置套件 v1.11-20150119-1511
* 建置套件包含已更新的 IBM JRE 7.1 版 SR2 FP1。
* 它也包含已更新的 WebSphere eXterme Scale Client 8.6.0.6 版，以及 Auto-Scaling 服務的已更新代理程式。
* [New Relic](newRelic.html) 服務支援已經過加強，可支援使用者定義的服務。
* 建置套件已改良，可報告 Liberty 設定檔及 IBM JRE 的詳細版本。

### 2014 年 12 月 19 日：已更新 Liberty 建置套件 v1.10-20141218-0103
* 建置套件提供應用程式的開發模式。開發模式是一種特殊模式，可讓開發人員為應用程式實例進行許多以前無法進行的活動。利用這個特性，此版本的 IBM Eclipse Tools for Bluemix 現在可以透過對 Bluemix 中所執行之 Liberty 應用程式的遞增式檔案更新，來支援遠端除錯。這讓使用 Eclipse 的開發人員可以方便在雲端對應用程式進行除錯，並即時套用變更至該應用程式。
* 建置套件也包含根據 [12 月的測試版](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/)之 Liberty 設定檔的更新版本。
* 此外，先前以測試版特性提供的下列四項 Liberty 特性，現在已可用於正式作業：
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0。
* 建置套件提供與 New Relic 服務的整合。一旦應用程式連結至 New Relic 服務，建置套件就會自動使用 New Relic 代理程式下載及配置執行時期。
* 建置套件具有下列已知限制：
  * 在開發模式中，無法連結 SessionCache 服務。
  * 在開發模式中，無法建立執行緒傾出。
  * 使用 servlet-3.1 或 websocket-v1.0 特性時，無法連結 Monitoring & Analytics 服務。

### 2014 年 12 月 5 日：已更新 Liberty 建置套件 v1.9-20141202-0947
* 建置套件提供加強型 JVM 選項支援。現在只要透過重新啟動作業，就可以套用 JVM 選項。不需要重新編譯打包應用程式。預設 JVM 選項也已針對快速失敗進行最佳化，並預先配置共同位置，以方便尋找所產生的傾出。[Custom Configuration of Java JVM for the Liberty Runtime](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/) 文章提供相關的詳細資料。
* 建置套件包含已更新的 DB2 JDBC 驅動程式 4.17.29 版。
* 它也針對導致無法為 Monitoring & Analytics 服務收集 Liberty 執行緒儲存區用量資訊的問題，包含問題的修正程式。

### 2014 年 11 月 21 日：已更新 Liberty 建置套件 v1.8-20141118-1610
* 建置套件包含已更新的 IBM JRE 7.1 版 SR2，它提供 [POODLE 漏洞](http://www-01.ibm.com/support/docview.wss?uid=swg21687173)的修正程式。
* 它也包含根據 [11 月的測試版](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/)之 Liberty 設定檔的更新版本。

### 2014 年 10 月 30 日：已更新 Liberty 建置套件 v1.7-20141020-1759
* 建置套件包含已更新的 IBM JRE 7.1 版 SR1 FP3。
* 它也針對導致無法以包含 Unicode 字元的伺服器配置來部署應用程式的問題，提供問題的修正程式。

### 2014 年 10 月 23 日：已更新 Liberty 建置套件 v1.6-20141013-1628
* 現在，建置套件隨附了 [Monitoring and Analytics](../../services/monana/index.html) 的新資料收集器。新的資料收集器會收集診斷深入探索資訊，這讓服務的「診斷」方案使用者能診斷其應用程式的問題，往下直到特定一行的程式碼。
* 建置套件包含更新版本的管理及自動擴充代理程式，其中包括錯誤修正程式及次要改良功能。它也包括 [Liberty 設定檔](https://developer.ibm.com/wasdev/)的更新版本及 [Java MongoDB 驅動程式](https://docs.mongodb.org/ecosystem/drivers/java/) 2.12.3 版。
* 在 cloudAutowiring 特性中，已修正在部分應用程式中導致發生資源注入錯誤的錯誤 (bug)。

### 2014 年 10 月 3 日：已更新 Liberty 建置套件 v1.5-20140923-1143
* 使用已更新的建置套件後，應用程式現在可以使用 Liberty 測試版特性，包括 WebSocket 1.0、Servlet 3.1 或 JAX-RS 2.0。如需相關資訊，請參閱[使用測試版特性](usingBetaFeatures.html)。

### 2014 年 9 月 30 日：已更新 Liberty 建置套件 v1.4-20140908-1803
* 建置套件現在提供 ElephantSQL 及 ClearDB MySQL Database 協力廠商服務的支援。自動配置支援也適用於 posgresql 及 mysql 實驗性服務。總計新增 13 種服務，因此 Liberty 建置套件中的自動配置支援，能夠讓您在 Liberty 應用程式中取用 Bluemix 服務時更加快速且更為輕鬆。
* 在應用程式編譯打包期間，建置套件會顯示有關自動配置及其採取之其他動作的已改良日誌訊息。
* 建置套件包含更新版本的 Liberty 設定檔，內含修正程式和改良功能。
* 它也包含 IBM JRE 7.1 版的更新版本，其中含有效能改良功能。如需詳細的變更集，請參閱[新增功能](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html)頁面。

### 2014 年 8 月 28 日：已更新 Liberty 建置套件 v1.3-20140818-1538
* 建置套件包含 [Liberty 設定檔](https://developer.ibm.com/wasdev/)的更新版本，以及最新修正程式及改良功能。
* 這個版本的建置套件會修正 JAVA_OPTS
環境變數的支援，將其他的 JVM 選項傳給應用程式執行時期。

* 它也修正了導致無法部署獨立式、以 Spring 為基礎之 Jar 應用程式的問題。
* 現在可以使用 Bluemix 使用者介面來產生及下載 IBM JVM SNAP 追蹤。請參閱 IBM JVM 文件中的[疑難排解主題](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html)，以進一步瞭解 SNAP 追蹤或 JVM 所產生的其他診斷資訊。

### 2014 年 7 月 29 日：已更新 Liberty 建置套件 v1.1-20140725-1341
* 現在 Liberty 的 Bluemix Edition 已有新版本！
  * 使用這個版本的 Liberty，除了新特性之外還有修正程式，讓您能夠更有效率地取用 Bluemix 服務！
  * 有了新的 CouchDB 特性之後，Cloudant® 服務現在可以自動配置它，讓連接器物件變得垂手可得！不再需要剖析 VCAP_SERVICES 及提供 ektorp 用戶端 jar。
* 現在 IBM SDK for Java 已有新版本！
  * 重新推送您的應用程式時，它們會使用 IBM SDK for Java 7.1-1.0 版。這具有顯著的效能升級。您的應用程式產量會變更好，且使用更少的記憶體。如需進一步瞭解 IBM Java SDK，請查看[這裡](http://www-01.ibm.com/support/docview.wss?uid=swg21671466)。

  # 相關鏈結
  ## 一般
  * [Liberty 執行時期](index.html)
  * [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
