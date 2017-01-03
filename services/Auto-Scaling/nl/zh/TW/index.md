---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.autoscaling}} 服務
{: #autoscaling}
前次更新：2016 年 11 月 2 日
{: .last-updated}

在 {{site.data.keyword.Bluemix_notm}} 中，您可以自動管理應用程式產能。使用 {{site.data.keyword.autoscaling}} 服務可自動提高或降低應用程式的運算能力。應用程式實例的數目會根據您定義的 {{site.data.keyword.autoscaling}} 原則動態調整。
{:shortdesc} 

## 目錄
  * [使用 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.autoscaling}} 服務](#as-service)
  * [使用 {{site.data.keyword.autoscaling}} 服務配置 Node.js 應用程式](#node-asagent)
  * [透過 RESTful API 管理 {{site.data.keyword.autoscaling}} 服務](#RESTAPI)
  * [透過 {{site.data.keyword.autoscaling}} CLI 管理 {{site.data.keyword.autoscaling}} 服務](#CLI)
  * [{{site.data.keyword.autoscaling}} 服務的原則欄位](#policy_fields)
  * [錯誤訊息](#err_msg)

## 使用 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.autoscaling}} 服務
{: #as-service}

若要使用 {{site.data.keyword.autoscaling}} 服務，請完成下列步驟：


1. 在 {{site.data.keyword.Bluemix_notm}} 的「儀表板」上，按一下*新增服務或 API*，然後從服務型錄中的 DevOps 區段選取 {{site.data.keyword.autoscaling}} 服務。會顯示新的視窗，以呈現 {{site.data.keyword.autoscaling}} 服務的概觀。
2. 選取您要連結 {{site.data.keyword.autoscaling}} 服務的應用程式，然後按一下*建立*。<br/>
*請記住：*您只能連結「一個」{{site.data.keyword.autoscaling}} 服務至應用程式。如果應用程式已經與另一個 {{site.data.keyword.autoscaling}} 服務連結，在此步驟中請不要選取該應用程式。否則，您將取得 CWSCV2004E 錯誤。<br/>即會顯示「重新編譯打包應用程式」視窗。
3. 在「重新編譯打包應用程式」視窗中，按一下*重新編譯打包*以重新編譯打包您的應用程式，然後才使用您剛新增的 {{site.data.keyword.autoscaling}} 服務。<br/>
<ul><li>對於 Liberty 應用程式，{{site.data.keyword.autoscaling}} 會自動配置並準備好在重新編譯打包應用程式之後使用。</li> <li>對於 Node.js 應用程式，您必須更新您的應用程式碼以啟用 {{site.data.keyword.autoscaling}} 服務，然後才將應用程式推送到 {{site.data.keyword.Bluemix_notm}}。如需詳細資訊，請參閱[使用 {{site.data.keyword.autoscaling}} 服務配置 Node.js 應用程式](index.html#node_asagent)。</ul><br/>
完成重新編譯打包應用程式之後，您可以開始為您的應用程式配置 {{site.data.keyword.autoscaling}} 服務。
4. 若要為應用程式配置 {{site.data.keyword.autoscaling}}，請在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，按一下 {{site.data.keyword.autoscaling}} 服務連結至的應用程式。
5. 在「儀表板」上的服務區段，按一下 *Auto-Scaling* 圖示。

6. 如果尚未完成，請按一下*建立 {{site.data.keyword.autoscaling}} 原則*來定義應用程式的 {{site.data.keyword.autoscaling}} 原則。

現在您可以配置 {{site.data.keyword.autoscaling}} 原則、查看度量統計資料，或檢視應用程式的調整歷程。
<dl>
<dt>原則配置</dt>
<dd>您可以使用本節來建立或編輯調整規則，以指定要觸發特定調整活動的狀況。<ul>
<li> 若為 Liberty for Java™ 應用程式，您可以定義資料堆、記憶體、回應時間及產量的調整規則。  
<li> 若為 Node.js 應用程式，您可以定義資料堆、記憶體及產量的調整規則。<li> 若為 Ruby 應用程式，您可以定義記憶體的調整規則。</ul>
*附註：*您可以針對多個度量值類型定義多個調整規則。不過，{{site.data.keyword.autoscaling}} 服務不會偵測調整原則之間的衝突。在您定義調整原則時，必須確定多個調整規則不會彼此衝突。否則，您可能看到實例總數上下變動，因為應用程式前 1 分鐘可能橫向縮編，但在下一分鐘卻橫向擴充。<br/><br/>
如果應用程式的工作負載在尖峰時間與空閒時間大幅變動，您可以建立調整排程來處理不同時段的不同調整需求。請使用排程中指定的實例計數下限參數，來定義應用程式實例數的基準線，而動態調整規則仍然適用於排程，可以觸發橫向縮編與橫向擴充動作。</dd>
<dt>度量值統計資料</dt>
<dd>顯示您的應用程式實例的度量值統計資料。您可以看到平均統計資料，並選取特定的實例以查看其統計資料。</dd>
<dt>調整歷程</dt>
<dd>顯示應用程式的調整歷程。<ul>
<li> 過去一星期：顯示過去一星期的調整歷程。
<li> 過去一個月：顯示過去一個月的調整歷程。
<li> 自訂範圍：您可以設定時段。</ul>
*附註：*您可以選取「調整狀態」或「橫向縮編/擴充」來過濾歷程記錄。</dd>
</dl>


## 使用 {{site.data.keyword.autoscaling}} 服務配置 Node.js 應用程式
{: #node-asagent}

若要對 Node.js 應用程式啟用 {{site.data.keyword.autoscaling}} 服務，除了服務佈建和連結步驟之外，您還需要完成下列步驟，然後才將應用程式推送至 {{site.data.keyword.Bluemix_notm}}。

1. 使用下列步驟更新 package.json 檔案：<ol><li>建立 `blumix-autoscaling-agent` 的相依關係項目，例如 `"bluemix-autoscaling-agent": "*"`。<br/><li>（選用）根據您為應用程式配置的記憶體，在 `scripts` 區段內設定資料堆限制，例如 `"start": "node --max-old-space-size=600 app.js"`。<br/>*附註：*如果您想要根據資料堆用量觸發擴充，請設定 `max-old-space-size` 的值。如果啟動應用程式時未設定此值，則會使用預設 Node.js 資料堆限制 1.4GB，而不論配置多少記憶體給您的應用程式，這可能會導致不適當的自動擴充決策。<br/>
```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. 更新您的主要檔案，以新增代理程式宣告 `var as_agent = require('bluemix-autoscaling-agent');`。下列程式碼 Snippet 顯示具有自動擴充代理程式宣告的完整項目 js 檔案。<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## 透過 RESTful API 管理 {{site.data.keyword.autoscaling}} 服務 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} RESTful API 提供除了 Bluemix 使用者介面以外的另一種方式來管理 {{site.data.keyword.autoscaling}} 服務，它也支援擴充資料擷取和分析。它提供類似於 {{site.data.keyword.Bluemix_notm}} 使用者介面的 API 的功能，例如建立原則以及取得擴充歷程。

若要使用 {{site.data.keyword.autoscaling}} RESTful API 來管理 {{site.data.keyword.autoscaling}} 服務，請完成下列必要條件：如前一節所指示連結 {{site.data.keyword.autoscaling}} 服務與您的應用程式，取得 `AccessToken`、{{site.data.keyword.autoscaling}} API 伺服器的 URL，以及您要擴充或縮減之應用程式的 `app_id`：

1. 基於安全目的，在每個 {{site.data.keyword.autoscaling}} RESTful API 的要求標頭中，透過 CloudFoundry UAA 程序取得的適當 `AccessToken` 必須提供於 `Authorization` 標頭中，以表示要求的必要驗證。如果無法符合此 `AccessToken` 會導致「401 未獲授權」的回應。安裝 Cloud Foundry 指令行工具並登入 {{site.data.keyword.Bluemix_notm}} 之後，您有兩種方式可以得到此 `AccessToken`：<ul><li>您可以透過 `cf oauth-token` 指令取得這個記號：

   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
所傳回開頭為 "bearer" 的長字串是 AccessToken，它可以用於 {{site.data.keyword.autoscaling}} RESTful API 的要求中。如果您遇到例如找不到指令的錯誤，可以將您的 Cloud Foundry 指令行工具更新至較新的版本。</li><li>您也可以在起始目錄中找到這個 AccessToken。從指令行介面登入 {{site.data.keyword.Bluemix_notm}} 之後，會在您的起始資料夾建立一個 `.cf` 資料夾，您可以在其中找到名為 `config.json` 的 JSON 檔案，檔案中包含現行登入環境資訊的清單，例如組織、空間、鑑別端點和版本。您可以在檔案中找到項目 `AccessToken`，如下所示：
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
`config.json` 中的 `AccessToken` 僅在一段時間內有效。如果您針對 REST API 要求收到「401 未獲授權」的回應，可能必須從指令行介面重新登入以重新整理檔案，並取得新的 `AcessToken`。</li></ul>
 
2.  若要取得 {{site.data.keyword.autoscaling}} API 伺服器的 URL，可以在連結應用程式與 {{site.data.keyword.autoscaling}} 服務之後，檢查 `VCAP_SERVICE` 環境變數。在 `VCAP_SERVICE` 中，您可以找到 {{site.data.keyword.autoscaling}} 服務區段，而 `api_url` 則是您應用程式連結的 API 伺服器 URL。您需要此 API 伺服器 URL 來連接至 {{site.data.keyword.autoscaling}} RESTful API 服務：

   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
請注意，也可以透過 `cf env APPNAME` 指令找到這個 URL：
```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {"VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  您可以從 `VCAP_SERVICES` 環境變數取得 `app_id`，或是就執行 `cf app APPNAME --guid` 指令：

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

有了上述所有必要條件，您現在可以在瀏覽器中使用 RestClient 附加程式，或是透過像是 `curl` 這樣的工具，提出 REST API 要求。 

使用 REST 用戶端附加程式，像是 Firefox 或 Chrome 的附加程式，您可以觸發對 {{site.data.keyword.autoscaling}} API 伺服器的 REST 要求，以執行您的指令。您只需要在主體部分提供這些附加程式，以及 REST API 的 URL、此 REST API 需要的方法及標頭，還有參數。如需每個 API 的詳細資訊，請參閱 [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} 的 REST API](https://new-console.ng.bluemix.net/apidocs/48){:new_window}。

使用像是 `curl` 等工具，您可以在 Script 內管理 {{site.data.keyword.autoscaling}} 服務，如下所示：    
```
    cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)

    echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## 透過 {{site.data.keyword.autoscaling}} CLI 管理 {{site.data.keyword.autoscaling}} 服務 
{: #CLI}

{{site.data.keyword.autoscaling}} CLI 提供與 {{site.data.keyword.autoscaling}} RESTful API 類似的功能，但配置 {{site.data.keyword.autoscaling}} 服務的方式更友善。使用 {{site.data.keyword.autoscaling}} CLI，您不必在乎 {{site.data.keyword.autoscaling}} RESTful API 中的詳細資料，例如 `AccessToken` 和 API 伺服器的 URL。您只需要遵循 CLI 提供的逐步指示。如需如何安裝及使用 {{site.data.keyword.autoscaling}} CLI 的詳細資料，請參閱 [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}



## {{site.data.keyword.autoscaling}} 服務的原則欄位
{: #policy_fields}

| 欄位名稱  | 說明 |
|-------------|----------------------|
|*允許的實例計數上限* |	可以啟動的應用程式實例數目上限。如果應用程式實例的現行數目等於此值，{{site.data.keyword.autoscaling}} 服務不會再橫向擴充應用程式。預設實例計數下限：可以啟動的應用程式實例數目下限。如果實例數目等於此值，{{site.data.keyword.autoscaling}} 服務不會再橫向縮編應用程式。 |
| *度量值類型*	| 	可以監視的受支援度量值類型。如需相關資訊，請參閱表格 2。 |
| *橫向擴充* | 	指定觸發橫向擴充動作的臨界值，以及觸發橫向擴充動作時，要增加多少實例。 |
| *橫向縮編* |	指定觸發橫向縮編動作的臨界值，以及觸發橫向縮編動作時，要減少多少實例。 |
| *統計資料時間範圍* |	過去期間的長度，此時刻，收到的度量值視為有效。度量值只有在時間戳記落在這個期間內的情況下才會有效。「統計資料時間範圍」參數的單位是秒。 |
| *中斷持續時間*	| 過去期間的長度，此時刻，可能會觸發調整動作。調整動作會在收集的度量值高於上臨界值，或低於下臨界值，且維持時間超過指定的時間時觸發。「中斷持續時間」參數的單位是秒。 |
| *橫向縮編的冷卻期間* | 橫向縮編動作發生之後，在「橫向縮編的冷卻期間」參數所指定的期間長度內，會忽略其他調整要求。這個參數的單位是秒。 |
| *橫向擴充的冷卻期間*	| 橫向擴充動作發生之後，在「橫向擴充的冷卻期間」參數所指定的期間長度內，會忽略其他調整要求。這個參數的單位是秒。 |
| *時區*	| 排程適用的時區。 |
| *開始時間*  |	循環排程的開始時間。 |
| *結束時間*    |	循環排程的結束時間。	|
| *重複於*	|	在每週的星期幾套用循環排程。 |
| *實例計數下限* |	在排程的指定時段期間，可以為應用程式啟動的實例數下限。 |
| *開始日期和時間* |	在特定日期設定之排程的開始日期和時間。 |
| *結束日期和時間* |	在特定日期設定之排程的結束日期和時間。	|

表 1. 調整原則中的原則欄位

| 度量值名稱 | 說明 | 支援的應用程式類型 |
|-------------|----------------------| ------------------- |
| *資料堆* |	資料堆記憶體的用量百分比。	| Liberty for Java、Node.js SDK |
| *記憶體*   |	記憶體的用量百分比。	|  全部 |
| *產量* | 每秒處理的要求數。| Liberty for Java、Node.js SDK |
| *回應時間* |	已處理要求的回應時間。	| Liberty for Java |

表 2. 支援的度量名稱

*附註：*若要收集 Auto-Scaling 度量資料，您的應用程式必須部署為 Liberty Web 應用程式，以便測量 HTTP/HTTPS 要求會透過 Liberty Web 容器來處理。例如，如果您將 Spring Boot 應用程式執行為「主要類別」應用程式，則 Liberty 建置套件只提供 Java 環境，應用程式實際上會在 Spring 內嵌 Tomcat 容器中執行，因此 Auto-Scaling 服務不會收集任何度量資料。您必須將應用程式執行為 Liberty WAR，才能使用 Auto-Scaling 服務。

## 錯誤訊息
{: #err_msg}
本節列出 {{site.data.keyword.autoscaling}} 服務所產生的警告及錯誤訊息。
 
### CWSCV2004E 另一個 {{site.data.keyword.autoscaling}} 服務已連結至應用程式。
**您只能連結一個 {{site.data.keyword.autoscaling}} 服務至一個應用程式。此錯誤發生在您要將 {{site.data.keyword.autoscaling}} 服務連結至已和另一個 {{site.data.keyword.autoscaling}} 服務連結的應用程式時。**

請選取另一個沒有連結任何其他 {{site.data.keyword.autoscaling}} 服務的應用程式，並將目標 {{site.data.keyword.autoscaling}} 服務連結至此應用程式。如果您在所有其他情況下遇到此錯誤，請聯絡「IBM 支援中心」。

### CWSCV6001E API 伺服器無法剖析 API 的輸入 JSON 字串：{0}。
**剖析輸入 JSON 字串時發生問題。**

利用 API 文件檢查「輸入 JSON」，並更正其中的錯誤。

### CWSCV6002E API 伺服器無法剖析 API 的輸出 JSON 字串：{0}。
**剖析輸入 JSON 字串時發生問題。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6003E API 的輸入 JSON：{1} 中，輸入 JSON 字串格式錯誤：{0}。
**剖析輸入 JSON 字串時發現格式錯誤。**

利用 API 文件檢查「輸入 JSON」，並更正其中的錯誤。

### CWSCV6004E API 的輸出 JSON：{1} 中，輸出 JSON 字串格式錯誤：{0}。
**剖析輸出 JSON 字串時發現格式錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6005E {0} 期間發生內部伺服器錯誤。
**處理要求時發生內部伺服器錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6006E 呼叫 CloudFoundry API 失敗：{0}
**呼叫 CloudFoundry API 時發生錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6007E 找不到應用程式：{0}
**找不到應用程式。**

如需相關資訊，請檢查應用程式資訊。

### CWSCV6008E 擷取應用程式 {0} 的資訊時發生下列錯誤：{1} 
**擷取應用程式資訊失敗，發生某些錯誤。**

如需相關資訊，請檢查應用程式資訊。

### CWSCV6009E 找不到應用程式 {1} 的服務：{0}。
**找不到此應用程式的服務。**

如需相關資訊，請檢查此應用程式的服務連結。

### CWSCV6010E 找不到應用程式 {0} 的原則
**找不到此應用程式的原則。**

如需相關資訊，請檢查應用程式配置。

### CWSCV6011E {0} 期間內部鑑別失敗
**「內部鑑別」失敗。**

如需相關資訊，請聯絡「雲端管理者」。


# 相關鏈結
{: #rellinks}

## 範例
{: #samples}

* [指導教學：在 {{site.data.keyword.Bluemix_notm}} 上讓您的應用程式具有彈性](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry 架構實驗室](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## SDK
{: #sdk}

* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} 的 REST API](https://new-console.{DomainName}/apidocs/48){:new_window}

## 一般
{: #general}

* [擴充容器](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [擴充虛擬伺服器](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [Node.js 的 {{site.data.keyword.autoscaling}} 代理程式](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

