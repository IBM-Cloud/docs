---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 部署應用程式
{: #deployingapps}

若要將應用程式部署至 {{site.data.keyword.Bluemix}}，您可以使用各種方式，例如，指令行介面及整合開發環境 (IDE)。還可以使用應用程式資訊清單來部署應用程式。使用應用程式資訊清單，可讓您減少每次將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，所必須指定的部署詳細資料數量。
{:shortdesc}

## 應用程式部署
{: #appdeploy}

將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 包含兩個階段：編譯打包應用程式及啟動應用程式。

Cloud Foundry 支援 Diego，Diego 是新的預設運行環境架構，可提供一組功能來增強用於管理及建構雲端平台的應用程式開發體驗。此架構更新可改善 Cloud Foundry 平台的整體作業及效能。新的架構支援數個應用程式容器技術（包括 Garden 及 Windows）、一個容許直接登入應用程式容器的 SSH 套件，以及其他創新變更。如需最新架構升級的相關資訊，請參閱 [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![外部鏈結圖示](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}。


您建立的所有新應用程式都會在 Diego 上執行，而且您必須開始將 DEA 上執行的現有應用程式移轉至新的 Diego 架構。

**附註**：Cloud Foundry Diego 架構會影響所有「{{site.data.keyword.Bluemix_notm}} 公用」地區環境。稍後將會更新「{{site.data.keyword.Bluemix_notm}} 專用」及「{{site.data.keyword.Bluemix_notm}} 本端」環境。

### 編譯打包應用程式
{: #diego}

在編譯打包階段期間，Diego 會處理所有與應用程式容器編排相關的層面。當您推送應用程式時，Cloud Controller 會將編譯打包要求傳送給 Diego，而 Diego 會處理應用程式實例的配置作業。Diego 後端會透過確保容錯及長期一致性的方式來編排應用程式容器，以平衡一系列虛擬機器（稱為儲存格）的負載。此外，Diego 確保使用者可以存取其應用程式的日誌。所有 Diego 元件的設計旨在叢集化，表示您可以建立不同的可用性區域。

為了驗證應用程式性能，Diego 支援之前用於 DEA 的相同 PORT 型檢查。不過，Diego 的設計也可以具有更多的一般選項（如 URL 型性能檢查），未來可能會啟用這些選項。

#### 編譯打包新的應用程式
{: #stageapp}

所有新的應用程式都會部署至 Diego 架構。若要編譯打包新的應用程式，請使用 **cf push** 指令來部署應用程式：

  1. 部署應用程式：
  ```
  $ cf push APPLICATION_NAME
  ```

如需 **cf push** 指令的詳細資料，請參閱 [cf push](/docs/cli/reference/cfcommands/index.html#cf_push)。

### 將現有應用程式移轉至 Diego
{: #migrateapp}

Diego 是 {{site.data.keyword.Bluemix_notm}} 的預設 Cloud Foundry 架構，將移除 DEA 支援，因此您必須更新每一個應用程式來移轉所有現有應用程式。請開始將應用程式移轉至 Diego，方法是使用 Diego 旗標來更新應用程式。應用程式會立即嘗試開始在 Diego 上執行，並停止在 DEA 上執行。 

因為您的應用程式是從 DEA 架構更新為 Diego，所以如果應用程式與 Diego 不相容，您可能會經歷短時間的關閉或長時間的關閉。若要限制關閉時間，請執行[藍綠部署](/docs/manageapps/updapps.html#blue_green)，方法是將應用程式副本部署至 Diego，然後交換路徑並縮減 DEA 應用程式。

完成下列步驟，以將應用程式移轉至 Diego：

 1.  安裝 [cf CLI ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 及 [Diego-Enabler CLI 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}。
 2. 檢閱[已知問題清單](depapps.html#knownissues)。
 3. 設定 Diego 旗標，以將應用程式變更為在 Diego 上執行：
  ```
  $ cf enable-diego APPLICATION_NAME
  ```

更新您的應用程式之後，請確認您的應用程式已啟動。如果您的已移轉應用程式無法啟動，則除非您識別及解決問題，然後重新啟動應用程式，否則應用程式會保持離線。

IBM 會在移除 DEA 架構支援時，警示您即將發生必要移轉，如果您尚未移轉應用程式，則作業團隊將會移轉所有應用程式。
  
若要驗證應用程式是在哪個後端上執行，請使用下列指令：

  ```
  $ cf has-diego-enabled APPLICATION_NAME
  ```

#### Diego 移轉已知問題
{: #knownissues}

將應用程式移轉至 Diego 時，下列是需要解決的已知問題：

  * 使用 `--no-route` 選項部署的工作者應用程式不會報告為健全。若要防止此問題，請使用 `cf set-health-check APP_NAME none` 指令，停用埠型性能檢查。
  * 不再支援 **cf files** 指令。**cf ssh** 指令將取而代之。如需 **cf ssh** 指令的詳細資料，請參閱 [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)。
  * 部分應用程式可能使用大量的檔案描述子 (inode)。如果發生此問題，您必須使用 `cf scale APP_NAME [-k DISK]` 指令，增加應用程式的磁碟限額。

如需完整的已知問題清單，請參閱 [Migrating to Diego ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window} 的 Cloud Foundry 文件頁面。

除非舊 DEA 架構支援已被移除，否則您可以執行下列指令來轉移回 DEA：`cf disable-diego APPLICATION_NAME`。除非支援已被移除，否則您還是可以將新的應用程式部署至 DEA 架構：

**附註**：您必須已安裝 [cf CLI ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} 及 [Diego-Enabler CLI 外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}，才能使用 `disable-diego` 指令。

1. 部署應用程式而不啟動它：
```
$ cf push APPLICATION_NAME --no-start
```
2. 執行 disable-diego 指令：
```
$ cf disable-diego APPLICATION_NAME
```
3. 啟動應用程式：
```
$ cf start APPLICATION_NAME
```

### 啟動應用程式
{: #startapp}

啟動應用程式時，即會建立應用程式容器實例。針對在 Diego 上執行的應用程式，您可以使用 **cf ssh** 或 **cf scp** 指令來存取包括日誌之應用程式容器的檔案系統。**cf files** 指令不適用於在 Diego 架構上執行的應用程式。

**附註**：如果您仍然有在 DEA 上執行的應用程式，則除非 DEA 支援已被移除，否則可以使用 **cf files** 指令來檢視應用程式容器內的檔案。

如果應用程式無法啟動，則會停止該應用程式，並移除應用程式容器的所有內容。因此，如果應用程式停止或應用程式的編譯打包處理程序失敗，您將無法使用日誌檔。

如果應用程式的日誌不再可用，也就無法再使用 **cf ssh**、**cf scp** 或 **cf files** 指令來查看應用程式容器內編譯打包錯誤的原因，您可以改用 **cf logs** 指令。**cf logs** 指令使用 Cloud Foundry 日誌聚集器來收集應用程式日誌及系統日誌的詳細資料，而且您可以看見在日誌聚集器中緩衝的項目。如需日誌聚集器的相關資訊，請參閱 [Logging in Cloud Foundry ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}。

**附註：**緩衝區大小有限制。如果應用程式執行一段很長的時間且未重新啟動，則當您輸入 `cf logs appname --recent` 指令時可能不會顯示日誌，因為日誌緩衝區可能已被清除。因此，若要針對大型應用程式編譯打包錯誤進行除錯，您可以在不同於 cf 指令行介面的個別指令行中輸入 `cf logs appname` 指令，以在部署應用程式時追蹤日誌。

如果您在 {{site.data.keyword.Bluemix_notm}} 中編譯打包應用程式時遇到問題，可以遵循[針對編譯打包錯誤進行除錯](/docs/debug/index.html#debugging-staging-errors)中的步驟來解決問題。


## 使用 cf 指令來部署應用程式
{: #dep_apps}

從指令行介面將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，必須依據您的應用程式語言及架構，提供建置套件作為運行環境。您也可以使用 Delivery Pipeline 服務，將應用程式部署至 {{site.data.keyword.Bluemix_notm}}。

{{site.data.keyword.Bluemix_notm}} 提供支援 Java 及 Node.js 的內建建置套件。如果您是使用這些語言及架構，則在使用指令行介面來部署應用程式時，不需要指定建置套件。因為 {{site.data.keyword.Bluemix_notm}} 是建置在 Cloud Foundry 上，所以指令預設為這些建置套件。

如果您使用外部建置套件，則必須在從命令提示字元將應用程式部署至 {{site.data.keyword.Bluemix_notm}} 時，使用 **-b** 選項來指定建置套件的 URL。

  * 若要將 Liberty 伺服器套件部署至 {{site.data.keyword.Bluemix_notm}}，請從來源目錄中使用下列指令：

  ```
cf push
  ```

  如需「Liberty 建置套件」的相關資訊，請參閱 [Liberty for Java](/docs/runtimes/liberty/index.html)。

  * 若要將 Java Tomcat 應用程式部署至 {{site.data.keyword.Bluemix_notm}}，請使用下列指令：

  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```

  * 若要將 WAR 套件部署至 {{site.data.keyword.Bluemix_notm}}，請使用下列指令：

  ```
  cf push appname -p app.war
  ```
  或者，您可以使用下列指令來指定包含應用程式檔案的目錄：

  ```
  cf push appname -p "./app"
  ```

  * 若要將 Node.js 應用程式部署至 {{site.data.keyword.Bluemix_notm}}，請使用下列指令：

  ```
  cf push appname -p app_path
  ```

`package.json` 檔案必須位於 Node.js 應用程式中，Node.js 建置套件才能辨識該應用程式。`app.js` 檔案是應用程式的登錄 Script，可以在 `package.json` 檔案中指定。下列範例顯示簡式 `package.json` 檔案：

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  如需 `package.json` 檔案的相關資訊，請參閱 [package.json ![外部鏈結圖示](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}。

  * 若要將 PHP、Ruby 或 Python 應用程式部署至 {{site.data.keyword.Bluemix_notm}}，請從包含應用程式原始檔的目錄中，使用下列指令：

  ```
  cf push appname
  ```

### 在多個空間中部署應用程式

應用程式專屬於它部署到的空間。您無法在 {{site.data.keyword.Bluemix_notm}} 中，將應用程式從一個空間移動或複製到另一個空間。若要在多個空間中部署應用程式，您必須在每個要在其中使用應用程式的空間裡部署應用程式，步驟如下：

  1. 使用 **cf target** 指令與 **-s** 選項，切換至您要部署應用程式的空間：

  ```
  cf target -s <space_name>
  ```

  2. 移至應用程式目錄，然後使用 **cf push** 指令部署您的應用程式，其中 appname 在您的網域內必須是唯一的。

  ```
  cf push appname
  ```

## 應用程式資訊清單
{: #appmanifest}

應用程式資訊清單包含套用於 **cf push** 指令的選項。您可以使用應用程式資訊清單來減少每次將應用程式推送至 {{site.data.keyword.Bluemix_notm}} 時，必須指定的部署詳細資料數量。

在應用程式資訊清單中，您可以指定一些選項，例如要建立的應用程式實例數、要配置給應用程式的記憶體量和磁碟限額，以及應用程式的其他環境變數。您還可以使用應用程式資訊清單，將應用程式部署自動化。資訊清單檔的預設名稱是 `manifest.yml`。

### 資訊清單檔支援的選項

下表顯示您可以在應用程式資訊清單檔中使用的支援選項。如果您選擇使用 `manifest.yml` 以外的不同檔名，則必須使用 **-f** 選項與 **cf push** 指令搭配。在下列範例中，`appManifest.yml` 是檔名：

```
cf push -f appManifest.yml
```

<p>  </p>


|選項	|說明	|用法或範例|
|:----------|:--------------|:---------------|
|**buildpack**	|自訂建置套件的 URL 或名稱。	|`buildpack: ` *buildpack_URL*|
|**disk_quota**	|配置給應用程式的磁碟限額。預設值為 1 G。	|`disk_quota: 500M`|
|**domain**	|{{site.data.keyword.Bluemix_notm}} 中應用程式的網域名稱。	|`domain:` ng.bluemix.net|
|**host**	|{{site.data.keyword.Bluemix_notm}} 中應用程式的主機名稱。此值必須是 {{site.data.keyword.Bluemix_notm}} 環境中的唯一值。	|`host: ` *host_name*|
|**name**	|{{site.data.keyword.Bluemix_notm}} 中的應用程式名稱。此值必須是 {{site.data.keyword.Bluemix_notm}} 環境中的唯一值。	|`name: ` *appname*|
|**path**	|應用程式的位置。此值可以是相對路徑或絕對路徑。	|`path: ` *path_to_application*|
|**command**	|應用程式的自訂啟動指令，或執行 Script 檔的指令。	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|要配置給應用程式的記憶體量。預設值為 1G。	|`memory: 512M`|
|**instances**	|要為應用程式建立的實例數。	|`instances: 2`|
|**timeout**	|用來啟動應用程式的時間量上限（秒）。預設值為 60 秒。	|`timeout: 80`|
|**no-route**	|布林值，避免在應用程式只是在背景中執行時指派路徑給該應用程式。預設值為 **false**。	|`no-route: true`|
|**random-route**	|布林值，將隨機路徑指派給應用程式。預設值為 **false**。	|`random-route: true`|
|**services**	|要連結至應用程式的服務。	|`services:   - mysql_maptest`|
|**env**	|應用程式的自訂環境變數。|`env: DEV_ENV: production`|
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### 範例 `manifest.yml` 檔案

下列範例顯示 Node.js 應用程式的資訊清單檔，該應用程式在 {{site.data.keyword.Bluemix_notm}} 中使用內建的社群 Node.js 建置套件。

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## 環境變數
{: #app_env}

環境變數包含 {{site.data.keyword.Bluemix_notm}} 上已部署應用程式的環境資訊。除了 *Droplet Execution Agent (DEA)* 及建置套件所設定的環境變數之外，您還可以設定 {{site.data.keyword.Bluemix_notm}} 上應用程式的應用程式特有環境變數。

您可以使用 **cf env** 指令或從 {{site.data.keyword.Bluemix_notm}} 使用者介面，檢視執行中 {{site.data.keyword.Bluemix_notm}} 應用程式的下列環境變數：

  * 應用程式特有的使用者定義變數。如需如何將使用者定義的變數新增至應用程式的相關資訊，請參閱[新增使用者定義的環境變數 ![外部鏈結圖示](../icons/launch-glyph.svg)](#ud_env){:new_window}。

  * VCAP_SERVICES 變數包含可存取服務實例的連線資訊。如果您的應用程式連結至多個服務，則 VCAP_SERVICES 變數會包含每個服務實例的連線資訊。例如：

  ```
  {
   "VCAP_SERVICES": {"AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

您也可以存取 DEA 及建置套件所設定的環境變數。

下列變數透過 DEA 定義：

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>已部署應用程式的根目錄。</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>每一個應用程式實例可使用的記憶體量上限。您可以在應用程式 <span class="ph filepath">manifest.yml</span> 檔案中指定值，或在推送應用程式時在指令行中指定值。</dd>
  <dt><strong>PORT</strong></dt>
  <dd>DEA 上與應用程式通訊所使用的埠。DEA 會在編譯打包時配置埠給應用程式。</dd>
  <dt><strong>PWD</strong></dt>
  <dd>執行建置套件的現行工作目錄。</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>儲存暫存檔及編譯打包檔的目錄。</dd>
  <dt><strong>USER</strong></dt>
  <dd>用來執行 DEA 的使用者 ID。</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>DEA 主機的 IP 位址。</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>JSON 字串，包含已部署應用程式的相關資訊。此資訊包括應用程式名稱、URI、記憶體限制、應用程式達到其現行狀態的時間戳記等等。例如：
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>JSON 字串，包含連結至已部署應用程式的服務資訊。例如：
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
      "tags":[
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

對於每一個建置套件，透過建置套件所定義的變數會不同。如需任何其他相容建置套件，請參閱 [Buildpacks ![外部鏈結圖示](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}。

<ul>
    <li>下列變數透過「Liberty 建置套件」定義：
	
	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>執行應用程式的 Java SDK 位置。</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>要在執行應用程式時使用的 Java SDK 選項。</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>在 DEA 中啟動 Liberty 設定檔伺服器實例的 Java 指令。</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>在 DEA 中啟動 Liberty 設定檔伺服器實例時，共用資源及伺服器定義的位置。</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>所產生輸出的位置，例如執行中 Liberty 設定檔伺服器實例的日誌檔及工作目錄。</dd>
	  </dl>
</li>   
<li>下列變數透過「Node.js 建置套件」定義：
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Node.js 運行環境的目錄。</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Node.js 運行環境用於快取的目錄。</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Node.js 運行環境所使用的系統路徑。</dd>
	</dl>
</li>
</li>
</ul>

您可以使用下列範例 Node.js 程式碼來取得 VCAP_SERVICES 環境變數的值：

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

如需每一個環境變數的相關資訊，請參閱 [Cloud Foundry Environment Variables ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}。

## 自訂應用程式部署
{: #customize_dep}

您可以自訂應用程式的部署作業。例如，您可以指定應用程式的啟動指令，且可以配置應用程式啟動環境。
{:shortdesc}

### 指定啟動指令

若要指定應用程式的啟動指令，您可以使用下列其中一種方式。您指定的啟動指令將會改寫建置套件提供的預設啟動指令。

**附註：**如果您要優先使用建置套件啟動指令，請指定 **null** 作為啟動指令。

  * 使用 **cf push** 指令並指定 -c 參數。例如，當您部署 Node.js 應用程式時，您可以在 -c 參數中指定 **node app.js** 啟動指令：

  ```
  cf push appname -p app_path -c "node app.js"
  ```

  * 在 `manifest.yml` 檔案中使用 command 參數。例如，當您部署 Node.js 應用程式時，您可以在資訊清單檔中指定 **node app.js** 啟動指令：


  ```
  command: node app.js
  ```


### 新增使用者定義的環境變數
{: #ud_env}

使用者定義的環境變數，是應用程式特有的變數。您有下列選項，可將使用者定義的環境變數新增至執行中的應用程式：

  * 使用 {{site.data.keyword.Bluemix_notm}} 使用者介面。請完成下列步驟：

    1. 在 {{site.data.keyword.Bluemix_notm}}「儀表板」上，按一下應用程式磚。即會顯示「應用程式詳細資料」頁面。
	2. 按一下**環境變數**。
	3. 按一下**使用者定義**，然後按一下**新增**。
	4. 填寫必要欄位，然後按一下**儲存**。
  * 使用 cf 指令行介面。使用 `cf set-env` 指令新增使用者定義的變數。例如：
    ```
cf set-env appname env_var_name env_var_value
    ```

  * 使用 `manifest.yml` 檔案。在該檔案中新增值配對。例如：
    ```
	env:
      VAR1:value1
      VAR2:value2
    ```

新增使用者定義的環境變數之後，您可以使用下列範例 Node.js 程式碼來取得所定義變數的值：

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```

### 配置啟動環境

若要配置應用程式的啟動環境，您可以新增 Shell Script 至 `/.profile.d` 目錄。`/.profile.d` 目錄位於應用程式的建置目錄下。執行應用程式之前，先由 {{site.data.keyword.Bluemix_notm}} 執行 `/.profile.d` 目錄中的 Script。例如，您可以將包含下列內容的 `node_env.sh` 檔案置於 `/.profile.d` 目錄下，以將 NODE_ENV 環境變數設為 **production**：

```
export NODE_ENV=production;
```

###避免上傳檔案及目錄

當您使用 cf 指令行介面來部署應用程式時，可以跳過 {{site.data.keyword.Bluemix_notm}} 可以在它處取得的某些檔案和目錄，以節省上傳時間。若要避免這些檔案及目錄上傳至 {{site.data.keyword.Bluemix_notm}}，您可以在應用程式的根目錄建立 `.cfignore` 檔案。

**附註：**`.cfignore` 檔案必須採用 UTF-8 格式。

`.cfignore` 檔案包含您要忽略的檔案名稱及目錄名稱，每行放置一個名稱。您可以使用星號 (*) 作為萬用字元。當您指定目錄時，也會忽略該目錄底下的所有檔案及子目錄。例如，`.cfignore` 檔案中的下列內容表示，所有 `.swp` 檔案，以及在 `tmp/` 目錄下的所有檔案和子目錄都將不會上傳至 {{site.data.keyword.Bluemix_notm}}。

```
*.swp
tmp/
```

# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [Deploying with Application Manifests ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![外部鏈結圖示](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6 ![外部鏈結圖示](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [開始使用 IBM Continuous Delivery Pipeline for Bluemix](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
