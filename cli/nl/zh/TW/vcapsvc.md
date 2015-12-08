
{:shortdesc: .shortdesc}

# VCAP 服務

*前次更新：2015 年 11 月 9 日*


VCAP_SERVICES 環境變數是含有資訊的 JSON 物件，而您可以使用這項資訊來與
{{site.data.keyword.Bluemix_notm}} 中的服務實例互動。{:shortdesc}


## 擷取 VCAP_SERVICES 環境變數的值
{:retrieving}

VCAP_SERVICES 環境變數是含有資訊的 JSON 物件，而您可以使用這項資訊來與
{{site.data.keyword.Bluemix_notm}} 中的服務實例互動。這項資訊包括服務實例的服務實例名稱、認證及連線 URL。將應用程式連結至 {{site.data.keyword.Bluemix_notm}} 中的服務實例時，會將這些值移入 VCAP_SERVICES 環境變數中。

只有在將服務實例連結至應用程式時，才能使用 VCAP_SERVICES 環境變數的值。您可以使用 WebSocket 主控台驅動程式來檢視應用程式環境變數。下列範例顯示如何使用 WebSocket 主控台驅動程式來檢視 Node.js 應用程式的環境變數。

首先，執行指令來重新推送 Node.js 應用程式。```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp```
接下來，輸入下列 URL：```
https://yourapp.{APPDomain}/bash.sh
```
在顯示的頁面中，按一下勾號以連接工具，然後發出 env 指令來查看應用程式的環境變數。如需 cf-debug-tools 的相關資訊，請參閱 [Debug Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools)。


## 檢視 Bluemix 基礎架構層
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} 會抽出並隱藏作業系統與基礎架構層，因此您不需要管理它們。不過，您有時可能想要為了您的應用程式而更瞭解作業系統及中介軟體。

您可以執行 cf stacks 指令以顯示可用的堆疊（或根檔案系統），您的應用程式即將部署到該處。您也可以在使用 cf push 指令時，以 *-s* 選項和 *stack_name* 指定堆疊，其中 stack_name 是根檔案系統，例如 `lucid64` 或 `cflinuxfs2`：
```
cf push appName -s stack_name
```
您可以使用 `cf buildpacks` 指令來顯示中介軟體元件，例如 WebSphere Liberty 設定檔和 SDK for Node.js，這些可用來作為您應用程式在其中執行的執行時期。您也可以使用下列指令為您的應用程式指定執行時期環境：
```
cf push appName -b buildpackname
```
