---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 記載和追蹤
{: #logging_tracing}

## 日誌檔
{: #log_files}

IBM Bluemix 中提供標準 Liberty 日誌，例如 `messages.log` 或 `ffdc` 目錄，它們位於每一個應用程式實例的 `logs` 目錄中。這些日誌可以從 IBM Bluemix 主控台或透過 CF CLI 進行存取。例如：

* 若要存取應用程式的最新日誌，請執行下列指令：

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* 若要查看執行於 DEA 節點上之應用程式的 `messages.log` 檔案，請執行下列指令：

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* 若要查看執行於 Diego cell 上之應用程式的 `messages.log` 檔案，請執行下列指令：

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

您可以透過 Liberty 配置檔來設定記載層次和其他追蹤選項。如需相關資訊，請參閱 [Liberty 設定檔：記載和追蹤](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)。也可以使用 IBM Bluemix 主控台，在執行中的應用程式實例調整追蹤。

## 使用 trace 及 dump 功能
{: #using_trace_and_dump}

您可以直接從 IBM Bluemix 主控台調整執行中應用程式的 Liberty 追蹤配置。此主控台也會提供要求與下載執行緒及資料堆傾出的功能。若要調整追蹤配置或要求傾出，請在 Bluemix 主控台中選取 Liberty 應用程式，然後選擇導覽中的「運行環境」功能表。在「運行環境」視圖中，選取實例，然後按*追蹤* 或*傾出* 按鈕。若要調整追蹤層次，請參閱 [Liberty 設定檔：追蹤和記載](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)，以取得追蹤規格語法的詳細資料。

### Diego：透過 SSH 觸發傾出

針對執行於 Diego cell 中的應用程式，也可以使用 SSH 特性，透過 CF CLI 觸發執行緒及資料堆傾出。例如：

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

如需下載已產生之傾出檔案的詳細資料，請參閱下面的文件。

## 下載傾出檔案
{: #download_dumps}

各種傾出檔案預設會放在應用程式容器的 `dumps` 目錄中。

### DEA 應用程式

針對執行於 DEA 節點中的應用程式，使用 "cf files" 功能來檢視及下載傾出檔案。

* 若要查看已產生的傾出，請執行下列指令：

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* 若要下載傾出檔案，請執行下列指令：

    1. 取得應用程式 GUID

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. 下載傾出檔案

      ```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```
      {: codeblock}

### Diego 應用程式

針對執行於 Diego cell 中的應用程式，使用 "cf ssh" 功能來檢視及下載傾出檔案。

* 若要查看已產生的傾出，請執行下列指令：

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* 若要下載傾出檔案，請執行下列指令：

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

您也可以使用 `scp` 及其他類似工具來檢視及下載傾出檔案。如需相關資訊，請參閱[使用 SSH 存取應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)。

# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty 運行環境](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
