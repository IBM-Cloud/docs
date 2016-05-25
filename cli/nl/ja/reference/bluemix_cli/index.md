---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} (bx) コマンド
{: #bluemix_cli}

*最終更新日: 2016 年 4 月 15 日*

{{site.data.keyword.Bluemix_notm}} コマンド・ライン・インターフェース (CLI) では、ユーザーが {{site.data.keyword.Bluemix_notm}} と対話できるように、名前空間別にグループ化したコマンドのセットが提供されています。{{site.data.keyword.Bluemix_notm}} コマンドには、既存の cf コマンドのラッパーになっているものもあれば、{{site.data.keyword.Bluemix_notm}} ユーザー向けの拡張機能を提供するものもあります。以下の説明では、{{site.data.keyword.Bluemix_notm}} CLI によってサポートされるすべてのコマンドをリストし、名前、オプション、使用法、前提条件、説明、および例を示します。
{:shortdesc}
 
**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件となるアクションのないコマンドでは、**なし**とリストされています。それ以外の場合、前提条件には以下のアクションのうちの 1 つ以上が含まれます。
<dl>
<dt>エンドポイント</dt>
<dd>このコマンドを使用する前に、<code>bluemix api</code> を介して API エンドポイントを設定する必要があります。</dd>
<dt>login</dt>
<dd>このコマンドを使用する前に、<code>bluemix login</code> コマンドを使用してログインする必要があります。</dd>
<dt>ターゲット</dt>
<dd>このコマンドを使用する前に、<code>bluemix target</code> コマンドを使用して組織およびスペースを設定する必要があります。</dd>
<dt>Docker</dt>
<dd>このコマンドを実行するためには、Docker CLI (docker) がインストールされている必要があります。</dd>
</dl>

以下の {{site.data.keyword.Bluemix_notm}} コマンドが使用できます:

 <table role="presentation"> 
 <tbody> 
 <tr> 
 <td>[bluemix help](index.html#bluemix_help)</td> 
 <td>[bluemix api](index.html#bluemix_api)</td> 
 <td>[bluemix login](index.html#bluemix_login)</td>
 <td>[bluemix logout](index.html#bluemix_logout)</td>
 <td>[bluemix target](index.html#bluemix_target)</td>
 </tr> 
 <tr> 
 <td> 
 [bluemix info](index.html#bluemix_info) </td> 
 <td>[bluemix config](index.html#bluemix_config)</td> 
 <td>[bluemix list](index.html#bluemix_list)</td>
 <td>[bluemix scale](index.html#bluemix_scale)</td>
 <td>[bluemix curl](index.html#bluemix_curl)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam orgs](index.html#bluemix_iam_orgs) </td> 
 <td>[bluemix iam org](index.html#bluemix_iam_org)</td> 
 <td>[bluemix iam org-create](index.html#bluemix_iam_org_create)</td>
 <td>[bluemix iam org-replicate](index.html#bluemix_iam_org_replicate)</td>
 <td>[bluemix iam org-rename](index.html#bluemix_iam_org_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-delete](index.html#bluemix_iam_org_delete) </td> 
 <td>[bluemix iam spaces](index.html#bluemix_iam_spaces)</td> 
 <td>[bluemix iam space](index.html#bluemix_iam_space)</td>
 <td>[bluemix iam space-create](index.html#bluemix_iam_space_create)</td>
 <td>[bluemix iam space-rename](index.html#bluemix_iam_space_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam space-delete](index.html#bluemix_iam_space_delete) </td> 
 <td>[bluemix iam account-users](index.html#bluemix_iam_account-users)</td> 
 <td>[bluemix iam account-user-invite](index.html#bluemix_iam_account-user-invite)</td>
 <td>[bluemix iam org-users](index.html#bluemix_iam_org_users)</td>
 <td>[bluemix iam org-role-set](index.html#bluemix_iam_org_role_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix iam org-role-unset](index.html#bluemix_iam_org_role_unset) </td> 
 <td>[bluemix iam space-users](index.html#bluemix_iam_space_users)</td> 
 <td>[bluemix iam space-role-set](index.html#bluemix_iam_space_role_set)</td>
 <td>[bluemix iam space-role-unset](index.html#bluemix_iam_space_role_unset)</td>
 <td>[bluemix app push](index.html#bluemix_app_push)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app list](index.html#bluemix_app_list) </td> 
 <td>[bluemix app show](index.html#bluemix_app_show)</td> 
 <td>[bluemix app scale](index.html#bluemix_app_scale)</td>
 <td>[bluemix app delete](index.html#bluemix_app_delete)</td>
 <td>[bluemix app rename](index.html#bluemix_app_rename)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app start](index.html#bluemix_app_start) </td> 
 <td>[bluemix app stop](index.html#bluemix_app_stop)</td> 
 <td>[bluemix app restart](index.html#bluemix_app_restart)</td>
 <td>[bluemix app restage](index.html#bluemix_app_restage)</td>
 <td>[bluemix app instance-restart](index.html#bluemix_app_instance_restart)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app events](index.html#bluemix_app_events) </td> 
 <td>[bluemix app files](index.html#bluemix_app_files)</td> 
 <td>[bluemix app logs](index.html#bluemix_app_logs)</td>
 <td>[bluemix app env](index.html#bluemix_app_env)</td>
 <td>[bluemix app env-set](index.html#bluemix_app_env_set)</td>
 </tr>
 
 <tr> 
 <td>[bluemix app env-unset](index.html#bluemix_app_env_unset) </td> 
 <td>[bluemix app stacks](index.html#bluemix_app_stacks)</td> 
 <td>[bluemix app stack](index.html#bluemix_app_stack)</td>
 <td>[bluemix app manifest-create](index.html#bluemix_app_manifest_create)</td>
 <td>[bluemix service offerings](index.html#bluemix_service_offerings)</td>
 </tr>
 
 <tr> 
 <td>[bluemix service list](index.html#bluemix_service_list) </td> 
 <td>[bluemix service show](index.html#bluemix_service_show)</td> 
 <td>[bluemix service create](index.html#bluemix_service_create)</td>
 <td>[bluemix service update](index.html#bluemix_service_update)</td>
 <td>[bluemix service delete](index.html#bluemix_service_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service rename](index.html#bluemix_service_rename) </td> 
 <td>[bluemix service bind](index.html#bluemix_service_bind)</td> 
 <td>[bluemix service unbind](index.html#bluemix_service_unbind)</td>
 <td>[bluemix service key-create](index.html#bluemix_service_key_create)</td>
 <td>[bluemix service key-delete](index.html#bluemix_service_key_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix service keys](index.html#bluemix_service_keys) </td> 
 <td>[bluemix service key-show](index.html#bluemix_service_key_show)</td> 
 <td>[bluemix service user-provided-create](index.html#bluemix_service_user_provided_create)</td>
 <td>[bluemix service user-provided-update](index.html#bluemix_service_user_provided_update)</td>
 <td>[bluemix catalog templates](index.html#bluemix_catalog_templates)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix catalog template](index.html#bluemix_catalog_template) </td> 
 <td>[bluemix catalog template-run](index.html#bluemix_catalog_template_run)</td> 
 <td>[bluemix network regions](index.html#bluemix_network_regions)</td>
 <td>[bluemix network region-set](index.html#bluemix_network_region_set)</td>
 <td>[bluemix network routes](index.html#bluemix_network_routes)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network route-check](index.html#bluemix_network_route_check)</td> 
 <td>[bluemix network route-map](index.html#bluemix_network_route_map)</td> 
 <td>[bluemix network route-unmap](index.html#bluemix_network_route_unmap)</td>
 <td>[bluemix network route-create](index.html#bluemix_network_route_create)</td>
 <td>[bluemix network route-delete](index.html#bluemix_network_route_delete)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network orphaned-routes-delete](index.html#bluemix_network_orphaned_routes_delete)</td> 
 <td>[bluemix network domains](index.html#bluemix_network_domains)</td> 
 <td>[bluemix network domain-create](index.html#bluemix_network_domain_create)</td>
 <td>[bluemix network domain-delete](index.html#bluemix_network_domain_delete)</td>
 <td>[bluemix network shared-domain-create](index.html#bluemix_network_shared_domain_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix network shared-domain-delete](index.html#bluemix_network_shared_domain_delete)</td> 
 <td>[bluemix security cert](index.html#bluemix_security_cert)</td> 
 <td>[bluemix security cert-add](index.html#bluemix_security_cert_add)</td>
 <td>[bluemix security cert-remove](index.html#bluemix_security_cert_remove)</td>
 <td>[bluemix plugin repos](index.html#bluemix_plugin_repos)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin repo-add](index.html#bluemix_plugin_repo_add)</td> 
 <td>[bluemix plugin repo-remove](index.html#bluemix_plugin_repo_remove)</td> 
 <td>[bluemix plugin repo-plugins](index.html#bluemix_plugin_repo_plugins)</td>
 <td>[bluemix plugin list](index.html#bluemix_plugin_list)</td>
 <td>[bluemix plugin install](index.html#bluemix_plugin_install)</td>
 </tr>
 
 <tr> 
 <td>[bluemix plugin uninstall](index.html#bluemix_plugin_uninstall)</td> 
 <td>[bluemix ic init](index.html#bluemix_ic_init)</td> 
 <td>[bluemix ic attach](index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](index.html#bluemix_ic_build)</td>
 <td>[bluemix ic create](index.html#bluemix_ic_create)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic cpi](index.html#bluemix_ic_cpi)</td> 
 <td>[bluemix ic exec](index.html#bluemix_ic_exec)</td> 
 <td>[bluemix ic groups](index.html#bluemix_ic_groups)</td>
 <td>[bluemix ic group-inspect](index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](index.html#bluemix_ic_group_instances)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic group-create](index.html#bluemix_ic_group_create)</td> 
 <td>[bluemix ic group-update](index.html#bluemix_ic_group_update)</td> 
 <td>[bluemix ic group-remove](index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic images](index.html#bluemix_ic_images)</td>
 <td>[bluemix ic inspect](index.html#bluemix_ic_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic info](index.html#bluemix_ic_info)</td> 
 <td>[bluemix ic ips](index.html#bluemix_ic_ips)</td> 
 <td>[bluemix ic ip-request](index.html#ip_request)</td>
 <td>[bluemix ic ip-release](index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-bind](index.html#bluemix_ic_ip_bind)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic ip-unbind](index.html#bluemix_ic_ip_unbind)</td> 
 <td>[bluemix ic kill](index.html#bluemix_ic_kill)</td> 
 <td>[bluemix ic namespace-get](index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](index.html#pause)</td>
 </tr>
 
 <tr> 
 <td>[bluemix ic unpause](index.html#unpause)</td> 
 <td>[bluemix ic port](index.html#bluemix_ic_port)</td> 
 <td>[bluemix ic ps](index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic restart](index.html#bluemix_ic_restart)</td>
 <td>[bluemix ic rm](index.html#bluemix_ic_rm)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic rmi](index.html#bluemix_ic_rmi)</td> 
 <td>[bluemix ic run](index.html#bluemix_ic_run)</td> 
 <td>[bluemix ic route-map](index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic start](index.html#ic_start)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic stop](index.html#ic_stop)</td> 
 <td>[bluemix ic stats](index.html#bluemix_ic_stats)</td> 
 <td>[bluemix ic top](index.html#bluemix_ic_top)</td>
 <td>[bluemix ic volumes](index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic volume-inspect](index.html#bluemix_ic_volume_inspect)</td>
 </tr>
 
 
 <tr> 
 <td>[bluemix ic volume-create](index.html#bluemix_ic_volume_create)</td> 
 <td>[bluemix ic volume-remove](index.html#bluemix_ic_volume_remove)</td> 
 <td>[bluemix ic volume-fs](index.html#bluemix_ic_volume_fs)</td> 
 <td>[bluemix ic volume-fs-create](index.html#bluemix_ic_volume_fs_create)</td> 
 <td>[bluemix ic volume-fs-remove](index.html#bluemix_ic_volume_fs_remove)</td> 
 </tr>
 
 <tr>
 <td>[bluemix ic volume-fs-inspect](index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](index.html#bluemix_ic_volume_fs_flavors)</td> 
 <td>[bluemix ic wait](index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic version](index.html#bluemix_ic_version)</td>
 </tr>
 
 
 </tbody> 
 </table> 

  

## bluemix help
{: #bluemix_help}
{{site.data.keyword.Bluemix_notm}} CLI の第 1 レベルの組み込みコマンドおよびサポートされる名前空間に関する一般ヘルプを表示するか、または、特定の組み込みコマンドまたは名前空間に関するヘルプを表示します。

```
bluemix help [COMMAND|NAMESPACE]
```

**前提条件**: なし

**コマンド・オプション**:

*COMMAND*|*NAMESPACE* (オプション): ヘルプを表示する対象のコマンドまたは名前空間。指定されない場合、{{site.data.keyword.Bluemix_notm}} CLI の一般ヘルプが表示されます。

**例**:

{{site.data.keyword.Bluemix_notm}} CLI の一般ヘルプを表示します。

```
bluemix help
```

`info` コマンドのヘルプを表示します。

```
bluemix help info
```

`ic` 名前空間のヘルプを表示します。

```
bluemix help ic
```

または 

```
bluemix ic help
```

`ic` 名前空間の下の `group-create` コマンドのヘルプを表示します。

```
bluemix ic help group-create
```


## bluemix api
{: #bluemix_api}
{{site.data.keyword.Bluemix_notm}} API エンドポイントを設定または表示します。このコマンドは `cf api` コマンドをラップします。

```
bluemix api [API_ENDPOINT][--unset]
```

**前提条件**: なし

**コマンド・オプション**:

*API_ENDPOINT* (オプション): ターゲットの API エンドポイント (例えば https://api.ng.bluemix.net)。 *API_ENDPOINT* オプションと `--unset` オプションのどちらも指定されない場合、現行 API エンドポイントが表示されます。

`--unset` (オプション): API エンドポイント設定を削除します。

**例**:

API エンドポイントを api.ng.bluemix.net に設定します。

```
bluemix api api.ng.bluemix.net
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

ユーザーをログインします。このコマンドは `cf login` コマンドをラップします。コマンド・オプションは `cf login` コマンドのオプションと同じです。

```
bluemix login [OPTIONS...]
```

**前提条件**: エンドポイント

**コマンド・オプション**: `login` コマンドでサポートされるオプションについては、アプリケーション管理用 cf コマンドの `cf login` コマンド使用法の説明を参照してください。


## bluemix logout
{: #bluemix_logout}

ユーザーをログアウトします。このコマンドは `cf logout` コマンドをラップします。

```
bluemix logout
```

**前提条件**: なし


## bluemix target
{: #bluemix_target}


ターゲットの組織またはスペースを設定または表示します。このコマンドは `cf target` コマンドをラップします。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

-o *ORG_NAME* (オプション): ターゲットになる組織の名前。

-s *SPACE_NAME* (オプション): ターゲットになるスペースの名前。

-o *ORG_NAME* と -s *SPACE_NAME* のどちらも指定されない場合、現行の組織およびスペースが表示されます。

**例**:

現行の組織を `MyOrg` に、スペースを `MySpace` に設定します。

```
bluemix target -o MyOrg -s MySpace
```

現行の組織およびスペースを表示します。

```
bluemix target
```


## bluemix info
{: #bluemix_info}

基本的な {{site.data.keyword.Bluemix_notm}} 情報を表示します。これには、現行領域、クラウド・コントローラーのバージョン、および、いくつかの有用なエンドポイント (例えば、ログイン用のエンドポイントや、アクセス・トークン交換用のエンドポイントなど) が含まれます。

```
bluemix info
```

**前提条件**: エンドポイント


## bluemix config
{: #bluemix_config}


構成ファイルにデフォルト値を書き込みます。

```
bluemix config --http-timeout TIMEOUT_IN_SECONDS | --trace (true|false|path/to/file) | --color (true|false) | --locale (LOCALE|CLEAR)
```

**前提条件**: なし

**コマンド・オプション**:

--http-timeout *TIMEOUT_IN_SECONDS*:  HTTP 要求のタイムアウト値。デフォルト値は 60 秒です。

--trace true|false|*path/to/file*:  端末または指定されたファイルへの HTTP 要求をトレースします。

--color true|false:  カラー出力を使用可能または使用不可にします。カラー出力はデフォルトで使用可能に設定されています。

--locale *LOCALE*:  デフォルト・ロケールを設定します。LOCALE が *CLEAR* の場合は、前のロケールが削除されます。

一度に指定できるのは、これらのオプションの 1 つだけです。

**例**:

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


## bluemix list
{: #bluemix_list}

現行スペース内のすべての cf アプリケーション、コンテナー、コンテナー・グループ、および VM グループをリストします。

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

apps (オプション): アプリケーション情報のみを表示します。

containers (オプション): コンテナー情報のみを表示します。

container-groups (オプション): コンテナー・グループ情報のみを表示します。

vm-groups (オプション): VM グループ情報のみを表示します。

一度に指定できるのは、apps、containers、container-groups、または vm-groups のいずれか 1 つのみです。これらのどれも指定されない場合、すべての cf アプリケーション、コンテナー、コンテナー・グループ、および VM グループがリストされます。

**例**:

すべての cf アプリケーションをリストします。

```
bluemix list apps
```

すべてのコンテナー・インスタンスをリストします。

```
bluemix list containers
```

すべてのアプリケーション、コンテナー、コンテナー・グループ、および VM グループをリストします。

```
bluemix list
```


## bluemix scale
{: #bluemix_scale}

cf アプリケーションまたはコンテナー・グループを、指定されたインスタンス数、ディスク割り当て量、およびメモリー・サイズになるよう拡大または縮小します。

**注:** コンテナー・グループのスケーリングに指定できるのはインスタンス数のみです。オプションが何も指定されない場合、このコマンドは、コンテナー・グループの現行インスタンス数をリストし、cf アプリケーションではディスク割り当て量とメモリー・サイズもリストします。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT][-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (必須):  スケーリングする cf アプリケーションまたはコンテナー・グループの名前。

-i *INSTANCE_COUNT*  (オプション): スケーリングする cf アプリケーションまたはコンテナー・グループの新しいインスタンス数。コンテナー・グループのスケーリングの場合は、このオプションは唯一の有効なオプションです。

-k *DISK_QUOTA* (オプション): cf アプリケーションの新しいディスク割り当て量。コンテナー・グループのスケーリングの場合は無効です。

-m *MEMORY_SIZE* (オプション): cf アプリケーションの新しいメモリー・サイズ。コンテナー・グループのスケーリングの場合は無効です。

**例**:

`my-container-group` の現行インスタンス数を表示します。

```
bluemix scale my-container-group
```

`my-container-group` を 2 インスタンスにスケーリングします。

```
bluemix scale my-container-group -i 2
```

`my-java-app` を、3 インスタンス、8G ディスク割り当て量、および 1024M メモリー・サイズにスケーリングします。

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{: #bluemix_curl}

{{site.data.keyword.Bluemix_notm}} への未加工 HTTP 要求を実行します。*Content-Type* はデフォルトで *application/json* に設定されます。このコマンドは、要求を {{site.data.keyword.Bluemix_notm}} マルチクラウド制御プロキシーに送信します。サポートされるパスについては、[CloudFoundry API 資料](http://apidocs.cloudfoundry.org/){: new_window}内の API パス定義を参照してください。

```
bluemix curl PATH [OPTIONS...]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*PATH* (必須): リソースの URL パス。例えば、/v2/apps です。

*OPTIONS* (オプション): `bluemix curl` コマンドでサポートされるオプションは、`cf curl` コマンドのオプションと同じです。

**例**:

現行アカウントのすべての組織に関する情報を表示するには、次のように指定します。

```
bluemix curl /v2/organizations
```


## bluemix iam orgs
{: #bluemix_iam_orgs}

すべての組織をリストします。

```
bluemix iam orgs [-r REGION --guid]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*-r REGION* (オプション): どの地域の組織情報を表示するかを指定します。'all' に設定された場合は、すべての地域のすべての組織がリストされます。

*--guid* (オプション): 組織の GUID を表示します。

**例**:
地域 `us-south` 内のすべての組織を、GUID の出力と共にリストします

```
bluemix iam orgs -r us-south --guid
```

## bluemix iam org
{: #bluemix_iam_org}

指定された組織の情報を表示します。

```
bluemix iam org ORG_NAME [--guid]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須): 組織の名前。

*--guid* (オプション): 組織の GUID を表示します。


**例**: 組織 `IBM` の情報を、GUID の出力と共に表示します

```
bluemix iam org IBM --guid
```

## bluemix iam org-create
{: #bluemix_iam_org_create}

新しい組織を作成します。この操作は、アカウントの所有者のみが実行できます。  

```
bluemix iam org-create ORG_NAME
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須): 作成する組織の名前。

**例**:
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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須):  複製する既存の組織の名前。

*REGION_NAME*  (必須):  複製された組織をホストする地域の名前。

**例**:

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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*OLD_ORG_NAME* (必須): 名前を変更する組織の古い名前。

*NEW_ORG_NAME* (必須): 名前を変更する組織の新しい名前。


## bluemix iam org-delete
{: #bluemix_iam_org_delete}

現行地域内の指定された組織を削除します。

```
bluemix iam org-delete ORG_NAME [-f --all]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須):  削除する既存の組織の名前。

*-f*  (オプション):  確認なしで削除を強制します。

*--all* (オプション): その組織をすべての地域から削除します。


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


## bluemix iam account-users

{: #bluemix_iam_account_users}

アカウントに関連付けられているユーザーを表示します。この操作は、アカウントの所有者のみが実行できます。

```
bluemix iam account-users
```

## bluemix iam account-user-invite
{: #bluemix_iam_account-user_inviate}


組織とスペースの役割が既に設定されているアカウントにユーザーを招待します。この操作は、アカウントの所有者のみが実行できます。

```
bluemix iam account-user-invite USER_NAME ORG_NAME ORG_ROLE SPACE_NAME SPACE_ROLE
```

**前提条件**: エンドポイント、ログイン


**コマンド・オプション**:

*USER_NAME* (必須): 招待されるユーザーの名前。

*ORG_NAME* (必須): このユーザーの招待先の組織の名前。

*ORG_ROLE* (必須): このユーザーの招待先の組織内での役割の名前。例えば次のようにします。

<dl>
<dt>OrgManager</dt>
<dd>この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</dd>
<dt>BillingManager</dt>
<dd>この役割は、請求アカウントと支払い情報の作成および管理を行えます。</dd>
<dt>OrgAuditor</dt>
<dd>この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</dd>
</dl> 

*SPACE_NAME* (必須): このユーザーの招待先のスペースの名前。

*SPACE_ROLE* (必須): このユーザーの招待先のスペース内での役割の名前。例えば次のようにします。

<dl>
<dt>SpaceManager</dt>
<dd>この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</dd>
<dt>SpaceDeveloper</dt>
<dd>この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</dd>
<dt>SpaceAuditor</dt>
<dd>この役割は、ログ、レポート、スペースの設定を表示できます。</dd>
</dl> 

**例**:

ユーザー `Mary` を組織 `IBM` に役割 `OrgManager` として招待し、スペース `Cloud` に役割 `SpaceAuditor` として招待するには、次のように指定します。

```
bluemix iam account-user-inviate Mary IBM OrgManager Cloud SpaceAuditor
```

## bluemix iam org-users
{: #bluemix_iam_org_users}

指定された組織内のユーザーを役割別に表示します

```
bluemix iam org-users ORG_NAME [-a]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須): 組織の名前。

*-a* (オプション): 指定された組織内のすべてのユーザーを、役割別にグループ化せずにリストします。


## bluemix iam org-role-set
{: #bluemix_iam_org_role_set}

組織の役割をユーザーに割り当てます。この操作は、組織の管理者のみが実行できます。  

```
bluemix iam org-role-set USER_NAME ORG_NAME ORG_ROLE
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*USER_NAME* (必須): 割り当てられるユーザーの名前。

*ORG_NAME* (必須): このユーザーの割り当て先の組織の名前。

*ORG_ROLE* (必須): このユーザーの割り当て先の組織内での役割の名前。例えば次のようにします。

<dl>
<dt>OrgManager</dt>
<dd>この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</dd>
<dt>BillingManager</dt>
<dd>この役割は、請求アカウントと支払い情報の作成および管理を行えます。</dd>
<dt>OrgAuditor</dt>
<dd>この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</dd>
</dl> 

**例**:

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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*USER_NAME* (必須): 削除されるユーザーの名前。

*ORG_NAME* (必須): このユーザーの削除元の組織の名前。

*ORG_ROLE* (必須): このユーザーの削除元の組織内での役割の名前。例えば次のようにします。

<dl>
<dt>OrgManager</dt>
<dd>この役割は、ユーザーの招待と管理、プランの選択と変更、支払上限の設定を行います。</dd>
<dt>BillingManager</dt>
<dd>この役割は、請求アカウントと支払い情報の作成および管理を行えます。</dd>
<dt>OrgAuditor</dt>
<dd>この役割は、組織の情報とレポートに読み取りアクセスだけが可能です。</dd>
</dl> 

**例**:

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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須): 組織の名前

*SPACE_NAME* (required): スペースの名前。


## bluemix iam space-role-set
{: #bluemix_iam_space_role_set}

スペースの役割をユーザーに割り当てます。この操作は、スペースの管理者のみが実行できます。  

```
bluemix iam space-role-set USER_NAME ORG_NAME SPACE_NAME SPACE_ROLE
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*USER_NAME* (必須): 割り当てられるユーザーの名前。

*ORG_NAME* (必須): このユーザーの割り当て先の組織の名前。

*SPACE_NAME* (必須): このユーザーの割り当て先のスペースの名前。

*SPACE_ROLE* (必須): このユーザーの割り当て先のスペース内での役割の名前。例えば次のようにします。

<dl>
<dt>SpaceManager</dt>
<dd>この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</dd>
<dt>SpaceDeveloper</dt>
<dd>この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</dd>
<dt>SpaceAuditor</dt>
<dd>この役割は、ログ、レポート、スペースの設定を表示できます。</dd>
</dl> 


**例**:

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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*USER_NAME* (必須): 削除されるユーザーの名前。

*ORG_NAME* (必須): このユーザーの削除元の組織の名前。

*SPACE_NAME* (必須): このユーザーの削除元のスペースの名前。

*SPACE_ROLE* (必須): このユーザーの削除元のスペース内での役割の名前。例えば次のようにします。

<dl>
<dt>SpaceManager</dt>
<dd>この役割は、ユーザーの招待と管理を行い、特定のスペースに対してフィーチャーを有効にします。</dd>
<dt>SpaceDeveloper</dt>
<dd>この役割は、アプリとサービスを作成して管理し、ログとレポートを表示します。</dd>
<dt>SpaceAuditor</dt>
<dd>この役割は、ログ、レポート、スペースの設定を表示できます。</dd>
</dl> 

**例**:

ユーザー `Mary` を組織 `IBM` と、役割 `SpaceManager` としてのスペース `Cloud` から削除するには、次のように指定します。

```
bluemix iam space-role-unset Mary IBM Cloud SpaceManager
```


## bluemix app push
{: #bluemix_app_push}

このコマンドの機能とオプションは `cf push` コマンドと同じです。


## bluemix app list
{: #bluemix_app_list}

このコマンドの機能とオプションは `cf apps` コマンドと同じです。


## bluemix app show
{: #bluemix_app_show}

このコマンドの機能とオプションは `cf app` コマンドと同じです。


## bluemix app scale
{: #bluemix_app_scale}

このコマンドの機能とオプションは `cf scale` コマンドと同じです。


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


## bluemix app stack
{: #bluemix_app_stack}

このコマンドの機能とオプションは `cf stack` コマンドと同じです。


## bluemix app manifest-create
{: #bluemix_app_manifest_create}

このコマンドの機能とオプションは `cf create-app-manifest` コマンドと同じです。


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

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

-d (オプション): `-d` オプションが指定されている場合、各テンプレートの説明も表示されます。それ以外の場合、各テンプレートの ID および名前のみが表示されます。


## bluemix catalog template
{: #bluemix_catalog_template}

指定されたボイラープレート・テンプレートの詳細情報を表示します。

```
bluemix catalog template TEMPLATE_ID
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*TEMPLATE_ID* (必須): ボイラープレート・テンプレートの ID。すべてのテンプレートの ID を表示するには、「bluemix templates」を使用します。

**例**:

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

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*TEMPLATE_ID* (必須): アプリケーション作成のベースになるテンプレート。すべてのテンプレートの ID を表示するには、`bluemix templates` を使用します。

*CF_APP_NAME* (必須): 作成する cf アプリケーションの名前。

-u *URL* (オプション): アプリケーションの経路。指定されない場合、経路は、アプリケーション名およびデフォルト・ドメインに基づいて {{site.data.keyword.Bluemix_notm}} によって自動的に設定されます。

-d *DESCRIPTION* (オプション): アプリケーションの説明。

--no-start (オプション): 作成後のアプリケーションを自動的に開始しません。指定されない場合、アプリケーションは作成された後で自動的に開始されます。

**例**:

`javaHelloWorld` テンプレートをベースにして cf アプリケーション `my-app` を作成します。

```
bluemix catalog template-run javaHelloWorld my-app
```

`rubyHelloWorld` テンプレートに基づき、経路 `myrubyapp.ng.bluemix.net` と説明 `My first ruby app on {{site.data.keyword.Bluemix_notm}}.` を使用してアプリケーション `my-ruby-app` を作成するには、以下のように指定します。

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

`pythonHelloWorld` テンプレートをベースにして、自動開始なしでアプリケーション `my-python-app` を作成します。

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{: #bluemix_network_regions}

{{site.data.keyword.Bluemix_notm}} のすべての地域の情報を表示します。

```
bluemix network regions
```

**前提条件**: エンドポイント


## bluemix network region-set
{: #bluemix_network_region_set}

指定された地域に切り替えます。このコマンドは、可能な場合、新しい地域の同じ組織およびスペースに自動的にターゲットを変更します。さもなければ、コマンドは、ユーザーが既にログインしている場合、新しい組織とスペースを選択するようユーザーにプロンプトを出します。API エンドポイントはそれに合わせて変更されます。

```
bluemix network region-set REGION_NAME
```

**前提条件**: エンドポイント

**コマンド・オプション**:

*REGION_NAME* (required):  (必須): 切り替える先の地域の名前。`bluemix network regions` コマンドを使用すると、すべての地域名を表示することができます。

**例**:

現行地域を `eu-gb` に設定します。

```
bluemix network region-set eu-gb
```


## bluemix network routes
{: #bluemix_network_routes}

このコマンドの機能とオプションは `cf routes` コマンドと同じです。


## bluemix network route-check
{: #bluemix_network_route_check}

このコマンドの機能とオプションは `cf check-route` コマンドと同じです。


## bluemix network route-map
{: #bluemix_network_route_map}

指定されたドメインおよびホスト名を持つ経路を既存 cf アプリケーションまたはコンテナー・グループにマップします。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (必須): 経路でマップされる cf アプリケーションまたはコンテナー・グループの名前。

*DOMAIN* (必須): 経路のドメイン。例えば、mybluemix.net または ng.bluemix.net などです。 

-n *HOST_NAME* (オプション): 経路のホスト名。指定されない場合、ホスト名は、デフォルトで、アプリケーション名またはコンテナー・グループ名に設定されます。

**例**:

指定されたドメインで `my-app` に経路をマップします。

```
bluemix network route-map my-app mybluemix.net
```

指定されたドメインとホスト名で「my-container-group」に経路をマップします。

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
{: #bluemix_network_route_unmap}

指定された経路を既存 cf アプリケーションまたはコンテナー・グループからマップ解除します。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (必須): cf アプリケーションまたはコンテナー・グループの名前。

*DOMAIN* (必須): 経路のドメイン (例えば、mybluemix.net または ng.bluemix.net などです)。 

-n *HOST_NAME* (オプション): 経路のホスト名。指定されない場合、ホスト名は、デフォルトで、アプリケーション名またはコンテナー・グループ名に設定されます。

**例**:

`my-app.mybluemix.net` を `my-app` からマップ解除するには、以下のように指定します。

```
bluemix network route-unmap my-app mybluemix.net
```

`abc.ng.bluexmix.net` を `my-container-group` からマップ解除するには、以下のように指定します。

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
{: #bluemix_network_route_create}

このコマンドの機能とオプションは `cf create-route` コマンドと同じです。


## bluemix network route-delete
{: #bluemix_network_route_delete}

このコマンドの機能とオプションは `cf delete-route` コマンドと同じです。


## bluemix network orphaned-routes-delete
{: #bluemix_network_orphaned_routes_delete}

このコマンドの機能とオプションは `cf delete-orphaned-routes` コマンドと同じです。


## bluemix network domains
{: #bluemix_network_domains}

このコマンドの機能とオプションは `cf domains` コマンドと同じです。


## bluemix network domain-create
{: #bluemix_network_domain_create}

このコマンドの機能とオプションは `cf create-domain` コマンドと同じです。


## bluemix network domain-delete
{: #bluemix_network_domain_delete}

このコマンドの機能とオプションは `cf delete-domain` コマンドと同じです。


## bluemix network shared-domain-create
{: #bluemix_network_shared_domain_create}

このコマンドの機能とオプションは `cf create-shared-domain` コマンドと同じです。


## bluemix network shared-domain-delete
{: #bluemix_network_shared_domain_delete}

このコマンドの機能とオプションは `cf delete-shared-domain` コマンドと同じです。


## bluemix security cert
{: #bluemix_security_cert}

ドメインの証明書情報をリストします。

```
bluemix security cert DOMAIN_NAME
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*DOMAIN_NAME* (必須): 証明書をホストするドメイン。

**例**:

ドメイン `ibmcxo-eventconnect.com` の証明書情報を表示するには、次のように指定します。

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add
{: #bluemix_security_cert_add}

現在の組織内の、指定したドメインに証明書を追加します。

```
bluemix security cert-add DOMAIN -k PRIVATE_KEY_FILE -c CERT_FILE [-p PASSWORD][-i INTERMEDIATE_CERT_FILE] [--verify-client]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*DOMAIN* (必須):  証明書を追加するドメイン。

-k *PRIVATE_KEY_FILE* (必須):  秘密鍵ファイルのパス。

-c *CERT_FILE* (必須):  証明書ファイルのパス。

-p *PASSWORD* (オプション):  証明書のパスワード。

-i *INTERMEDIATE_CERT_FILE* (オプション):  中間証明書ファイルのパス。

--verify-client (オプション):  クライアント証明書の検証を使用可能にするかどうか。

**例**:

ドメイン `ibmcxo-eventconnect.com` に証明書を追加するには、以下のように指定します。

```
bluemix security cert-add ibmcxo-eventconnect.com -k key_file.key -c cert_file.crt -p 123 -i inter_cert.cert
```


## bluemix security cert-remove
{: #bluemix_security_cert_remove}

現在の組織内の、指定したドメインから証明書を削除します。

```
bluemix security cert-remove DOMAIN [-f]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*DOMAIN* (必須):  証明書を削除するドメイン。

-f  (オプション):  確認なしで削除を強制します。







## bluemix plugin repos
{: #bluemix_plugin_repos}

{{site.data.keyword.Bluemix_notm}} CLI に登録されているすべてのプラグイン・リポジトリーをリストします。

```
bluemix plugin repos
```

**前提条件**: なし


## bluemix plugin repo-add
{: #bluemix_plugin_repo_add}

新規プラグイン・リポジトリーを {{site.data.keyword.Bluemix_notm}} CLI に追加します。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**前提条件**: なし

**コマンド・オプション**:

*REPO_NAME* (必須): 追加するリポジトリーの名前。各リポジトリーに対して任意の名前を定義できます。

*REPO_URL* (必須): 追加するリポジトリーの URL。リポジトリー URL にはプロトコルが含まれている必要があります (例えば、plugins.ng.bluemix.net ではなく、http://plugins.ng.bluemix.net)。{{site.data.keyword.Bluemix_notm}} CLI の公式プラグイン・リポジトリーは http://plugins.ng.bluemix.net です。

**例**:

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

**前提条件**: なし

**コマンド・オプション**:

*REPO_NAME* (必須): 削除するリポジトリーの名前。

**例**:

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

**前提条件**: なし

**コマンド・オプション**:

-r *REPO_NAME* (オプション): 指定されたリポジトリー内のプラグインのみをリストします。

**例**:

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

**前提条件**: なし


## bluemix plugin install
{: #bluemix_plugin_install}

指定したパスまたはリポジトリーから、特定のバージョンのプラグインを {{site.data.keyword.Bluemix_notm}} CLI にインストールします。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME][-v VERSION]
```

**前提条件**: なし

**コマンド・オプション**:

*PLUGIN_PATH*|*PLUGIN_NAME* (必須): `-r *REPO_NAME*` が指定されない場合、指定されたローカル・パスまたはリモート URL からプラグインがインストールされます。

-r *REPO_NAME* (オプション): プラグイン・バイナリーが置かれているリポジトリーの名前。-v *VERSION*  (オプション):  インストールするプラグインのバージョン。指定されていない場合は、最新バージョンのプラグインがインストールされます。このオプションは、リポジトリーからプラグインをインストールする場合にのみ有効です。

**例**:

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






## bluemix plugin uninstall
{: #bluemix_plugin_uninstall}

指定されたプラグインを {{site.data.keyword.Bluemix_notm}} CLI からアンインストールします。

```
bluemix plugin uninstall PLUGIN_NAME
```

**前提条件**: なし

**コマンド・オプション**:

*PLUGIN_NAME* (必須): アンインストールするプラグインの名前。

**例**:

前にインストールされた `IBM-Containers` プラグインをアンインストールします。

```
bluemix plugin uninstall IBM-Containers
```


## bluemix ic init
{: #bluemix_ic_init}

IBM Containers サービスの全機能を使用できるようにローカル・マシン上のコンテナー環境を初期化します。

```
bluemix ic init
```

**前提条件**: エンドポイント、ログイン、ターゲット

**注:** 初期化を行う前に、Docker CLI (docker) がインストールされ、PATH 環境変数内に構成されていることを確認してください。別の地域に切り替えるには、`bluemix region-set` コマンドを使用します。 

**例**:

`us-south` 地域に切り替えます。

```
bluemix region-set us-south
```


## bluemix ic attach
{: #bluemix_ic_attach}

実行中のコンテナーを制御するか、その出力を表示します。終了してコンテナーを停止するには `CTRL+C` を使用します。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [attach](https://docs.docker.com/reference/commandline/attach/){: new_window} コマンドを参照してください。 

```
bluemix ic attach [--no-stdin][--sig-proxy] CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

--no-stdin (オプション): 標準入力を含めません。

--sig-proxy (オプション): 受信したすべてのシグナルをプロセスに伝達します。デフォルトは **true** です。

*CONTAINER* (必須): コンテナーの名前または ID。

**例**:

次の例は、コンテナー `my_container` にアタッチする要求です。
```
bluemix ic attach my_container
```


## bluemix ic build
{: #bluemix_ic_build}

IBM Containers ビルド・サービスを呼び出して、Docker イメージをローカルにビルドするか、またはプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドします。このコマンドは Docker CLI を呼び出します。詳細については、Docker ヘルプで [build](https://docs.docker.com/reference/commandline/build/){: new_window} コマンドを参照してください。 

```
bluemix ic build -t TAG|--tag TAG [--no-cache][-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-t *TAG*|--tag *TAG* (必須): 作成されたイメージに適用するリポジトリー名。

--no-cache (オプション): イメージをビルドするときにキャッシュを使用しません。デフォルトは **false** です。

-p|--pull (オプション): レジストリーからベース・イメージを (それがキャッシュされている場合でも) プルしようとします。

-q|--quiet (オプション): コンテナーが生成する詳細出力を抑止します。デフォルトは **false** です。

*DOCKERFILE_LOCATION* (必須): ローカル・ホスト上の Dockerfile およびコンテキストへのパス。

**例**:

次の例は、*myimage* という名前のイメージをビルドする要求です。ビルドで使用される Dockerfile および他の成果物は、コマンドが実行されるディレクトリーと同じディレクトリー内にあります。レジストリーおよび名前空間がイメージ名と共に含まれているため、イメージは組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内にビルドされます。
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage
```


## bluemix ic create
{: #bluemix_ic_create}

{{site.data.keyword.Bluemix_notm}} リポジトリー内に新規コンテナーを作成します。このコマンドは `docker create` コマンドをラップします。詳細については、Docker ヘルプで [create](https://docs.docker.com/reference/commandline/create/){: new_window} コマンドを参照してください。


## bluemix ic cpi
{: #bluemix_ic_cpi}

Docker Hub イメージ、またはローカル・レジストリーからのイメージにアクセスし、そのイメージをプライベート {{site.data.keyword.Bluemix_notm}} リポジトリーにコピーします。

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*SOURCE_IMAGE* (必須): ソース・リポジトリーおよびソース・イメージ名。

*DESTINATION_IMAGE* (必須): プライベート {{site.data.keyword.Bluemix_notm}} リポジトリー URL (名前空間を含む) および宛先イメージ名。イメージのタグはオプションです。

**例**:

ソース・リポジトリーからプライベート・リポジトリーにイメージをコピーし、そのイメージのタグを追加します。

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

`sinatra` イメージを `training` リポジトリーからプライベート・リポジトリー `registry.ng.bluemix.net/mynamespace` にコピーし、そのイメージの名前を `mysinatra` にします。イメージ `mysinatra` 用にタグ `v1` を追加します。 

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}


コンテナー内でコマンドを実行します。詳細については、Docker ヘルプで [exec](https://docs.docker.com/reference/commandline/exec/){: new_window} コマンドを参照してください。

```
bluemix ic exec [-d|--detach][-it] [-u USER|--user USER] CONTAINER [CMD]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-d|--detach (オプション): 指定されたコマンドをバックグラウンドで実行します。

-it (オプション): 対話モード。標準入力が表示されている状態を維持します。終了するには「exit」と入力します。

-u *USER*|--user *USER* (オプション): ユーザー名。

*CONTAINER* (必須): コンテナーの名前または ID。

*CMD* (オプション): 指定されたコンテナー内で実行するコマンド。

**例**:

`bash` コマンドを `my_container` コンテナー内で対話モードで実行します。

```
bluemix ic exec -it my_container bash
```

`date` コマンドを `my_container` コンテナー内で実行します。

```
bluemix ic exec my_container date
```


## bluemix ic groups
{: #bluemix_ic_groups}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のコンテナー・グループをリストします。

```
bluemix ic groups
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

コンテナー・グループの作成時に指定された詳細情報 (環境変数、ポート、メモリーなど) を表示します。

```
bluemix ic group-inspect CONTAINER_GROUP
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

次の例は、コンテナー・グループ `my_group` を検査する要求を示しています。
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

指定されたコンテナー・グループのインスタンスをリストします。

```
bluemix ic group-instances CONTAINER_GROUP
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

コンテナー・グループ `my_group` のすべてのインスタンスをリストします。
```
bluemix ic group-instances my_group
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

スケーラブル・コンテナー・グループを作成します。

```
bluemix ic group-create [-p PORT|--publish port][-m MEMORY|--memory MEMORY] [-e ENV|--env ENV][-v VOLUME:CONTAINER_PATH] [--min MIN][--max MAX] [--desired DESIRED][--auto] [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] [--name NAME] IMAGE [CMD]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

-m *MEMORY*|--memory *MEMORY* (オプション): グループにメモリー限度 (MB) を割り当てます。CLI からコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は `64` MB です。{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は `256` MB です。受け入れられる値は、`64`、`256`、`512`、`1024`、および `2048` です。メモリー限度が割り当てられた後、その値を変更することはできません。

-e *ENV*|--env *ENV* (オプション): 環境変数を設定します。**ENV** は、「キー = 値」のペアです。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。例えば、`-e "key1=value1" -e "key2=value2" -e "key3=value3"` のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。

|  環境変数                              |     説明                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。ブリッジ・アプリの作成について詳しくは、[コンテナーへのサービスのバインド](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}を参照してください。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | コンテナー作成時に SSH 鍵をコンテナーに追加します。{{site.data.keyword.Bluemix_notm}} ダッシュボードまたは CLI からコンテナーを作成するときに、この環境変数を使用して SSH 鍵を追加できます。SSH 鍵について詳しくは、[コンテナーへのログイン](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}を参照してください。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
*表 1. 一般的に使用される環境変数*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro](optional):  詳細を `VolumeId:ContainerPath[:ro]` 形式で指定して、ボリュームをコンテナーにアタッチします。

- *VOLUME*: ボリュームの ID または名前。
- *CONTAINER_PATH*: コンテナー内でのボリュームへの絶対パス。
- ro (オプション):`ro` を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく、読み取り専用になります。

-p *PORT*|--publish *PORT* (オプション): HTTP トラフィック用のポートを公開します。グループ内のコンテナーは、この HTTP ポートを listen する必要があります。HTTPS 要求を行うことはできません。コンテナー・グループに対して複数のポートを含めることはできません。

ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。これにより、{{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーは、そのポートを使用して、同じ {{site.data.keyword.Bluemix_notm}} スペース内のホストおよびアプリにアクセスできるようになります。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。

**ヒント:**

- IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。
- IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。

--min *MIN* (オプション): インスタンスの最小数。デフォルトは **1** です。
インスタンスの最小数を設定した場合、その値をコンテナー・グループ作成後に変更することはできません。

--max *MAX* (オプション): インスタンスの最大数。デフォルトは **2** です。インスタンスの最大数を設定した場合、その値をコンテナー・グループ作成後に変更することはできません。

--desired *DESIRED* (オプション): 必要なインスタンス数。デフォルトは **2** です。

--auto (オプション): コンテナー・グループが作成され、自動リカバリーが有効にされている場合、IBM Containers は、割り当てられたポートへの HTTP 要求を使用して各インスタンスの正常性を検査します。

その後 2 回の 90 秒間隔のうちにコンテナー・インスタンスから応答を受け取らなければ、そのインスタンスは削除され、新しいインスタンスに置き換えられます。コンテナーが応答すればアクションは行われません。このプロセスは連続して繰り返されます。30 分の時間枠の間に、グループ・メンバーとなった異なるコンテナーの総数が、最大グループ・サイズの 3 倍以上になった場合、そのコンテナー・グループに対する自動リカバリーは永続的に無効になります。自動リカバリーを再度有効にするには、コンテナー・グループを再作成する必要があります。

-n *HOST*|--hostname *HOST* (オプション): ホスト名。例えば、`mycontainerhost` です。ホストとドメインが結合して、完全なパブリック経路 URL (例えば `http://mycontainerhost.mybluemix.net`) を形成します。`bluemix ic group-inspect` コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。

-d *DOMAIN*|--domain *DOMAIN* (オプション): 通常、ドメインは `.mybluemix.net` です。ホストとドメインが結合して、完全なパブリック経路 URL (例えば `http://mycontainerhost.mybluemix.net`) を形成します。`bluemix ic group-inspect` コマンドを使用してコンテナーの詳細をレビューすると、ホストとドメインが経路として一緒にリストされます。

--name *NAME* (必須): グループに名前を付けます。`-n` は推奨されません。

**ヒント:** コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (`.`)、下線 (`_`)、およびハイフン (`-`) を使用できます。

*IMAGE* (必須): コンテナー・グループ内の各コンテナー・インスタンスに含まれるイメージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合、形式 `registry.ng.bluemix.net/NAMESPACE/IMAGE` でイメージを指定します。

IBM Containers によって提供されるイメージを使用する場合、組織の名前空間を含めないでください。形式 `registry.ng.bluemix.net/IMAGE` でイメージを指定してください。

*CMD* (オプション): コンテナー・グループに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、**/bin/date** など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。

**注:**
- コマンドおよびその引数は、`bluemix ic run` コマンド・ラインの末尾に指定する必要があります。
- コマンド引数にハイフン (`-`) が含まれる場合 (前のコマンド例の `-c` のような場合)、コマンドの前に 2 個のハイフン (`--`) を置く必要があります。



**例**:

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `ping localhost` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

IBM Containers によって提供される `registry.ng.bluemix.net/ibmnode` イメージを使用してコンテナー・グループ `my_container_group` を作成し、そのコンテナー・グループで長時間実行コマンド `tail -f /dev/null` を実行します。

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

`registry.ng.bluemix.net/ibmliberty` イメージを使用して、スケーラブル・グループ `mygroup` を自動リカバリーを有効にして作成します。ポートは `9080`、ホスト名は `mycontainerhost`、ドメイン名は `.mybluemix.net` です。
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d .mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty 
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

コンテナー・グループを更新します。


```
bluemix ic group-update [--min MIN][--max MAX] [--desired DESIRED][--auto] CONTAINER_GROUP
```

**ヒント:** コンテナー・グループのホスト名またはドメインを更新するには、`bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP` を使用します。

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

--min *MIN* (オプション): インスタンスの最小数。デフォルトは **1** です。
インスタンスの最小数を設定した後は、その値を変更することはできません。

--max *MAX* (オプション): インスタンスの最大数。デフォルトは **2** です。
インスタンスの最大数を設定した後は、その値を変更することはできません。

--desired *DESIRED* (オプション): 必要なインスタンス数。デフォルトは **2** です。

**ヒント:** 一度に指定できるのは、`--min MIN`、`--max MAX`、または `--desired DESIRED` のいずれか 1 つのオプションのみです。

--auto (オプション): 自動リカバリーを有効にすることによって、障害が起こったインスタンスを自動的に再始動します。

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

次の例は、コンテナー・グループ `my_group` を更新する要求です。
```
bluemix ic group-update --max 5 my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリーからコンテナー・グループを削除します。

```
bluemix ic group-remove [-f|--force] CONTAINER_GROUP
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

-f|--force (オプション): 実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除します。

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

次の例は、コンテナー・グループを削除する要求です。ここで、`my_group` はコンテナー・グループの名前です。
```
bluemix ic group-remove my_group
```


## bluemix ic images
{: #bluemix_ic_images}

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内の使用可能なすべてのイメージのリストを表示します。詳細については、Docker ヘルプで [images](https://docs.docker.com/reference/commandline/images){: new_window} コマンドを参照してください。リストには、イメージ ID、作成日、およびイメージ名が含まれます。

```
bluemix ic images [-a|--all][--no-trunc] [-q|--quiet]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-a|--all (オプション): 組織のリポジトリー内の各イメージについて、最新のイメージ層のみではなく、すべてのイメージ層を含めます。

--no-trunc (オプション): 出力を切り捨てません。

-q|--quiet (オプション): 数字の ID のみを表示します。

**例**:

次の例は、組織の使用可能なイメージのリストを受け取る要求です。
```
bluemix ic images```


## bluemix ic inspect
{: #bluemix_ic_inspect}

コンテナーに関する情報を表示します。詳細については、Docker ヘルプで [inspect](https://docs.docker.com/reference/commandline/inspect){: new_window} コマンドを参照してください。

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*IMAGE* (必須): イメージの名前または ID を指定することによって、特定のイメージについての詳細情報を表示します。

images (必須): リポジトリー内のすべてのイメージについての詳細情報を表示します。

*CONTAINER* (必須): コンテナーの名前または ID を指定することによって、特定のコンテナーについての詳細情報を表示します。

**ヒント:** 一度に指定できるのは、*IMAGE*、images、または *CONTAINER* のいずれか 1 つのみです。 

**例**:

次の例は、`proxy` という名前のコンテナーを検査する要求です。
```
bluemix ic inspect proxy
```


## bluemix ic info
{: #bluemix_ic_info}

コンテナー・クラウド・サービス・インスタンスの状態を説明する情報を表示します。この情報に含まれるのは、コンテナーの限度、コンテナーの使用状況、実行中のコンテナー、メモリーの限度、メモリーの使用状況、浮動 IP アドレスの限度、浮動 IP アドレスの使用状況、CCS ホスト URL、レジストリー・ホスト URL、およびデバッグ・モード状況です。

```
bluemix ic info
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix ic ips
{: #bluemix_ic_ips}

ログインしているユーザーが使用可能な浮動 IP アドレスをリストします。このリストには、IP アドレスと、IP アドレスがリンクされている先のコンテナー ID が含まれます。IP アドレスが未使用の場合、コンテナー ID は示されません。

```
bluemix ic ips [-a|--all]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

-a|--all (オプション): すべての IP アドレスをリストします。デフォルトでは、使用可能な IP アドレスのみが戻されます。


**例**:

次の例は、使用可能かどうかに関係なく、組織のすべての IP アドレスのリストを受け取る要求です。
```
bluemix ic ips -a
```


## bluemix ic ip-request
{: #ip_request}
新しい浮動 IP アドレスを要求します。

```
bluemix ic ip-request
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

コンテナー・クラウド・サービス・インスタンスから浮動 IP アドレスを解放します。

```
bluemix ic ip-release IP_ADDRESS
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*IP_ADDRESS* (必須): 解放する IP アドレス。


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

使用可能な浮動 IP アドレスをコンテナーにバインドします。

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*IP_ADDRESS* (必須): バインドする IP アドレス。

*CONTAINER* (必須): バインドするコンテナーの ID または名前。

**例**:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` にバインドする要求です。
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

浮動 IP アドレスをそのコンテナーからアンバインドします。

パブリック IP アドレスは、IBM Containers の制限付きリソースです。したがって、スペースに割り当てられていてコンテナーにバインドされていないパブリック IP アドレスは、およそ週 1 回の頻度で無料試用ユーザーから定期的に再要求されます。アンバインドされたパブリック IP アドレスは、従量制課金カスタマーまたはサブスクリプション・カスタマーから再要求されることはありません。

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*IP_ADDRESS* (必須): アンバインドする IP アドレス。

*CONTAINER* (必須): アンバインドするコンテナーの ID または名前。

**例**:

次の例は、IP アドレス `192.123.12.12` をコンテナー `proxy` からアンバインドする要求です。
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic kill
{: #bluemix_ic_kill}

コンテナーを停止せずにコンテナー内の実行中のプロセスを停止します。詳細については、Docker ヘルプで [kill](https://docs.docker.com/reference/commandline/kill/){: new_window} コマンドを参照してください。

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-s *CMD*|--signal *CMD* (オプション): コンテナー内の実行中のプロセスにコマンドを送信します。

*CONTAINER* (必須): コンテナーの ID または名前。

**例**:

次の例は、`proxy` という名前のコンテナー内のプロセスを停止する要求です。
```
bluemix ic kill proxy
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を表示します。

```
bluemix ic namespace-get
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

ログイン先の組織のプライベート {{site.data.keyword.Bluemix_notm}} イメージ・リポジトリーの名前を設定します。

*制限*: リポジトリー名前空間の名前にハイフン (`-`) を使用することはできません。

```
bluemix ic namespace-set NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*NAME* (必須): 組織のリポジトリー名前空間を (まだ設定されていない場合に) 設定する一回限りの機能です。名前空間を設定した後、続行する前に、`bluemix ic init` コマンドを使用して IBM Containers を再初期化してください。


## bluemix ic pause
{: #pause}

実行中のコンテナー内のすべてのプロセスを休止します。詳細については、Docker ヘルプで [pause](https://docs.docker.com/reference/commandline/pause/){: new_window} コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic unpause](#unpause) コマンドを参照してください。

```
bluemix ic pause CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

**応答**:

- コンテナーは正常に休止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`
  
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを休止する要求です。
```
bluemix ic pause proxy
```


## bluemix ic unpause
{: #unpause}

実行中のコンテナー内のすべてのプロセスを休止解除します。詳細については、Docker ヘルプで [unpause](https://docs.docker.com/reference/commandline/unpause/){: new_window} コマンドを参照してください。コンテナーを休止する場合は、[bluemix ic pause](#pause) コマンドを参照してください。

```
bluemix ic unpause CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

**応答**:

- コンテナーは正常に休止解除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。 

 `{message}` 
 
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを休止解除する要求です。
```
bluemix ic unpause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

コンテナーのポート・マッピングまたは特定のマッピングをリストします。このコマンドは `docker port` コマンドをラップします。詳細については、Docker ヘルプで [port](https://docs.docker.com/reference/commandline/port/){: new_window} コマンドを参照してください。


## bluemix ic ps
{: #bluemix_ic_ps}
ログインしているユーザーの名前空間で実行中のコンテナーのリストを表示します。デフォルトでは、このコマンドは実行中のコンテナーのみを表示します。詳細については、Docker ヘルプで [ps](https://docs.docker.com/reference/commandline/ps/){: new_window} コマンドを参照してください。

```
bluemix ic ps [-a|--all][-s|--size] [-l NUM|--limit NUM][-q|--quiet]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-a|--all (オプション): 実行中のコンテナーも停止状態のコンテナーも、どちらもすべて表示します。

-s|--size (オプション): コンテナーのサイズをリストします。

-l *NUM*|--limit *NUM* (オプション): 最近作成されたコンテナーをリストします。ここで、*NUM* は、最近作成されたコンテナーのうちのいくつのコンテナーを返すかを指定する数です。

例えば、`node1` から `node5` までのコンテナーを順次作成した場合、コマンド `bluemix ic ps --limit 2` は、作成されたコンテナーのうちの最新の 2 つである node4 と node5 を返します。

-q|--quiet (オプション): コンテナー ID のみを表示します。

**例**:

次の例は、実行中と停止状態のすべてのコンテナーを表示する要求です。
```
bluemix ic ps -a
```


## bluemix ic restart
{: #bluemix_ic_restart}

コンテナーを再始動します。詳細については、Docker ヘルプで [restart](https://docs.docker.com/reference/commandline/restart/){: new_window} コマンドを参照してください。

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

-t *SECS*|--time *SECS* (オプション): コンテナーを再始動するまでの待機秒数。

**応答**:

- コンテナーは正常に再始動されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。 

 `{message}` 
 
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを再始動する要求です。
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

コンテナーを削除します。詳細については、Docker ヘルプで [rm](https://docs.docker.com/reference/commandline/rm/){: new_window} コマンドを参照してください。

```
bluemix ic rm [-f|--force] CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-f|--force (オプション): 実行中のコンテナーまたは障害が起こったコンテナーを強制的に削除します。

*CONTAINER* (必須): コンテナーの名前または ID。

**応答**:

- コンテナーは正常に削除されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。 

 `{message}` 
 
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを削除する要求です。
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

ログインしているユーザーの名前空間からイメージを削除します。詳細については、Docker ヘルプで [rmi](https://docs.docker.com/reference/commandline/rmi/){: new_window} コマンドを参照してください。

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-R *REGISTRY*|--registry *REGISTRY* (オプション): レジストリー・ホストを変更します。デフォルトでは、`bluemix ic init` コマンドに指定したレジストリーが使用されます。

*IMAGE* (必須): 削除するイメージの名前。イメージ名にタグが指定されていない場合、
`latest` とタグ付けされたイメージはデフォルトで削除されます。


**応答**:

- 削除されました: `{IMAGE}`

 ここで、`{IMAGE}` は削除されたイメージの名前です。
 
- エラー! レジストリー・ホストが指定されていません。

- イメージ削除は失敗しました - コンテナー・クラウド・レジストリーに接続できませんでした。

- コンテナー・クラウド・サービスでコマンドが失敗しました。 

 `{message}`
 
 ここで、`{message}` は関連するエラーです。


**例**:

次の例は、イメージ `mynamespace/myimage:latest` を削除する要求です。
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic run
{: #bluemix_ic_run}

イメージ名を使用して、コンテナー・クラウド・サービスで新しいコンテナーを開始します。
詳細については、Docker ヘルプで [run](https://docs.docker.com/reference/commandline/run/){: new_window} コマンドを参照してください。



```
bluemix ic run [-p PORT|--publish PORT][-P] [-m MEMORY|--memory MEMORY][-e ENV|--env ENV] [-v VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS][-it] IMAGE [CMD [CMD ...]]
```
**注:** Cloud Foundry コマンド・ツールがインストールされていること、および Cloud Foundry トークンがあることを確認してください。`bluemix login` を使用した正常なログインおよび `bluemix ic init` によって、必要なトークンおよび証明書が生成されます。 


**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

-p *PORT*|--publish *PORT* (オプション): HTTP トラフィック用のポートを公開します。使用するイメージの Dockerfile 内に指定されているポートがあれば、それらのポートを含めます。複数の `-p` オプションを使用して、複数のポートを含めることができます。ポートを公開すると、パブリック IP アドレスが使用可能な場合、パブリック IP アドレスがコンテナーに自動的にバインドされます。

コンテナーにバインドしたい IP アドレスがスペース内に既に存在する場合、後でバインドするのでなく、その IP アドレスを指定できます。IP アドレスは、*&lt;ip-address&gt;:&lt;container-port&gt;:&lt;container-port&gt;* 形式で指定する必要があります。

スペース用の IP アドレスの要求について詳しくは、[bluemix ic ip-request](#ip_request) コマンドを参照してください。

ポートを指定したら、同じ {{site.data.keyword.Bluemix_notm}} スペース内でホストにアクセスしようとする {{site.data.keyword.Bluemix_notm}} Load Balancer またはコンテナーがアプリを使用できるように設定します。使用するイメージの Dockerfile 内にポートが指定されている場合、そのポートを含めてください。

**ヒント:**

- IBM 認定 Liberty Server イメージ、またはこのイメージの変更版の場合、ポート 9080 を入力します。
- IBM 認定 Node.js イメージ、またはこのイメージの変更版の場合、ポート 8000 を入力します。

-P (オプション): イメージの Dockerfile 内に指定されたポートを HTTP トラフィック用に自動的に公開します。

-m *MEMORY*|--memory *MEMORY* (オプション): グループにメモリー限度 (MB) を割り当てます。CLI からコンテナー・グループを作成する場合、各コンテナー・インスタンスのデフォルト値は `64` MB です。{{site.data.keyword.Bluemix_notm}} ダッシュボードからコンテナー・グループを作成する場合、各インスタンスのデフォルト値は `256` MB です。受け入れられる値は、`64`、`256`、`512`、`1024`、および `2048` です。メモリー限度が割り当てられた後、その値を変更することはできません。

-e *ENV*|--env *ENV* (オプション): 環境変数を設定します。**ENV** は、「キー = 値」のペアです。複数のキーは別々にリストしてください。引用符を含める場合、環境変数名と値の両方を囲むように指定します。例えば、`-e "key1=value1" -e "key2=value2" -e "key3=value3"` のようにします。指定可能な環境変数のうち、一般的に使用されるものを次の表に示します。

|      環境変数                          |   説明                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;appname&gt;*       | コンテナーにサービスをバインドします。`CCS_BIND_APP` 環境変数を使用して、アプリをコンテナーにバインドします。このアプリはターゲット・サービスにバインドされ、ブリッジとして機能します。これにより、{{site.data.keyword.Bluemix_notm}} は、ブリッジ・アプリの `VCAP_SERVICES` 情報を、実行中のコンテナー・インスタンスに注入することができます。ブリッジ・アプリの作成について詳しくは、[コンテナーへのサービスのバインド](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_binding_ov){: new_window}を参照してください。 |
| CCS_SSH_KEY=*&lt;public_ssh_key&gt;* | コンテナー作成時に SSH 鍵をコンテナーに追加します。{{site.data.keyword.Bluemix_notm}} ダッシュボードまたは CLI からコンテナーを作成するときに、この環境変数を使用して SSH 鍵を追加できます。SSH 鍵について詳しくは、[コンテナーへのログイン](http://www.ng.bluemix.net/docs/containers/container_creating_ov.html#container_cli_login_ssh){: new_window}を参照してください。 |
| LOG_LOCATIONS=*&lt;path_to_file&gt;* | コンテナー内でモニターされるログ・ファイルを追加します。`LOG_LOCATIONS` 環境変数をログ・ファイルへのパスと共に組み込んでください。 |
*表 2. 一般的に使用される環境変数*

-v VOLUME:CONTAINER_PATH[:ro]|--volume VOLUME:CONTAINER_PATH[:ro](optional): 詳細を `VolumeId:ContainerPath[:ro]` 形式で指定して、ボリュームをコンテナーにアタッチします。

- *VOLUME*: ボリュームの ID または名前。
- *CONTAINER_PATH*: コンテナー内でのボリュームへの絶対パス。
- ro (オプション):`ro` を指定すると、ボリュームはデフォルトの読み取り/書き込みではなく、読み取り専用になります。

-n *NAME*|--name *NAME* (必須): コンテナーに名前を付けます。

*ヒント:* コンテナー名の先頭は文字でなければなりません。名前には、大文字、小文字、数字、ピリオド (`.`)、下線 (`_`)、およびハイフン (`-`) を使用できます。

--link *NAME*:*ALIAS* (オプション): あるコンテナーが実行中の別のコンテナーと通信するようにしたい場合は、ホスト名の別名を使用してそのコンテナーを指定できます。

-it (オプション): コンテナーを対話モードで実行します。コンテナーが作成された後、標準入力が表示されている状態を維持します。終了するには `exit` と入力します。

*IMAGE* (必須): コンテナーに含めるイメージ。イメージの後にコマンドをリストできますが、イメージの後にオプションを置かないでください。イメージを指定する前に、すべてのオプションを含めてください。

組織のプライベート {{site.data.keyword.Bluemix_notm}} リポジトリー内のイメージを使用する場合は、形式 *registry.ng.bluemix.net/NAMESPACE/IMAGE* でイメージを指定します。

IBM Containers によって提供されるイメージを使用する場合は、形式 *registry.ng.bluemix.net/IMAGE* でイメージを指定します。

*CMD* (オプション): コンテナーに渡されて実行されるコマンドと引数。このコマンドは長時間実行コマンドでなければなりません。実行時間があまり長くない一時的なコマンド (例えば、`/bin/date` など) は、コンテナーがクラッシュする原因となる可能性があるため、使用しないでください。



**例**:

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


## bluemix ic route-map
{: #bluemix_ic_route_map}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-map [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

-n *HOST*|--hostname *HOST* (オプション): 経路のホスト名。ホスト名は、完全なパブリック経路 URL の最初の部分です。例えば、URL `mycontainerhost.mybluemix.net` 中の `mycontainerhost` です。

-d *DOMAIN*|--domain *DOMAIN* (オプション): 完全なパブリック経路 URL の 2 番目の部分である、経路のドメイン名。ほとんどの場合、ドメインは `mybluemix.net` です。このパラメーターを使用してプライベート・ドメインを指定することもできます。

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

次の例は、`GROUP1` という名前のグループの経路をマップする要求です。ここで、`my_host` はホスト名、`organization.com` はドメインです。
```
bluemix ic route-map -n my_host -d organization.com GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

コンテナー・グループへのアクセスに使用するインターネット・トラフィックの経路を設定します。このコマンドを使用して、新規経路を設定するか、既存の経路を更新できます。

```
bluemix ic route-unmap [-n HOST|--hostname HOST][-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

-n *HOST*|--hostname *HOST* (オプション): 経路のホスト名。

-d *DOMAIN*|--domain *DOMAIN* (オプション): 経路のドメイン・ネーム。

*CONTAINER_GROUP* (必須): コンテナー・グループの ID または名前。

**例**:

次の例は、`GROUP1` という名前のグループの経路をマップ解除する要求です。ここで、`my_host` はホスト名、`organization.com` はドメインです。
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic start
{: #ic_start}
停止しているコンテナーを開始します。詳細については、Docker ヘルプで [start](https://docs.docker.com/reference/commandline/start/){: new_window} コマンドを参照してください。コンテナーを停止する場合は、[bluemix ic stop](#ic_stop) コマンドを参照してください。

```
bluemix ic start CONTAINER
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

**応答**:

- コンテナーは正常に開始しました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`
  
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを開始する要求です。
```
bluemix ic start proxy
```


## bluemix ic stop  
{: #ic_stop}
実行中のコンテナーを停止します。詳細については、Docker ヘルプで [stop](https://docs.docker.com/reference/commandline/stop/){: new_window} コマンドを参照してください。コンテナーを開始する場合は、[bluemix ic start](#ic_start) コマンドを参照してください。

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

-t *SECS*|--time *SECS* (オプション): コンテナーを停止するまでの待機秒数。

**応答**:

- コンテナーは正常に停止されました。

- コンテナー・クラウド・サービスでコマンドが失敗しました。

 `{message}`
  
 ここで、`{message}` は関連するエラーです。

 
- コマンド失敗 - コンテナー・クラウド・サービスに接続できませんでした。

**例**:

次の例は、`proxy` という名前のコンテナーを停止する要求です。
```
bluemix ic stop proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

1 つ以上のコンテナーについて、使用状況統計をライブで表示します。終了するには `CTRL+C` を使用します。詳細については、Docker ヘルプで [stats](https://docs.docker.com/reference/commandline/stats/){: new_window} コマンドを参照してください。

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

--no-stream (オプション): 最新の結果のみを表示し、それ以前の情報を含めません。

**例**:

次の例は、1 つのコンテナーについての最新の統計情報を表示する要求です。
```
bluemix ic stats --no-stream my_container
```


## bluemix ic top
{: #bluemix_ic_top}

コンテナーで実行されているプロセスを表示します。詳細については、Docker ヘルプで [top](https://docs.docker.com/reference/commandline/top/){: new_window} コマンドを参照してください。

```
bluemix ic top CONTAINER [CONTAINER]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

**例**:

次の例は、`my_container` という名前のコンテナー内のプロセスを表示する要求です。
```
bluemix ic top my_container
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

ボリュームをリストします。

```
bluemix ic volumes
```

**前提条件**: エンドポイント、ログイン、ターゲット


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

ボリュームを検査します。


```
bluemix ic volume-inspect VOLUME_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*VOLUME_NAME* (必須): ボリューム名。

**例**:

次の例は、ボリュームを検査する要求です。ここで、`volume_name` はボリュームの名前です。
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

ボリュームを作成します。

```
bluemix ic volume-create VOLUME_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*VOLUME_NAME* (必須): ボリューム名。名前には、小文字、数字、下線 (`_`)、およびハイフン (`-`) を使用できます。

**例**:

次の例は、ボリュームを作成する要求です。
```
bluemix ic volume-create volume_name 
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

ボリュームを削除します。

```
bluemix ic volume-remove VOLUME_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*VOLUME_NAME* (必須): ボリューム名。

**例**:

次の例は、ボリュームを削除する要求です。ここで、`volume_name` はボリュームの名前です。
```
bluemix ic volume-remove volume_name
```

## bluemix ic volume-fs

{: #bluemix_ic_volume_fs}

ファイル・システムをリストします。

```
bluemix ic volume-fs
```

## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

新しいファイル・システムを作成します。

```
bluemix ic volume-fs-create FILE_SYSTEM_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*FILE_SYSTEM_NAME* (必須): ファイル・システム名。名前には、小文字、数字、下線 (`_`)、およびハイフン (`-`) を使用できます。

**例**:

次の例は、ファイル・システムを作成する要求です。
```
bluemix ic volume-fs-create my_file_system 
```

## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

ファイル・システムを削除します。

```
bluemix ic volume-fs-remove FILE_SYSTEM_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*FILE_SYSTEM_NAME* (必須): ファイル・システム名。

**例**:

次の例は、ファイル・システムを削除する要求を示しています。ここで、`my_file_system` は、ファイル・システムの名前です。
```
bluemix ic volume-fs-remove my_file_system
```

## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

ファイル・システムを検査します。

```
bluemix ic volume-fs-inspect FILE_SYSTEM_NAME
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*FILE_SYSTEM_NAME* (必須): ファイル・システム名。

**例**:

次の例は、ファイル・システムを検査する要求です。ここで、`my_file_system` は、ボリュームの名前です。
```
bluemix ic volume-fs-inspect my_file_system
```
## bluemix ic volume-fs-flavors

{: #bluemix_ic_volume_fs_flavors}

すべてのファイル・システムのフレーバーをリストします。

```
bluemix ic volume-fs-flavors
```

**前提条件**: エンドポイント、ログイン、ターゲット

## bluemix ic wait
{: #bluemix_ic_wait}

コンテナーを終了し、確認のために終了コードを表示します。詳細については、Docker ヘルプで [wait](https://docs.docker.com/reference/commandline/wait/){: new_window} コマンドを参照してください。

```
bluemix ic wait CONTAINER [CONTAINER]
```

**前提条件**: エンドポイント、ログイン、ターゲット、Docker

**コマンド・オプション**:

*CONTAINER* (必須): コンテナーの名前または ID。

**例**:

次の例は、`my_container` という名前のコンテナーを終了する要求です。
```
bluemix ic wait my_container
```


## bluemix ic version
{: #bluemix_ic_version}

Docker のバージョンを表示します。 

```
bluemix ic version
```

**前提条件**:  Docker

IBM Containers のバージョンを表示するには、`bluemix ic info` を実行します。詳細については、Docker ヘルプで [version](https://docs.docker.com/reference/commandline/version/){: new_window} コマンドを参照してください。
