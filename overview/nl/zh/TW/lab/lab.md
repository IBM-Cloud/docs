---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud 身分及存取管理 (IAM)
{: #iam_overview}

IBM Cloud IAM 提供一種安全的方式來管理使用者和服務身分，以及這些身分的資源存取。取決於您獲授權管理的存取選項，您可以檢視及管理帳戶或組織的使用者。您可以為使用者執行所有作業，包括邀請及管理使用者與其指派的角色，以及他們可以存取的帳戶及（或）組織。身為帳戶擁有者，您可以管理您與使用者兩者都是目前帳戶成員（不論角色為何）的存取選項。

身分管理包括下列各項：
 * 使用者管理 
   * 建立、刪除、更新使用者資訊
   * API 金鑰管理
   * 記號建立、重新整理及交換
   * 使用者身分鑑別
 * 服務 ID 管理
   * 建立、刪除、更新使用者資訊
   * API 金鑰管理
   * 記號建立、重新整理及交換
   * 服務身分鑑別
   
   
「存取管理」包括下列各項：
 * 原則管理
   * 建立、刪除及更新原則
 * 資源存取的決策
 
## 身分概觀
{: #identity}

「Cloud IAM 記號服務」是 IBM Cloud 的鑑別服務，以 [OAuth 2.0]( https://tools.ietf.org/html/rfc6749)、[JWT](https://tools.ietf.org/html/rfc7519)、[JWT Profile](https://tools.ietf.org/html/rfc7523) 及 [JWKS](https://tools.ietf.org/html/rfc7517) 所指定的開放式標準為建置基礎。

「記號服務」的一個焦點是 IBM Cloud Platform 開發人員、操作員及管理者的鑑別。對於此鑑別，「記號服務」會連接至 IBM ID 系統來鑑別使用者，而在專用及本端環境中，則可以連接至 LDAP 這類客戶選擇的鑑別系統。 

若要擷取 IAM 記號，您可以使用 `password` 這類標準 OAuth 2.0 授權類型，例如：
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

身為 OAuth 2.0 的延伸，您需要提供帳戶資訊，讓記號帳戶更為特別。您也可以列出不同的回應類型，來取得 `UAA` 或 `IMS` 記號，以與 CloudFoundry API 或 IMS API 進行互動。

「Cloud IAM 記號服務」可讓您建立、更新、刪除及使用使用者的 API 金鑰。使用 API 呼叫或「Bluemix 主控台」，即可建立這些 API 金鑰。運用 API 金鑰，採用者即可使用下列延伸授權類型：
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

可以使用產生的記號，例如使用密碼授權或使用者介面登入所擷取的記號。

「Cloud IAM 記號服務」為進一步的變異，可讓您利用使用者介面透過互動方式登入。這是使用 OAuth 2.0 授權類型 `authorization_code` 實作的，也稱為 `OAuth Dance`，因為它會導致鑑別階段期間有多個 Web 瀏覽器重新導向。

「記號服務」的另一個焦點是可以建立「服務 ID」以及「服務 ID」的 API 金鑰。「服務 ID」與「功能 ID」或「應用程式 ID」類似，用來根據服務（而不是代表使用者）進行鑑別。

使用者可以建立「服務 ID」，並將它們連結至 Bluemix 帳戶、CloudFoundry 組織或 CloudFoundry 空間這類範圍。這項連結會提供「服務 ID」所在的容器。此容器也會定義可以更新及刪除「服務 ID」的人員，以及可以建立、更新、讀取及刪除與該「服務 ID」相關聯的「API 金鑰」的人員。「服務 ID」與使用者「無關」。

若要深入瞭解如何使用「服務 ID」，您可以試用可示範 API 的[展示應用程式](https://iam.ng.bluemix.net/demo)。

## 存取管理概觀
{: #access_management}

IAM 是具有 [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf) 發佈所引起的條件的「屬性型存取控制 (ABAC)」系統。  

IAM 使用屬性組合來判定資源的存取。IAM 原則的規則會套用至角色、使用者/服務 ID 屬性、資源屬性及條件。這提供彈性且功能強大的方式來定義使用者及服務 ID 的存取。

例如，採用虛擬機器，VM123 可能有下列屬性： 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
您可以使用這些資源屬性的任意組合來建立原則。

如需詳細範例，請參閱 [IAM 原則範例](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples)。

ABAC 與「角色型存取控制 (RBAC)」不同，後者會將預先定義的角色指派給使用者。這些預先定義的角色具有特定專用權，而具有該角色的使用者會擁有該角色所定義的所有專用權。 
 
例如，「虛擬機器 `Administrator` 角色」。此角色是指任何虛擬機器資源的所有「管理者」類型專用權。 

考量 ABAC 的簡單方式是：

1. 有「使用者」、「資源」、「環境定義」及「動作」。
1. 「使用者」、「資源」、「環境定義」及「動作」的每一個實例都會有唯一 ID。
1. 每一個實例都會有屬性。
   基本上，這表示：「從授權觀點，關於實例，什麼是真的」。
   範例：
   1. 「使用者」是 Pisces，生於 1960 年代。
   1. 「資源」是籃球團隊名冊。
   1. 「環境定義」是東部時間早上 9:00 到下午 5:00。
   1. 「動作」是「可以更新」。
1. 建立原則，以判定哪個屬性集具有許可權，可讓「使用者」對「資源」執行「動作」。
1. 「使用者」要求對「資源」執行「動作」時，會諮詢原則以查看是否允許要求。

下列影像顯示授權序列的詳細視圖。

![授權序列](auth_sequence.png)

## 設定服務的存取控制
{: #setup_access_mgmt}

讓服務上線到 {{site.data.keyword.Bluemix_notm}}，是與使用 Cloud IAM 將服務上線不同的一組作業。就技術上而言，您可以獨立並依任何順序使用 {{site.data.keyword.Bluemix_notm}} 及 Cloud IAM 上線。Cloud IAM 團隊將會與 {{site.data.keyword.Bluemix_notm}} 服務上線團隊合作，因此上線處理程序上的 {{site.data.keyword.Bluemix_notm}} 服務也會包括 Cloud IAM 上線。

若要設定服務的存取控制，您必須在上線處理程序過程中使用下列步驟：

### 步驟 1：提出此 http 要求來建立服務 ID：
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Curl 指令：
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

下列更詳細說明 `curl` 指令中所使用的 `Service id` 及 `Service crn` 值：
  
#### Service id 
  
服務 ID 名稱可以與出現在服務 crn 中的服務名稱相同。
  
服務 ID 必須連結至帳戶、組織或空間。此連結判斷可以管理您服務 ID 的人員。例如，可以更新或刪除已連結服務 ID 的管理者。{{site.data.keyword.Bluemix_notm}} 記號需要 ID 所連結的帳戶、組織及空間的存取權。若要連結至帳戶，`boundTo` crn 必須類似下列內容： 

`crn:v1:::<service name>::a/<account id>:::` 
  
若為組織，它必須類似下列內容：
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
若為空間，它必須類似下列內容：
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
指定的 `boundTo` 值不會影響您服務 ID 可存取的資源。 
  
IAM 存取原則控制您服務 ID 可存取的資源。即使服務 ID 連結至 IBM 組織，還是可以建立 IAM 原則，以容許服務 ID 存取該組織外部的資源。當您使用 IAM 上線時，IAM 團隊所建立的第一個存取原則會容許服務 ID 建立服務所擁有的任何資源的原則。

如需此 API 及相關 API 的相關資訊，請參閱 [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/)。

#### Service crn

`boundTo` crn 中的 service-name 必須符合出現在服務 crn 中的服務名稱。
  
如需完成這些欄位的說明，請參閱 [CRN 規格](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md)。

從回應中，儲存 meta 資料 -> uuid 及 meta 資料 -> crn（即服務 ID 及服務 ID crn）。


### 步驟 2：在 [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters) 與 AccessControl Squad 聯絡。 
您的服務 ID 獲授與服務資源原則的「管理者」角色。

請使用此格式：
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### 步驟 3：您必須從服務 ID 建立 api-key。請使用下列 http 要求：
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Curl 指令： 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` 需要是服務 ID 的 crn（欄位 meta 資料 -> 從步驟 1 的回應所儲存的 crn）。名稱及說明可以是任何項目。

從回應中，儲存實體 -> apiKey。

如需此 API 及相關 API 的相關資訊，請參閱 [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey)。

### 步驟 4：取得服務 ID API 金鑰的存取記號。 

建立許可權時，您的服務可以提出服務資源的 PAP 及 PDP 要求。

使用步驟 #3 中的實體 **apiKey** 欄位（即 API 金鑰值 (apikey_value)）。

  * 然後，使用 API 金鑰值取得記號（請確定您使用跳出字元）：

    Curl 指令：
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

使用結果中的 **access_token** 欄位，即您服務 ID 的 api-key 記號。用於先前顯示的 curl 指令時，**access_token** 需要進行 URL 編碼。


### 步驟 5：登錄服務名稱的可能服務動作清單。

  a. 將服務動作對映至「IAM 系統定義的角色」。稍後在服務登錄期間會使用這個對映。

  * 執行下列要求，可以找到「IAM 系統定義的角色」清單：
  
Curl 指令：
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**附註：**使用服務登錄有效負載中「IAM 系統定義的角色」的 *crn 版本*。

下列範例說明如何將服務動作對映至角色。

  <table>
    <tr>
      <th>API 端點</th>
      <th>服務動作</th>
      <th>IAM 系統定義的角色</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>管理者</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>檢視者、編輯者、管理者</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>編輯者、管理者</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>管理者</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>編輯者、管理者</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>編輯者、管理者</td>
    </tr>
  </table>

  b. 使用下列指令行，向 `PAP` 登錄服務：
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
必須如[服務動作格式](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format)中所指定的來定義動作。
  
例如，使用標準格式時：

  `<service-name>.<component>.<verb>`
  
  使用前一個範例中的動作 `key-protect.keys.decode` 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### 步驟 6：根據步驟 5 的詳細資料，驗證所登錄的服務。

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 步驟 7（選用）：刪除您在步驟 5 中登錄的服務。

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 步驟 8：配置服務使用 PEP SDK，以檢查 PDP 的許可權。請選擇對應的 SDK 語言。

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## 術語
{: #terminology}

### 身分術語

* IBM ID (IBMid) - IBM 所提供及管理的身分，可存取 IBM Cloud、IBM 應用程式、社群及支援。
* 使用者 ID (User Id) - 代表實際人員的識別。
* 服務 ID (Service Id) - 代表技術使用者、機器、應用程式或服務的識別。與也代表技術使用者的「功能 ID」或「應用程式 ID」類似，但使用「使用者 ID」實體類型。
* OAuth 2.0 - 授權存取應用程式及 API 而不需要向目標服務提供認證的開放式標準。OAuth 也用來包含鑑別資訊。
* OpenID Connect - 以 OAuth 2.0 為建置基礎的開放式標準，著重在提供已鑑別使用者的相關資訊。
* 用戶端 ID (Client Id) - 與 OAuth 2.0 相容端點互動的應用程式需要有秘密用戶端 ID/秘密配對，才能進行鑑別。應用程式需要向「記號服務」登錄，才能取得用戶端 ID。
* 記號端點 (Token endpoint) - 用戶端用來透過呈現識別資訊（例如使用者名稱或密碼、授權或重新整理記號）以取得一個以上的記號。
* 授權端點 (Authorization endpoint) - 用戶端用來透過記號服務的使用者介面以鑑別使用者。
* 記號 (Token) - 不透明或透明的字串，可讓應用程式擷取身分的鑑別及（或）授權。
* 存取記號 (Access token) - 此記號用來當作識別資訊傳送給 API。它包含識別資訊，而且只能使用一小段時間。
* 重新整理記號 (Refresh token) - 此記號儲存在僅要求鑑別的用戶端上。它用來在存取記號到期時可以取得新的存取記號（即重新整理存取記號）。因為重新整理記號會存留較長的時間，所以它不得離開用戶端系統，但重新整理存取記號本身的用途除外。
* 身分 Cookie (Identity cookie) - 登入「IBM Cloud 記號服務」時，會向瀏覽器發出包含您身分的 Cookie。只要此 Cookie 存在且有效，登入就不再困難。如果登出「IBM Cloud 記號服務」，或關閉瀏覽器，則它會在 24 小時之後到期。
* JSON Web 記號 (JSON Web Token) - 代表存取記號的 JSON 型標準 (RFC 7519)。存取記號的內容十分透明（亦即可以輕鬆地讀取）。一般要簽署 JWT 型記號，才能驗證該記號的出處證明。
* 公開金鑰 (Public Key) - 可以用來驗證「JSON Web 記號」的簽章。如果使用非對稱加密，則可以放心地發佈公開金鑰，以供用戶端使用。
* 私密金鑰 (Private Key) - 可以用來建立「JSON Web 記號」的簽章。此金鑰必須保密，否則其他人可以建立有效的存取記號。
* realmid - 用來區分使用者與不同使用者登錄的 ID。對於 IBM ID 系統所鑑別的使用者，目前使用的值是 "IBMid"，而對於「記號服務」所鑑別的「服務 ID」，則為 "iam"。
* ID (identifier) - 永不變更且可唯一識別某個使用者登錄內部的使用者的 ID（透過 `realmid` 參數表示）。<realmid>-<identifier> 組合一律會導致唯一可識別的使用者。如果是 IBM ID，則會使用 IBM 唯一 ID 'IUI'。             
* 主體 (subject) - 身分的使用者名稱。通常使用相同的形式，例如電子郵件位址。如果是 IBM ID，則這是身分的 IBM ID。
* 自訂宣告 (Custom claims) -「JSON Web 記號」內部的其他非標準資訊。

### 存取管理術語

* (PAP) 原則管理點 (Policy Administration Point) - 可管理存取授權原則的點。
* (PDP) 原則決策點 (Policy Decision Point) - 發出存取決策前，可根據授權原則來評估存取要求的點。
* (PEP) 原則強制執行點 (Policy Enforcement Point) - 可透過這個點來截取使用者資源存取要求、對 PDP 提出決策要求以取得存取決策（亦即，核准或拒絕資源存取），並處理收到的決策。
* (PIP) 原則資訊點 (Policy Information Point) - 作為屬性值來源的系統實體（亦即資源、主體、環境）。
* (PRP) 原則擷取點 (Policy Retrieval Point) - 儲存 XACML 存取授權原則的點，一般是資料庫或檔案系統。
* 主體 (subject) - 資源與主體授權配對中的「對象」，例如使用者或群組。資源就是主體可存取的資源。
* 角色 (role) - 許可權集合，可指派給使用者、使用者群組、系統、服務或應用程式，讓它能夠執行特定作業。
* 資源 (resource) - 可對其執行動作的實體或邏輯物件，例如組織、空間、資料庫或表格。
* 條件 (conditions) - 評估為 "True"、"False" 或 "Indeterminate" 的函數。
* 動作 (actions) - 應用程式因事件而對物件或資源執行的已定義作業。
* 原則 (policy) - 一組規則、規則合併演算法的 ID，以及（選用的）一組義務或建議。可以是原則集的元件。

## 系統定義的角色
{: #system_defined_roles}

「IBM Cloud 角色」代表動作集合，這些動作是由已啟用 IAM 的服務所提供。

使用一組最小的「系統定義的角色」，將動作分組為各角色，以提供彈性來支援任何服務或資源的動作。例如，如果 VM、「儲存空間」及「網路」都需要`管理者`，則可以針對這三個項目使用`管理者`角色，只需要變更原則的目標即可。VM 上的`管理者`、「儲存空間」上的`管理者`，以及「網路」上的`管理者`。

*IBM Cloud IAM 不執行的作業*：其他存取管理系統所使用的替代方案是將資源建置到角色。此方式會不小心地為系統中引進的每種資源類型產生新的角色名稱。例如，使用此方式，您需要 `VMAdministrator` 角色、`StorageAdministrator` 角色及 `NetworkAdministrator` 角色來涵蓋 VM、「儲存空間」及「網路」資源的管理。


下表顯示「IAM 系統定義的角色」以及與其對映的動作範例。

|IBM Cloud 角色名稱| 說明 | 動作範例|
|:-----------------|:-----------------|:-----------------|
|檢視者|不會變更狀態的動作（即唯讀）| <ul><li>列出裝置</li><li>讀取儲存空間物件</li><li>執行查詢</li><li>執行搜尋</li></ul>|
|編輯者|可修改狀態及建立/刪除子資源的動作|<ul><li>建立 VM</li><li>刪除 VM</li><li>連接儲存空間</li><li>重新開機</li><li>啟動/停止</li><li>重新命名</li></ul>|
|操作員|配置及操作資源所需的動作|<ul><li>更新配置</li><li>啟動/停止 VM</li><li>檢視日誌</li><li>備份/還原</li></ul>|
|管理者|所有動作，包括可以管理存取控制|<ul><li>邀請使用者</li><li>建立 VM</li>更新使用者存取原則</li><li>列出裝置</li><li>建立 VM</li><li>刪除 VM</li><li>連接儲存空間</li><li>重新開機</li><li>啟動/停止</li><li>重新命名</li><li>備份/還原</li></ul>|
|計費管理者|與計費管理相關的動作|<ul><li>更新信用卡</li><li>列出發票</li><li>下載發票</li></ul>|

您可以在下列網址從 PAP micro-service 查詢最新的「系統定義的角色」清單：

Curl 指令： 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## 服務動作格式
{: #action_format}

您必須使用以下 2 種格式中的其中一種來定義動作：
  
* 標準：

    `<service-name>.<component>.<verb>`
* 存取控制截取點： 

    `<METHOD> /<api_route>`
  
### 標準
大部分服務都會直接呼叫 IAM PDP，而且可以修改原始碼來支援標準動作格式。  
 
 此格式必須包括以下這三個部分，而且為英數字、沒有空格，或 '-' 以外的特殊字元。

`<service-name>.<component>.<verb>`

其中 
* service-name - CRN service-name 欄位中所定義的服務名稱。
* component - 服務的資源或子資源。
* verb - 可定義服務名稱元件所支援動作的動詞。 
  
例如：`key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### REST API 存取控制截取點
{: intercept_point}

在某些情況下，會透過作為「存取控制截取點」的閘道來導向 REST API 要求。直接先從截取點呼叫 IAM PDP，然後再呼叫實際 REST API 服務。處理 REST API 要求的服務絕對不會呼叫 IAM PDP。

截取點只會知道 REST API 路徑以及要將要求傳送至其中的端點。如需詳細資料，請參閱[存取控制截取點考量](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview)。


 此格式必須包括以下這兩個部分，並支援 [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt) 所指定的 URL 的安全字元。
 
 
`<METHOD> /<api_route>`
  
其中
* METHOD - REST API 方法。 
* api_route - REST API 的 URI。

例如：`GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata&ndash>uuid and metadata&ndash>crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata&ndash>crn saved from step 1’s response). The name and description can be anything.

From the response, save entity&ndash>apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET &ndash&ndashheader 'Accept: application/json' &ndash&ndashheader 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# 實驗室服務 ID 及 API 金鑰

interconnect-service1：
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2：
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3：
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4：
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5：
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6：
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7：
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8：
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9：
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10：
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11：
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12：
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13：
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14：
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15：
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16：
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17：
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18：
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19：
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20：
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21：
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22：
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23：
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24：
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25：
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26：
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27：
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28：
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29：
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30：
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31：
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32：
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33：
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34：
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35：
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36：
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37：
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38：
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39：
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40：
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41：
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42：
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43：
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44：
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45：
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46：
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47：
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48：
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49：
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50：
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


