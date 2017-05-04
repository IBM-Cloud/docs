---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM 提供了一种安全的方法来管理用户和服务身份以及对这些身份的资源的访问权。您可以根据有权管理的访问权选项来查看和管理整个帐户或组织中的用户。还可以对用户执行所有操作，包括邀请和管理用户及其分配的角色，以及管理用户可以访问的帐户和/或组织。作为帐户所有者，您可以通过当前帐户管理您与用户都属于其成员的访问权选项，与角色无关。

身份管理包含以下内容：
 * 用户管理 
   * 创建、删除和更新用户信息
   * API 密钥管理
   * 令牌创建、刷新和交换
   * 用户身份认证
 * 服务标识管理
   * 创建、删除和更新用户信息
   * API 密钥管理
   * 令牌创建、刷新和交换
   * 服务身份认证
   
   
访问管理包含以下内容：
 * 策略管理
   * 创建、删除和更新策略
 * 决定对资源的访问权
 
## 身份概述
{: #identity}

Cloud IAM Token Service 是 IBM Cloud 的认证服务，基于 [OAuth2.0]( https://tools.ietf.org/html/rfc6749)、[JWT](https://tools.ietf.org/html/rfc7519)、[JWT 概要文件](https://tools.ietf.org/html/rfc7523)和 [JWKS](https://tools.ietf.org/html/rfc7517) 指定的开放标准进行构建。

Token Service 的一个关注点是向 IBM Cloud 平台认证开发者、操作员和管理员。为了进行此认证，Token Service 会连接到 IBM 标识系统来认证用户，而在专用和本地环境中，Token Service 可以连接到客户选择的认证系统，如 LDAP。 

要检索 IAM 令牌，可以使用像 `password` 这样的标准 OAuth 2.0 授权类型，例如：
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

作为 OAuth 2.0 的扩展，您需要提供帐户信息来使令牌特定于帐户。此外，还可以列出不同的响应类型，从而获取 `UAA` 或 `IMS` 令牌以用于与 CloudFoundry API 或 IMS API 进行交互。

通过 Cloud IAM Token Service，可以创建、更新、删除和使用用户的 API 密钥。这些 API 密钥可以通过 API 调用或 Bluemix 控制台进行创建。要利用 API 密钥，采用者可以使用以下扩展的授权类型：
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

生成的令牌可以像通过密码授权或 UI 登录检索到的令牌一样使用。

作为进一步的变体，Cloud IAM Token Service 允许您使用 UI 以交互方式登录。这是使用 OAuth 2.0 授权类型 `authorization_code` 来实现的，也称为 `OAuth Dance`，因为它会在认证阶段产生多次 Web 浏览器重定向。

Token Service 的另一个关注点是能够创建服务标识以及服务标识的 API 密钥。服务标识类似于“功能标识”或“应用程序标识”，用于向服务进行认证，而不代表用户。

用户可以创建服务标识，并将其绑定到作用域，如 Bluemix 帐户、CloudFoundry 组织或 CloudFoundry 空间。执行此绑定会为服务标识提供一个用于存放该标识的容器。此容器还会定义谁可以更新和删除该服务标识，谁可以创建、更新、读取和删除与该服务标识关联的 API 密钥。服务标识与用户无关。

为了更好地了解如何使用服务标识，您可以试用用于演示 API 的[演示应用程序](https://iam.ng.bluemix.net/demo)。

## 访问管理概述
{: #access_management}

IAM 是一种基于属性的访问控制系统 (ABAC)，其中条件根据 [NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf) 出版物制定。  

IAM 使用属性的组合来确定对资源的访问权。IAM 策略包含应用于角色的规则、用户/服务标识属性、资源属性和条件。这样就可以采用一种灵活而强大的方法来为用户和服务标识定义访问权。

例如，假设虚拟机 VM123 可能具有以下属性： 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
这些资源属性的任意组合都可用于创建策略。

有关更详细的示例，请参阅 [IAM 策略示例](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples)。

ABAC 不同于基于角色的访问控制 (RBAC)，后者是将预定义的角色分配给用户。这些预定义的角色具有特定的特权，具有该角色的用户即拥有该角色定义的所有特权。 
 
例如，虚拟机`管理员`角色。此角色暗含对任何虚拟机资源的所有管理员类型特权。 

下面是理解 ABAC 的简单思路：

1. 有用户、资源、上下文和操作。
1. 用户、资源、上下文和操作的每个实例都具有唯一标识。
1. 每个实例都提供有属性。基本上这意味着：“从授权角度来看实例的真实情况”。示例：
   1. 用户为 Pisces，生于 20 世纪 60 年代。
   1. 资源为“棒球队名单”。
   1. 上下文为“上午 9:00 到下午 5:00（东部时间）”。
   1. 操作为“可以更新”。
1. 将创建策略以确定哪组属性使用户有权对资源执行操作。
1. 用户发起请求，要求对资源执行操作时，系统会检查策略以确定是否允许请求。

下图显示了授权序列的详细视图。

![授权序列](auth_sequence.png)

## 为服务设置访问控制
{: #setup_access_mgmt}

使服务在 {{site.data.keyword.Bluemix_notm}} 上线的一组操作不同于使服务在 Cloud IAM 上线的操作。从技术上说，可以在 {{site.data.keyword.Bluemix_notm}} 和 Cloud IAM 独立上线，顺序任意。Cloud IAM 团队将与 {{site.data.keyword.Bluemix_notm}} 服务上线团队合作，这样 {{site.data.keyword.Bluemix_notm}} 服务上线过程也将包含 Cloud IAM 上线。

要为服务设置访问控制，必须在上线过程中使用以下步骤：

### 第 1 步：通过发起以下 HTTP 请求来创建服务标识：
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

Curl 命令：
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

下面更详细地描述了在 `curl` 命令中使用的 `Service id` 和 `Service crn` 值：
  
#### Service id 
  
service id name 可以与服务的 crn 中显示的服务名称相同。
  
服务标识必须绑定到帐户、组织或空间。此绑定将确定谁可以管理服务标识。例如，服务标识绑定的管理员能够执行更新或删除操作。{{site.data.keyword.Bluemix_notm}} 令牌需要有权访问要将标识绑定到的帐户、组织和空间。要绑定到帐户，`boundTo` crn 必须类似于以下内容： 

`crn:v1:::<service name>::a/<account id>:::` 
  
对于组织，必须类似于以下内容：`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
对于空间，必须类似于以下内容：`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
指定的 `boundTo` 值对于服务标识可以访问哪些资源没有任何作用。 
  
IAM 访问策略控制服务标识可以访问哪些资源。尽管服务标识是绑定到 IBM 组织，也可以创建 IAM 策略以允许服务标识访问该组织外部的资源。在 IAM 上线时，IAM 团队创建的第一个访问策略允许服务标识为服务拥有的任何资源创建策略。

有关此 API 和相关 API 的更多信息，请参阅 [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/)。

#### Service crn

`boundTo` crn 中的 service-name 必须与服务的 crn 中显示的服务名称匹配。
  
有关填写这些字段的帮助，请参阅 [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md)。

从响应中，保存“元数据”-> uuid 和“元数据”-> crn，这分别是服务标识和服务标识 crn。


### 第 2 步：联系 AccessControl Squad：[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters)。 
将为您的服务标识提供对服务资源的策略的“管理员”角色。

使用以下格式：
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### 第 3 步：必须通过服务标识创建 API 密钥。请使用以下 HTTP 请求：
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

Curl 命令： 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` 需要是服务标识的 crn（从第 1 步的响应中保存的字段“元数据”-> crn）。名称和描述可以为任意内容。

从响应中，保存“实体”-> apiKey。

有关此 API 和相关 API 的更多信息，请参阅 [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey)。

### 第 4 步：获取服务标识 API 密钥的访问令牌。 

确定了许可权后，服务可以对服务的资源发起 PAP 和 PDP 请求。

使用第 3 步中的实体 **apiKey** 字段，即 API 密钥值 (apikey_value)。

  * 然后，获取具有 API 密钥值的令牌（确保使用转义字符）：

    Curl 命令：
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

使用结果中的 **access_token** 字段，即服务标识的 API 密钥令牌。**access_token** 在用于先前所示的 curl 命令中时，需要进行 URL 编码。


### 第 5 步：注册服务名称的可能服务操作的列表。

  a. 将服务操作映射到“IAM 系统定义的角色”。在服务注册期间的后续部分会使用此映射。

  * “IAM 系统定义的角色”的列表可以通过执行以下请求来获取：
  
Curl 命令：
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**注：**使用服务注册有效内容中“IAM 系统定义的角色”的 *crn 版本*。

下面是将服务操作映射到角色的示例。

  <table>
    <tr>
      <th>API 端点</th>
      <th>服务操作</th>
      <th>IAM 系统定义的角色</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>管理员</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>查看者、编辑者、管理员</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>编辑者、管理员</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>管理员</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>编辑者、管理员</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>编辑者、管理员</td>
    </tr>
  </table>

  b. 使用以下命令行向 `PAP` 注册服务：
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
  
操作必须如[服务操作格式](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format)中所指定的那样进行定义。
  
例如，使用标准格式时：

  `<service-name>.<component>.<verb>`
  
  使用先前示例中的操作 `key-protect.keys.decode` 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### 第 6 步：验证根据第 5 步中的详细信息注册的服务。

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 第 7 步（可选）：删除第 5 步中注册的服务。

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### 第 8 步：将服务配置为使用 PEP SDK，以便使用 PDP 检查许可权。选择相应的 SDK 语言。

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## 术语
{: #terminology}

### 身份术语

* IBM 标识 - 由 IBM 提供和托管的身份，用于访问 IBM Cloud、IBM 应用程序、社区和支持。
* 用户标识 - 代表真实个人的标识。
* 服务标识 - 代表技术用户、机器、应用程序或服务的标识。类似于也代表技术用户的“功能标识”或“应用程序标识”，但使用“用户标识”实体类型。
* OAuth 2.0 - 一种开放标准，用于授予对应用程序和 API 的访问权，而不向目标服务提供凭证。OAuth 还用于包含认证信息。
* OpenID Connect - 一种基于 OAuth 2.0 构建的开放标准，专注于提供有关已认证用户的信息。
* 客户机标识 - 与符合 OAuth 2.0 的端点进行交互的应用程序需要私密客户机标识/私密信息对进行认证。应用程序需要向 Token Service 注册才能获得客户机标识。
* 令牌端点 - 由客户机用于通过提供身份信息（例如，用户名或密码、授权或刷新令牌）来获取一个或多个令牌。
* 授权端点 - 由客户机用于通过 UI 向 Token Service 认证用户。
* 令牌 - 一个模糊或透明的字符串，支持应用程序检索身份的认证和/或授权。
* 访问令牌 - 此令牌用于作为身份信息发送给 API。它包含身份信息，并仅在短时间内有效。
* 刷新令牌 - 此令牌存储在仅请求认证的客户机上。如果访问令牌到期，刷新令牌用于获取新的访问令牌（即，刷新访问令牌）。由于刷新令牌生命周期很长，因此不能离开客户机系统，除非要用于刷新访问令牌本身。
* 身份 cookie - 登录到 IBM Cloud Token Service 时，会向浏览器发放包含您身份的 cookie。只要此 cookie 存在并有效，您要登录时就不会对您重新质询。如果从 IBM Cloud Token Service 注销或者如果关闭了浏览器，那么此 cookie 在 24 小时后到期。
* JSON Web 令牌 - 一种基于 JSON 的标准 (RFC 7519)，用于表示访问令牌。访问令牌的内容是透明的（即，可以轻松读取）。基于 JWT 的令牌通常会进行签名，以便能够验证该令牌的来源证明。
* 公用密钥 - 可用于验证 JSON Web 令牌的签名。如果使用非对称加密，那么可以安全地发布公用密钥以供客户机使用。
* 专用密钥 - 可用于为 JSON Web 令牌创建签名。此密钥必须保密，否则其他人可以创建有效的访问令牌。
* realmid - 用于使用户与其他用户注册表相区分的标识。对于 IBM 标识系统认证的用户，当前使用的值是“IBMid”，对于 Token Service 认证的服务标识，值为“iam”。
* identifier - 从不更改且唯一地识别一个用户注册表内部某个用户的标识（由 `realmid` 参数表示）。组合 <realmid>-<identifier> 必须始终生成可唯一识别的用户。对于 IBM 标识，会使用 IBM 唯一标识“IUI”。             
* 主体 - 身份的用户名。格式通常类似于电子邮件地址。对于 IBM 标识，这是身份的 IBM 标识。
* 定制声明 - JSON Web 令牌内部的其他非标准信息。

### 访问管理术语

* (PAP) 策略管理点 - 用于管理访问授权策略的点。
* (PDP) 策略决策点 - 用于在发出访问决策之前，根据授权策略对访问请求求值的点。
* (PEP) 策略实施点 - 用于拦截用户对资源的访问请求，向 PDP 发出决策请求以获取访问决策（即，是批准还是拒绝对资源的访问），然后对收到的决策执行操作的点。
* (PIP) 策略信息点 - 充当属性值的来源（即，资源、主体和环境）的系统实体。
* (PRP) 策略检索点 - 存储 XACML 访问授权策略的点，通常为数据库或文件系统。
* 主体 - 资源和主体授权对中的“对象”，例如用户或组。资源是指主体可以访问的资源。
* 角色 - 可以分配给用户、用户组、系统、服务或应用程序的许可权集合，以支持其执行特定任务。
* 资源 - 可以对其执行操作的物理或逻辑对象，例如组织、空间、数据库或表。
* 条件 - 求值为“True”、“False”或“Indeterminate”的函数。
* 操作 - 一种定义的任务，作为事件的结果，应用程序对对象或资源执行该任务。
* 策略 - 一组规则、规则组合算法的标识和（可选）一组责任或建议。可以是策略集的组成部分。

## 系统定义的角色
{: #system_defined_roles}

IBM Cloud 角色表示操作的集合，这些操作由 IAM 启用的服务提供。

通过将操作分组为角色，能灵活地使用一组最少的系统定义角色来支持对任何服务或资源的操作。例如，如果需要 VM、存储器和网络的`管理员`，那么可以通过仅更改策略的目标，将`管理员`角色用于所有这三项：VM 的`管理员`、存储器的`管理员`和网络的`管理员`。

*IBM Cloud IAM 不会执行的操作*：其他访问管理系统使用的替代方法是将资源构建到角色中。这种方法会无意中为系统中引入的每种资源类型生成新的角色名称。例如，通过此方法，您将需要 `VMAdministrator` 角色、`StorageAdministrator` 角色和 `NetworkAdministrator` 角色来承担 VM、存储器和网络资源的管理工作。


下表显示了 IAM 系统定义的角色和映射到这些角色的操作的示例。

|IBM Cloud 角色名称| 描述 | 示例操作|
|:-----------------|:-----------------|:-----------------|
|查看者|不会更改状态的操作（即，只读操作）| <ul><li>列出设备</li><li>读取存储对象</li><li>运行查询</li><li>执行搜索</li></ul>|
|编辑者|可以修改状态和创建/删除子资源的操作|<ul><li>创建 VM</li><li>删除 VM</li><li>连接存储器</li><li>重新引导</li><li>启动/停止</li><li>重命名</li></ul>|
|操作员|配置和运行资源所需的操作|<ul><li>更新配置</li><li>启动/停止 VM</li><li>查看日志</li><li>备份/复原</li></ul>|
|管理员|所有操作，包括管理访问控制的能力|<ul><li>邀请用户</li><li>创建 VM</li>更新用户访问策略</li><li>列出设备</li><li>创建 VM</li><li>删除 VM</li><li>连接存储器</li><li>重新引导</li><li>启动/停止</li><li>重命名</li><li>备份/复原</li></ul>|
|记帐管理员|与记帐管理相关的操作|<ul><li>更新信用卡</li><li>列出发票</li><li>下载发票</li></ul>|

系统定义的角色的最新列表可以通过 PAP 微服务查询：

Curl 命令： 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## 服务操作格式
{: #action_format}

操作必须定义为下面两种格式中的一种格式：
  
* 标准：

    `<service-name>.<component>.<verb>`
* 访问控制拦截点： 

    `<METHOD> /<api_route>`
  
### 标准
大部分服务会直接调用 IAM PDP，并可以修改源代码以支持标准操作格式。  
 
 此格式必须包含所有三个部分，并且只能使用字母数字，不能包含空格以及除“-”以外的其他特殊字符。

`<service-name>.<component>.<verb>`

其中 
* service-name - 在 CRN service-name 字段中定义的服务名称。
* component - 服务的资源或子资源。
* verb - 用于为服务名称组件定义受支持操作的动词。 
  
例如：`key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### REST API 访问控制拦截点
{: intercept_point}

在某些情况下，REST API 请求会通过充当访问控制拦截点的网关进行定向。在调用实际 REST API 服务之前，会从该拦截点直接调用 IAM PDP。用于处理 REST API 请求的服务从不会调用 IAM PDP。

拦截点仅知道有关 REST API 路径以及要将请求发送到的目标端点的信息。有关更多详细信息，请参阅[访问控制拦截点注意事项](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview)。


 此格式必须包含所有两个部分，并支持 URL 的安全字符，如 [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt) 所指定。
 
 
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

# 实验室服务标识和 API 密钥

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


