---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用 Dynatrace
{: #using_dynatrace}

*前次更新：2016 年 3 月 23 日*

Dynatrace 是協力廠商服務，可為您的應用程式提供監視功能。

如需 Dynatrace 服務所提供功能的相關資訊，請參閱 [Dynatrace 應用程式監視](http://www.dynatrace.com/en/products/application-monitoring.html)。

當您啟用要與 Liberty 應用程式搭配使用的 Dynatrace 服務時，請遵循下列處理程序步驟：

1. 獲得及管理 Dynatrace 代理程式 Jar 檔，讓 Liberty 建置套件能夠下載它。
2. 設定 Dynatrace 伺服器的實例，讓搭配 Liberty 應用程式執行的 Dynatrace 代理程式可以與它進行通訊。
3. 配置 Liberty 應用程式，讓它可以下載 Dynatrace 代理程式並與 Dynatrace 伺服器進行連線。

## 管理 Dynatrace 代理程式
{: #hosting_dynatrace_agent}
Dynatrace 代理程式必須在 Web 伺服器上進行管理，而 Liberty 建置套件必須能夠從該伺服器下載代理程式 Jar。必須以指定代理程式 Jar 相關詳細資料的 index.yml 檔案來配置伺服器。請完成下列步驟，以設定 Dynatrace 代理程式：
  1. 下載 Dynatrace 代理程式 Jar。請參閱 Dynatrace 社群網站的 [Dynatrace 伺服器平台安裝程式](https://community.dynatrace.com/community/display/EVAL/Step+1+-+Download+and+install+Dynatrace)，以取得下載 Dynatrace 代理程式 Jar 的指示。要在 Bluemix 上執行的適當代理程式 Jar 檔是 **dynatrace-agent-unix.jar** **6.3.0+** 版。
  2. 在 Liberty 建置套件可從中下載它的位置管理代理程式 Jar 檔。您可以使用任何可用的伺服器機能在 Bluemix 上管理它，也可以在某個公用的位置上管理它。
     * 請確定您在該管理位置提供 index.yml 檔案。index.yml 檔案必須包含一個項目，它是由代理程式 Jar 的版本 ID、緊接著的冒號和該代理程式 Jar 位置的完整 URL 所組成。例如：```
      ---
      6.3.0: https://my-dynatrace-agent.mybluemix.net/dynatrace-agent-6.3.0-unix.jar
```  
{: #codeblock}
     * 在 URL 的結尾，Jar 檔的名稱必須是 **dynatrace-agent-version-unix.jar**。版本必須為 **6.3.0** 或 **6.3.0_nnnn**，其中 nnnn 是微指令版本 ID。請注意，這可能與 Dynatrace 使用的 Jar 檔名稱不同，因此您可能需要將 Jar 重新命名。       
     * index.yml 檔案所指定的位置上必須有可用的 **dynatrace-agent-6.3.0-unix.jar** 檔案。Jar 檔和 index.yml 的位置可以是相同的目錄。

## 設定 Dynatrace 收集器

接下來，您必須設定 Dynatrace 代理程式可存取的 Dynatrace 收集器。您也必須建立一個使用者提供的服務來傳遞 Dynatrace 代理程式的資訊，以便與 Dynatrace 收集器進行連線。請參閱 [Dynatrace 架構](https://community.dynatrace.com/community/display/DOCDT63/Architecture)，以更充分地瞭解 Dynatrace 元件之間的關係。

  1. 設定 Dynatrace 收集器。
    * 請參閱 [Dynatrace 社群網站](https://community.dynatrace.com/community/display/EVAL/Step+3+-+Connect+Agent+to+Dynatrace)，以取得下載和設定 Dynatrace 收集器的指示。
    * 請確定收集器是設定在 Dynatrace 代理程式（它與您的應用程式一起在 Bluemix 中執行）可存取的位置中。
  2. 建立一個使用者提供的服務來指向執行中的 Dynatrace 收集器。例如，使用下列指令：
<pre>
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring"}'
</pre>
{: #codeblock}
在這個範例中，DynatraceCollectorIPaddress 是您已配置的 Dynatrace 收集器的 IP 位址，而 profile 是與此受監視應用程式相關聯的選用 Dynatrace 設定檔名稱。預設設定檔值是 Monitoring。您可以指定選用的參數，如下列範例所示。
<pre>
    $ cf cups my-dynatrace-collector -p '{"server":"DynatraceCollectorIPaddress","profile":"Monitoring",
                                          "options" : {
                                                       "dynatrace-parameter-1": "value",
                                                       "dynatrace-parameter-2": "value"
                                         }}'
</pre>
{: #codeblock}
如需可用選項的相關資訊，請參閱 Dynatrace 社群網站的[代理程式配置的代理程式設定區段](https://community.dynatrace.com/community/display/DOCDT62/Agent+Configuration)。例如，使用排除選項，您可以排除類別使其不受 Dynatrace 監視。如需配置使用者所提供服務的相關詳細資料，請參閱 [DynaTrace 代理程式架構](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/framework-dynatrace-agent.md)。
  3. 將您的應用程式推送到 Bluemix 之後，請將您建立的使用者所提供服務連結到該應用程式。例如，使用下列指令：
<pre>
    $ cf bs myApp my-dynatrace-service
</pre>  
**附註**：您必須在連結該服務之後重新編譯打包應用程式。

## 配置 Liberty 應用程式
{: #configuring_liberty_app}

必須配置您要監視的 Liberty 應用程式，才能找出管理您先前設定的代理程式 Jar 的伺服器。您可以使用 **JBP_CONFIG_DYNATRACEAGENT** 環境變數配置應用程式。**JBP_CONFIG_DYNATRACEAGENT** 環境變數告知建置套件從何處下載 Dynatrace 代理程式。若要設定此環境變數，請完成下列步驟：
<ol>
   <li> 將 **JBP_CONFIG_DYNATRACEAGENT** 變數的值設為 *"repository_root：URL_of_server_hosting_index.yml"*。例如，在推送您的應用程式之後發出下列指令：
<pre>   
    $ cf se myApp JBP_CONFIG_DYNATRACEAGENT 'repository_root: https://my-dynatrace-agent-host.mybluemix.net'
</pre>
{: #codeblock}
在這個範例中，*my-dynatrace-agent-host.mybluemix.net* 是您先前配置的伺服器所管理的 index.yml 檔案的 URL。
 </li>
  <li> 在設定此環境變數之後，請重新編譯打包您的應用程式。Liberty 應用程式的 staging_task.log 會發出一則訊息，指出從代理主機管理伺服器順利下載了 Dynatrace 代理程式。例如：<pre>
    Downloading dynatrace-agent-6.3.0-unix.jar 6.3.0 from https://my-dynatrace-agent-host.mybluemix.net/dynatrace-agent-6.3.0-unix.jar (17.8s)
</pre>
{: #codeblock}
</li>
<li>若要查看 staging_task.log，請發出下列指令：
<pre>
    $ cf files myAppName logs/staging_task.log
</pre>  
{: #codeblock}
</li>
</ol>

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
