---



copyright:

  years: 2015，2017

lastupdated: "2017-01-12"



---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# （已淘汰）開發模式 CLI
{: #devmodecli}

**這個 CLI 已淘汰：**請不要使用開發模式 (dev_mode) CLI，而是改用 IBM Eclipse Tools for Bluemix 或 DevOps Web IDE。您可以繼續使用 dev_mode CLI 到 2016 年 6 月 30 日止。

您可以使用 Bluemix 開發模式指令行介面 (dev_mode CLI)，在應用程式於雲端執行時更新應用程式。dev_mode CLI 建置為 cf CLI 外掛程式，且同時支援 Liberty 和 IBM Node.js 應用程式。
{: shortdesc}


您可以使用 dev_mode CLI 來執行下列作業：
- 在開發模式與標準模式之間切換應用程式。
- 漸進式地更新應用程式檔案，而不必進行新的推送。
- 在現有容器中啟動、停止或重新啟動應用程式。

## 安裝 dev_mode 外掛程式
**必要條件：**開始之前，請先安裝 Cloud Foundry CLI。如需詳細資料，請參閱[開始使用 Cloud Foundry 指令行介面撰寫程式碼](https://github.com/cloudfoundry/cli)。


使用下列其中一個方法安裝 dev_mode 指令行工具：
- 在本端安裝。
  1. 從 [IBM Bluemix CLI 外掛程式儲存庫](http://plugins.ng.bluemix.net)下載您的平台的 dev_mode 外掛程式。
  2. 移至儲存 dev_mode 外掛程式的資料夾，然後使用 cf install-plugin 指令來安裝 dev_mode 外掛程式。例如：

        ```
cf install-plugin dev_mode-linux64
        ```

- 從 Bluemix CLI 儲存庫安裝。
  1. 使用下列指令將 bluemix-repo 儲存庫新增至 Cloud Foundry CLI 儲存庫：

        ```
cf add-plugin-repo bluemix-repo http://plugins.ng.bluemix.net
        ```

  2. 鍵入 cf repo-plugins。dev_mode 外掛程式會出現在 bluemix-repo 儲存庫中。

		```
cf repo-plugins
        ```

  3. 使用下列指令將 dev_mode 外掛程式安裝至 Cloud Foundry CLI 外掛程式：

        ```
cf install-plugin dev_mode -r bluemix-repo
        ```

## 檢視 dev_mode 指令

若要顯示所有 dev_mode CLI 指令，請使用下列指令：

```
cf plugins
```

## dev_mode CLI 指令索引
{: #dev_mode_cmds_index}

使用下表中的索引來參照常用的 dev_mode CLI 指令：

<table summary="dev_mode 指令索引">
 <caption>表格 1. dev_mode 指令</caption>
 <thead>
 <th colspan="4">dev_mode 指令</th>
 </thead>
 <tbody>
 <tr>
 <td>[help](#help)</td>
 <td>[mode](#mode)</td>
 <td>[status](#status)</td>
 <td>[update-file](#update_file)</td>
 </tr>
 <tr>
 <td>[delete-file](#delete_file)</td>
 <td>[start-inplace](#start_inplace)</td>
 <td>[stop-inplace](#stop_inplace)</td>
 <td>[restart-inplace](#restart_inplace)</td>
 </tr>
  </tbody>
 </table>


## help
{: #help}

顯示指令的相關說明。

```
cf help <commandName>
```


## mode
{: #mode}

變更應用程式模式。

```
cf mode <appName> <dev|normal>
```
<strong>指令選項</strong>：<dl>
   <dt>dev</dt>
   <dd>開發模式。</dd>
   <dt>normal</dt>
   <dd>正式作業模式。</dd>
   </dl>


## status
{: #status}

顯示應用程式模式及運行環境狀態。
```
cf status <appName>
```



## update-file
{: #update_file}

在雲端更新應用程式檔案。

```
cf update-file <remotePath> <localPath> [command_options]
```


<strong>指令選項</strong>：

   <dl>
   <dt>expand</dt>
   <dd>指出是否必須從 zip 檔案擷取上傳的檔案。</dd>
   <dt>restart</dt>
   <dd>檔案更新之後，重新啟動應用程式運行環境。</dd>
   </dl>



## delete-file
{: #delete_file}

在雲端刪除應用程式檔案。

```
cf delete-file <remotePath> [command_options]
```


<strong>指令選項</strong>：
 <dl>
   <dt>restart</dt>
   <dd>檔案更新之後，重新啟動應用程式運行環境。</dd>
  </dl>


## start-inplace
{: #start_inplace}
在現有容器中啟動應用程式。

```
cf start-inplace <appName>
```



## stop-inplace
{: #stop_inplace}
在現有容器中停止應用程式。

```
cf stop-inplace <appName>
```



## restart-inplace
{: #restart_inplace}

在現有容器中重新啟動應用程式。

```
cf restart-inplace <appName>
```



# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}
* [Development mode CLI ![外部鏈結圖示](../../../icons/launch-glyph.svg)](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){:new_window}
* [DevOps Web IDE ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://hub.jazz.net/docs/deploy/){:new_window}
