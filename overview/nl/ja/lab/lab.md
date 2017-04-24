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

IBM Cloud IAM により、ユーザーとサービスの ID、および、そうした ID のリソースへのアクセスを安全に管理することができます。管理を許可されたアクセス・オプションに応じて、アカウント全体または組織全体のユーザーの表示および管理を行えます。ユーザーの招待、ユーザーおよび割り当てられた役割の管理、アクセスできるアカウントや組織の管理など、ユーザーに関するすべての操作を実行できます。アカウント所有者は、現行アカウントで、役割に関係なく、自分とユーザーがともにメンバーとなっているアクセス・オプションを管理できます。

ID 管理には、以下のものがあります。
 * ユーザー管理 
   * ユーザー情報の作成、削除、更新
   * API キー管理
   * トークン作成、リフレッシュ、および交換
   * ユーザー ID 認証
 * サービス ID 管理
   * ユーザー情報の作成、削除、更新
   * API キー管理
   * トークン作成、リフレッシュ、および交換
   * サービス ID 認証
   
   
アクセス管理には、以下のものがあります。
 * ポリシー管理
   * ポリシーの作成、削除、更新
 * リソースへのアクセスに関する判断
 
## ID の概要
{: #identity}

Cloud IAM Token Service は、IBM Cloud の認証サービスで、[OAuth 2.0]( https://tools.ietf.org/html/rfc6749)、[JWT](https://tools.ietf.org/html/rfc7519)、[JWT Profile](https://tools.ietf.org/html/rfc7523)、および [JWKS](https://tools.ietf.org/html/rfc7517) で規定されたオープン・スタンダードを基に構築されています。

Token Service の焦点の 1 つは、IBM Cloud プラットフォームの開発者、オペレーター、および管理者の認証です。この認証で、Token Service はユーザーを認証するために IBMid システムに接続されますが、専用環境およびローカル環境では、LDAP のようなお客様が選択した認証システムに接続することが可能です。 

IAM トークンを取得するには、`password` のような標準 OAuth 2.0 認可タイプを使用できます。以下に例を示します。
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

OAuth 2.0 の拡張として、トークンをアカウント固有にするためにアカウント情報を提供する必要があります。また、さまざまな応答タイプをリストして、CloudFoundry API または IMS API による対話のために `UAA` または `IMS` のトークンを取得することができます。

Cloud IAM Token Service により、ユーザーの API キーの作成、更新、削除、および使用が可能になります。そうした API キーは、API 呼び出しまたは Bluemix コンソールで作成できます。API キーを活用するために、利用者は以下の拡張認可タイプを使用することができます。
```
curl
    -u "<clientid>:<clientsecret>"
    –H "Content-Type: application/x-www-form-urlencoded"
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

取得したトークンは、パスワード認可または UI ログインで取得したものと同じように使用できます。

さらなるバリエーションとして、Cloud IAM Token Service では、UI による対話的なログインが可能です。これは、OAuth 2.0 認可タイプ `authorization_code` を使用して実装されます。認証フェーズ中に複数の Web ブラウザー・リダイレクトが発生するため、`OAuth Dance` とも呼ばれています。

Token Service のもう 1 つの焦点は、サービス ID、およびサービス ID 用の API キーを作成する機能です。サービス ID は、「機能 ID」や「アプリケーション ID」に似たもので、ユーザーを表すのではなく、サービスに対して認証するために使用されます。

ユーザーはサービス ID を作成し、Bluemix アカウント、CloudFoundry 組織、CloudFoundry スペースのようなスコープにそれらをバインドすることができます。このバインドは、サービス ID に、それが入るコンテナーを示すために行われます。また、このコンテナーでは、サービス ID の更新および削除を誰ができるか、そのサービス ID に関連付けられた API キーの作成、更新、読み取り、削除を誰ができるかも定義します。サービス ID はユーザーに関連しません。

サービス ID の使用法の理解を深めるために、API をデモンストレーションする[デモ・アプリケーション](https://iam.ng.bluemix.net/demo)を試すことができます。

## アクセス管理の概要
{: #access_management}

IAM は、[NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf) の資料で示唆された条件の属性ベース・アクセス制御 (ABAC: Attribute Based Access Control) システムです。  

IAM では属性を組み合わせて、リソースへのアクセスを決定します。IAM ポリシーには、役割、ユーザー/サービス ID 属性、リソース属性、および状態に適用されるルールが含まれます。これにより、ユーザーおよびサービス ID のアクセスを定義するための柔軟で強力なアプローチが実現されます。

例えば、仮想マシンで、VM123 に以下の属性がある場合があります。 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
これらのリソース属性を任意に組み合わせて、ポリシーを作成できます。

詳しい例については、[IAM ポリシーの例](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples)を参照してください。

ABAC は、事前定義の役割がユーザーに割り当てられる役割ベース・アクセス制御 (RBAC: Role Based Access Control) とは異なります。これらの事前定義の役割には特定の特権が含まれ、その役割を持つユーザーには、該当の役割で定義されたすべての特権があります。 
 
例えば、仮想マシンの `Administrator` 役割があります。この役割は、任意の仮想マシン・リソースにおけるすべての Administrator タイプ特権を意味します。 

ABAC について簡単に考えると、以下のようになります。

1. ユーザー、リソース、コンテキスト、およびアクションがあります。
1. ユーザー、リソース、コンテキスト、およびアクションの各インスタンスには、固有の ID があります。
1. 各インスタンスには、属性が与えられます。
   基本的にこれは、「インスタンスに関する許可の見地からの事実」を意味します。
   例:
   1. ユーザーは Pisces で、1960 年代に生まれました。
   1. リソースは、野球チームの名簿です。
   1. コンテキストは、東部標準時の午前 9:00 から午後 5:00 です。
   1. アクションは「更新可能」です。
1. ユーザーがリソースにアクションを実行するための許可をどんな属性セットが持っているかを決定するために、ポリシーが作成されます。
1. ユーザーによってリソースにアクションを実行する要求が行われると、要求が許可されるかどうかをポリシーで調べます。

許可シーケンスの詳細ビューを以下のイメージで示します。

![許可シーケンス](auth_sequence.png)

## サービスのアクセス制御のセットアップ
{: #setup_access_mgmt}

{{site.data.keyword.Bluemix_notm}} へのサービスのオンボードは、Cloud IAM でのサービスのオンボードとは異なる一連操作です。技術的には、{{site.data.keyword.Bluemix_notm}} と Cloud IAM でのオンボードは独立して任意の順序で行えます。{{site.data.keyword.Bluemix_notm}} サービスのオンボード・プロセスが Cloud IAM のオンボードも含むように、Cloud IAM チームが {{site.data.keyword.Bluemix_notm}} サービス・オンボード・チームと作業しています。

サービスのアクセス制御をセットアップするには、オンボード・プロセスの中で以下のステップを使用する必要があります。

### ステップ 1: この HTTP 要求を行ってサービス ID を作成します。
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

Curl コマンド:
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

 `curl` コマンドで使用される `Service id` および `Service crn` の値について、以下で詳細に説明します。
  
#### サービス ID 
  
サービス ID 名は、サービスの crn に出現するサービス名と同じにすることが可能です。
  
サービス ID は、アカウント、組織、またはスペースにバインドされなければなりません。このバインドでは、サービス ID を誰が管理できるかを決定します。例えば、サービス ID がバインドされた管理者は、更新または削除を行えます。{{site.data.keyword.Bluemix_notm}} トークンは、ID をバインドするアカウント、組織、およびスペースへのアクセス権限を持たなければなりません。アカウントにバインドするには、`boundTo` crn が以下のようなものでなければなりません。 

`crn:v1:::<service name>::a/<account id>:::` 
  
組織の場合には、以下のようなものでなければなりません。
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
スペースの場合には、以下のようなものでなければなりません。
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
指定された `boundTo` 値は、サービス ID がどのリソースにアクセスできるかには影響しません。 
  
IAM アクセス・ポリシーは、サービス ID がどのリソースにアクセスできるかを制御します。サービス ID が IBM 組織にバインドされていても、サービス ID にその組織外のリソースへのアクセスを許可する IAM ポリシーを作成可能です。IAM でオンボードすると、IAM チームによって作成される最初のアクセス・ポリシーでは、サービス ID に、サービスが所有する任意のリソースに対するポリシーの作成が許可されます。

この API と関連 API について詳しくは、[createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) を参照してください。

#### サービス crn

`boundTo` crn の service-name は、サービスの crn に出現するサービス名と一致する必要があります。
  
これらのフィールドの指定に関するヘルプについては、[CRN の仕様](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md)を参照してください。

応答から、metadata->uuid と metadata->crn を保存します。これらはサービス ID とサービス ID の crn です。


### ステップ 2: [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters) の AccessControl Squad にコンタクトします。 
サービス ID には、サービスのリソースに対するポリシーの管理者役割が付与されます。

以下のフォーマットを使用してください。
```
IAM adopter service info

service id: ステップ 1 の UUID
service name: サービスの crn に示されるサービス名
```
{: codeblock}

### ステップ 3: サービス ID から api-key を作成する必要があります。以下の http 要求を使用してください。
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

Curl コマンド: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` は、サービス ID の crn (ステップ 1 の応答から保存されたフィールド metadata->crn) でなければなりません。name と description は任意のものにすることができます。

応答から entity->apiKey を保存します。

この API と関連 API について詳しくは、[createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) を参照してください。

### ステップ 4: サービス ID API キーのアクセス・トークンを取得します。 

許可が設定されたら、サービスは、サービスのリソースに対する PAP 要求および PDP 要求を行えます。

ステップ 3 のエンティティー **apiKey** フィールドを使用します。これは API キーの値 (apikey_value) です。

  * その後、以下のようにして API キー値でトークンを取得します (必ず、エスケープ文字を使用してください)。

    Curl コマンド:
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

結果の **access_token** フィールドを使用します。これは (サービス ID の) api-key トークンです。上記の curl コマンドで使用されたとき、**access_token** は URL エンコードされる必要があります。


### ステップ 5: サービス名に可能なサービス・アクションのリストを登録します。

  a. サービス・アクションを IAM システム定義役割にマップします。このマッピングは、後でサービスの登録中に使用されます。

  * IAM システム定義役割のリストは、以下の要求を実行して入手できます。
  
Curl コマンド:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**注:** サービス登録のペイロードでは、IAM システム定義役割の *crn バージョン* を使用してください。

サービス・アクションを役割にマッピングする例を以下に示します。

  <table>
    <tr>
      <th>API エンドポイント</th>
      <th>サービス・アクション</th>
      <th>IAM システム定義役割</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>管理者</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>ビューアー、エディター、管理者</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>エディター、管理者</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>管理者</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>エディター、管理者</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>エディター、管理者</td>
    </tr>
  </table>

  b. 以下のコマンド・ラインを使用して、サービスを `PAP` に登録します。
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
  
アクションは、
[サービス・アクション・フォーマット](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format)で規定されたように定義する必要があります。
  
例えば、標準フォーマットの使用時には以下のようにします。

  `<service-name>.<component>.<verb>`
  
  上記の例のアクション `key-protect.keys.decode` を使用 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### ステップ 6: ステップ 5 の詳細に従ってサービスが登録されたことを検証します。

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### ステップ 7 (オプション): ステップ 5 で登録したサービスを削除します。

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### ステップ 8: PDP の許可をチェックするために PEP SDK を使用するようにサービスを構成します。対応する SDK 言語を選択してください。

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## 用語
{: #terminology}

### ID の用語

* IBMid - IBM Cloud、IBM アプリケーション、コミュニティー、サポートにアクセスするために IBM が提供し、ホストする ID。
* ユーザー ID - 実際の人を表す ID。
* サービス ID - テクニカル・ユーザー、マシン、アプリケーション、またはサービスを表す ID。テクニカル・ユーザーも表す「機能 ID」や「アプリケーション ID」と似ていますが、「ユーザー ID」エンティティー・タイプを使用します。
* OAuth 2.0 - ターゲット・サービスに資格情報を提供せずに、アプリケーションおよび API へのアクセスを許可するオープン・スタンダード。認証情報を含むためにも、OAuth は使用されます。
* OpenID Connect - OAuth 2.0 の上に構築され、認証ユーザーに関する情報の提供に焦点をあてたオープン・スタンダード。
* クライアント ID - OAuth 2.0 準拠エンドポイントと対話するアプリケーションには、認証する秘密クライアント ID/秘密のペアが必要です。アプリケーションは、クライアント ID を取得するために Token Service に登録する必要があります。
* トークン・エンドポイント - クライアントが、ユーザー名またはパスワード、権限認可またはリフレッシュ・トークンのような ID 情報を示すことで 1 つ以上のトークンを取得するために使用します。
* 許可エンドポイント - クライアントが、トークン・サービスに対して UI を通じてユーザーを認証するために使用します。
* トークン - ID の認証または許可あるいはその両方をアプリケーションが取得できるようにする不透明または透明のストリング。
* アクセス・トークン - このトークンは、API に ID 情報として送るために使用されます。ID 情報を含み、有効なのは短時間のみです。
* リフレッシュ・トークン - このトークンは、認証を要求したクライアント上にのみ保管されます。アクセス・トークンが期限切れの場合に、新しいアクセス・トークンを取得する (つまり、アクセス・トークンをリフレッシュする) ために使用されます。リフレッシュ・トークンが長く存続する間に、アクセス・トークンのリフレッシュの目的以外でリフレッシュ・トークンがクライアント・システムの外部に出てはなりません。
* ID Cookie - IBM Cloud Token Service にログインすると、ID を含む Cookie がブラウザーに発行されます。この Cookie が存在して有効である限り、ログインを再要求されることはありません。24 時間経過するか、IBM Cloud Token Service からログアウトするか、ブラウザーを閉じると、期限切れになります。
* JSON Web トークン - アクセス・トークンを表す JSON ベース標準 (RFC 7519)。アクセス・トークンのコンテンツは透明です (つまり、簡単に読み取れます)。JWT ベース・トークンは通常、そのトークンのオリジンの証明を検証できるように署名されています。
* 公開鍵 - JSON Web トークンの署名の検証に使用できます。非対称暗号化を使用している場合、公開鍵はクライアントによる消費のために安全に公開できます。
* 秘密鍵 - JSON Web トークンの署名の作成に使用できます。この鍵は、秘密を保たれなければなりません。そうでないと、他者が有効なアクセス・トークンを作成する可能性があります。
* realmid -異なるユーザー・レジストリーからのユーザーを区別するための識別子。現在使用されている値は、IBMid システムで認証されたユーザー用の「IBMid」と、Token Service によって認証されたサービス ID 用の「iam」です。
* identifier - (`realmid` パラメーターで示された) 1 つのユーザー・レジストリー内でユーザーを一意的に識別する不変の識別子。<realmid>-<identifier> を組み合わせて、常に、一意的に識別可能なユーザーになる必要があります。IBMid の場合、IBM 固有の ID の「IUI」が使用されます。             
* サブジェクト - 該当 ID のユーザー名。多くの場合、E メール・アドレスと同様の形式です。IBMid のケースで、これは該当 ID の IBMid です。
* カスタム・クレーム - JSON Web トークン内の追加の非標準情報。

### アクセス管理の用語

* (PAP) ポリシー管理ポイント (Policy Administration Point) - アクセス許可ポリシーを管理するポイント。
* (PDP) ポリシー決定ポイント (Policy Decision Point) - アクセス決定を発行する前に、許可ポリシーに対してアクセス要求を評価するポイント。
* (PEP) ポリシー実施ポイント (Policy Enforcement Point) - リソースへのユーザーのアクセス要求をインターセプトし、PDP に決定要求を行ってアクセス決定 (つまり、リソースへのアクセスが承認されるか、拒否されるか) を取得し、受け取った決定に基づいて動作するポイント。
* (PIP) ポリシー情報ポイント (Policy Information Point) - 属性値のソースとして機能するシステム・エンティティー (つまり、リソース、サブジェクト、環境)。
* (PRP) ポリシー取得ポイント (Policy Retrieval Point) - XACML アクセス許可ポリシーが保管されるポイント。一般的に、データベースまたはファイル・システム。
* サブジェクト - リソースとサブジェクトの許可ペアにおける「誰」の部分。ユーザーまたはグループなど。リソースは、サブジェクトがどのリソースにアクセスできるかを指します。
* 役割 - ユーザー、ユーザー・グループ、システム、サービス、またはアプリケーションに対して割り当てられ、特定タスクの実行を可能にする許可の集合。
* リソース - アクションを実行可能な物理オブジェクトまたは論理オブジェクト。組織、スペース、データベース、または表など。
* 条件 - "True (真)"、"False (偽)"、または "Indeterminate (不確定)" に評価される関数。
* アクション - イベントの結果、アプリケーションがオブジェクトまたはリソースで実行する定義済みタスク。
* ポリシー - ルールのセット、ルール結合アルゴリズムの識別子、および (オプションで) 一連の責務またはアドバイス。ポリシー・セットのコンポーネントであることが可能です。

## システム定義役割
{: #system_defined_roles}

IBM クラウド役割はアクションの集合を表します。これらのアクションは IAM 対応サービスによって提供されます。

役割でアクションをグループ化することで、システム定義役割の最小セットを使用してどんなサービスやリソースにもアクションを柔軟にサポートできます。
例えば、VM、ストレージ、ネットワーキングに `Administrator` が必要な場合、
3 つすべてに `Administrator` 役割を使用して、ポリシーのターゲットだけを変更することができます。
VM の `Administrator`、ストレージの `Administrator`、ネットワーキングの
`Administrator` のようになります。

*IBM Cloud IAM と他との違い*: 他のアクセス管理システムで使用される別の方法では、役割にリソースを組み込みます。
このアプローチでは、システムに導入されるすべてのタイプのリソースごとに新しい役割名が生じます。
例えば、VM、ストレージ、ネットワークのリソースの管理に対応するために、このアプローチを使用すると `VMAdministrator` 役割、
`StorageAdministrator` 役割、`NetworkAdministrator` 役割が必要になります。


以下の表に、IAM システム定義役割と、それらにマップされるアクションの例を示します。

|IBM クラウド役割名| 説明 | アクションの例|
|:-----------------|:-----------------|:-----------------|
|ビューアー|状態を変更しないアクション (つまり、読み取り専用)| <ul><li>デバイスのリスト</li><li>ストレージ・オブジェクトの読み取り</li><li>照会の実行</li><li>検索の実行</li></ul>|
|エディター|状態の変更およびサブリソースの作成/削除が可能なアクション|<ul><li>VM の作成</li><li>VM の削除</li><li>ストレージの接続</li><li>リブート</li><li>開始と停止</li><li>名前変更</li></ul>|
|オペレーター|リソースの構成および運用に必要なアクション|<ul><li>構成の更新</li><li>VM の開始と停止</li><li>ログの表示</li><li>バックアップ/リストア</li></ul>|
|管理者|アクセス制御の管理機能を含むすべてのアクション|<ul><li>ユーザーの招待</li><li>VM の作成</li>ユーザー・アクセス・ポリシーの更新</li><li>デバイスのリスト</li><li>VM の作成</li><li>VM の削除</li><li>ストレージの接続</li><li>リブート</li><li>開始と停止</li><li>名前変更</li><li>バックアップ/リストア</li></ul>|
|請求管理者|請求の管理に関連するアクション|<ul><li>クレジット・カードの更新</li><li>請求書のリスト</li><li>請求書のダウンロード</li></ul>|

システム定義役割の最新リストは、以下の PAP マイクロサービスで照会できます。

Curl コマンド: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## サービス・アクションのフォーマット
{: #action_format}

アクションは、次の 2 つのフォーマットの 1 つで定義する必要があります。
  
* 標準:

    `<service-name>.<component>.<verb>`
* アクセス制御インターセプト・ポイント: 

    `<METHOD> /<api_route>`
  
### Standard
ほとんどのサービスは IAM PDP を直接呼び出し、標準のアクション・フォーマット設定をサポートするようにソース・コードを変更することが可能です。  
 
 このフォーマットは、3 つのすべてのパートを含む必要があります。英数字を使用し、スペースも「-」以外の特殊文字も使用できません。

`<service-name>.<component>.<verb>`

各部の意味は、次のとおりです。 
* service-name - CRN service-name フィールドで定義されたサービス名。
* component - サービスのリソースまたはサブリソース。
* verb - サービス名のコンポーネントにサポートされるアクションを定義する verb。 
  
例として、`key-protect.keys.decode` があります。 
* service-name = key-protect
* component = keys
* verb = decode

### REST API アクセス制御インターセプト・ポイント
{: intercept_point}

場合によって、REST API 要求は、アクセス制御インターセプト・ポイントとして機能するゲートウェイを通して送信されます。実際の REST API サービスを呼び出す前に、IAM PDP がインターセプト・ポイントから直接呼び出されます。REST API 要求を処理するサービスが IAM PDP を呼び出すことはありません。

REST API の経路と、要求送信先のエンドポイントについては、インターセプト・ポイントのみが把握しています。詳細については、[アクセス制御インターセプト・ポイントの考慮事項](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview)を参照してください。


 このフォーマットは、両方のパートをすべて含む必要があり、[RFC 1738](https://www.ietf.org/rfc/rfc1738.txt) で示された、URL に安全に使用できる文字をサポートします。
 
 
`<METHOD> /<api_route>`
  
各部の意味は、次のとおりです。
* METHOD - REST API メソッド。 
* api_route - REST API の URI。

例として、`GET /v1/things/thing123` があります。
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

# Lab サービス ID と API キー

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


