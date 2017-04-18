---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 記載和追蹤
{: #logging_tracing}

## 日誌檔
{: #log_files}

IBM Bluemix 中有標準 Liberty 日誌可供使用，例如 messages.log 或 ffdc 目錄，它們位於每一個應用程式實例的 logs 目錄中。這些日誌可以從 IBM Bluemix 主控台或使用 cf logs 和 cf files 指令進行存取。例如，若要查看 messages.log 檔案，請執行下列指令：

```
$ cf files <yourappname> logs/messages.log
```
{: codeblock}

您可以透過 Liberty 配置檔來設定記載層次和其他追蹤選項。如需相關資訊，請參閱 [Liberty 設定檔：記載和追蹤](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0)。也可以使用 IBM Bluemix 主控台，在執行中的應用程式實例調整追蹤。

## 使用 trace 及 dump 功能
{: #using_trace_and_dump}

在 IBM Bluemix 使用者介面中，有 trace 及 dump 功能。
* 使用 Trace 可以檢視及更新執行中之應用程式實例上的 Liberty 記載 traceSpecification。
* 使用 Dump 可以在執行中應用程式實例上建立執行緒與資料堆傾出。

若要執行此動作，請在使用者介面中選取 Liberty 應用程式。在導覽中的「運行環境」種類中，您可以開啟實例詳細資料。
請選取一個或多個實例。在「動作」功能表中，您可以選擇 TRACE 或 DUMP。

## 下載傾出檔案
{: #download_dumps}

<strong>必要條件：</strong>
* [安裝 CF CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* 如果您的應用程式在 Diego 中執行，請[安裝 Diego-Enabler 外掛程式](https://github.com/cloudfoundry-incubator/Diego-Enabler)

<strong>如果您的應用程式在 DEA 中執行，請使用下列步驟：</strong>
  
1. 取得 app_guid
```
$ cf app <app_name> --guid
```

2. 下載傾出檔案
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>如果您的應用程式在 Diego 中執行，請使用下列步驟：</strong>
  
1. 取得 app_guid
```
$ cf app <app_name> --guid
```

2. 取得 app_ssh_endpoint（主機和埠）及 app_ssh_host_key_fingerprint
```
$ cf curl /v2/info
```

3. 取得 scp 指令的 ssh-code
```
$ cf ssh-code
```

4. scp 遠端傾出檔案到本端，並在提示輸入密碼時使用 ssh-code
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

如需詳細資料，請參閱[使用 SSH 存取應用程式](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)


# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [Liberty 運行環境](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

