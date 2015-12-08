{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} と対話するための bx コマンド
{: #bluemix_cli}

*最終更新日:* 2015 年 10 月 19 日

{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェース (CLI) では、ユーザーが {{site.data.keyword.Bluemix_notm}} と対話できるように、名前空間別にグループ化したコマンドのセットが提供されています。一部の {{site.data.keyword.Bluemix_notm}} CLI コマンドは既存の cf コマンドのラッパーであり、bx コマンドと呼ばれます。それ以外は {{site.data.keyword.Bluemix_notm}} に固有のものです。以下の説明では、{{site.data.keyword.Bluemix_notm}} CLI によってサポートされるすべてのコマンドをリストし、名前、オプション、使用法、前提条件、説明、および例を示します。
{:shortdesc}
 
**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件となるアクションのないコマンドでは、**なし**とリストされています。それ以外の場合、前提条件には以下のアクションのうちの 1 つ以上が含まれます。
<dl>
<dt>**エンドポイント**</dt>
<dd>このコマンドを使用する前に、`bluemix api` を介して API エンドポイントを設定する必要があります。</dd>
<dt>**ログイン**</dt>
<dd>このコマンドを使用する前に、`bluemix login` コマンドを使用してログインする必要があります。</dd>
<dt>**ターゲット**</dt>
<dd>このコマンドを使用する前に、`bluemix target` コマンドを使用して組織およびスペースを設定する必要があります。</dd>
</dl>

## bluemix help
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

`catalog` 名前空間のヘルプを表示します。

```
bluemix help catalog
```

```
bluemix catalog help
```

`info` コマンドのヘルプを表示します。

```
bluemix help info
```

`catalog` 名前空間の下の `templates` コマンドのヘルプを表示します。

```
bluemix catalog help templates
```


## bluemix api
{{site.data.keyword.Bluemix_notm}} API エンドポイントを設定または表示します。このコマンドは `cf api` コマンドをラップします。

```
bluemix api [API_ENDPOINT][--unset]
```

**前提条件**: なし

**コマンド・オプション**:

*API_ENDPOINT* (オプション): ターゲットの API エンドポイント (例えば https://api.ng.bluemix.net)。*API_ENDPOINT* オプションと `--unset` オプションのどちらも指定されない場合、現行 API エンドポイントが表示されます。

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
ユーザーをログインします。このコマンドは `cf login` コマンドをラップします。コマンド・オプションは `cf login` コマンドのオプションと同じです。

```
bluemix login [OPTIONS...]
```

**前提条件**: エンドポイント

**コマンド・オプション**: `login` コマンドでサポートされるオプションについては、アプリケーション管理用 cf コマンドの `cf login` コマンド使用法の説明を参照してください。


## bluemix logout
ユーザーをログアウトします。このコマンドは `cf logout` コマンドをラップします。

```
bluemix logout
```

**前提条件**: なし


## bluemix target
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

現行の組織を「MyOrg」に、スペースを「MySpace」に設定します。

```
bluemix target -o MyOrg -s MySpace
```

現行の組織およびスペースを表示します。

```
bluemix target
```


## bluemix info
基本的な {{site.data.keyword.Bluemix_notm}} 情報を表示します。これには、現行領域、クラウド・コントローラーのバージョン、および、いくつかの有用なエンドポイント (例えば、ログイン用のエンドポイントや、アクセス・トークン交換用のエンドポイントなど) が含まれます。

```
bluemix info
```

**前提条件**: エンドポイント


## bluemix list
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
cf アプリケーションまたはコンテナー・グループを、指定されたインスタンス数、ディスク割り当て量、およびメモリー・サイズになるよう拡大または縮小します。

**注:** コンテナー・グループのスケーリングに指定できるのはインスタンス数のみです。オプションが何も指定されない場合、このコマンドは、コンテナー・グループの現行インスタンス数をリストし、cf アプリケーションではディスク割り当て量とメモリー・サイズもリストします。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME* (必須): スケーリングの対象にする cf アプリケーションまたはコンテナー・グループの名前。

-i *INSTANCE_COUNT* (オプション): スケーリングする cf アプリケーションまたはコンテナー・グループの新しいインスタンス数。コンテナー・グループのスケーリングの場合は、このオプションは唯一の有効なオプションです。

-k *DISK_QUOTA* (オプション): cf アプリケーションの新しいディスク割り当て量。コンテナー・グループのスケーリングの場合は無効です。

-m *MEMORY_SIZE* (オプション): cf アプリケーションの新しいメモリー・サイズ。コンテナー・グループのスケーリングの場合は無効です。

**例**:

「my-container-group」の現行インスタンス数を表示します。

```
bluemix scale my-container-group
```

「my-container-group」を 2 インスタンスにスケーリングします。

```
bluemix scale my-container-group -i 2
```

「my-java-app」を、3 インスタンス、8G ディスク割り当て量、および 1024M メモリー・サイズにスケーリングします。

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
{{site.data.keyword.Bluemix_notm}} への未加工 HTTP 要求を実行します。「Content-Type」はデフォルトで「application/json」に設定されます。このコマンドは、cf API エンドポイント (例えば、https://api.ng.bluemix.net) ではなく、{{site.data.keyword.Bluemix_notm}} コンソール・サーバー (例えば、https://console.ng.bluemix.net) に要求を送信します。

```
bluemix curl PATH [OPTIONS...]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*PATH* (必須): リソースの URL パス。例えば、/rest/v2/apps です。

*OPTIONS* (オプション): `bluemix curl` コマンドでサポートされるオプションは、`cf curl` コマンドのオプションと同じです。

**例**:

すべてのボイラープレート・テンプレートの情報を取得します。

```
bluemix curl /rest/templates
```


## bluemix iam orgs
このコマンドの機能とオプションは `cf orgs` コマンドと同じです。


## bluemix iam org
このコマンドの機能とオプションは `cf org` コマンドと同じです。


## bluemix iam org-create
このコマンドの機能とオプションは `cf create-org` コマンドと同じです。


## bluemix iam org-rename
このコマンドの機能とオプションは `cf rename-org` コマンドと同じです。


## bluemix iam org-delete
このコマンドの機能とオプションは `cf delete-org` コマンドと同じです。


## bluemix iam spaces
このコマンドの機能とオプションは `cf spaces` コマンドと同じです。


## bluemix iam space
このコマンドの機能とオプションは `cf space` コマンドと同じです。


## bluemix iam space-create
このコマンドの機能とオプションは `cf create-space` コマンドと同じです。


## bluemix iam space-rename
このコマンドの機能とオプションは `cf rename-space` コマンドと同じです。


## bluemix iam space-delete
このコマンドの機能とオプションは `cf delete-space` コマンドと同じです。


## bluemix iam user-create
このコマンドの機能とオプションは `cf create-user` コマンドと同じです。


## bluemix iam user-delete
このコマンドの機能とオプションは `cf delete-user` コマンドと同じです。


## bluemix iam org-users
このコマンドの機能とオプションは `cf org-users` コマンドと同じです。


## bluemix iam org-role-set
このコマンドの機能とオプションは `cf set-org-role` コマンドと同じです。


## bluemix iam org-role-unset
このコマンドの機能とオプションは `cf unset-org-role` コマンドと同じです。


## bluemix iam space-users
このコマンドの機能とオプションは `cf space-users` コマンドと同じです。


## bluemix iam space-role-set
このコマンドの機能とオプションは `cf set-space-role` コマンドと同じです。


## bluemix iam space-role-unset
このコマンドの機能とオプションは `cf unset-space-role` コマンドと同じです。


## bluemix catalog templates
Bluemix のボイラープレート・テンプレートを表示します。

```
bluemix catalog templates [-d]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

-d (オプション): -d オプションが指定されている場合、各テンプレートの説明も表示されます。それ以外の場合、各テンプレートの ID および名前のみが表示されます。


## bluemix catalog template-run
指定されたテンプレートをベースにした、指定された URL と説明を持つ cf アプリケーションを作成します。デフォルトでは、この新規アプリケーションは自動的に開始されます。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*TEMPLATE_ID* (必須): アプリケーション作成のベースになるテンプレート。すべてのテンプレートの ID を表示するには、「bluemix templates」を使用します。

*CF_APP_NAME* (必須): 作成する cf アプリケーションの名前。

-u *URL* (オプション): アプリケーションの経路。指定されない場合、経路は、アプリケーション名およびデフォルト・ドメインに基づいて {{site.data.keyword.Bluemix_notm}} によって自動的に設定されます。

-d *DESCRIPTION* (オプション): アプリケーションの説明。

--no-start (オプション): 作成後のアプリケーションを自動的に開始しません。指定されない場合、アプリケーションは作成された後で自動的に開始されます。

**例**:

「javaHelloWorld」テンプレートをベースにして cf アプリケーション「my-app」を作成します。

```
bluemix catalog template-run javaHelloWorld my-app
```

経路を「myrubyapp.ng.bluemix.net」とし、説明を「My first ruby app on {{site.data.keyword.Bluemix_notm}}.」として、「rubyHelloWorld」テンプレートをベースにしてアプリケーション「my-ruby-app」を作成します。

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on {{site.data.keyword.Bluemix_notm}}."
```

「pythonHelloWorld」テンプレートをベースにして、自動開始なしでアプリケーション「my-python-app」を作成します。

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
{{site.data.keyword.Bluemix_notm}} のすべての地域の情報を表示します。

```
bluemix network regions
```

**前提条件**: エンドポイント


## bluemix network region-set
指定された地域に切り替えます。このコマンドは、新しい地域の同じ組織およびスペースに自動的にターゲットを変更する (可能な場合) か、または、新しい組織およびスペースを選択するようユーザーにプロンプトを出します (ユーザーが既にログインしている場合)。API エンドポイントはそれに合わせて変更されます。

```
bluemix network region-set REGION_NAME
```

**前提条件**: エンドポイント

**コマンド・オプション**:

*REGION_NAME* (必須): 切り替える先の地域の名前。`bluemix regions` コマンドを使用してすべての地域名を表示できます。

**例**:

現行地域を「eu-gb」に設定します。

```
bluemix network region-set eu-gb
```


## bluemix network routes
このコマンドの機能とオプションは `cf routes` コマンドと同じです。


## bluemix network route-check
このコマンドの機能とオプションは `cf check-route` コマンドと同じです。


## bluemix network route-map
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

指定されたドメインで「my-app」に経路をマップします。

```
bluemix network route-map my-app mybluemix.net
```

指定されたドメインとホスト名で「my-container-group」に経路をマップします。

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
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

「my-app」から「my-app.mybluemix.net」をマップ解除します。

```
bluemix network route-unmap my-app mybluemix.net
```

「my-container-group」から「abc.ng.bluexmix.net」をマップ解除します。

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
このコマンドの機能とオプションは `cf create-route` コマンドと同じです。


## bluemix network route-delete
このコマンドの機能とオプションは `cf delete-route` コマンドと同じです。


## bluemix network orphaned-routes-delete
このコマンドの機能とオプションは `cf delete-orphaned-routes` コマンドと同じです。


## bluemix network domains
このコマンドの機能とオプションは `cf domains` コマンドと同じです。


## bluemix network domain-create
このコマンドの機能とオプションは `cf create-domain` コマンドと同じです。


## bluemix network domain-delete
このコマンドの機能とオプションは `cf delete-domain` コマンドと同じです。


## bluemix network shared-domain-create
このコマンドの機能とオプションは `cf create-shared-domain` コマンドと同じです。


## bluemix network shared-domain-delete
このコマンドの機能とオプションは `cf delete-shared-domain` コマンドと同じです。


## bluemix plugin repos
{{site.data.keyword.Bluemix_notm}} CLI に登録されているすべてのプラグイン・リポジトリーをリストします。

```
bluemix plugin repos
```

**前提条件**: なし


## bluemix plugin repo-add
新規プラグイン・リポジトリーを {{site.data.keyword.Bluemix_notm}} CLI に追加します。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**前提条件**: なし

**コマンド・オプション**:

*REPO_NAME* (必須): 追加するリポジトリーの名前。各リポジトリーに対して任意の名前を定義できます。

*REPO_URL* (必須): 追加するリポジトリーの URL。リポジトリー URL にはプロトコルが含まれている必要があります (例えば、plugins.ng.bluemix.net ではなく、http://plugins.ng.bluemix.net)。{{site.data.keyword.Bluemix_notm}} CLI の公式プラグイン・リポジトリーは http://plugins.ng.bluemix.net です。

**例**:

Bluemix CLI の公式プラグイン・リポジトリーを「bluemix-repo」として追加します。

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
{{site.data.keyword.Bluemix_notm}} CLI からプラグイン・リポジトリーを削除します。

```
bluemix plugin repo-remove REPO_NAME
```

**前提条件**: なし

**コマンド・オプション**:

*REPO_NAME* (必須): 削除するリポジトリーの名前。

**例**:

{{site.data.keyword.Bluemix_notm}} CLI から「bluemix-repo」リポジトリーを削除します。

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
追加されたすべてのリポジトリーまたは特定のリポジトリー内にある使用可能なプラグインをすべてリストします。

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**前提条件**: なし

**コマンド・オプション**:

-r *REPO_NAME* (オプション): 指定されたリポジトリー内のプラグインのみをリストします。

**例**:

追加されたすべてのリポジトリー内のすべてのプラグインをリストします。

```
bluemix plugin repo-plugin-list
```

「bluemix-repo」リポジトリー内のすべてのプラグインをリストします。

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
{{site.data.keyword.Bluemix_notm}} CLI 内のインストールされたプラグインをすべてリストします。

```
bluemix plugin list
```

**前提条件**: なし


## bluemix plugin install
指定されたパスまたはリポジトリーからプラグインを {{site.data.keyword.Bluemix_notm}} CLI にインストールします。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**前提条件**: なし

**コマンド・オプション**:

*PLUGIN_PATH*|*PLUGIN_NAME* (必須): 「-r *REPO_NAME*」が指定されない場合、指定されたローカル・パスまたはリモート URL からプラグインがインストールされます。

-r *REPO_NAME* (オプション): プラグイン・バイナリーが置かれているリポジトリーの名前。

**例**:

ローカル・ファイルからプラグインをインストールします。

```
bluemix plugin install /downloads/new_plugin
```

リモート URL からプラグインをインストールします。

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

「IBM-Containers」プラグインを「bluemix-repo」リポジトリーからインストールします。

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
指定されたプラグインを {{site.data.keyword.Bluemix_notm}} CLI からアンインストールします。

```
bluemix plugin uninstall PLUGIN_NAME
```

**前提条件**: なし

**コマンド・オプション**:

*PLUGIN_NAME* (必須): アンインストールするプラグインの名前。

**例**:

前にインストールされた「IBM-Containers」プラグインをアンインストールします。

```
bluemix plugin uninstall IBM-Containers
```
