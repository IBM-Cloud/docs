---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# 自動配置已連結的服務
{: #auto_config}

*前次更新：2016 年 3 月 31 日*

您可以將各種服務連結到您的 Liberty 應用程式。依據開發人員的需求，服務可以由儲存器管理及/或由應用程式管理。

應用程式管理的服務是完全由應用程式管理的服務，沒有任何來自 Liberty 的協助。應用程式一般會讀取 VCAP_SERVICES，以取得已連結服務的相關資訊，並直接存取該服務。應用程式提供了所有必要的用戶端存取程式碼。與 Liberty 特性或 server.xml 檔案配置沒有任何相依關係。Liberty 建置套件自動配置不適用於此類型的服務。


儲存器管理的服務是由 Liberty 執行時期管理的服務。在某些情況下，應用程式可能會在 JNDI 中查閱已連結的服務，而在其他情況下，Liberty 會自己直接使用服務。Liberty 建置套件會讀取 VCAP_SERVICES，以取得已連結服務的相關資訊。針對每一個儲存器管理的服務，建置套件會執行三項功能。

* 為連結的服務產生[雲端變數](optionsForPushing.html#accessing_info_of_bound_services)。
* 安裝 Liberty 特性及存取連結服務所需的用戶端存取程式碼。
* 產生或更新服務所需的 server.xml 檔案段落。

這個處理程序稱為自動配置。Liberty 建置套件提供下列服務類型的自動配置：

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* ClearDB MySQL Database
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

如前所述，部分服務可以由應用程式管理，也可以由儲存器管理。Mongo 和 SQLDB 便是此類服務的範例。依預設，Liberty 建置套件會假設這些服務是由儲存器管理，並自動加以配置。
如果您要讓應用程式管理服務，則可以設定 services_autoconfig_excludes 環境變數，拒絕自動配置服務。如需相關資訊，請參閱[拒絕服務自動配置](autoConfig.html#opting_out)。

## 安裝 Liberty 特性及用戶端存取程式碼
{: #installation_of_liberty_features}

當您連結至儲存器管理的服務時，該服務可能會要求得在 server.xml 檔案的 featureManager 段落中配置 Liberty 特性。Liberty 建置套件會更新 featureManager 段落，並安裝必要的支援二進位檔。如果服務需要用戶端驅動程式 Jar，會將 Jar 下載到 Liberty 安裝中的已知位置。

如需詳細資料，請參閱已連結之服務類型的文件。

## 產生或更新 server.xml 配置段落
{: #generating_or_updating_serverxml}

當您推送獨立式應用程式時，Liberty 建置套件會如[推送 Liberty 應用程式的選項](optionsForPushing.html#options_for_pushing)中所述，產生 server.xml 段落。當您推送獨立式應用程式並連結至儲存器管理的服務時，Liberty 建置套件會為已連結的服務產生必要的 server.xml 段落。

當您提供 server.xml 檔案並連結至儲存器管理的服務時，Liberty 建置套件會執行下列動作：

* 如果所提供的 server.xml 檔案不包含已連結服務的配置段落，則會為已連結的服務產生配置。
* 如果所提供的 server.xml 檔案包含已連結服務的配置段落，則會為已連結的服務更新配置。

如需詳細資料，請參閱已連結之服務類型的文件。

## 拒絕服務自動配置
{: #opting_out}

在某些情況下，您可能會不想讓 Liberty 建置套件自動配置已連結的服務。請考慮下列情境。

* 我的應用程式使用 MongoDB，但我想要應用程式直接管理資料庫連線。應用程式中包含必要的用戶端驅動程式 jar。我不想讓 Liberty 建置套件自動配置 Mongo 服務。
* 我有提供 server.xml 檔案，而且已經為 SQLDB 實例提供配置段落，因為我需要非標準的資料來源配置。我不想要 Liberty 建置套件更新我的 server.xml 檔案，但是我仍然需要 Liberty 建置套件確定已經安裝適當的支援軟體。

若要拒絕自動服務配置，請使用 services_autoconfig_excludes 環境變數。您可以在 manifest.yml 中包含此環境變數，或使用 cf 用戶端設定它。

您可以針對每個服務類型來拒絕服務的自動配置。您可以選擇完全拒絕（例如在 Mongo 情境中）或只拒絕 server.xml 檔案配置更新（例如在 SQLDB 情境中）。您為 services_autoconfig_excludes 環境變數指定的值是字串，如下所示。

* 字串可以包含一個以上服務的拒絕規格。
* 特定服務的拒絕規格是 service_type=option，其中：
  * service_type 是 VCAP_SERVICES 中所顯示的服務標籤。
  * option 是 all 或 config。
* 如果字串包含多個服務的拒絕規格，則必須以單一空格字元隔開個別拒絕規格。

更正式地說，字串的文法如下。

```
    Opt_out_string :: <service_type_specification[<delimiter>service_type_specification]*
    <service_type_specification> :: <service_type>=<option>
    <service_type> :: service type（如同 VCAP_SERVICES 中顯示的服務標籤）
    <option> :: all | config
    <delimiter> :: one white space character
```
{: #codeblock}

**重要事項**：您指定的服務類型必須符合出現在 VCAP_SERVICES 環境變數中的服務標籤。不接受空格。**重要事項**：在 &lt;service_type_specification> 內不接受空格。唯一接受使用空格的情況是要隔開多個 &lt;service_type_specification> 實例。

使用 "all" 選項可拒絕服務的所有自動配置動作，如同上述的 Mongo 情境。使用 "config" 選項只拒絕配置更新動作，如同上述的 SQLDB 情境。

以下是 manifest.yml 檔案中用於 Mongo 和 SQLDB 情境的拒絕規格範例。

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

以下是如何使用指令行介面來為 myapp 應用程式設定 services_autoconfig_excludes 環境變數的範例。

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
