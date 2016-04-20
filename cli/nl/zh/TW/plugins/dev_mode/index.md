---

 

copyright:

  years: 2015, 2016

 

---
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}


# 開發模型 CLI
{: #devmodecli}

*前次更新：2016 年 2 月 25 日*

開發模型 (dev_mode) 是一項 Bluemix 特性，您可以用來在應用程式於雲端執行時處理應用程式。開發模型包括 dev_mode 指令行介面。dev_mode CLI 建置為 cf CLI 外掛程式，且同時支援 Liberty 和 IBM Node.js 應用程式。

dev_mode CLI 提供下列特性：
- 在開發模式與標準模式之間切換應用程式。
- 漸進式地更新應用程式檔案，而不必進行新的推送。
- 在現有儲存器中啟動、停止或重新啟動應用程式。

## 開始使用
**必要條件：**開始之前，請先安裝 Cloud Foundry CLI。如需詳細資料，請參閱[開始使用 Cloud Foundry 指令行撰寫程式碼](https://github.com/cloudfoundry/cli)。 


使用下列其中一個方法安裝 dev_mode 指令行工具：
- 在本端安裝。
  1. 從 [IBM Bluemix CLI 外掛程式儲存庫](http://plugins.ng.bluemix.net)下載您的平台的 dev_mode 外掛程式。
  2. 使用 cf install-plugin 指令安裝 dev_mode 外掛程式：
  
        ```
        cf install-plugin dev_mode-linux_amd64
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

## 用法
**若要顯示所有 dev_mode CLI 指令，請使用下列指令：**

```
cf plugins
```

### dev_mode 指令

### mode

```
cf mode <appName> <dev|normal>
```

變更應用程式模式。

### status

```
cf status <appName>
```

顯示應用程式模式及執行時期狀態。

### update-file

```
cf update-file <remotePath> <localPath> [command_options]
```

在雲端更新應用程式檔案。

指令選項：

**expand**

指出是否必須從 zip 檔案擷取上傳的檔案。

**restart**

檔案更新之後，重新啟動應用程式執行時期。
  
### delete-file

```
cf delete-file <remotePath> [command_options]
```

在雲端刪除應用程式檔案。

指令選項：

**restart**

檔案刪除之後，重新啟動應用程式執行時期。

### start-inplace

```
cf start-inplace <appName>
```

在現有儲存器中啟動應用程式。

### stop-inplace

```
cf stop-inplace <appName>
```

在現有儲存器中停止應用程式。

### restart-inplace

```
cf restart-inplace <appName>
```

在現有儲存器中重新啟動應用程式。



### help

```
cf help <commandName>
```
顯示指令的相關說明。
