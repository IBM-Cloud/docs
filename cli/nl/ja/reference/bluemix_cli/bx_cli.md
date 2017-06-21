---



copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) コマンド
{: #bluemix_cli}

バージョン: 0.5.2

{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェース (CLI) では、ユーザーが {{site.data.keyword.Bluemix_notm}} と対話できるように、名前空間別にグループ化したコマンドのセットが提供されています。
{{site.data.keyword.Bluemix_notm}} コマンドには、既存の cf コ
マンドのラッパーになっているものもあれば、
{{site.data.keyword.Bluemix_notm}} ユーザー向けの拡張機能を提
供するものもあります。以下の説明では、{{site.data.keyword.Bluemix_notm}}
CLI によってサポートされるコマンドをリストし、名前、オプショ
ン、使用法、前提条件、説明、および例を示します。
{:shortdesc}

**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件となるアクションのないコマンドでは、**なし**とリストされています。それ以外の場合、前提条件には以下のアクションのうちの 1 つ以上が含まれます。

<dl>
<dt>エンドポイント</dt>
<dd>このコマンドを使用する前に、<code>bluemix api</code> を介して API エンドポイントを設定する必要があります。</dd>
<dt>ログイン</dt>
<dd>このコマンドを使用する前に、<code>bluemix login</code> コマンドを使用してログインする必要があります。フェデレーテッド ID でログインする場合は、「--sso」オプションを使用してワンタイム・パスコードで認証するか、「--apikey」を使用して API キーで認証します。{{site.data.keyword.Bluemix_notm}} コンソールで**「管理」** &gt; **「セキュリティー」** &gt; **「Bluemix API キー」**に移動して、API キーを作成します。
</dd>
<dt>ターゲット</dt>
<dd>このコマンドを使用する前に、<code>bluemix target</code> コマンドを使用して組織およびスペースを設定する必要があります。</dd>
<dt>Docker</dt>
<dd>このコマンドを実行するためには、Docker CLI (docker) がインストールされている必要があります。</dd>
</dl>

## bluemix コマンドの索引
{: #bx_commands_index}

以下の表の索引を使用して、使用頻度の高い bluemix コマンドを
参照してください。

**注:** 短形式の Bluemix コマンドを使用できます。例えば、`bx api` は `bluemix api` の短形式です。



<table summary="汎用 Bluemix コマンド。">
 <caption>表 1. 汎用 bluemix コマンド</caption>
 <thead>
 <th colspan="5">汎用 Bluemix コマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix help](bx_cli.html#bluemix_help)</td>
 <td>[bluemix api](bx_cli.html#bluemix_api)</td>
 <td>[bluemix login](bx_cli.html#bluemix_login)</td>
 <td>[bluemix logout](bx_cli.html#bluemix_logout)</td>
 <td>[bluemix target](bx_cli.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](bx_cli.html#bluemix_info) </td>
 <td>[bluemix regions](bx_cli.html#bluemix_regions) </td>
 <td>[bluemix config](bx_cli.html#bluemix_config)</td>
 <td>[bluemix curl](bx_cli.html#bluemix_curl)</td>
 <td>[bluemix update](bx_cli.html#bluemix_update)</td>
 </tr>
 </tbody>
 </table>

<table summary="アカウント、組織、スペース、役割、および API キーを管理するために使用できる bluemix コマンド。">
<caption>表 2. アカウント、組織、スペース、役割、および API キーを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">アカウント、組織、スペース、役割、および API キーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](bx_cli.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](bx_cli.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](bx_cli.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](bx_cli.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](bx_cli.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](bx_cli.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](bx_cli.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](bx_cli.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](bx_cli.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](bx_cli.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](bx_cli.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam org-users](bx_cli.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-user-add](bx_cli.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](bx_cli.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-roles](bx_cli.html#bluemix_iam_org_roles)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-role-set](bx_cli.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](bx_cli.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](bx_cli.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-roles](bx_cli.html#bluemix_iam_space_roles)</td>
 <td>[bluemix iam space-role-set](bx_cli.html#bluemix_iam_space_role_set)</td>
</tr>
 <tr>
 <td>[bluemix iam space-role-unset](bx_cli.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix iam accounts](bx_cli.html#bluemix_iam_accounts)</td>
 <td>[bluemix iam org-account](bx_cli.html#bluemix_iam_org_account)</td>
 <td>[bluemix iam account-users](bx_cli.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](bx_cli.html#bluemix_iam_account_users_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam account-user-invite](bx_cli.html#bluemix_iam_account_user_invite)</td>
  <td>[bluemix iam account-user-reinvite](bx_cli.html#bluemix_iam_account_user_reinvite)</td>
  <td>[bluemix iam api-keys](bx_cli.html#bluemix_iam_api_keys)</td>
  <td>[bluemix iam api-key-create](bx_cli.html#bluemix_iam_api_key_create)</td>
  <td>[bluemix iam api-key-delete](bx_cli.html#bluemix_iam_api_key_delete)</td>
 </tr>
 <tr>
  <td>[bluemix iam api-key-update](bx_cli.html#bluemix_iam_api_key_update)</td>
  <td></td>
  <td></td>
  <td></td>
  <td></td>
 </tr>
 </tbody>
 </table>

<table summary="CF アプリとアプリ関連ドメイン、経路、および証明書を管理するために使用できる bluemix コマンド。">
<caption>表 3. CF アプリとアプリ関連ドメイン、経路、および証明書を管理するためのコマンド</caption>
 <thead>
 <th colspan="5">CF アプリとアプリ関連ドメイン、経路、および証明書を管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](bx_cli.html#bluemix_app_push)</td>
 <td>[bluemix app list](bx_cli.html#bluemix_app_list)</td>
 <td>[bluemix app show](bx_cli.html#bluemix_app_show)</td>
 <td>[bluemix app delete](bx_cli.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](bx_cli.html#bluemix_app_rename)</td>
 </tr>
 <tr>
 <td>[bluemix app start](bx_cli.html#bluemix_app_start)</td>
 <td>[bluemix app stop](bx_cli.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](bx_cli.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](bx_cli.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](bx_cli.html#bluemix_app_instance_restart)</td>
 </tr>
 <tr>
 <td>[bluemix app events](bx_cli.html#bluemix_app_events)</td>
 <td>[bluemix app files](bx_cli.html#bluemix_app_files)</td>
 <td>[bluemix app logs](bx_cli.html#bluemix_app_logs)</td>
 <td>[bluemix app env](bx_cli.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](bx_cli.html#bluemix_app_env_set)</td>
 </tr>
 <tr>
 <td>[bluemix app env-unset](bx_cli.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](bx_cli.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack-show](bx_cli.html#bluemix_app_stack_show)</td>
 <td>[bluemix app manifest-create](bx_cli.html#bluemix_app_manifest_create)</td>
 <td>[bluemix app domain-cert](bx_cli.html#bluemix_app_domain_cert)</td>
 </tr>
 <tr>
  <td>[bluemix app domain-cert-add](bx_cli.html#bluemix_app_domain_cert_add)</td>
  <td>[bluemix app domain-cert-remove](bx_cli.html#bluemix_app_domain_cert_remove)</td>
  <td>[bluemix app domains](bx_cli.html#bluemix_app_domains)</td>
  <td>[bluemix app domain-create](bx_cli.html#bluemix_app_domain_create)</td>
  <td>[bluemix app domain-delete](bx_cli.html#bluemix_app_domain_delete)</td>
 </tr>
 <tr>
  <td>[bluemix app shared-domain-create](bx_cli.html#bluemix_app_shared_domain_create)</td>
  <td>[bluemix app shared-domain-delete](bx_cli.html#bluemix_app_shared_domain_delete)</td>
  <td>[bluemix app routes](bx_cli.html#bluemix_app_routes)</td>
  <td>[bluemix app route-check](bx_cli.html#bluemix_app_route_check)</td>
  <td>[bluemix app route-map](bx_cli.html#bluemix_app_route_map)</td>
 </tr>
 <tr>
  <td>[bluemix app route-unmap](bx_cli.html#bluemix_app_route_unmap)</td>
  <td>[bluemix app route-create](bx_cli.html#bluemix_app_route_create)</td>
  <td>[bluemix app route-delete](bx_cli.html#bluemix_app_route_delete)</td>
  <td>[bluemix app orphaned-routes-delete](bx_cli.html#bluemix_app_orphaned_routes_delete)</td>
  <td></td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix サービスの管理に使用することができる Bluemix コマンド。">
 <caption>表 4. Bluemix サービスを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">Bluemix サービスを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix service offerings](bx_cli.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](bx_cli.html#bluemix_service_list)</td>
 <td>[bluemix service show](bx_cli.html#bluemix_service_show)</td>
 <td>[bluemix service create](bx_cli.html#bluemix_service_create)</td>
 <td>[bluemix service update](bx_cli.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](bx_cli.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](bx_cli.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](bx_cli.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](bx_cli.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](bx_cli.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](bx_cli.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](bx_cli.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](bx_cli.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](bx_cli.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](bx_cli.html#bluemix_service_user_provided_update)</td>
 </tr>
  </tbody>
 </table>

<table summary="Bluemix カタログ、プラグイン、請求、およびセキュリティー設定の管理に使用できる Bluemix コマンド。">
 <caption>表 5. Bluemix カタログ、プラグイン、請求、およびセキュリティー設定を管理するためのコマンド</caption>
 <thead>
 <th colspan="5">Bluemix カタログ、プラグイン、請求、およびセキュリティー設定を管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix catalog templates](bx_cli.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](bx_cli.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](bx_cli.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](bx_cli.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](bx_cli.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](bx_cli.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](bx_cli.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](bx_cli.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](bx_cli.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](bx_cli.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix plugin update](bx_cli.html#bluemix_plugin_update)</td>
 <td>[bluemix billing account-usage](bx_cli.html#bluemix_billing_account_usage)</td>
 <td>[bluemix billing org-usage](bx_cli.html#bluemix_billing_org_usage)</td>
 <td>[bluemix billing orgs-usage-summary](bx_cli.html#bluemix_billing_orgs_usage_summary)</td>
 <td></td>
 </tr>
 </tbody>
 </table>
 
## bluemix help
{: #bluemix_help}
{{site.data.keyword.Bluemix_notm}} CLI の第 1 レベルの組み込みコマンドおよびサポートされる名前空間に関する一般ヘルプを表示するか、または、特定の組み込みコマンドまたは名前空間に関するヘルプを表示します。

```
bluemix help [COMMAND|NAMESPACE]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>COMMAND|NAMESPACE (オプション)</dt>
   <dd>ヘルプを表示する対象のコマンドまたは名前空間。指定されない場合、{{site.data.keyword.Bluemix_notm}} CLI の一般ヘルプが表示されます。</dd>
   </dl>



<strong>例</strong>:

{{site.data.keyword.Bluemix_notm}} CLI の一般ヘルプを表示します。

```
bluemix help
```

`info` コマンドのヘルプを表示します。

```
bluemix help info
```



## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API エンドポイントを設定または表示します。

```
bluemix api [API_ENDPOINT] [--unset] [--skip-ssl-validation]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>API_ENDPOINT (オプション)</dt>
   <dd>ターゲットの API エンドポイント (例えば `https://api.chinabluemix.net`)。 *API_ENDPOINT* オプションと `--unset` オプションのどちらも指定されない場合、現行 API エンドポイントが表示されます。</dd>
   <dt>--unset (オプション)</dt>
   <dd>API エンドポイント設定を削除します。</dd>
   <dt>--skip-ssl-validation (オプション)</dt>
   <dd>HTTP 要求の SSL 検証をバイパスします。 </dd>
   </dl>
<strong>例</strong>:

API エンドポイントを api.chinabluemix.net に設定します。

```
bluemix api api.chinabluemix.net
```

```
bluemix api https://api.chinabluemix.net --skip-ssl-validation
```

現行 API エンドポイントを表示します。

```
bluemix api
```

API エンドポイントを設定解除します。

```
bluemix api --unset
```


## bluemix login
{: #bluemix_login}

ユーザーをログインします。 

```
bluemix login [OPTIONS...]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
<dl>
  <dt>-a <i>API_ENDPOINT</i> (オプション)</dt>
  <dd> API エンドポイント (例: api.ng.bluemix.net)</dd>
  <dt> --apikey <i>API_KEY または @API_KEY_FILE_PATH</i>
  <dd> API キーの内容、または @ で示された API キー・ファイルのパス</dd>
  <dt> --sso (オプション) </dt>
  <dd> ワンタイム・パスコードを使用してログインします </dd>
  <dt> -u <i>USERNAME</i> (オプション)</dt>
  <dd> ユーザー名</dd>
  <dt> -p <i>PASSWORD</i> (オプション)</dt>
  <dd> パスワード</dd>
  <dt> -c <i>ACCOUNT_ID</i> (オプション) </dt>
  <dd> ターゲット・アカウントの ID</dd>
  <dt> -o <i>ORG_NAME</i> (オプション)</dt>
  <dd> ターゲット組織の名前 </dd>
  <dt> -s <i>SPACE_NAME</i> (オプション)</dt>
  <dd> ターゲット・スペースの名前</dd>
  <dt> --skip-ssl-validation (オプション) </dt>
  <dd> HTTP 要求の SSL 検証をバイパスします。このオプションは推奨されません。</dd>
</dl>

<strong>例</strong>:

対話式ログイン:

```
bluemix login```

ユーザー名とパスワードを使用してログインし、ターゲット・アカウント、組織、およびスペースを設定します。

```
bluemix login -u username -p password -c MyAccountID -o MyOrg -s MySpace
```

ワンタイム・パスコードを使用してログインし、ターゲット・アカウント、組織、およびスペースを設定します

```
bluemix login --sso -c MyAccountID -o MyOrg -s MySpace
```

API キーを使用してログインし、ターゲットを設定します。

* API キーにアカウントが関連付けられている

```
bluemix login --apikey api-key-string -o MyOrg -s MySpace
```

```
bluemix login --apikey @filename -o MyOrg -s MySpace
```

* API キーにアカウントが関連付けられていない

```
bluemix login --apikey api-key-string -c MyAccountID -o MyOrg -s MySpace
```

```
bluemix login --apikey @fileName -c MyAccountID -o MyOrg -s MySpace
```

<strong>注:</strong> API キーにアカウントが関連付けられている場合、別のアカウントへの切り替えは許可されません。


## bluemix logout
{: #bluemix_logout}

ユーザーをログアウトします。

```
bluemix logout
```

<strong>前提条件</strong>: なし


## bluemix target
{: #bluemix_target}


ターゲット・アカウント、地域、組織、またはスペースを設定するか表示します。

```
bluemix target [-c ACCOUNT_ID] [-r REGION] [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>-c <i>ACCOUNT_ID</i> (オプション)</dt>
   <dd>ターゲットとなるアカウントの ID。</dd>
   <dt>-r <i>REGION</i> (オプション)</dt>
   <dd>切り替える先の地域。</dd>
   <dt>-o <i>ORG_NAME</i> (オプション)</dt>
   <dd>ターゲットとなる組織の名前。</dd>
   <dt>-s <i>SPACE_NAME</i> (オプション)</dt>
   <dd>ターゲットとなるスペースの名前。</dd>
   </dl>
どのオプションも指定されていない場合、現行のアカウント、地域、組織、およびスペースが表示されます。

<strong>例</strong>:

現行のアカウント、組織、およびスペースを設定します

```
bluemix target -c MyAccountID -o MyOrg -s MySpace
```

新しい地域に切り替えます

```
bluemix target -r eu-gb
```

現行のアカウント、地域、組織、およびスペースを表示します。

```
bluemix target
```


## bluemix info
{: #bluemix_info}

基本的な {{site.data.keyword.Bluemix_notm}} 情報を表示します。これには、現行領域、クラウド・コントローラーのバージョン、および、いくつかの有用なエンドポイント (例えば、ログイン用のエンドポイントや、アクセス・トークン交換用のエンドポイントなど) が含まれます。

```
bluemix info
```

<strong>前提条件</strong>: エンドポイント


## bluemix config
{: #bluemix_config}


構成ファイルにデフォルト値を書き込みます。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR) | --check-version (true|false)
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>--http-timeout <i>TIMEOUT_IN_SECONDS</i></dt>
   <dd>HTTP 要求のタイムアウト値。デフォルト値は 60 秒です。</dd>
   <dt>--trace true|false|<i>path-to-file</i></dt>
   <dd>端末または指定されたファイルへの HTTP 要求をトレースします。</dd>
   <dt>--color true|false</dt>
   <dd>カラー出力を使用可能または使用不可にします。カラー出力はデフォルトで使用可能に設定されています。</dd>
   <dt>--locale <i>LOCALE|CLEAR</i></dt>
   <dd>デフォルト・ロケールを設定します。LOCALE が <i>CLEAR</i> の場合は、前のロケールが削除されます。</dd>
   <dt>--check-version true|false</dt>
   <dd>CLI バージョン・チェックを使用可能または使用不可にします。</dd>
   </dl>

一度に指定できるのは、これらのオプションの 1 つだけです。

<strong>例</strong>:

次のように、HTTP 要求タイムアウトを 30 秒に設定します。

```
bluemix config --http-timeout 30
```

次のように、HTTP 要求のトレース出力を使用可能にします。

```
bluemix config --trace true
```

次のように、指定されたファイル */home/usera/my_trace* への HTTP 要求をトレースします。

```
bluemix config --trace /home/usera/my_trace
```

次のように、カラー出力を使用不可にします。

```
bluemix config --color false
```

次のように、ロケールを zh_Hans に設定します。

```
bluemix config --locale zh_Hans
```

次のように、ロケール設定をクリアします。

```
bluemix config --locale CLEAR
```


## bluemix curl
{: #bluemix_curl}

{{site.data.keyword.Bluemix_notm}} への未加工 HTTP 要求を実行します。*Content-Type* はデフォルトで *application/json* に設定されます。このコマンドは、要求を {{site.data.keyword.Bluemix_notm}} マルチクラウド制御プロキシーに送信します。サポートされるパスについては、[CloudFoundry API 資料 ](http://apidocs.cloudfoundry.org/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) 内の API パス定義を参照してください。

```
bluemix curl PATH [OPTIONS...]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt><i>PATH</i> (必須)</dt>
   <dd>リソースの URL パス。例えば、/v2/apps です。</dd>
   <dt><i>OPTIONS</i> (オプション)</dt>
   <dd>`bluemix curl` コマンドでサポートされるオプションは、`cf curl` コマンドのオプションと同じです。</dd>
   </dl>

<strong>例</strong>:

現行アカウントのすべての組織に関する情報を表示するには、次のように指定します。

```
bluemix curl /v2/organizations
```

## bluemix update
{: #bluemix_update}

CLI を最新バージョンに更新します

```
bluemix update
```

<strong>前提条件</strong>: なし

## bluemix regions
{: #bluemix_regions}

{{site.data.keyword.Bluemix_notm}} のすべての地域の情報を表示します。

```
bluemix regions
```

<strong>前提条件</strong>: エンドポイント


## bluemix iam orgs
{: #bluemix_iam_orgs}

すべての組織をリストします。

```
bluemix iam orgs [-r REGION] [--guid]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>-r <i>REGION</i> (オプション)</dt>
   <dd>どの地域の組織情報を表示するかを指定します。'all' に設定された場合は、すべての地域のすべての組織がリストされます。</dd>
   <dt>--guid (オプション)</dt>
   <dd>組織の GUID を表示します。</dd>
   </dl>

<strong>例</strong>:

地域 `us-south` 内のすべての組織を、GUID の
出力と共にリストします。

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

指定された組織の情報を表示します。

```
bluemix iam org ORG_NAME [--guid]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>ORG_NAME (必須)</dt>
   <dd>組織の名前。</dd>
   <dt>--guid (オプション)</dt>
   <dd>組織の GUID を表示します。</dd>
   </dl>

<strong>例</strong>:

組織 `IBM`
の情報を、GUID の出力と共に表示します

```
bluemix iam org IBM --guid
```


## bluemix iam org-create
{: #bluemix_iam_org_create}

新しい組織を作成します。この操作は、アカウントの所有者のみが実行できます。  

```
bluemix iam org-create ORG_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>ORG_NAME (必須)</dt>
   <dd>作成される組織の名前。</dd>
   </dl>

<strong>例</strong>:

名前が `IBM` という組織を作成します。

```
bluemix iam org-create IBM
```

## bluemix iam org-replicate
{: #bluemix_iam_org_replicate}

現在の地域から別の地域に組織を複製します。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>ORG_NAME (必須)</dt>
   <dd>複製する既存の組織の名前。</dd>
   <dt>REGION_NAME (必須)</dt>
   <dd>複製された組織をホストする地域の名前。</dd>
   </dl>

<strong>例</strong>:

組織 `myorg` を地域 `eu-gb` に複製します。

```
bluemix iam org-replicate myorg eu-gb
```


## bluemix iam org-rename
{: #bluemix_iam_org_rename}

組織の名前を変更します。この操作は、組織の管理者のみが実行できます。

```
bluemix iam org-rename OLD_ORG_NAME NEW_ORG_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>OLD_ORG_NAME (必須)</dt>
   <dd>名前を変更する組織の古い名前。</dd>
   <dt>NEW_ORG_NAME (必須)</dt>
   <dd>名前を変更する組織の新しい名前。</dd>
   </dl>

## bluemix iam org-delete
{: #bluemix_iam_org_delete}

現行地域内の指定された組織を削除します。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>ORG_NAME (必須)</dt>
   <dd>削除する既存の組織の名前。</dd>
   <dt>-f (オプション)</dt>
   <dd>確認なしで削除を強制します。</dd>
   <dt>--all (オプション)</dt>
   <dd>その組織をすべての地域から削除します。</dd>
   </dl>


## bluemix iam spaces
{: #bluemix_iam_spaces}

このコマンドの機能とオプションは `cf spaces` コマンドと同じです。


## bluemix iam space
{: #bluemix_iam_space}

このコマンドの機能とオプションは `cf space` コマンドと同じです。


## bluemix iam space-create
{: #bluemix_iam_space_create}

このコマンドの機能とオプションは `cf create-space` コマンドと同じです。


## bluemix iam space-rename
{: #bluemix_iam_space_rename}


このコマンドの機能とオプションは `cf rename-space` コマンドと同じです。


## bluemix iam space-delete
{: #bluemix_iam_space_delete}


このコマンドの機能とオプションは `cf delete-space` コマンドと同じです。

## bluemix iam org-users
{: #bluemix_iam_org_users}

指定された組織内のユーザーを役割別に表示します

```
bluemix iam org-users ORG_NAME [-a]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>ORG_NAME (必須)</dt>
<dd>組織の名前。</dd>
<dt>-a (オプション)</dt>
<dd>指定された組織内のすべてのユーザーを、役割別にグループ化せずにリストします。</dd>
</dl>

## bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

組織にユーザーを追加します (組織管理者が必要)。

```
 bluemix iam org-user-add USER_NAME ORG
```

## bluemix iam org-user-remove
{: #bluemix_iam_org_user_remove}

組織からユーザーを削除します (組織管理者またはユーザー本人のみ)

```
   bluemix iam org-user-remove USER_NAME ORG [-f, --force]
```

<strong>コマンド・オプション</strong>:
<dl>
<dt>--force, -f</dt>
<dd>確認なしで削除を強制します。</dd>
</dl>

## bluemix iam org-roles
{: #bluemix_iam_org_roles}

現行のユーザーのすべての組織の役割を取得します

```
bluemix iam org-roles
```

<strong>前提条件</strong>: エンドポイント、ログイン

## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

組織の役割をユーザーに割り当てます。この操作は、組織の管理者のみが実行できます。  

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
  <dl>
   <dt>USER_NAME (必須)</dt>
   <dd>割り当てられるユーザーの名前。</dd>
   <dt>ORG_NAME (必須)</dt>
   <dd>このユーザーの割り当て先の組織の名前。</dd>
   <dt>ORG_ROLE (必須)</dt>
   <dd>このユーザーの割り当て先の組織内での役割の名前。以下に例を示します。
<ul>
   <li>OrgManager: この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</li>
   <li>BillingManager: この役割は、請求アカウントと支払い情報の作成および管理を行えます。</li>
   <li>OrgAuditor: この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</li>
   </ul>
   </dd>
  </dl>

<strong>例</strong>:

ユーザー `Mary` を組織 `IBM` に役割 `OrgManager` として割り当てるには、次のように指定します。

```
bluemix iam org-role-set Mary IBM OrgManager
```


## bluemix iam org-role-unset
{: #bluemix_iam_org_role_unset}

組織の役割をユーザーから削除します。この操作は、組織の管理者のみが実行できます。  

```
bluemix iam org-role-unset USER_NAME ORG_NAME ORG_ROLE
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>USER_NAME (必須)</dt>
   <dd>削除されるユーザーの名前。</dd>
   <dt>ORG_NAME (必須)</dt>
   <dd>このユーザーの削除元の組織の名前。</dd>
   <dt>ORG_ROLE (必須)</dt>
   <dd>このユーザーの削除元の組織内での役割の名前。以下に例を示します。
<ul>
   <li>OrgManager: この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</li>
   <li>BillingManager: この役割は、請求アカウントと支払い情報の作成および管理を行えます。</li>
   <li>OrgAuditor: この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</li>
   </ul>
   </dd>
    </dl>

<strong>例</strong>:

ユーザー `Mary` を組織 `IBM` の役割 `OrgManager` から削除するには、次のように指定します。

```
bluemix iam org-role-unset Mary IBM OrgManager
```

## bluemix iam space-users
{: #bluemix_iam_space_users}

指定されたスペース内のユーザーを役割別に表示します

```
bluemix iam space-users ORG_NAME SPACE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>ORG_NAME (必須)</dt>
   <dd>組織の名前。</dd>
   <dt>SPACE_NAME (必須)</dt>
   <dd>スペースの名前。</dd>
   </dl>


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

スペースの役割をユーザーに割り当てます。この操作は、スペースの管理者のみが実行できます。  

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>USER_NAME (必須)</dt>
   <dd>割り当てられるユーザーの名前。</dd>
   <dt>ORG_NAME (必須)</dt>
   <dd>このユーザーの割り当て先の組織の名前。</dd>
   <dt>SPACE_NAME (必須)</dt>
   <dd>このユーザーの割り当て先のスペースの名前。</dd>
   <dt>SPACE_ROLE (必須)</dt>
   <dd>このユーザーの割り当て先のスペース内での役割の名前。以下に例を示します。
<ul>
   <li>SpaceManager: この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</li>
   <li>SpaceDeveloper: この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</li>
   <li>SpaceAuditor: この役割は、ログ、レポート、スペースの設定を表示できます。 </li>
   </ul></dd>
    </dl>

<strong>例</strong>:

ユーザー `Mary` を組織 `IBM` およびスペース `Cloud` に役割 `SpaceManager` として割り当てるには、次のように指定します。

```
bluemix iam space-role-set Mary IBM Cloud SpaceManager
```

## bluemix iam space-role-unset
{: #bluemix_iam_space_role_unset}

スペースの役割をユーザーから削除します。この操作は、スペースの管理者のみが実行できます。  

```
bluemix iam space-role-unset USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>USER_NAME (必須)</dt>
   <dd>削除されるユーザーの名前。</dd>
   <dt>ORG_NAME (必須)</dt>
   <dd>このユーザーの削除元の組織の名前。</dd>
   <dt>SPACE_NAME (必須)</dt>
   <dd>このユーザーの削除元のスペースの名前。</dd>
   <dt>SPACE_ROLE (必須)</dt>
   <dd>このユーザーの削除元のスペース内での役割の名前。以下に例を示します。
<ul>
   <li>SpaceManager: この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</li>
   <li>SpaceDeveloper: この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</li>
   <li>SpaceAuditor: この役割は、ログ、レポート、スペースの設定を表示できます。 </li>
   </ul></dd>
    </dl>


<strong>例</strong>:

ユーザー `Mary` を組織 `IBM` と、役割 `SpaceManager` としてのスペース `Cloud` から削除するには、次のように指定します。

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```

## bluemix iam accounts
{: #bluemix_iam_accounts}

現行のユーザーのすべてのアカウントをリストします

```
bluemix iam accounts
```

<strong>前提条件</strong>: エンドポイント、ログイン


## bluemix iam org-account
{: #bluemix_iam_org_account}

指定された組織のアカウントを表示します (組織のユーザーが必要)

```
bluemix iam org-account ORG_NAME [--guid]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
  <dt>--guid (オプション)</dt>
  <dd>アカウント ID のみを表示します</dd>
</dl>


## bluemix iam account-users

{: #bluemix_iam_account_users}

アカウントに関連付けられているユーザーを表示します。この操作は、アカウントの所有者のみが実行できます。

```
bluemix iam account-users
```

## bluemix iam account-user-delete
{: #bluemix_iam_account_user_delete}

現行アカウントからユーザーを削除します (アカウント所有者のみ)

```
bluemix iam account-user-delete USERNAME [-f]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>USERNAME (必須)</dt>
<dd>ユーザー名</dd>
<dt>--force、-f (オプション)</dt>
<dd>確認なしで削除を強制します。</dd>
</dl>

## bluemix iam account-user-invite
{: #bluemix_iam_account_user_invite}

組織とスペースの役割が既に設定されているアカウントにユーザーを招待します。この操作は、アカウントの所有者のみが実行できます。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
   <dt>USER_NAME (必須)</dt>
   <dd>招待されるユーザーの名前。</dd>
   <dt>ORG_NAME (必須)</dt>
   <dd>このユーザーの招待先の組織の名前。</dd>
   <dt>ORG_ROLE (必須)</dt>
   <dd>このユーザーの招待先の組織内での役割の名前。以下に例を示します。
<ul>
  <li>OrgManager: この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</li>
  <li>BillingManager: この役割は、請求アカウントと支払い情報の作成および管理を行えます。</li>
  <li>OrgAuditor: この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</li>
  </ul> </dd>
   <dt>SPACE_NAME (必須)</dt>
   <dd>このユーザーの招待先のスペースの名前。</dd>
   <dt>SPACE_ROLE (必須)</dt>
   <dd>このユーザーの招待先のスペースの名前。このユーザーの招待先のスペース内での役割の名前。以下に例を示します。
<ul>
<li>SpaceManager: この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</li>
<li>SpaceDeveloper: この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</li>
<li>SpaceAuditor: この役割は、ログ、レポート、スペースの設定を表示できます。 </li>
</ul>
</dd>
</dl>

<strong>例</strong>:

ユーザー `Mary` を組織 `IBM` に役割 `OrgManager` として招待し、スペース `Cloud` に役割 `SpaceAuditor` として招待するには、次のように指定します。

```
bluemix iam account-user-invite Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

ユーザーに招待を再送信します (組織管理者かアカウント所有者が必要)

```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```

## bluemix iam api-keys
{: #bluemix_iam api_keys}

すべての Bluemix プラットフォーム API キーをリストします

```
bluemix iam api-keys```

<strong>前提条件</strong>: エンドポイント、ログイン

## bluemix iam api-key-create
{: #bluemix_iam_api_key_create}

新しい Bluemix プラットフォーム API キーを作成します

```
bluemix iam api-key-create NAME [-d DESCRIPTION] [-f, --file FILE]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>NAME (必須)</dt>
<dd>作成する API キーの名前。</dd>
<dt>-d <i>DESCRIPTION</i> (オプション)</dt>
<dd>API キーの説明。</dd>
<dt>-f, -- file <i>FILE</i></dt>
<dd>指定されたファイルに API キー情報を保存します。設定されていない場合、JSON コンテンツが表示されます。</dd>
</dl>

<strong>例</strong>:

API キーを作成してファイルに保存します

```
bluemix iam api-key-create MyKey -d "this is my API key" -f key_file
```

## bluemix iam api-key-update
{: #bluemix_iam_api_key_update}

Bluemix プラットフォーム API キーを更新します

```
bluemix iam api-key-update NAME [-n NAME] [-d DESCRIPTION]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>NAME (必須)</dt>
<dd>更新する API キーの古い名前。</dd>
<dt>-n <i>NAME</i> (オプション)</dt>
<dd>API キーの新しい名前。</dd>
<dt>-d <i>DESCRIPTION</i> (オプション)</dt>
<dd>API キーの新しい説明。</dd>
</dl>

<strong>例</strong>:

API キーの説明を更新します。

```
bluemix iam api-key-update MyKey -d "the new description of my key"
```

## bluemix api-key-delete
{: #bluemix_api_key_delete}

Bluemix プラットフォーム API キーを削除します

```
bluemix iam api-key-delete NAME [-f]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>NAME (必須)</dt>
<dd>削除する API キーの名前。</dd>
<dt>-f (オプション)</dt>
<dd>確認なしで削除を強制します。</dd>
</dl>


## bluemix app push
{: #bluemix_app_push}

このコマンドの機能とオプションは `cf push` コマンドと同じです。


## bluemix app list
{: #bluemix_app_list}

このコマンドの機能とオプションは `cf apps` コマンドと同じです。


## bluemix app show
{: #bluemix_app_show}

このコマンドの機能とオプションは `cf app` コマンドと同じです。


## bluemix app delete
{: #bluemix_app_delete}

このコマンドの機能とオプションは `cf delete` コマンドと同じです。


## bluemix app rename
{: #bluemix_app_rename}

このコマンドの機能とオプションは `cf rename` コマンドと同じです。


## bluemix app start
{: #bluemix_app_start}

このコマンドの機能とオプションは `cf start` コマンドと同じです。


## bluemix app stop
{: #bluemix_app_stop}

このコマンドの機能とオプションは `cf stop` コマンドと同じです。


## bluemix app restart
{: #bluemix_app_restart}

このコマンドの機能とオプションは `cf restart` コマンドと同じです。


## bluemix app restage
{: #bluemix_app_restage}


このコマンドの機能とオプションは `cf restage` コマンドと同じです。


## bluemix app instance-restart
{: #bluemix_app_instance_restart}


このコマンドの機能とオプションは `cf restart-app-instance` コマンドと同じです。


## bluemix app events
{: #bluemix_app_events}

このコマンドの機能とオプションは `cf events` コマンドと同じです。


## bluemix app files
{: #bluemix_app_files}

このコマンドの機能とオプションは `cf files` コマンドと同じです。


## bluemix app logs
{: #bluemix_app_logs}

このコマンドの機能とオプションは `cf logs` コマンドと同じです。


## bluemix app env
{: #bluemix_app_env}

このコマンドの機能とオプションは `cf env` コマンドと同じです。


## bluemix app env-set
{: #bluemix_app_env_set}

このコマンドの機能とオプションは `cf set-env` コマンドと同じです。


## bluemix app env-unset
{: #bluemix_app_env_unset}

このコマンドの機能とオプションは `cf unset-env` コマンドと同じです。


## bluemix app stacks
{: #bluemix_app_stacks}

このコマンドの機能とオプションは `cf stacks` コマンドと同じです。


## bluemix app stack-show
{: #bluemix_app_stack_show}

このコマンドの機能とオプションは `cf stack` コマンドと同じです。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

このコマンドの機能とオプションは `cf create-app-manifest` コマンドと同じです。

## bluemix app domain-cert 
{: #bluemix_app_domain_cert}

ドメインの証明書情報をリストします。

```
bluemix app domain-cert DOMAIN_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
<dl>
<dt>DOMAIN_NAME (必須)</dt>
<dd>証明書をホストするドメイン。</dd>
</dl>


<strong>例</strong>:

ドメイン `ibmcxo-eventconnect.com` の証明書情報を表示するには、次のように指定します。

```
bluemix app domain-cert ibmcxo-eventconnect.com
```

## bluemix app domain-cert-add
{: #bluemix_app_domain_cert_add}

現在の組織内の、指定したドメインに証明書を追加します。

```
bluemix app domain-cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [-t TRUST_STORE_FILE]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>DOMAIN (必須)</dt>
   <dd>証明書を追加するドメイン。</dd>
   <dt>-k <i>PRIVATE_KEY_FILE</i> (必須)</dt>
   <dd>秘密鍵ファイル・パス。</dd>
   <dt>-c <i>CERT_FILE</i> (必須)</dt>
   <dd>証明書ファイル・パス。</dd>
   <dt>-p <i>PASSWORD</i> (オプション)</dt>
   <dd>証明書のパスワード。</dd>
   <dt>-i <i>INTERMEDIATE_CERT_FILE</i> (オプション)</dt>
   <dd>中間証明書ファイル・パス。</dd>
   <dt>-t <i>TRUST_STORE_FILE</i> (オプション)</dt>
   <dd>トラストストア・ファイル。</dd>
   </dl>


<strong>例</strong>:

ドメイン `ibmcxo-eventconnect.com` に証明書を追加するには、以下のように指定します。

```
bluemix app domain-cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```

## bluemix app domain-cert-remove
{: #bluemix_app_domain_cert_remove}

現在の組織内の、指定したドメインから証明書を削除します。

```
bluemix app domain-cert-remove DOMAIN [-f]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>DOMAIN (必須)</dt>
   <dd>証明書を削除するドメイン。</dd>
   <dt>-f (オプション)</dt>
   <dd>確認なしで削除を強制します。</dd>
   </dl>

## bluemix app domains
{: #bluemix_app_domains}

このコマンドの機能とオプションは `cf domains` コマンドと同じです。


## bluemix app domain-create
{: #bluemix_app_domain_create}

このコマンドの機能とオプションは `cf create-domain` コマンドと同じです。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

このコマンドの機能とオプションは `cf delete-domain` コマンドと同じです。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

このコマンドの機能とオプションは `cf create-shared-domain` コマンドと同じです。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

このコマンドの機能とオプションは `cf delete-shared-domain` コマンドと同じです。

## bluemix app routes
{: #bluemix_app_routes}

このコマンドの機能とオプションは `cf routes` コマンドと同じです。


## bluemix app route-check
{: #bluemix_app_route_check}

このコマンドの機能とオプションは `cf check-route` コマンドと同じです。


## bluemix app route-map
{: #bluemix_app_route_map}

指定されたドメインおよびホスト名を持つ経路を既存 cf アプリケーションまたはコンテナー・グループにマップします。

```
bluemix app route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (必須)</dt>
   <dd>経路によってマップされる cf アプリケーションまたはコンテナー・
グループの名前。</dd>
   <dt>DOMAIN (必須)</dt>
   <dd>経路のドメイン。例えば、mychinabluemix.net または chinabluemix.net などです。</dd>
   <dt>-n <i>HOST_NAME</i> (オプション)</dt>
   <dd>経路のホスト名。指定されない場合、ホスト名は、デフォルトで、アプリケーション名またはコンテナー・グループ名に設定されます。</dd>
   </dl>

<strong>例</strong>:

指定されたドメインで `my-app` に経路をマップします。

```
bluemix app route-map my-app mychinabluemix.net
```

指定されたドメインとホスト名で「my-container-group」に経路をマップします。

```
bluemix app route-map my-container-group chinabluemix.net -n abc
```


## bluemix app route-unmap
{: #bluemix_app_route_unmap}

指定された経路を既存 cf アプリケーションまたはコンテナー・グループからマップ解除します。

```
bluemix app route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>CF_APP_NAME|CONTAINER_GROUP_NAME (必須)</dt>
   <dd>cf アプリケーションまたはコンテナー・グループの名前。</dd>
   <dt>DOMAIN (必須)</dt>
   <dd>経路のドメイン (例えば、mychinabluemix.net または chinabluemix.net)。</dd>
   <dt>-n <i>HOST_NAME</i> (オプション)</dt>
   <dd>経路のホスト名。指定されない場合、ホスト名は、デフォルトで、アプリケーション名またはコンテナー・グループ名に設定されます。</dd>
   </dl>

<strong>例</strong>:

`my-app.mychinabluemix.net` を `my-app` からマップ解除するには、以下のように指定します。

```
bluemix app route-unmap my-app mychianbluemix.net
```

`abc.chinabluexmix.net` を `my-container-group` からマップ解除するには、以下のように指定します。

```
bluemix app route-unmap my-container-group chinabluemix.net -n abc
```


## bluemix app route-create
{: #bluemix_app_route_create}

このコマンドの機能とオプションは `cf create-route` コマンドと同じです。


## bluemix app route-delete
{: #bluemix_app_route_delete}

このコマンドの機能とオプションは `cf delete-route` コマンドと同じです。


## bluemix app orphaned-routes-delete
{: #bluemix_app_orphaned_routes_delete}

このコマンドの機能とオプションは `cf delete-orphaned-routes` コマンドと同じです。


## bluemix app domains
{: #bluemix_app_domains}

このコマンドの機能とオプションは `cf domains` コマンドと同じです。


## bluemix app domain-create
{: #bluemix_app_domain_create}

このコマンドの機能とオプションは `cf create-domain` コマンドと同じです。


## bluemix app domain-delete
{: #bluemix_app_domain_delete}

このコマンドの機能とオプションは `cf delete-domain` コマンドと同じです。


## bluemix app shared-domain-create
{: #bluemix_app_shared_domain_create}

このコマンドの機能とオプションは `cf create-shared-domain` コマンドと同じです。


## bluemix app shared-domain-delete
{: #bluemix_app_shared_domain_delete}

このコマンドの機能とオプションは `cf delete-shared-domain` コマンドと同じです。


## bluemix service offerings
{: #bluemix_service_offerings}


このコマンドの機能とオプションは `cf marketplace` コマンドと同じです。


## bluemix service list
{: #bluemix_service_list}

このコマンドの機能とオプションは `cf services` コマンドと同じです。


## bluemix service show
{: #bluemix_service_show}

このコマンドの機能とオプションは `cf service` コマンドと同じです。


## bluemix service create
{: #bluemix_service_create}

このコマンドの機能とオプションは `cf create-service` コマンドと同じです。


## bluemix service update
{: #bluemix_service_update}

このコマンドの機能とオプションは `cf update-service` コマンドと同じです。


## bluemix service delete
{: #bluemix_service_delete}

このコマンドの機能とオプションは `cf delete-service` コマンドと同じです。


## bluemix service rename
{: #bluemix_service_rename}

このコマンドの機能とオプションは `cf rename-service` コマンドと同じです。


## bluemix service bind
{: #bluemix_service_bind}

このコマンドの機能とオプションは `cf bind-service` コマンドと同じです。


## bluemix service unbind
{: #bluemix_service_unbind}

このコマンドの機能とオプションは `cf unbind-service` コマンドと同じです。


## bluemix service key-create
{: #bluemix_service_key_create}

このコマンドの機能とオプションは `cf create-service-key` コマンドと同じです。


## bluemix service key-delete
{: #bluemix_service_key_delete}

このコマンドの機能とオプションは `cf delete-service-key` コマンドと同じです。


## bluemix service keys
{: #bluemix_service_keys}

このコマンドの機能とオプションは `cf service-keys` コマンドと同じです。


## bluemix service key-show
{: #bluemix_service_key_show}

このコマンドの機能とオプションは `cf service-key` コマンドと同じです。


## bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

このコマンドの機能とオプションは `cf create-user-provided-service` コマンドと同じです。


## bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

このコマンドの機能とオプションは `cf update-user-provided-service` コマンドと同じです。


## bluemix catalog templates
{: #bluemix_catalog_templates}

Bluemix のボイラープレート・テンプレートを表示します。

```
bluemix catalog templates [-d]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-d (オプション)</dt>
   <dd><i>-d</i> オプションが指定されている場合、各テンプレートの説明
も表示されます。それ以外の場合、各テンプレートの ID および名前のみが表示されます。</dd>
   </dl>


## bluemix catalog template
{: #bluemix_catalog_template}

指定されたボイラープレート・テンプレートの詳細情報を表示します。

```
bluemix catalog template TEMPLATE_ID
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>TEMPLATE_ID (必須)</dt>
   <dd>ボイラープレート・テンプレートの ID。すべてのテンプレートの ID を表示するには、
<i>bluemix templates</i> を使用します。</dd>
   </dl>


<strong>例</strong>:

テンプレート `mobileBackendStarter` の詳細を表示します。

```
bluemix catalog template mobileBackendStarter
```


## bluemix catalog template-run
{: #bluemix_catalog_template_run}

指定されたテンプレートをベースにした、指定された URL と説明を持つ cf アプリケーションを作成します。デフォルトでは、この新規アプリケーションは自動的に開始されます。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>TEMPLATE_ID (必須)</dt>
   <dd>アプリケーションの作成時にそのアプリケーションの基盤とするテンプレート。すべてのテンプレートの ID を表示するには、<i>bluemix templates</i> を使用します。</dd>
   <dt>CF_APP_NAME (必須)</dt>
   <dd>作成される cf アプリケーションの名前。</dd>
   <dt>-u <i>URL</i> (オプション)</dt>
   <dd>アプリケーションの経路。指定しない場合、経路はアプリ名とデフォルト・ドメインに基づき、Bluemix が自動的に設定します。</dd>
   <dt>-d <i>DESCRIPTION</i> (オプション)</dt>
   <dd>アプリケーションの説明。</dd>
   <dt>--no-start (オプション)</dt>
   <dd>作成後のアプリケーションを自動的に開始しません。
指定されない場合、アプリケーションは作成された後で自動的に開始されます。</dd>
   </dl>


<strong>例</strong>:

`javaHelloWorld` テンプレートをベースにして cf アプリケーション `my-app` を作成します。

```
bluemix catalog template-run javaHelloWorld my-app
```

`rubyHelloWorld` テンプレートに基づき、経路 `myrubyapp.chinabluemix.net` と説明 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.` を使用してアプリケーション `my-ruby-app` を作成するには、以下のように指定します。

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.chinabluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

`pythonHelloWorld` テンプレートをベースにして、自動開始なしでアプリケーション `my-python-app` を作成します。

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```

## bluemix billing account-usage
{: #bluemix_billing_account_usage}

アカウントの月次使用量とコストを表示します。

```
bluemix billing account-usage [-d YYYY-MM] [--json]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

<dl>
  <dt>-d MONTH_DATE (オプション)</dt>
  <dd>YYYY-MM 形式を使用して指定する日付のデータを表示します。指定されていない場合、今月の使用量が表示されます。</dd>
  <dt>--json (オプション)</dt>
  <dd>使用量の結果を JSON 形式で表示します。</dd>
</dl>

<strong>例</strong>:

2016 年 6 月のマイ・アカウントの使用量とコストのレポートを表示します。

```
bluemix billing account-usage -d 2016-06
```

## bluemix billing org-usage
{: #bluemix_billing_org_usage}

組織の月次使用量の詳細を表示します。この操作は、組織の請求管理者のみ実行できます。

```
bluemix billing org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

<dl>
  <dt>ORG_NAME (必須)</dt>
  <dd>組織の名前。</dd>
  <dt>-d MONTH_DATE (オプション)</dt>
  <dd>YYYY-MM 形式を使用して指定された日付のデータを表示します。指定されていない場合、今月の使用量が表示されます。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>組織をホストする地域の名前。「all」に設定されている場合、すべての地域の組織の使用量が表示されます。</dd>
  <dt>--json (オプション)</dt>
  <dd>使用量の結果を JSON 形式で表示します。</dd>
</dl>



## bluemix billing orgs-usage-summary
{: #bluemix_billing_orgs_usage_summary}

マイ・アカウント内の組織の月次使用量サマリーを表示します。

```
bluemix billing orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:

<dl>
  <dt>-d MONTH_DATE (オプション)</dt>
  <dd>YYYY-MM 形式を使用して指定された日付のデータを表示します。指定されていない場合、今月の使用量が表示されます。</dd>
  <dt>-r REGION_NAME</dt>
  <dd>組織をホストする地域の名前。「all」に設定されている場合、すべての地域の組織の使用量サマリーが表示されます。</dd>
  <dt>--json (オプション)</dt>
  <dd>使用量の結果を JSON 形式で表示します。</dd>
</dl>


## bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI に登録されているすべてのプラグイン・リポジトリーをリストします。

```
bluemix plugin repos
```

<strong>前提条件</strong>: なし


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

新規プラグイン・リポジトリーを {{site.data.keyword.Bluemix_notm}} CLI に追加します。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>REPO_NAME (必須)</dt>
   <dd>追加するリポジトリーの名前。各リポジトリーに対して任意の名前を定義できます。</dd>
   <dt>REPO_URL (必須)</dt>
   <dd>追加するリポジトリーの URL。リポジトリー URL にはプロトコルが含まれている必要があります (例えば、plugins.ng.bluemix.net ではなく、http://plugins.ng.bluemix.net)。http://plugins.ng.bluemix.net は、Bluemix CLI の公式プラグイン・リポジトリーです。</dd>
    </dl>


<strong>例</strong>:

Bluemix CLI の公式プラグイン・リポジトリーを `bluemix-repo` として追加します。

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{: #bluemix_plugin_repo_remove}

{{site.data.keyword.Bluemix_notm}} CLI からプラグイン・リポジトリーを削除します。

```
bluemix plugin repo-remove REPO_NAME
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>REPO_NAME (必須)</dt>
   <dd>削除するリポジトリーの名前。</dd>
   </dl>

<strong>例</strong>:

{{site.data.keyword.Bluemix_notm}} CLI から `bluemix-repo` リポジトリーを削除します。

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugins
{: #bluemix_plugin_repo_plugins}

追加されたすべてのリポジトリーまたは特定のリポジトリー内にある使用可能なプラグインをすべてリストします。

```
bluemix plugin repo-plugins [-r REPO_NAME]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-r <i>REPO_NAME</i> (オプション)</dt>
   <dd>指定されたリポジトリー内のプラグインのみをリストします。</dd>
   </dl>

<strong>例</strong>:

追加されたすべてのリポジトリー内のすべてのプラグインをリストします。

```
bluemix plugin repo-plugins
```

`bluemix-repo` リポジトリー内のすべてのプラグインをリストします。

```
bluemix plugin repo-plugins -r bluemix-repo
```


## bluemix plugin list
{: #bluemix_plugin_list}

{{site.data.keyword.Bluemix_notm}} CLI 内のインストールされたプラグインをすべてリストします。

```
bluemix plugin list
```

<strong>前提条件</strong>: なし


## bluemix plugin install
{: #bluemix_plugin_install}

指定したパスまたはリポジトリーから、特定のバージョンのプラグインを {{site.data.keyword.Bluemix_notm}} CLI にインストールします。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME] [-v VERSION]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>PLUGIN_PATH|PLUGIN_NAME (必須)</dt>
   <dd>「-r <i>REPO_NAME</i>」が指定されない場合、指定されたローカル
・パスまたはリモート URL からプラグインがインストールされます。</dd>
   <dt>-r <i>REPO_NAME</i> (オプション)</dt>
   <dd>プラグインのバイナリーが配置されているリポジトリーの名前。</dd>
   <dt>-v <i>VERSION</i> (オプション)</dt>
   <dd>インストールするプラグインのバージョン。指定されていない場合は、最新バージョンのプラグインがインストールされます。このオプションは、リポジトリーからプラグインをインストールする場合にのみ有効です。</dd>
    </dl>

<strong>例</strong>:

ローカル・ファイルからプラグインをインストールします。

```
bluemix plugin install /downloads/new_plugin
```

リモート URL からプラグインをインストールします。

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

最新バージョンの `IBM-Containers` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
バージョン `0.5.800` の `IBM-Containers` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
```

## bluemix plugin update
{: #bluemix_plugin_update}

リポジトリーからプラグインをアップグレードします

```
bluemix plugin update -r REPO_NAME [PLUGIN NAME [-v VERSION]]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
<dl>
 <dt>-r REPO_NAME (必須)</dt>
 <dd>プラグインのバイナリーが配置されているリポジトリーの名前。</dd>
 <dt><i>PLUGIN_NAME</i> (オプション)</dt>
 <dd>指定されていない場合、特定のリポジトリーで更新可能なすべてのプラグインが、選択できるようにリストされます。</dd>
 <dt>-v <i>VERSION</i> (オプション)</dt>
 <dd>更新するプラグインのバージョン。表示されない場合、プラグインを入手可能な最新バージョンに更新してください。</dd>
</dl>

<strong>例</strong>:

プラグイン・リポジトリー「My-Repo」で使用可能なすべてのアップグレードを確認します。

```
bluemix plugin update -r My-Repo
```

リポジトリー「My-Repo」内のプラグイン「plugin-echo」を最新にアップグレードします。

```
bluemix plugin update -r My-Repo plugin-echo
```

リポジトリー「My-Repo」内のプラグイン「plugin-echo」をバージョン「1.0.1」に更新します。

```
bluemix plugin update -r My-Repo plugin-echo -v 1.0.1
```

## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

指定されたプラグインを {{site.data.keyword.Bluemix_notm}} CLI からアンインストールします。

```
bluemix plugin uninstall PLUGIN_NAME
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>PLUGIN_NAME (必須)</dt>
   <dd>アンインストールされるプラグインの名前。</dd>
    </dl>

<strong>例</strong>:

前にインストールされた `IBM-Containers` プラグインをアンインストールします。

```
bluemix plugin uninstall IBM-Containers
```
