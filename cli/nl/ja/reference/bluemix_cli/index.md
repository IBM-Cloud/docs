---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-24"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} CLI 入門
{: #getting-started}

{{site.data.keyword.Bluemix_notm}} CLI は、{{site.data.keyword.Bluemix_notm}} 内のアプリケーション、仮想サーバー、コンテナー、およびその他のサービスとの対話をコマンド・ライン・インターフェースを使用して行うための一元化された手法を提供します。また、{{site.data.keyword.Bluemix_notm}} CLI は、各種コミュニティー・ツール (Cloud Foundry CLI、Docker CLI、OpenStack CLI など) を統合し、さまざまな計算タイプとの対話のための環境設定を初期化します。

**制約事項:** {{site.data.keyword.Bluemix_notm}} CLI は Cygwin ではサポートされないため、Cygwin コマンド・ライン・ウィンドウでは {{site.data.keyword.Bluemix_notm}} CLI を使用しないでください。

**注:** CLI および {{site.data.keyword.Bluemix_notm}} が稼働しているホストとの間に HTTP プロキシー・サーバーがあるネットワークを使用している場合、HTTP_PROXY 環境変数にプロキシー・サーバーのホスト名または IP アドレスを指定する必要があります。

## {{site.data.keyword.Bluemix_notm}} CLI のインストール
{: #install_bluemix_cli}

{{site.data.keyword.Bluemix_notm}} CLI をインストールする前に、ご使用のシステムに Cloud Foundry CLI がインストールされていることを確認してください。

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

これで、{{site.data.keyword.Bluemix_notm}} CLI の使用を開始するか、追加プラグインをインストールすることができます。

## プラグインのインストール
{: #install_plug-in}

Cloud Foundry CLI と同様に、{{site.data.keyword.Bluemix_notm}} CLI でも、組み込みコマンド以外の他のコマンドを統合するためのプラグイン拡張フレームワークがサポートされています。

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

  2. 次に、`bluemix plugin install` コマンドを使用して、`Bluemix` リポジトリーからプラグインをインストールします。例えば次のようにします。

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

{{site.data.keyword.Bluemix_notm}} CLI をインストールした後、{{site.data.keyword.Bluemix_notm}} アカウントおよびパスワードを使用して {{site.data.keyword.Bluemix_notm}} にログインできます。例えば次のようにします。

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

<table summary="Bluemix 上のコンテナーの管理に使用することができる bluemix コマンド。">
 <caption>表 7. Bluemix 上のコンテナーを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">Bluemix 上のコンテナーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](index.html#bluemix_ic_service-bind)</td>
 <td>[bluemix ic service-unbind](index.html#bluemix_ic_service-unbind)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](index.html#unpause)</td>
 <td>[bluemix ic unprovision](index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
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

`ic` プラグインのヘルプを表示します。

```
bluemix help ic
```

または

```
bluemix ic help
```

`ic` プラグインの下の `group-create` コマンドのヘルプを表示します。

```
bluemix ic help group-create
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

最新バージョンの `IBM-Containers` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install IBM-Containers -r bluemix-repo
```
バージョン `0.5.800` の `IBM-Containers` プラグインを `bluemix-repo` リポジトリーからインストールするには、以下のように指定します。

```
bluemix plugin install IBM-Containers -r bluemix-repo -v 0.5.800
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

前にインストールされた `IBM-Containers` プラグインをアンインストールします。

```
bluemix plugin uninstall IBM-Containers
```


### bluemix ic attach
{: #bluemix_ic_attach}

実行中のコンテナーを制御するか、その出力を表示します。終了してコンテナーを停止するには `CTRL+C` を使用します。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [attach ](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>--no-stdin (オプション)</dt>
   <dd>標準入力を含めません。</dd>
   <dt>--sig-proxy (オプション)</dt>
   <dd>受信したすべてのシグナルをプロセスに伝達します。デフォルト値は <i>true</i> です。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
    </dl>

<strong>例</strong>:

次の例は、コンテナー `my_container` にアタッチする要求です。

```
bluemix ic attach my_container
```


### bluemix ic build
{: #bluemix_ic_build}

IBM Containers ビルド・サービスを呼び出して、Docker イメージをローカルにビルドするか、またはプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドします。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [build ](https://docs.docker.com/engine/reference/commandline/build/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (必須)</dt>
   <dd>作成されたイメージに適用するリポジトリー名。</dd>
   <dt>--no-cache (オプション)</dt>
   <dd>イメージをビルドするときにキャッシュを使用しません。デフォルトは、<i>false</i> です。</dd>
   <dt>--pull (オプション)</dt>
   <dd>レジストリーからベース・イメージを (それがキャッシュさ
れている場合でも) プルしようとします。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>コンテナーが生成する詳細出力を抑止します。デフォルトは、<i>false</i> です。</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (必須)</dt>
   <dd>ローカル・ホスト上の Dockerfile およびコンテキストのパス。</dd>
    </dl>

<strong>例</strong>:

次の例は、
*myimage* という名前のイメージをビルドする要求です。
ビルドで使用される Dockerfile および他の成果物は、コマンドが実行されるディレクトリーと同じディレクトリー内にあります。レジストリーおよび名前空間がイメージ名と共に含まれているため、イメージは組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドされます。

```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage
```


### bluemix ic cp
{: #bluemix_ic_cp}
コンテナーとローカル・ファイル・システムの間でファイルまたはフォルダーをコピーします。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [cp ](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。


### bluemix ic cpi
{: #bluemix_ic_cpi}

Docker Hub イメージ、またはローカル・レジストリーからのイメージにアクセスし、そのイメージをプライベート {{site.data.keyword.Bluemix_notm}} リポジトリーにコピーします。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (必須)</dt>
   <dd>ソース・リポジトリーおよびイメージの名前。</dd>
   <dt><i>DESTINATION_IMAGE</i> (必須)</dt>
   <dd>プライベート {{site.data.keyword.Bluemix_notm}} リポジトリー URL (名前空間と宛先イメージ名を含む)。イメージのタグはオプションです。</dd>
   </dl>

<strong>例</strong>:

ソース・リポジトリーからプライベート・リポジトリーにイメージをコピーし、そのイメージのタグを追加します。

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

`sinatra` イメージを `training` リポジトリーからプライベート・リポジトリー `registry.ng.bluemix.net/mynamespace` にコピーし、そのイメージの名前を `mysinatra` にします。イメージ `mysinatra` 用にタグ `v1` を追加します。

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


### bluemix ic exec
{: #bluemix_ic_exec}

コンテナー内でコマンドを実行します。詳細については、Docker ヘルプで [exec ](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-d|--detach (オプション)</dt>
   <dd>バックグラウンドで指定されたコマンドを実行します。</dd>
   <dt>-it (オプション)</dt>
   <dd>対話モード。標準入力が表示されている状態を維持します。終了するには <i>exit</i> と入力します。</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (オプシ
ョン)</dt>
   <dd>ユーザー名。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>指定されたコンテナー内で実行するコマンド。</dd>
   </dl>

<strong>例</strong>:

`bash` コマンドを `my_container` コンテナー内で対話モードで実行します。

```
bluemix ic exec -it my_container bash
```

`date` コマンドを `my_container` コンテナー内で実行します。

```
bluemix ic exec my_container date
```


### bluemix ic group-create
{: #bluemix_ic_group_create}

スケーラブル・コンテナー・グループを作成します。

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRONMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ内の各コンテナー・インスタンスに含まれるイ
メージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。<br><br>組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合、形式 <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> でイメージを指定します。<br><br>IBM Containers によって提供されるイメージを使用する場合、組織の名前空間を含めないでください。形式 <i>registry.ng.bluemix.net/IMAGE</i> でイメージを指定してください。</dd>
   <dt>--name <i>GROUP_NAME</i> (required)</dt>
   <dd>グループに名前を割り当てます。<i>-n</i> は推奨されません。<br>
   <strong>ヒント:</strong> コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (.)、下線 (_)、およびハイフン (-) を使用できます。</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (オプション)</dt>
   <dd>グループにメモリー制限を MB 単位で割り当てます。CLI からコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は <i>64</i> MB です。{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は <i>256</i> MB です。受け入れられる値は、<i>64</i>、<i>256</i>、<i>512</i>、<i>1024</i>、および <i>2048</i> です。メモリー限度が割り当てられた後、その値を変更することはできません。</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (オプション)</dt>
   <dd>ホスト名 (<i>mycontainerhost</i> など)。ホストとドメインが結合して、完全なパブリック経路 URL (例えば
<i>http://mycontainerhost.mybluemix.net</i>) を形成します。<i>bluemix ic group-inspect</i> コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>通常は、このドメインは <i>.mybluemix.net</i> です。ホストとドメインが結合して、完全なパブリック経路 URL (例えば <i>http://mycontainerhost.mybluemix.net</i>) を形成します。<i>bluemix ic group-inspect</i> コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (オプション)</dt>
   <dd>環境変数を設定します。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。
例えば、`-e "key1=value1" -e "key2=value2" -e
"key3=value3"` のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。</dd>
    </dl>


|  環境変数                              |     説明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。|
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | ブリッジ・アプリを使用せずに Bluemix サービスをコンテナーに直接バインドするには、CCS_BIND_SRV を使用します。このバインディングにより、Bluemix は、実行中のコンテナー・インスタンスに VCAP_SERVICES 情報を注入できます。複数の Bluemix サービスをリストするには、同じ環境変数の一部としてそれらのサービスを組み込みます。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
{: caption="Table 8. Commonly used environment variables" caption-side="top"}


 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (オプション)</dt>
   <dd> ファイルから環境変数をインポートします。ここで、ENVFILE はローカル・ディレクトリー上のファイルのパスです。ファイル内の各行が、1 つの key=value ペアを表します。</dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (オプション)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 形式で詳細を指定して、コンテナーにボリュームを接続します。<ul>
   <li><i>VOLUME</i>: ボリュームの ID または名前。</li>
   <li><i>CONTAINER_PATH</i>: コンテナー内でのボリュームへの絶対パス。</li>
   <li>ro (オプション):<i>ro</i> を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく読み取り専用になります。</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (オプション)</dt>
   <dd>HTTP トラフィックのポートを公開します。グループ内のコンテナーは、この HTTP ポートを listen する必要があります。HTTPS 要求を行うことはできません。コンテナー・グループに対して複数のポートを含めることはできません。<br><br>ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。これにより、{{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーは、そのポートを使用して、同じ {{site.data.keyword.Bluemix_notm}} スペース内のホストおよびアプリにアクセスできるようになります。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。<br>
   <strong>ヒント</strong>: <ul>
   <li>IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。</li>
   <li>IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。</li>
   </ul>
   </dd>
   <dt>-P (オプション)</dt>
   <dd>すべてのポートを公開します。</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>インスタンスの最小数。デフォルトは 1 です。インスタンスの最小数を設定した
場合、その値をコンテナー・グループ作成後に変更することはできません。</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>インスタンスの最大数。デフォルトは 2 です。インスタンスの最大数を設定した
場合、その値をコンテナー・グループ作成後に変更することはできません。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>必要なインスタンス数。デフォルトは 2 です。</dd>
   <dt>--auto (オプション)</dt>
   <dd>コンテナー・グループが作成され、自動リカバリーが有効にされてい
る場合、IBM Containers は、割り当てられたポートへの HTTP 要求を使用して各インスタンスの正常性を検査します。<br>
その後 2 回の 90 秒間隔のうちにコンテナー・インスタンスから応答を受け取らなければ、そのインスタンスは削除され、新しいインスタンスに置き換えられます。コンテナーが応答すればアクションは行われません。このプロセスは連続して繰り返されます。30 分の時間枠の間に、グループ・メンバーとなった異なるコンテナーの総数が、最大グループ・サイズの 3 倍以上になった場合、そのコンテナー・グループに対する自動リカバリーは永続的に無効になります。自動リカバリーを再度有効にするには、コンテナー・グループを再作成する必要があります。</dd>
  <dt>--anti (オプション)</dt>
  <dd> アンチアフィニティーを使用して、コンテナー・グループの高可用性を高めます。--anti オプションを指定すると、グループ内の各コンテナー・インスタンスが、強制的に別個の物理計算ノードに配置されます。これにより、ハードウェア障害でグループ内の全コンテナーがクラッシュする可能性が低下します。各 Bluemix 地域および組織でデプロイメントに使用可能な計算ノードのセットは限られているため、グループ・サイズが大きい場合、このオプションを使用できないことがあります。デプロイメントが成功しない場合は、グループ内のコンテナー・インスタンスの数を減らすか、--anti オプションを削除してください。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>コンテナー・グループに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、<i>/bin/date</i> など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。<br> 
<strong>注:</strong> <ul>
   <li>コマンドおよびその引数は、<i>bluemix ic run</i> コマンド・ラインの末尾に指定する必要があります。</li>
   <li>コマンド引数にハイフン (-) が含まれる場合 (前のコマンド例の
<i>-c</i> のような場合)、コマンドの前にはハイフンを 2 つ (--) 付ける
必要があります。</li>
   </ul></dd>
   </dl>


<strong>例</strong>:

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `ping localhost` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `tail -f /dev/null` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

`registry.ng.bluemix.net/ibmliberty` イメージを使用して、スケーラブル・グループ `mygroup` を自動リカバリーを有効にして作成します。ポートは `9080`、ホスト名は `mycontainerhost`、ドメイン名は `mybluemix.net` です。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


### bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

コンテナー・グループの作成時に指定された詳細情報 (環境変数、ポート、メモリーなど) を表示します。

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、コンテナー・グループ `my_group` を検査する要求を示しています。

```
bluemix ic group-inspect my_group
```


### bluemix ic group-instances
{: #bluemix_ic_group_instances}

指定されたコンテナー・グループのインスタンスをリストします。

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

コンテナー・グループ `my_group` のすべてのインスタンスをリストします。

```
bluemix ic group-instances my_group
```


### bluemix ic group-remove
{: #bluemix_ic_group_remove}

スペースからコンテナー・グループを削除します。

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-f|--force (オプション)</dt>
   <dd>実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除
します。</dd>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>


<strong>例</strong>:

次の例は、コンテナー・グループを削除する要求です。ここで、`my_group` はコンテナー・グループの名前です。

```
bluemix ic group-remove my_group
```


### bluemix ic group-update
{: #bluemix_ic_group_update}

コンテナー・グループを更新します。


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**ヒント:** コンテナー・グループのホスト名またはドメインを更新するには、`bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP` を使用します。

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
 <dl>
   <dt>--anti (オプション)</dt>
   <dd>アンチアフィニティーを使用して、コンテナー・グループの高可用性を高めます。--anti オプションを指定すると、グループ内の各コンテナー・インスタンスが、強制的に別個の物理計算ノードに配置されます。これにより、ハードウェア障害でグループ内の全コンテナーがクラッシュする可能性が低下します。各 Bluemix 地域および組織でデプロイメントに使用可能な計算ノードのセットは限られているため、グループ・サイズが大きい場合、このオプションを使用できないことがあります。デプロイメントが成功しない場合は、グループ内のコンテナー・インスタンスの数を減らすか、--anti オプションを削除してください。</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (オプション)</dt>
   <dd>必要なインスタンス数。デフォルトは <i>2</i> です。</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>(オプション)</dt>
   <dd>環境変数を設定します。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。
例えば、`-e "key1=value1" -e "key2=value2" -e
"key3=value3"` のようにします。</dd>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、コンテナー・グループ `my_group` を更新する要求です。

```
bluemix ic group-update --desired 5 my_group
```


### bluemix ic groups
{: #bluemix_ic_groups}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のコンテナー・グループをリストします。

```
bluemix ic groups [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:
	<dl>
	<dt>-q (オプション)</dt>
   	<dd>グループ ID のみを表示します。</dd>
	</dl>


### bluemix ic images
{: #bluemix_ic_images}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内の使用可能なすべてのイメージのリストを表示します。詳細については、Docker ヘルプで [images ](https://docs.docker.com/engine/reference/commandline/images){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。リストには、イメージ ID、作成日、およびイメージ名が含まれます。

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-a|--all (オプション)</dt>
   <dd>組織のリポジトリー内の各イメージについて、最新のイメージ層のみ
ではなく、すべてのイメージ層を含めます。</dd>
   <dt>-f (オプション)</dt>
   <dd>指定した条件でイメージのリストをフィルターに掛けます。</dd>
   <dt>--no-trunc (オプション)</dt>
   <dd>出力を切り捨てません。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>数字の ID のみを表示します。</dd>
   </dl>

<strong>例</strong>:

次の例は、組織の使用可能なイメージのリストを受け取る要求です。

```
bluemix ic images
```


### bluemix ic info
{: #bluemix_ic_info}

コンテナー・クラウド・サービス・インスタンスの状態を説明する情報を表示します。この情報に含まれるのは、コンテナーの限度、コンテナーの使用状況、実行中のコンテナー、メモリーの限度、メモリーの使用状況、浮動 IP アドレスの限度、浮動 IP アドレスの使用状況、CCS ホスト URL、レジストリー・ホスト URL、およびデバッグ・モード状況です。

```
bluemix ic info
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


### bluemix ic init
{: #bluemix_ic_init}

IBM Containers サービスの全機能を使用できるようにローカル・マシン上のコンテナー環境を初期化します。

```
bluemix ic init
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

**注:** 初期化を行う前に、Docker CLI (docker) がインストールされ、PATH 環境変数内に構成されていることを確認してください。別の地域に切り替えるには、`bluemix region-set` コマンドを使用します。

<strong>例</strong>:

`us-south` 地域に切り替えます。

```
bluemix region-set us-south
```


### bluemix ic inspect
{: #bluemix_ic_inspect}

コンテナーに関する情報を表示します。詳細については、Docker ヘルプで [inspect](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} コマンドを参照してください。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>イメージの名前または ID を指定することによって、特定のイメージ
についての詳細情報を表示します。</dd>
   <dt>images (必須)</dt>
   <dd>リポジトリー内のすべてのイメージについての詳細情報を表示します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID を指定することによって、特定のコンテ
ナーについての詳細情報を表示します。</dd>
   </dl>

**ヒント:** 一度に指定できるのは、
*IMAGE*、*images*、または
*CONTAINER* のいずれか 1 つのみです。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを検査する要求です。

```
bluemix ic inspect proxy
```


### bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

使用可能な浮動 IP アドレスをコンテナーにバインドします。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>バインドする IP アドレス。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>バインドするコンテナーの ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` にバインドする要求です。

```
bluemix ic ip-bind 192.123.12.12 proxy
```


### bluemix ic ip-release
{: #bluemix_ic_ip_release}

コンテナー・クラウド・サービス・インスタンスから浮動 IP アドレスを解放します。

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>リリースする IP アドレス。</dd>
   </dl>


### bluemix ic ip-request
{: #ip_request}
新しい浮動 IP アドレスを要求します。

```
bluemix ic ip-request [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-q (オプション)</dt>
   <dd>IP アドレスのみをリストします。それらの IP アドレスにバインドされたコンテナーの ID はリストしません。</dd>
   </dl>


### bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

浮動 IP アドレスをそのコンテナーからアンバインドします。

パブリック IP アドレスは、IBM Containers の制限付きリソースです。したがって、スペースに割り当てられていてコンテナーにバインドされていないパブリック IP アドレスは、およそ週 1 回の頻度で無料試用ユーザーから定期的に再要求されます。アンバインドされたパブリック IP アドレスは、従量制課金カスタマーまたはサブスクリプション・カスタマーから再要求されることはありません。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (必須)</dt>
   <dd>アンバインドする IP アドレス。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>アンバインドするコンテナーの ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` からアンバインドする要求です。

```
bluemix ic ip-unbind 192.123.12.12 proxy
```


### bluemix ic ips
{: #bluemix_ic_ips}

ログインしているユーザーが使用可能な浮動 IP アドレスをリストします。このリストには、IP アドレスと、IP アドレスがリンクされている先のコンテナー ID が含まれます。IP アドレスが未使用の場合、コンテナー ID は示されません。

```
bluemix ic ips [-q]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-q (オプション)</dt>
   <dd>IP アドレスのみをリストします。それらの IP アドレスにバインドされたコンテナーの ID はリストしません。</dd>
   </dl>


<strong>例</strong>:

次の例は、組織のすべての IP アドレスのリストを受け取る要求を示しています。
```
bluemix ic ips -q
```


### bluemix ic kill
{: #bluemix_ic_kill}

コンテナーを停止せずにコンテナー内の実行中のプロセスを停止します。詳細については、Docker ヘルプで [kill ](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (オプション)</dt>
   <dd>コンテナー内の実行中のプロセスにコマンドを送信します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの ID または名前。</dd>
   </dl>


<strong>例</strong>:

次の例は、`proxy` という名前のコンテナー内のプロセスを停止する要求です。

```
bluemix ic kill proxy
```


### bluemix ic logs
{: #bluemix_ic_logs}

実行中のコンテナーの出力ログまたはエラー・ログを表示します。詳細については、Docker ヘルプで [logs ](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。
```
bluemix ic logs [OPTIONS] CONTAINER
```


### bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を表示します。

```
bluemix ic namespace-get
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


### bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を設定します。

*制限*: リポジトリー名前空間の名前にハイフン (`-`) を使用することはできません。

```
bluemix ic namespace-set NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>NAME</i> (必須)</dt>
   <dd>組織のリポジトリー名前空間を (まだ設定されていない場合に) 設定
する 1 回限りの機能です。名前空間を設定した後、続行する前に、`bluemix ic init` コマンドを使用して IBM Containers を再初期化してください。</dd>
   </dl>


### bluemix ic pause
{: #pause}

実行中のコンテナー内のすべてのプロセスを休止します。詳細については、Docker ヘルプで [pause ](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic unpause](#unpause) コマンドを参照してください。

```
bluemix ic pause CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:
   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に休止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを休止する要求です。

```
bluemix ic pause proxy
```


### bluemix ic port
{: #bluemix_ic_port}

コンテナーのポート・マッピングまたは特定のマッピングをリストします。このコマンドは `docker port` コマンドをラップします。詳細については、Docker ヘルプで [port ](https://docs.docker.com/engine/reference/commandline/port/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。


### bluemix ic ps
{: #bluemix_ic_ps}
ログインしているユーザーの名前空間で実行中のコンテナーのリストを表示します。デフォルトでは、このコマンドは実行中のコンテナーのみを表示します。詳細については、Docker ヘルプで [ps ](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-a|--all (オプション)</dt>
   <dd>実行中のコンテナーも停止状態のコンテナーも、どちらもすべて表示します。</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (オプション)</dt>
   <dd>特定の環境変数値を持つコンテナーを検索します。コンテナーの検査時に CLI 応答の「Env」セクションにリストされている任意の環境変数キーまたは値によって、コンテナーをフィルターに掛けることができます。SEARCH_CRITERIA は、検索するキーまたは値に置き換えてください。検索基準は、完全一致突き合わせである必要はありません。</dd>
   <dt>-s|--size (オプション)</dt>
   <dd>コンテナーのサイズをリストします。</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (オプション)</dt>
   <dd>最近作成されたコンテナーをリストします。ここで <i>NUM</i> は、
最近作成されたコンテナーのうちのいくつのコンテナーを返したいかを指定する数です。
<br><br> 例えば、<i>node1</i> から <i>node5</i> までのコンテ
ナーを順次作成した場合、コマンド <i>bluemix ic ps --limit 2</i> は、
作成されたコンテナーのうちの最新の 2 つである node4 と node5 を返します。</dd>
   <dt>-q|--quiet (オプション)</dt>
   <dd>コンテナー ID のみを表示します。</dd>
   </dl>


<strong>例</strong>:

次の例は、実行中と停止状態のすべてのコンテナーを表示する要求です。

```
bluemix ic ps -a
```


### bluemix ic rename
{: #bluemix_ic_rename}
コンテナーの名前を変更します。詳細については、Docker ヘルプで [rename ](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker<strong>コマンド・オプション</strong>:

<dl>
   <dt><i>OLD_NAME</i> (必須)</dt>
   <dd>コンテナーの古い名前。</dd>
   <dt><i>NEW_NAME</i> (必須)</dt>
   <dd>コンテナーの新しい名前。</dd>
   </dl>


### bluemix ic reprovision
{: #bluemix_ic_reprovision}

ログインしている Bluemix スペースで IBM Containers サービスを再作成します。スペースの元の割り当て量は維持されます。

<strong>重要</strong>: このコマンドを実行した場合、このスペース内の単一コンテナーおよびグループはどれも、再プロビジョンされたスペースにマイグレーションされず、マイグレーション・プロセス中に削除されます。

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>コマンド・オプション</strong>:<dl>
   <dt>--force|-f (オプション)</dt>
   <dd>Bluemix スペースで IBM Containers サービスを強制的に再作成します。</dd>
   <dt><i>AVAILABILITY_ZONE</i> (必須)</dt>
   <dd>コンテナーがデプロイされた IBM Containers アベイラビリティー・ゾーンの名前。アベイラビリティー・ゾーンが指定されない場合は、地域に設定されたデフォルト・アベイラビリティー・ゾーンが使用されます。</dd>
   </dl>


### bluemix ic restart
{: #bluemix_ic_restart}

コンテナーを再始動します。詳細については、Docker ヘルプで [restart ](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (オプション)</dt>
   <dd>コンテナーが再始動されるまでに待機する秒数。</dd>
   </dl>


<strong>応答</strong>:

- コンテナーは正常に再始動されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを再始動する要求です。

```
bluemix ic restart proxy
```


### bluemix ic rm
{: #bluemix_ic_rm}

コンテナーを削除します。詳細については、Docker ヘルプで [rm ](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-f|--force (オプション)</dt>
   <dd>実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除
します。</dd>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に削除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを削除する要求です。

```
bluemix ic rm proxy
```


### bluemix ic rmi
{: #bluemix_ic_rmi}

ログインしているユーザーの名前空間からイメージを削除します。詳細については、Docker ヘルプで [rmi ](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (オプション)</dt>
   <dd>レジストリー・ホストを変更します。
デフォルトでは、<i>bluemix ic init</i> コマンドに指定したレジストリーが使用されます。</dd>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>削除するイメージの名前。イメージ名にタグが指定されていない場合、
<i>latest</i> とタグ付けされたイメージはデフォルトで削除されます。
</dd>
   </dl>

<strong>応答</strong>:

- 削除されました: `{IMAGE}`

 ここで、`{IMAGE}` は削除されたイメージの名前です。

- エラー! レジストリー・ホストが指定されていません。

- イメージ削除は失敗しました - コンテナー・クラウド・レジストリーに接続できませんでした。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


<strong>例</strong>:

次の例は、イメージ `mynamespace/myimage:latest` を削除する要求です。

```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


### bluemix ic route-map
{: #bluemix_ic_route_map}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (オプション)</dt>
   <dd>経路のホスト名。ホスト名は、完全なパブリック経路 URL の最初の部分です。例えば、URL <i>mycontainerhost.mybluemix.net</i> 中の <i>mycontainerhost</i> です。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>完全なパブリック経路 URL の 2 番目の部分である、経路のドメイン名。
ほとんどの場合、ドメインは <i>mybluemix.net</i> です。このパラメーターを使用してプライベート・ドメインを指定することもできます。</dd>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、`GROUP1` と呼ばれるグループの経路をマップする要求です。ここで、`my_host` はホスト名で、`mybluemix.net` はドメインです。
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


### bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (オプション)</dt>
   <dd>経路のホスト名。</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (オプション)</dt>
   <dd>経路のドメイン名。</dd>
   <dt><i>CONTAINER_GROUP</i> (必須)</dt>
   <dd>コンテナー・グループ ID または名前。</dd>
   </dl>

<strong>例</strong>:

次の例は、`GROUP1` と呼ばれるグループ
の経路をマップ解除する要求です。ここで、`my_host` は
ホスト名、`organization.com` はドメインです。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


### bluemix ic run
{: #bluemix_ic_run}

イメージ名を使用して、コンテナー・クラウド・サービスで新しいコンテナーを開始します。
詳細については、Docker ヘルプで [run ](https://docs.docker.com/engine/reference/commandline/run/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**注:** Cloud Foundry コマンド・ツールがインストー
ルされていること、および Cloud Foundry トークンがあることを確認してください。
`bluemix login` および `bluemix ic
init` を使用した正常なログインによって、必要なトークンおよび
証明書が生成されます。
<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (オプション)</dt>
   <dd>HTTP トラフィックのポートを公開します。使用するイメージの Dockerfile 内に指定されているポートがあれば、それらのポートを含めます。複数の <i>-p</i> オプションを使用して、複数のポートを含めることができます。ポートを公開すると、パブリック IP アドレスが使用可能な場合、パブリック IP アドレスがコンテナーに自動的にバインドされます。<br><br>コンテナーにバインドしたい IP アドレスがスペース内に既に存在する場合、後でバインドするのでなく、その IP アドレスを指定できます。IP アドレスは、&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt; <br> 形式で指定する必要があります。<br>スペース用の IP アドレスの要求について詳しくは、<a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a> コマンドを参照してください。<br><br>ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。<br><br>
<strong>ヒント:</strong><ul><li>IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。</li><li>IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。</li></ul></dd>
   <dt>-P (オプション)</dt>
   <dd>イメージの Dockerfile 内に指定されたポートを HTTP トラフィック
用に自動的に公開します。</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (オプ
ション)</dt>
   <dd>グループにメモリー制限を MB 単位で割り当てます。CLI からコンテナー・グループを作成す
る場合、各コンテナー・インスタンスのデフォルト値は 64 MB です。
{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナ
ー・グループを作成する場合、各インスタンスのデフォルト値は 256 MB で
す。受け入れられる値は 64、256、512、1024、および 2048 です。メモリー限度が割り当てられた後、その値を変更することはできません。</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (オプション)</dt>
   <dd>環境変数を設定します。ここで、<i>ENV</i> は key=value ぺアです。
複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。例えば、-e
"key1=value1" -e "key2=value2" -e "key3=value3"のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。</dd>
   </dl>


|      環境変数                          |   説明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。ブリッジ・アプリの作成について詳しくは、[コンテナーへのサービスのバインド](/docs/containers/container_integrations_binding.html){: new_window}を参照してください。 |
| CCS_BIND_SRV=*&lt;service_instance_name1&gt;*,*&lt;service_instance_name2&gt;* | ブリッジ・アプリを使用せずに Bluemix サービスをコンテナーに直接バインドするには、CCS_BIND_SRV を使用します。このバインディングにより、Bluemix は、実行中のコンテナー・インスタンスに VCAP_SERVICES 情報を注入できます。複数の Bluemix サービスをリストするには、同じ環境変数の一部としてそれらのサービスを組み込みます。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
{: caption="Table 9. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (オプション)</dt>
   <dd><i>VolumeId:ContainerPath[:ro]</i> 形式で詳細を指定して、コンテナーにボリュームを接続します。<ul>
   <li><i>VOLUME</i>: ボリュームの ID または名前。</li>
   <li><i>CONTAINER_PATH</i>: コンテナー内でのボリュームへの絶対パス。</li>
   <li>ro (オプション):<i>ro</i> を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく読み取り専用になります。</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (必須)</dt>
   <dd>コンテナーに名前を割り当てます。<br> <strong>ヒント:</strong> コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (.)、下線 (_)、およびハイフン (-) を使用できます。</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (オプション)</dt>
   <dd>あるコンテナーが実行中の別のコンテナーと通信するようにしたい場合は、ホスト名の別名を使用してそのコンテナーを指定できます。</dd>
   <dt>-it (オプション)</dt>
   <dd>コンテナーを対話モードで実行します。コンテナーが作成された後、標準入力が表示されている状態を維持します。終了するには <i>exit</i> と入力します。</dd>
   <dt><i>IMAGE</i> (必須)</dt>
   <dd>コンテナーに含まれるイメージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。イメージを指定する前に、すべてのオプションを含めてください。<br><br>組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合、形式 <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i> でイメージを指定します。<br><br>
IBM Containers によって提供されるイメージを使用する場合は、形式
<i>registry.ng.bluemix.net/IMAGE</i> でイメージを指定します。</dd>
   <dt><i>CMD</i> (必須)</dt>
   <dd>コンテナー・グループに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、<i>/bin/date</i> など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。</dd>
   </dl>


<strong>例</strong>:

`registry.ng.bluemix.net/ibmnode` イメージに基づいて作成された `my_container` コンテナーで、長時間実行コマンド `sh -c "while true; do date; sleep 20; done"` を実行します。

```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


`my_namespace/nginx` イメージを使用して、メモリー限度が `1024` MB のコンテナー `proxy` を作成し、開始します。ここで、`my_namespace` は、ログイン・ユーザーと関連付けられた名前空間です。

```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

`my_namespace/blog` イメージを使用してコンテナーを作成して開始し、資格情報を環境変数として渡します。`my_namespace` は、ログイン・ユーザーと関連付けられた名前空間です。

```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

`my_namespace/blog` イメージを使用してボリュームをコンテナーに追加します。ここで、`my_namespace` は、ログイン・ユーザーに関連付けられた名前空間です。

```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


### bluemix ic service-bind
{: #bluemix_ic_service-bind}

実行中のコンテナー・グループにサービスを追加します。このコマンドは、コンテナー・グループにのみ使用可能です。単一コンテナーは、bluemix ic run コマンドの中でサービスをバインドする必要があります。

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>グループ ID または名前。</dd>
   <dt><i>SERVICE_INSTANCE</i> (必須)</dt>
   <dd>コンテナー・グループに追加するサービス・インスタンスの名前。</dd>
   </dl>


### bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

実行中のコンテナー・グループからサービスを削除します。このコマンドは、コンテナー・グループにのみ使用可能です。単一コンテナーは、コンテナーを削除し、サービスが含まれない新しいコンテナーを作成する必要があります。

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt><i>GROUP_NAME</i> (必須)</dt>
   <dd>グループ ID または名前。</dd>
   <dt><i>SERVICE_INSTANCE</i> (必須)</dt>
   <dd>コンテナー・グループに追加するサービス・インスタンスの名前。</dd>
   </dl>


### bluemix ic start
{: #ic_start}
停止しているコンテナーを開始します。詳細については、Docker ヘルプで [start ](https://docs.docker.com/engine/reference/commandline/start/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic stop](#ic_stop) コマンドを参照してください。

```
bluemix ic start CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>


<strong>応答</strong>:

- コンテナーは正常に開始しました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを開始する要求です。

```
bluemix ic start proxy
```


### bluemix ic stats
{: #bluemix_ic_stats}

1 つ以上のコンテナーについて、使用状況統計をライブで表示します。終了するには `CTRL+C` を使用します。詳細については、Docker ヘルプで [stats](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} コマンドを参照してください。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>--no-stream (オプション)</dt>
   <dd>最新の結果のみを表示し、それ以前の情報を含めません。</dd>
   </dl>

<strong>例</strong>:

次の例は、1 つのコンテナーについての最新の統計情報を表示する要求です。

```
bluemix ic stats --no-stream my_container
```


### bluemix ic stop
{: #ic_stop}
実行中のコンテナーを停止します。詳細については、Docker ヘルプで [stop ](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。コンテナーを開始する場合は、[bluemix ic start](#ic_start) コマンドを参照してください。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (オプション)</dt>
   <dd>コンテナーを強制終了するまでの待機秒数。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に停止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを停止する要求です。

```
bluemix ic stop proxy
```


### bluemix ic top
{: #bluemix_ic_top}

コンテナーで実行されているプロセスを表示します。詳細については、Docker ヘルプで [top ](https://docs.docker.com/engine/reference/commandline/top/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナー内のプロセスを表示する要求です。

```
bluemix ic top my_container
```


### bluemix ic unpause
{: #unpause}

実行中のコンテナー内のすべてのプロセスを休止解除します。詳細については、Docker ヘルプで [unpause ](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。コンテナーを休止する場合は、[bluemix ic pause](#pause) コマンドを参照してください。

```
bluemix ic unpause CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>応答</strong>:

- コンテナーは正常に休止解除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`

 ここで、`{message}` は関連するエラーです。


- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

<strong>例</strong>:

次の例は、`proxy` という名前のコンテナーを休止解除する要求です。

```
bluemix ic unpause proxy
```


### bluemix ic unprovision
{: #bluemix_ic_unprovision}

ログインしている Bluemix スペースから IBM Containers サービスを削除します。

<strong>注意</strong>: このコマンドを実行すると、単一コンテナーとコンテナー・グループがすべて失われます。Bluemix では、まだスペースを使用可能です。IBM Containers の使用を再び開始するには、`bluemix ic reprovision` を実行して IBM Containers サービスを再度プロビジョンする必要があります。

```
bluemix ic reprovision [--force|-f] 
```
<strong>コマンド・オプション</strong>:<dl>
   <dt>--force|-f (オプション)</dt>
   <dd>Bluemix スペースから Bluemix を強制的に削除します。</dd>
 </dl>


### bluemix ic version
{: #bluemix_ic_version}

Docker および IBM Containers API のバージョンを表示します。

```
bluemix ic version
```

<strong>前提条件</strong>:  Docker

IBM Containers のバージョンを表示するには、`bluemix ic info` を実行します。詳細については、Docker ヘルプで [version ](https://docs.docker.com/engine/reference/commandline/version/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。


### bluemix ic volume-create
{: #bluemix_ic_volume_create}

ボリュームを作成します。

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FS_NAME</i> (オプション)</dt>
   <dd>ファイル共有名ファイル共有が使用可能でないか指定されていない場合、ボリュームは、スペースのデフォルトのファイル共有上に作成されます。</dd>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。名前には、小文字、数字、下線 (_)、およびハイフン
(-) を 使用できます。</dd>
   </dl>


<strong>例</strong>:

次の例は、ボリュームを作成する要求です。

```
bluemix ic volume-create volume_name fileshare_name
```


### bluemix ic volume-fs

{: #bluemix_ic_volume_fs}

ファイル共有をリストします。

```
bluemix ic volume-fs
```


### bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

ファイル共有を作成します。

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名名前には、小文字、数字、下線 (_)、およびハイフン
(-) を 使用できます。</dd>
   </dl>

<strong>例</strong>:

以下の例では、ファイル共有を作成する要求を示します。
```
bluemix ic volume-fs-create my_file_share
```


### bluemix ic volume-fs-flavors

{: #bluemix_ic_volume_fs_flavors}

すべてのファイル共有のフレーバーをリストします。

```
bluemix ic volume-fs-flavors
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


### bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

ファイル共有を検査します。

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名</dd>
   </dl>

<strong>例</strong>:

次の例は、ファイル共有を検査する要求です。ここで、`my_file_share` は、ファイル共有の名前です。
```
bluemix ic volume-fs-inspect my_file_share
```


### bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

ファイル共有を削除します。

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (必須)</dt>
   <dd>ファイル共有名</dd>
   </dl>

<strong>例</strong>:

次の例では、ファイル共有を削除する要求を示します。ここで、`my_file_share` は、ファイル共有の名前です。
```
bluemix ic volume-fs-remove my_file_share
```


### bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

ボリュームを検査します。


```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。</dd>
   </dl>

<strong>例</strong>:

次の例は、ボリュームを検査する要求です。ここで、`volume_name` はボリュームの名前です。

```
bluemix ic volume-inspect volume_name
```


### bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

ボリュームを削除します。

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (必須)</dt>
   <dd>ボリューム名。</dd>
    </dl>

<strong>例</strong>:

次の例は、ボリュームを削除する要求です。ここで、`volume_name` はボリュームの名前です。

```
bluemix ic volume-remove volume_name
```


### bluemix ic volumes
{: #bluemix_ic_volumes}

ボリュームをリストします。

```
bluemix ic volumes
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット


### bluemix ic wait
{: #bluemix_ic_wait}

コンテナーを終了し、確認のために終了コードを表示します。詳細については、Docker ヘルプで [wait ](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg) コマンドを参照してください。

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナーを終了する要求です。

```
bluemix ic wait my_container
```


### bluemix ic wait-status
{: #bluemix_ic_wait_status}

単一コンテナーまたはコンテナー・グループが非過渡的な状態になるまで待機します。この待機時間中は、コマンド・ラインが戻らないため、コマンドを入力できません。コンテナーが非過渡的な状態になると、すぐに OK メッセージが表示されます。単一コンテナーの場合、非過渡的な状態には Running、Shutdown、Crashed、Paused、Suspended があります。コンテナー・グループの場合、非過渡的な状態には CREATE_COMPLETE、UPDATE_COMPLETE、FAILED があります。

```
bluemix ic wait-status CONTAINER
```

<strong>前提条件</strong>: エンドポイント、ログイン、ターゲット、Docker

<strong>コマンド・オプション</strong>:

   <dl>
   <dt><i>CONTAINER</i> (必須)</dt>
   <dd>コンテナーの名前または ID。</dd>
   </dl>

<strong>例</strong>:

次の例は、`my_container` という名前のコンテナーを終了する要求です。

```
bluemix ic wait my_container
```



# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [bx ツール ](http://clis.ng.bluemix.net/ui/home.html){: new_window} ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)
