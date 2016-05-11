---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 建置套件預設值
{: #buildpack_defauts}

*前次更新：2016 年 3 月 23 日*

Liberty 建置套件在 Bluemix 中經常更新。
每個版本都可能包含安全修正程式或特性加強功能。

建置套件針對 WAR 或 EAR 應用程式的 Java 版本或 Liberty 特性集等設定具有預設值。部分預設值可能視建置套件版本不同而變更，這可能會對應用程式有不利的影響。為了避免應用程式受到建置套件預設值變更的影響，請採取步驟來配置您的應用程式，避免依賴建置套件預設值。


## Liberty 特性
{: #liberty_features}

當您部署 WAR 或 EAR 檔時，建置套件會提供應用程式的配置，以及一組預設的 Liberty 特性。雖然很少見，但該組預設的
Liberty 特性可能會視建置套件版本不同而變更。
預設特性集的變更可能會對應用程式有不利的影響。
可設定一些選項來確定應用程式不會受到特性預設值變更的影響。


* 設定 JBP_CONFIG_LIBERTY 環境變數，以明確指定應用程式的已啟用特性清單。如需相關資訊，請參閱[獨立式應用程式](optionsForPushing.html#stand_alone_apps)。
* 部署應用程式作為[伺服器目錄](optionsForPushing.html#server_directory)或[包裝伺服器](optionsForPushing.html#packaged_server)。提供自訂的 server.xml 檔案，其中指定應用程式確切需要的特性集。

部署為伺服器目錄或包裝伺服器的應用程式，不會受到 Liberty 特性預設值變更的影響。


## Java 版本
{: #java_version}

建置套件提供應用程式的預設
JRE。JRE 的主要或次要版本可能會視建置套件版本不同而變更。JRE 的次要版本可能會經常更新，主要版本則很少更新。JRE 主要版本的變更可能會對應用程式有不利的影響。


為確保應用程式不受主要版本變更的影響，請以適當的 JRE 版本來設定環境變數，如[自訂 JRE](customizingJRE.html) 中所述。為求最佳結果，請針對您的應用程式採用 Java 8。

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
