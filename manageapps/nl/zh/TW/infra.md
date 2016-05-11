---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Bluemix 基礎架構層

*前次更新：2016 年 3 月 15 日*

{{site.data.keyword.Bluemix_notm}} 會抽象化並隱藏作業系統與基礎架構層，因此您不需要管理它們。不過，您有時可能會想要更瞭解適用於您應用程式的作業系統及中介軟體。
{:shortdesc}

## 檢視 Bluemix 基礎架構層
{:viewinfra}

您可以執行 cf stacks 指令，顯示您的應用程式即將部署至該處的可用堆疊（或根檔案系統）。您也可以在使用 cf push 指令時，以 *-s* 選項和 *stack_name* 指定堆疊，其中 stack_name 是根檔案系統，例如 `lucid64` 或 `cflinuxfs2`：
```
cf push appName -s stack_name
```
您可以使用 `cf buildpacks` 指令來顯示中介軟體元件，例如 WebSphere Liberty 設定檔和 SDK for Node.js，這些可用來作為您應用程式執行所在的執行時期。您也可以使用下列指令為您的應用程式指定執行時期環境：
```
cf push appName -b buildpackname
```
