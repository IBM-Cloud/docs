---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

{{site.data.keyword.dev_cli_long}} 提供一種可延伸的指令驅動方式，以使用 `dev` 外掛程式來建立、開發及部署 Web 專案。最理想的狀況是，開發人員在開發端對端微服務應用程式的同時使用指令行控制。

{: shortdesc}

{{site.data.keyword.dev_cli_notm}} 使用兩個容器來協助建置及測試應用程式。第一個是 tools 容器，內含建置及測試應用程式的必要公用程式。此容器的 Dockerfile 是透過 [dockerfile-tools](#command-parameters) 參數所定義。您可以將它視為開發容器，因為它包含的工具一般適用於開發特定運行環境。

第二個容器是 run 容器。例如，此容器的形式適用於部署在 {{site.data.keyword.Bluemix}} 中使用。因此，此容器一般會定義可啟動您應用程式的進入點。當您選擇透過 {{site.data.keyword.dev_cli_short}} 來執行應用程式時，它會使用此容器。此容器的 Dockerfile 是透過 [dockerfile-run](#run-parameters) 參數所定義。


## 新增 {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### 必要條件
{: #prereq}

需要有一些必要條件才能完整地探索及適當地利用 {{site.data.keyword.dev_cli_short}}，因為它可高度延伸，並可讓您運用其他增補技術。

1. 安裝 [Cloud Foundry CLI ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/cloudfoundry/cli#getting-started)。

2. 安裝 [{{site.data.keyword.Bluemix}} CLI ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html)。

3. 取得 [{{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net) ID。

4. 選用項目：如果您打算在本端執行及除錯應用程式，則也必須安裝 [Docker ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.docker.com/get-docker)。 只有針對非行動專案，這才是必要項目。


### 安裝
{: #installation}

1. 執行下列指令，以安裝 [{{site.data.keyword.dev_cli_short}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window}：
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	執行下列指令，以驗證安裝成功：  
 
	```
	bx dev
	```
	{: codeblock}
	

### 開始之前
{: #before-install}
	
1. 登入 {{site.data.keyword.Bluemix_notm}}。

	```
	bx login
	```
	{: codeblock}
	
	**附註：**如果您的認證遭到拒絕，則可以使用「聯合 ID」。請遵循下列步驟，以使用「聯合 ID」來進行鑑別。
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. 登入 [{{site.data.keyword.iamshort}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.bluemix.net/iam/#/apikeys){: new_window}。
	2. 選取**建立 API 金鑰**。
		* 輸入 apiKey 名稱及說明
	3. 下載 apiKey。
	4. 開啟檔案，並複製 `apiKey` 欄位中的值。
	5. 使用下列指令來登入：
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## 指令
{: #commands}

使用下列指令，以建立、部署、除錯及測試專案。

### Build
{: #build}

您可以使用 `build` 指令來建置應用程式。`build-cmd-run` 配置元素是用來建置應用程式。在正常作業期間，`test`、`debug` 及 `run` 指令都會使用與此指令相同的方式來執行建置，因此不需要在這些指令之前執行該指令。

在現行專案目錄中執行下列指令，以建置您的應用程式：  

```
bx dev build
```
{: codeblock}


[Build 指令參數](#command-parameters)


### Code
{: #code}

`code` 指令可讓您在部署之後下載應用程式碼，因此，您可以在本端進行檢閱或進行其他變更。

執行下列指令，以從指定的專案下載程式碼。

```
bx dev code <projectName>
```
{: codeblock}


### Create
{: #create}

提示輸入所有必要資訊（包括語言、專案名稱及應用程式型樣類型），以建立新的專案。將會在現行目錄中建立專案。 

若要在現行專案目錄中建立新專案，並建立服務與它的關聯，請執行下列指令：

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

您可以透過 `debug` 指令來除錯應用程式。會先使用與建置指示相同的 `build-cmd-debug` 配置元素，來完成專案的建置。接著會啟動容器，公開 `container-port-map-debug` 中所定義的除錯埠。請將最愛的除錯工具連接至埠，以如常除錯應用程式。

**限制**：目前無法對 Swift 專案進行除錯。

在現行專案目錄中執行下列指令，以除錯您的應用程式：

```
bx dev debug
```
{: codeblock}	

若要結束除錯階段作業，請使用 `CTRL-C`。


#### Debug 指令參數
{: #debug-parameters}

下列參數是 `debug` 指令特有的，可協助除錯應用程式。

##### `container-port-map-debug`
{: #port-map-debug}

* 除錯埠的埠對映。第一個值是在主機 OS 中使用的埠，第二個則是容器 (host:container) 中的埠。
* 用法：`bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* 用來建置程式碼，以進行除錯。
* 用法：`bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* 用來除錯 tools 容器中的程式碼。如果您的 `build-cmd-debug` 將以除錯模式啟動應用程式，則這是選用項目。
* 用法：`bx dev debug debug-cmd /the/debug/command`

#### 本端應用程式除錯：
{: #local-app-dev}

如需本端應用程式除錯的相關資訊，請參閱[本端應用程式除錯](docs/cloudnative/dev_cli_local_debug.html#local-debug)。


### Delete
{: #delete}

此指令可讓您移除 {{site.data.keyword.Bluemix}} 空間中的專案。

執行下列指令，以刪除 {{site.data.keyword.Bluemix}} 中的專案：

```
bx dev delete <projectName>
```
{: codeblock}
 

**附註**：**不會**移除 {{site.data.keyword.Bluemix}} 服務。


### Help
{: #help}

依預設，如果未傳入動作或引數，或是提供 'help' 動作，則此指令將會顯示一般「說明」文字。所顯示的一般說明會包括基礎引數的說明，以及可用動作清單。  

執行下列指令，以顯示一般說明資訊：

```
bx dev help
```
{: codeblock}


### List
{: #list}

您可以列出空間中的所有 {{site.data.keyword.Bluemix_notm}} 專案。

執行下列指令，以列出您的專案：

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Run
{: #run}

您可以透過 `run` 指令來執行應用程式。會先使用與建置指示相同的 `build-cmd-run` 配置元素，來完成專案的建置。接著會啟動 run 容器，公開 `container-port-map` 中所定義的埠。如果 run 容器未包含完成此步驟的進入點，則可以使用 `run-cmd` 來呼叫應用程式。 

在現行專案目錄中執行下列指令，以啟動您的應用程式：

```
bx dev run
```
{: codeblock}

若要結束階段作業，請使用 `CTRL-C`。


#### Run 參數
{: #run-parameters}

下列參數是 `run` 指令特有的，可協助管理 run 容器內的應用程式。

##### `container-name-run`
{: #container-name-run}
	
* run 容器的容器名稱。
* 用法：`bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* 執行時，容器中要共用的位置。
* 用法：`bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* 執行時，主機系統上容器中要共用的位置。
* 用法：`bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* run 容器的 Docker 檔案。
* 用法：`bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* 要從 dockerfile-run 建立的映像檔。
* 用法：`bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* 用來在 run 容器中執行程式碼的選用參數。如果您的映像檔將會啟動應用程式，則這是選用項目。
* 用法：`bx dev run run-cmd [/the/run/command]`
	
### Status
{: #status}

您可以查詢 `container-name-run` 及 `container-name-tools` 所定義之 {{site.data.keyword.dev_cli_short}} 使用的容器的狀態。 

在現行專案目錄中執行下列指令，以檢查容器狀態：

```
bx dev status
```
{: codeblock}


[Status 指令參數](#command-parameters)


### Stop
{: #stop}

您可以透過 `stop` 指令來停止容器。`container-name` 參數可讓您指定要停止的容器。如果未指定這個項目，則 stop 指令會停止 `container-name-run` 所定義的 run 容器。 

在現行專案目錄中執行下列指令，以停止容器：

```
bx dev stop
```
{: codeblock}


#### 其他 stop 參數： 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* tools 容器的容器名稱。
* 用法：`bx dev stop container-name <demo-tools>` 

### Test
{: #test}

您可以透過 `test` 指令來測試應用程式。會先使用與建置指示相同的 `build-cmd-run` 配置元素，來完成專案的建置。接著會使用 tools 容器，針對應用程式呼叫 `test-cmd`。

執行下列指令，以測試應用程式： 

```
bx dev test
```
{: codeblock}


[Test 指令參數](#command-parameters)


## build、debug、run 及 test 的參數
{: #command-parameters}

下列參數可以與 `build|debug|run|test` 指令搭配使用，並且可以透過指令行以及（或）直接更新專案的 `cli-config.yml` 檔案來指定。其他參數適用於 [`debug`](#debug-parameters) 及 [`run`](#run-parameters) 指令，並且記載於其個別小節中。

**附註**：在指令行上輸入的指令參數，其優先順序高於 `cli-config.yml` 配置。

##### `container-name-tools`  
{: #container-name-tools}

* tools 容器的容器名稱。
* 用法：`bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* 主機上基於建置、除錯、測試而共用的位置。
* 用法：`bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* 容器中基於建置、除錯、測試而共用的位置。
* 用法：`bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* 容器的埠對映。第一個值是在主機 OS 中使用的埠，第二個則是容器 (host:container) 中的埠。
* 用法：`bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* tools 容器的 Docker 檔案。
* 用法：`bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* 要從 dockerfile-tools 建立的映像檔。
* 用法：`bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* 基於所有使用而建置程式碼的指令，但「除錯」除外。
* 用法：`bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* 測試 tools 容器中程式碼的指令。
* 用法：`bx dev <build|debug|run|test> test-cmd [/the/test/command]`

