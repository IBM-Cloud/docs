---



copyright:

  years: 2015, 2017
lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 入門
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI は、アプリケーション、仮想サーバー、コンテナー、およびその他のサービスとの対話をコマンド・ライン・インターフェースを使用して行うための一元化された手法を提供します。また、{{site.data.keyword.Bluemix_notm}} CLI は、各種コミュニティー・ツール (Cloud Foundry CLI、Docker CLI、OpenStack CLI など) を統合し、さまざまな計算タイプとの対話のための環境設定を初期化します。

**制約事項:** {{site.data.keyword.Bluemix_notm}} CLI は Cygwin ではサポートされないため、Cygwin コマンド・ライン・ウィンドウでは {{site.data.keyword.Bluemix_notm}} CLI を使用しないでください。

**注:** CLI および {{site.data.keyword.Bluemix_notm}} が稼働しているホストとの間に HTTP プロキシー・サーバーがあるネットワークを使用している場合、HTTP_PROXY 環境変数にプロキシー・サーバーのホスト名または IP アドレスを指定する必要があります。

## {{site.data.keyword.Bluemix_notm}} CLI のインストール
{: #install_bluemix_cli}

{{site.data.keyword.Bluemix_notm}} CLI をインストールする前に、[cf CLI ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} をインストールしてください。

Mac OS および Windows の場合は、[{{site.data.keyword.Bluemix_notm}} CLI パッケージ](/docs/cli/index.html#downloads)をダウンロードし、インストーラーを実行してください。

Linux の場合は、以下のステップを実行してください。

  1. パッケージをダウンロードし、解凍します。例えば次のようにします。

  ```
  ~$ tar -xvf Bluemix_CLI.tar.gz
  Bluemix_CLI/
  Bluemix_CLI/update_global_config
  Bluemix_CLI/install_bluemix_cli
  Bluemix_CLI/bx/
  Bluemix_CLI/bx/bash_autocomplete
  Bluemix_CLI/bx/zsh_autocomplete
  Bluemix_CLI/bin/
  Bluemix_CLI/bin/bluemix
  ~$
  ```

  2. `Bluemix_CLI` ディレクトリーに移動し、root 権限で `./install_bluemix_cli` コマンドを実行します。このコマンドを root ユーザーで実行するか、または、`sudo` コマンドを使用して root 権限を取得してください。例えば次のようにします。

  ```
  ~# cd Bluemix_CLI
  ~/Bluemix_CLI# sudo ./install_bluemix_cli
  Superuser privileges are required to run this script.
  The Cloud Foundry CLI version 6.15 is already installed.
  Copying files...
  The Bluemix CLI installed successfully. To get started, open a new Linux terminal and enter "bluemix help", or enter "bx help" as short name.
  ~/Bluemix_CLI#
  ```

これで、{{site.data.keyword.Bluemix_notm}} CLI の使用を開始することも、追加プラグインをインストールすることもできます。

## プラグインのインストール
{: #install_plug-in}

Cloud Foundry CLI と同様に、{{site.data.keyword.Bluemix_notm}} CLI で、組み込みコマンド以外の他のコマンドを統合するためのプラグイン拡張フレームワークがサポートされています。

ローカル環境からプラグインをインストールするには、以下のステップを実行します。

  1. プラグインをダウンロードします。例えば次のようにします。

  ```
  ~$ wget http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2--2016-02-18 14:02:12-- http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64.0.2.2
  Resolving public.dhe.ibm.com... 9.17.248.112
  Connection to public.dhe.ibm.com|9.17.248.112|:80... connected.
  HTTP request sent, awaiting response... 200 OK
  Length: 9857792 (9.4M) [text/plain]
  Saving to: 'auto-scaling-darwin-amd64-0.2.2'

  auto-scaling-darwin-0.2.2 100%[===================>] 9.40M 518KB/s in 22s

  2016-02-18 14:02:34 (443 KB/s) - `auto-scaling-darwin-amd64-0.2.2' saved [9857792/9857792]
  ```

  2. UNIX 系システムの場合、`chmod` コマンドを使用することによって、ダウンロードされたファイルを実行可能にする必要があります。例えば次のようにします。

  ```
  ~$ sudo chmod 755 auto-scaling-darwin-amd64-0.2.2
  Password:
  ~$
  ```

  3. `bluemix plugin install` コマンドを使用してプラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install ./auto-scaling-darwin-amd64-0.2.2
  Installing pluign './auto-scaling-darwin-amd64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

リモート・サーバーからインストールするには、以下のステップを実行します。

  1. `bluemix plugin install` コマンドを使用することによって、リモート URL から直接プラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install http://public.dhe.ibm.com/cloud/bluemix/cli/bluemix-plugins/auto-scaling-darwin-amd64-0.2.2
  Attempting to download the binary file...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload274645142/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

リポジトリーからプラグインをインストールすることもできます。{{site.data.keyword.Bluemix_notm}} には、{{site.data.keyword.Bluemix_notm}} CLI プラグインおよび Cloud Foundry CLI プラグインをホストする以下のリポジトリーがあります。

  * Cloud Foundry CLI 用のプラグインをホストする [Cloud Foundry CLI プラグイン・リポジトリー ](http://clis.ng.bluemix.net/ui/repository.html#cf-plugins){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)
  * {{site.data.keyword.Bluemix_notm}} CLI 固有のプラグインをホストする [{{site.data.keyword.Bluemix_notm}} CLI プラグイン・リポジトリー ](http://clis.ng.bluemix.net/ui/repository.html#bluemix-plugins){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)

リポジトリーからインストールするには、以下のステップを実行します。

  1. リポジトリー内でプラグインを見つけます。{{site.data.keyword.Bluemix_notm}} CLI をインストールした後、デフォルトでオフィシャル・リポジトリー `Bluemix` が追加されます。`bluemix plugin repo-plugins` コマンドを使用して、`Bluemix` リポジトリー内のプラグインをリストできます。例えば次のようにします。

  ```
  ~$ bluemix plugin repo-plugins -r Bluemix
  Getting plug-ins from repository 'Bluemix'...

  Repository: Bluemix
  Name           Description                                    Versions
  auto-scaling   Bluemix CLI plugin for Auto-Scaling service    0.2.1, 0.2.2
  nsg            Bluemix Network Security Group plugin          0.1.1

  ~$
  ```

  2. `bluemix plugin install` コマンドを使用して、`Bluemix` リポジトリーからプラグインをインストールします。例えば次のようにします。

  ```
  ~$ bluemix plugin install auto-scaling -r Bluemix
  Looking up 'auto-scaling' from repository 'Bluemix'...
  9857792 bytes downloaded
  Installing plugin '/var/folder/v7/l3hnkz0x0b9b5mf1fyxh7yw00000gn/T/BluemixFileDownload062468676/auto-scaling-darwin-adm64-0.2.2'...
  OK
  Plugin 'auto-scaling 0.2.2' was successfully installed.
  ~$
  ```

## {{site.data.keyword.Bluemix_notm}} CLI へのログイン
{: #log_bmcli}

{{site.data.keyword.Bluemix_notm}} CLI をインストールした後、IBM ID およびパスワードを使用して {{site.data.keyword.Bluemix_notm}} にログインできます。例えば次のようにします。

```
~$ bluemix login -a https://api.ng.bluemix.net
API endpoint: https://api.ng.bluemix.net

Email> demo_user@foo.com

Password>
Authenticating...
OK
```

これで、{{site.data.keyword.Bluemix_notm}} 組み込みコマンドを使用する準備ができました。例えば、次のように、`bluemix catalog templates` コマンドを実行して、使用可能なすべての {{site.data.keyword.Bluemix_notm}} ボイラープレート・テンプレートをリストできます。

```
~$ bluemix catalog templates
Listing Bluemix boilerplate templates...

ID                      Name
pi-wdc-java-starter     Personality Insights Java Web Starter
xpages-starter          XPages Web Starter
mobileBackendStarter    Mobile Cloud
pi-wdc-nodejs-starter   Personality Insights Node.js Web Starter
mobileFirstPlatform     MobileFirst Services Starter
xspHelloWorld           IBM XPages
javacloudantbp          Java Cloudant Web Starter
```

# {{site.data.keyword.Bluemix_notm}} (bx) コマンド
{: #bluemix_cli}

バージョン: 0.4.6

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
<dd>このコマンドを使用する前に、<code>bluemix login</code> コマンドを使用してログインする必要があります。フェデレーテッド ID でログインする場合は、「--sso」オプションを使用し、ワンタイム・パスコードを使って認証します。</dd>
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
 <td>[bluemix help](index.html#bluemix_help)</td>
 <td>[bluemix api](index.html#bluemix_api)</td>
 <td>[bluemix_login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr>
 <tr>
 <td>[bluemix info](index.html#bluemix_info) </td>
 <td>[bluemix config](index.html#bluemix_config)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
  </tbody>
 </table>


<table summary="組織、スペース、ユーザーの管理に使用できる Bluemix コマンド。">
 <caption>表 2. 組織、スペース、ユーザーを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">組織、スペース、ユーザーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs)</td>
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td>
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete)</td>
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td>
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete)</td>
 <td>[bluemix iam account-users](index.html#bluemix_iam_account_users)</td>
 <td>[bluemix iam account-users-delete](index.html#bluemix_iam_account_users_delete)</td>
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account_user_invite)</td>
 <td>[bluemix iam account-user-reinvite](index.html#bluemix_iam_account_user_reinvite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 </tr>
 <tr>
 <td>[bluemix iam org-user-add](index.html#bluemix_iam_org_user_add)</td>
 <td>[bluemix iam org-user-remove](index.html#bluemix_iam_org_user_remove)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset)</td>
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td>
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 </tr>
 <tr>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 </tr>
 </tbody>
 </table>


<table summary="Cloud Foundry アプリケーションの管理に使用することができる Bluemix コマンド。">
 <caption>表 3. cf アプリケーションを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">cf アプリケーションを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 <td>[bluemix app list](index.html#bluemix_app_list)</td>
 <td>[bluemix app show](index.html#bluemix_app_show)</td>
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 </tr>
 <tr>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 <td>[bluemix app start](index.html#bluemix_app_start)</td>
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td>
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 </tr>
 <tr>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 <td>[bluemix app events](index.html#bluemix_app_events)</td>
 <td>[bluemix app files](index.html#bluemix_app_files)</td>
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 </tr>
 <tr>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset)</td>
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td>
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
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
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 <td>[bluemix service list](index.html#bluemix_service_list)</td>
 <td>[bluemix service show](index.html#bluemix_service_show)</td>
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 </tr>
 <tr>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 <td>[bluemix service rename](index.html#bluemix_service_rename)</td>
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td>
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 </tr>
 <tr>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 <td>[bluemix service keys](index.html#bluemix_service_keys)</td>
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td>
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
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
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 <td>[bluemix catalog template](index.html#bluemix_catalog_template)</td>
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td>
 </tr>
 <tr>
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td>
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td>
 </tr>
 <tr>
 <td>[bluemix bss account-usage](index.html#bluemix_bss_account_usage)</td>
 <td>[bluemix bss org-usage](index.html#bluemix_bss_org_usage)</td>
 <td>[bluemix bss orgs-usage-summary](index.html#bluemix_orgs_usage_summary)</td>
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td>
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 </tr>
 <tr>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td></td>
 <td></td>
 </tr>
  </tbody>
 </table>


<table summary="ネットワーク設定の管理に使用することができる Bluemix コマンド。">
 <caption>表 6. ネットワーク設定を管理するためのコマンド</caption>
 <thead>
 <th colspan="5">ネットワーク設定を管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td>
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td>
 </tr>
 <tr>
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td>
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td>
 </tr>
 <tr>
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td>
 <td></td>
 </tr>
  </tbody>
 </table>



### bluemix help
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



### bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API エンドポイントを設定または表示します。このコマンドは `cf api` コマンドをラップします。

```
bluemix api [API_ENDPOINT] [--unset]
```

<strong>前提条件</strong>: なし

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>API_ENDPOINT (オプション)</dt>
   <dd>ターゲットの API エンドポイント (例えば `https://api.chinabluemix.net`)。 *API_ENDPOINT* オプションと `--unset` オプションのどちらも指定されない場合、現行 API エンドポイントが表示されます。</dd>
   <dt>--unset (オプション)</dt>
   <dd>API エンドポイント設定を削除します。</dd>
    </dl>
<strong>例</strong>:

API エンドポイントを api.chinabluemix.net に設定します。

```
bluemix api api.chinabluemix.net
```

現行 API エンドポイントを表示します。

```
bluemix api
```

API エンドポイントを設定解除します。

```
bluemix api --unset
```


### bluemix login
{: #bluemix_login}

ユーザーをログインします。このコマンドは `cf login` コマンドをラップします。コマンド・オプションは `cf login` コマンドのオプションと同じです。

```
bluemix login [OPTIONS...]
```

<strong>前提条件</strong>: エンドポイント

<!-- staging comment for Atlas 45: might need prereq for federated ID/SSO option unless we expect them to just view the details from the cf login command -->

<strong>コマンド・オプション</strong>:
`login` コマンドでサポートされるオプションについては、アプリケーション管理用 cf コマンドの `cf login` コマンド使用法の説明を参照してください。

<strong>注</strong>:
フェデレーテッド ID でログインする場合は、「--sso」オプションを使用し、ワンタイム・パスコードを使って認証します。

### bluemix logout
{: #bluemix_logout}

ユーザーをログアウトします。このコマンドは `cf logout` コマンドをラップします。

```
bluemix logout
```

<strong>前提条件</strong>: なし


### bluemix target
{: #bluemix_target}


ターゲットの組織またはスペースを設定または表示します。このコマンドは `cf target` コマンドをラップします。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

<strong>前提条件</strong>: エンドポイント、ログイン

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>-o <i>ORG_NAME</i> (オプション)</dt>
   <dd>ターゲットとなる組織の名前。</dd>
   <dt>-s <i>SPACE_NAME</i> (オプション)</dt>
   <dd>ターゲットとなるスペースの名前。</dd>
   </dl>
-o *ORG_NAME* と -s *SPACE_NAME* のどちらも指定されない場合、現行の組織およびスペースが表示されます。
<strong>例</strong>:

現行の組織を `MyOrg` に、スペースを `MySpace` に設定します。

```
bluemix target -o MyOrg -s MySpace
```

現行の組織およびスペースを表示します。

```
bluemix target
```


### bluemix info
{: #bluemix_info}

基本的な {{site.data.keyword.Bluemix_notm}} 情報を表示します。これには、現行領域、クラウド・コントローラーのバージョン、および、いくつかの有用なエンドポイント (例えば、ログイン用のエンドポイントや、アクセス・トークン交換用のエンドポイントなど) が含まれます。

```
bluemix info
```

<strong>前提条件</strong>: エンドポイント


### bluemix config
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


### bluemix curl
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


### bluemix iam orgs
{: #bluemix_iam_orgs}

すべての組織をリストします。

```
bluemix iam orgs [-r REGION --guid]
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

### bluemix iam org
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

### bluemix iam org-create
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


### bluemix iam org-replicate
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


### bluemix iam org-rename
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

### bluemix iam org-delete
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


### bluemix iam spaces
{: #bluemix_iam_spaces}

このコマンドの機能とオプションは `cf spaces` コマンドと同じです。


### bluemix iam space
{: #bluemix_iam_space}

このコマンドの機能とオプションは `cf space` コマンドと同じです。


### bluemix iam space-create
{: #bluemix_iam_space_create}

このコマンドの機能とオプションは `cf create-space` コマンドと同じです。


### bluemix iam space-rename
{: #bluemix_iam_space_rename}


このコマンドの機能とオプションは `cf rename-space` コマンドと同じです。


### bluemix iam space-delete
{: #bluemix_iam_space_delete}


このコマンドの機能とオプションは `cf delete-space` コマンドと同じです。


### bluemix iam account-users

{: #bluemix_iam_account_users}

アカウントに関連付けられているユーザーを表示します。この操作は、アカウントの所有者のみが実行できます。

```
bluemix iam account-users
```

### bluemix iam account-user-invite
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


### bluemix iam account-user-reinvite
{: #bluemix_iam_account_user_reinvite}

ユーザーに招待を再送信します (組織管理者かアカウント所有者が必要)
```
 bluemix iam account-user-reinvite USER_EMAIL ORG_NAME
```


### bluemix iam org-users
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

### bluemix iam org-user-add
{: #bluemix_iam_org_user_add}

組織にユーザーを追加します (組織管理者が必要)。
```
 bluemix iam org-user-add USER_NAME ORG
```

### bluemix iam org-user-remove
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

### bluemix iam org-role-set
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


### bluemix iam org-role-unset
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


### bluemix iam space-users
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


### bluemix iam space-role-set
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

### bluemix iam space-role-unset
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


### bluemix app push
{: #bluemix_app_push}

このコマンドの機能とオプションは `cf push` コマンドと同じです。


### bluemix app list
{: #bluemix_app_list}

このコマンドの機能とオプションは `cf apps` コマンドと同じです。


### bluemix app show
{: #bluemix_app_show}

このコマンドの機能とオプションは `cf app` コマンドと同じです。


### bluemix app scale
{: #bluemix_app_scale}

このコマンドの機能とオプションは `cf scale` コマンドと同じです。


### bluemix app delete
{: #bluemix_app_delete}

このコマンドの機能とオプションは `cf delete` コマンドと同じです。


### bluemix app rename
{: #bluemix_app_rename}

このコマンドの機能とオプションは `cf rename` コマンドと同じです。


### bluemix app start
{: #bluemix_app_start}

このコマンドの機能とオプションは `cf start` コマンドと同じです。


### bluemix app stop
{: #bluemix_app_stop}

このコマンドの機能とオプションは `cf stop` コマンドと同じです。


### bluemix app restart
{: #bluemix_app_restart}

このコマンドの機能とオプションは `cf restart` コマンドと同じです。


### bluemix app restage
{: #bluemix_app_restage}


このコマンドの機能とオプションは `cf restage` コマンドと同じです。


### bluemix app instance-restart
{: #bluemix_app_instance_restart}


このコマンドの機能とオプションは `cf restart-app-instance` コマンドと同じです。


### bluemix app events
{: #bluemix_app_events}

このコマンドの機能とオプションは `cf events` コマンドと同じです。


### bluemix app files
{: #bluemix_app_files}

このコマンドの機能とオプションは `cf files` コマンドと同じです。


### bluemix app logs
{: #bluemix_app_logs}

このコマンドの機能とオプションは `cf logs` コマンドと同じです。


### bluemix app env
{: #bluemix_app_env}

このコマンドの機能とオプションは `cf env` コマンドと同じです。


### bluemix app env-set
{: #bluemix_app_env_set}

このコマンドの機能とオプションは `cf set-env` コマンドと同じです。


### bluemix app env-unset
{: #bluemix_app_env_unset}

このコマンドの機能とオプションは `cf unset-env` コマンドと同じです。


### bluemix app stacks
{: #bluemix_app_stacks}

このコマンドの機能とオプションは `cf stacks` コマンドと同じです。


### bluemix app stack
{: #bluemix_app_stack}

このコマンドの機能とオプションは `cf stack` コマンドと同じです。


### bluemix app manifest-create
{: #bluemix_app_manifest_create}

このコマンドの機能とオプションは `cf create-app-manifest` コマンドと同じです。


### bluemix service offerings
{: #bluemix_service_offerings}


このコマンドの機能とオプションは `cf marketplace` コマンドと同じです。


### bluemix service list
{: #bluemix_service_list}

このコマンドの機能とオプションは `cf services` コマンドと同じです。


### bluemix service show
{: #bluemix_service_show}

このコマンドの機能とオプションは `cf service` コマンドと同じです。


### bluemix service create
{: #bluemix_service_create}

このコマンドの機能とオプションは `cf create-service` コマンドと同じです。


### bluemix service update
{: #bluemix_service_update}

このコマンドの機能とオプションは `cf update-service` コマンドと同じです。


### bluemix service delete
{: #bluemix_service_delete}

このコマンドの機能とオプションは `cf delete-service` コマンドと同じです。


### bluemix service rename
{: #bluemix_service_rename}

このコマンドの機能とオプションは `cf rename-service` コマンドと同じです。


### bluemix service bind
{: #bluemix_service_bind}

このコマンドの機能とオプションは `cf bind-service` コマンドと同じです。


### bluemix service unbind
{: #bluemix_service_unbind}

このコマンドの機能とオプションは `cf unbind-service` コマンドと同じです。


### bluemix service key-create
{: #bluemix_service_key_create}

このコマンドの機能とオプションは `cf create-service-key` コマンドと同じです。


### bluemix service key-delete
{: #bluemix_service_key_delete}

このコマンドの機能とオプションは `cf delete-service-key` コマンドと同じです。


### bluemix service keys
{: #bluemix_service_keys}

このコマンドの機能とオプションは `cf service-keys` コマンドと同じです。


### bluemix service key-show
{: #bluemix_service_key_show}

このコマンドの機能とオプションは `cf service-key` コマンドと同じです。


### bluemix service user-provided-create
{: #bluemix_service_user_provided_create}

このコマンドの機能とオプションは `cf create-user-provided-service` コマンドと同じです。


### bluemix service user-provided-update
{: #bluemix_service_user_provided_update}

このコマンドの機能とオプションは `cf update-user-provided-service` コマンドと同じです。


### bluemix catalog templates
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


### bluemix catalog template
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


### bluemix catalog template-run
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


### bluemix network regions
{: #bluemix_network_regions}

{{site.data.keyword.Bluemix_notm}} のすべての地域の情報を表示します。

```
bluemix network regions
```

<strong>前提条件</strong>: エンドポイント


### bluemix network region-set
{: #bluemix_network_region_set}

指定された地域に切り替えます。このコマンドは、可能な場合、新しい地域の同じ組織およびスペースに自動的にターゲットを変更します。さもなければ、コマンドは、ユーザーが既にログインしている場合、新しい組織とスペースを選択するようユーザーにプロンプトを出します。API エンドポイントはそれに合わせて変更されます。

```
bluemix network region-set REGION_NAME
```

<strong>前提条件</strong>: エンドポイント

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>REGION_NAME (必須)</dt>
   <dd>切り替え先の地域の名前。<i>bluemix network regions</i> コマンドを使用すると、すべての地域名を表示することができます。</dd>
    </dl>

<strong>例</strong>:

現行地域を `eu-gb` に設定します。

```
bluemix network region-set eu-gb
```


### bluemix network routes
{: #bluemix_network_routes}

このコマンドの機能とオプションは `cf routes` コマンドと同じです。


### bluemix network route-check
{: #bluemix_network_route_check}

このコマンドの機能とオプションは `cf check-route` コマンドと同じです。


### bluemix network route-map
{: #bluemix_network_route_map}

指定されたドメインおよびホスト名を持つ経路を既存 cf アプリケーションまたはコンテナー・グループにマップします。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-map my-app mychinabluemix.net
```

指定されたドメインとホスト名で「my-container-group」に経路をマップします。

```
bluemix network route-map my-container-group chinabluemix.net -n abc
```


### bluemix network route-unmap
{: #bluemix_network_route_unmap}

指定された経路を既存 cf アプリケーションまたはコンテナー・グループからマップ解除します。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
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
bluemix network route-unmap my-app mychianbluemix.net
```

`abc.chinabluexmix.net` を `my-container-group` からマップ解除するには、以下のように指定します。

```
bluemix network route-unmap my-container-group chinabluemix.net -n abc
```


### bluemix network route-create
{: #bluemix_network_route_create}

このコマンドの機能とオプションは `cf create-route` コマンドと同じです。


### bluemix network route-delete
{: #bluemix_network_route_delete}

このコマンドの機能とオプションは `cf delete-route` コマンドと同じです。


### bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

このコマンドの機能とオプションは `cf delete-orphaned-routes` コマンドと同じです。


### bluemix network domains
{: #bluemix_network_domains}

このコマンドの機能とオプションは `cf domains` コマンドと同じです。


### bluemix network domain-create
{: #bluemix_network_domain_create}

このコマンドの機能とオプションは `cf create-domain` コマンドと同じです。


### bluemix network domain-delete
{: #bluemix_network_domain_delete}

このコマンドの機能とオプションは `cf delete-domain` コマンドと同じです。


### bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

このコマンドの機能とオプションは `cf create-shared-domain` コマンドと同じです。


### bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

このコマンドの機能とオプションは `cf delete-shared-domain` コマンドと同じです。



### bluemix bss account-usage
{: #bluemix_bss_account_usage}

アカウントの月次使用量とコストを表示します。

```
bluemix bss account-usage [-d YYYY-MM] [--json]
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
bluemix bss account-usage -d 2016-06
```

### bluemix bss org-usage
{: #bluemix_bss_org_usage}

組織の月次使用量の詳細を表示します。この操作は、組織の請求管理者のみ実行できます。

```
bluemix bss org-usage ORG_NAME [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix bss orgs-usage-summary
{: #bluemix_bss_orgs_usage_summary}

マイ・アカウント内の組織の月次使用量サマリーを表示します。

```
bluemix bss orgs-usage-summary [-d YYYY-MM] [-r REGION_NAME] [--json]
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



### bluemix security cert
{: #bluemix_security_cert}

ドメインの証明書情報をリストします。

```
bluemix security cert DOMAIN_NAME
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
bluemix security cert ibmcxo-eventconnect.com
```


### bluemix security cert-add
{: #bluemix_security_cert_add}

現在の組織内の、指定したドメインに証明書を追加します。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD] [-i INTERMEDIATE_CERT_FILE] [--verify-client]
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
   <dt>--verify-client (オプション)</dt>
   <dd>クライアント証明書の検証を使用可能にするかどうか。</dd>
   </dl>


<strong>例</strong>:

ドメイン `ibmcxo-eventconnect.com` に証明書を追加するには、以下のように指定します。

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


### bluemix security cert-remove
{: #bluemix_security_cert_remove}

現在の組織内の、指定したドメインから証明書を削除します。

```
bluemix security cert-remove DOMAIN [-f]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>DOMAIN (必須)</dt>
   <dd>証明書を削除するドメイン。</dd>
   <dt>-f (オプション)</dt>
   <dd>確認なしで削除を強制します。</dd>
   </dl>



### bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI に登録されているすべてのプラグイン・リポジトリーをリストします。

```
bluemix plugin repos
```

<strong>前提条件</strong>: なし


### bluemix plugin repo-add
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


### bluemix plugin repo-remove
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


### bluemix plugin repo-plugins
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


### bluemix plugin list
{: #bluemix_plugin_list}

{{site.data.keyword.Bluemix_notm}} CLI 内のインストールされたプラグインをすべてリストします。

```
bluemix plugin list
```

<strong>前提条件</strong>: なし


### bluemix plugin install
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

最新バージョンの `container-service` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install container-service -r bluemix-repo
```
バージョン `0.5.800` の `container-service` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install container-service -r bluemix-repo -v 0.1.217
```






### bluemix plugin uninstall
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

前にインストールされた `container-service` プラグインをアンインストールします。

```
bluemix plugin uninstall container-service
```



# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [bx ツール ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)
