---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 New Relic
{: #new_relic}

*前次更新：2016 年 3 月 23 日*

New Relic 是協力廠商服務，可為您的應用程式提供監視度量值。如需 New Relic 服務提供項目的相關資訊，請參閱 [New Relic](http://newrelic.com/java)。

根據這份 [Java agent manual installation](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation) 文件，要使用 New Relic 服務監視的 Java 應用程式通常需要進行組合，並配置 New Relic 代理程式和帳戶授權碼。在 IBM Bluemix 環境中，透過在 IBM Bluemix 中建立服務實例，即可取得 New Relic 授權合約和帳戶。然後，Java 應用程式就可以連結至 New Relic 服務實例，且 Liberty 建置套件會自動配置已準備好讓 New Relic 服務監視的應用程式。具體而言，建置套件會：

* 提供應用程式與 New Relic 代理程式。
* 從 VCAP_APPLICATION 和 VCAP_SERVICES 應用程式環境變數取得應用程式名稱和授權碼。
* 配置 New Relic 代理程式所需的內容和配置範本。

請參閱 Liberty 建置套件為應用程式產生的配置範例：

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## 新增 New Relic 服務
{: #add_new_relic}

對於要在 IBM Bluemix 中使用 New Relic 監視的現有 Java 應用程式，請遵循下列步驟。
1. 在 IBM Bluemix 中建立 New Relic 服務實例。
```
    $ cf create-service newrelic standard mynewrelic
```
{: #codeblock}

2. 使用 New Relic 服務，將您的應用程式部署至 IBM Bluemix。請參閱下列範例應用程式資訊清單：
```
        ---
        applications:
        - name: myapp
          memory: 1G
          instances: 1
          host: myapp
          domain: mybluemix.net
          path: myapp.war
          services:
          - mynewrelic
```
{: #codeblock}

3. 直接從您應用程式的 IBM Bluemix 儀表板，存取應用程式的 New Relic 儀表板。

### 新增使用者提供的 New Relic 服務
{: #add_user_provided_new_relic}

如果您有現有的 New Relic 帳戶和授權碼，可以利用「使用者提供的服務」，將現有的 New Relic 服務連結至應用程式。

1. 使用現有的授權碼來建立使用者提供的服務實例。例如，如果您現有的授權碼是 1234567，則可以使用 CF CLI 來進行 "create-user-provided-service"，並在出現提示時提供授權碼 1234567，如下所示：
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. 利用使用者提供的 New Relic 服務實例，將您的應用程式部署至 IBM Bluemix。以下是利用使用者提供的 New Relic 服務實例的範例應用程式資訊清單：
```
        ---
        applications:
        - name: myapp
          memory: 1G
          instances: 1
          host: myapp
          domain: mybluemix.net
          path: myapp.war
          services:
          - mynewrelic
```
{: #codeblock}

3. 存取 New Relic 儀表板以檢視應用程式度量值。

New Relic 服務的自動配置不同於其他服務的自動配置，因為它是透過建置套件架構來提供的儲存器管理服務。因為是透過該架構來提供，所以此服務的自動配置與其他服務有三點不同：
* 無法選擇拒絕。
* 服務整合仰賴 New Relic 的代理程式，這是一個 Java 代理程式。因此，它是透過 Java 選項來配置，而不是 server.xml 檔案中的雲端變數。
* 配置同時仰賴 VCAP_SERVICES 和 VCAP_APPLICATION。

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
