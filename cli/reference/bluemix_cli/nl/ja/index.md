{:shortdesc: .shortdesc}

# Bluemix のコマンド
{: #bluemix_cli}

*最終更新日:* 2015 年 10 月 19 日

Bluemix のコマンド・ライン・インターフェース (CLI) には、名前空間別にグループ分けされた、ユーザーが Bluemix と対話するためのコマンドが一式用意されています。Bluemix の CLI コマンドには、既存の cf コマンドのラッパーになっているものもあれば、Bluemix 固有のコマンドもあります。以下の情報には、Bluemix CLI でサポートされているすべてのコマンドがリストされており、コマンドの名前、オプション、使用法、前提条件、説明、および使用例が載っています。
{:shortdesc}
 
**注:** *前提条件*には、コマンドを使用する前に必要となるアクションがリストされています。前提条件となるアクションがないコマンドには、**なし**がリストされています。その他の場合は、前提条件に、以下に示すアクションが 1 つ以上含まれている場合があります。
<dl>
<dt>**エンドポイント**</dt>
<dd>このコマンドを使用する前に `bluemix api` を使用して API エンドポイントを設定する必要があります。</dd>
<dt>**ログイン**</dt>
<dd>このコマンドを使用する前に、`bluemix login` コマンドを使用してログインする必要があります。</dd>
<dt>**ターゲット**</dt>
<dd>このコマンドを使用する前に、`bluemix target` コマンドを使用して組織とスペースを設定する必要があります。</dd>
</dl>

## bluemix help
Bluemix CLI の第 1 レベルの組み込みコマンドとサポートされている名前空間に関する一般ヘルプ、または特定の組み込みコマンドもしくは名前空間に関するヘルプを表示します。

```
bluemix help [COMMAND|NAMESPACE]
```

**前提条件**:  なし

**コマンド・オプション**:

*COMMAND*|*NAMESPACE*  (オプション):  ヘルプの表示対象となるコマンドまたは名前空間。指定しない場合は、Bluemix CLI の一般ヘルプが表示されます。

**例**:

以下は、Bluemix CLI の一般ヘルプを表示します。

```
bluemix help
```

以下は、`catalog` という名前空間のヘルプを表示します。

```
bluemix help catalog
```

```
bluemix catalog help
```

以下は、`info` コマンドのヘルプを表示します。

```
bluemix help info
```

以下は、`catalog` という名前空間の下にある `templates` コマンドのヘルプを表示します。

```
bluemix catalog help templates
```


## bluemix api
Bluemix API エンドポイントを設定または表示します。このコマンドは、`cf api` コマンドのラッパーです。

```
bluemix api [API_ENDPOINT][--unset]
```

**前提条件**:  なし

**コマンド・オプション**:

*API_ENDPOINT*  (オプション):  ターゲットとする API エンドポイント。例えば https://api.ng.bluemix.net。*API_ENDPOINT* オプションと `–unset` オプションを両方とも指定しない場合は、現行の API エンドポイントが表示されます。

`--unset`  (オプション):  API エンドポイントの設定を削除します。

**例**:

以下は、API エンドポイントを api.ng.bluemix.net に設定します。

```
bluemix api api.ng.bluemix.net
```

以下は、現行の API エンドポイントを表示します。

```
bluemix api
```

以下は、API エンドポイントを設定解除します。

```
bluemix api --unset
```


## bluemix login
ユーザーにログインします。このコマンドは `cf login` コマンドのラッパーです。コマンドのオプションは `cf login` コマンドのオプションと同じです。

```
bluemix login [OPTIONS...]
```

**前提条件**:  エンドポイント

**コマンド・オプション**:
この `login` コマンドでサポートされているオプションについては、「アプリケーションを管理するための cf コマンド」に載っている `cf login` コマンドの使用法に関する情報を参照してください。


## bluemix logout
ユーザーをログアウトします。このコマンドは `cf logout` コマンドのラッパーです。

```
bluemix logout
```

**前提条件**:  なし


## bluemix target
ターゲットの組織またはスペースを設定または表示します。このコマンドは `cf target` コマンドのラッパーです。

```
bluemix target [-o ORG_NAME] [-s SPACE_NAME]
```

**前提条件**:  エンドポイント、ログイン

**コマンド・オプション**:

-o *ORG_NAME*  (オプション):  ターゲットとする組織の名前。

-s *SPACE_NAME*  (オプション):  ターゲットとするスペースの名前。

-o *ORG_NAME* と -s *SPACE_NAME* のいずれも指定しない場合は、現行の組織とスペースが表示されます。

**例**:

以下は、現行の組織を「MyOrg」に、そしてスペースを「MySpace」にそれぞれ設定します。

```
bluemix target -o MyOrg -s MySpace
```

以下は、現行の組織とスペースを表示します。

```
bluemix target
```


## bluemix info
基本の Bluemix 情報 (現行の地域とクラウド・コントローラーのバージョン、およびログイン用エンドポイントやアクセス・トークン交換用エンドポイントといった有用なエンドポイントなど) を表示します。

```
bluemix info
```

**前提条件**:  エンドポイント


## bluemix list
現行のスペースに含まれている cf アプリケーション、コンテナー、コンテナー・グループ、および VM グループをすべてリストします。

```
bluemix list [apps|containers|container-groups|vm-groups]
```

**前提条件**:  エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

apps  (オプション):  アプリケーション情報のみ表示します。

containers  (オプション):  コンテナー情報のみ表示します。

container-groups  (オプション):  コンテナー・グループ情報のみ表示します。

vm-groups  (オプション):  VM グループ情報のみ表示します。

一度に指定できるのは、「apps」、「containers」、「container-groups」、または「vm-groups」のいずれか 1 つのみです。これらをどれも指定しない場合は、cf アプリ、コンテナー、コンテナー・グループ、および VM グループがすべてリストされます。

**例**:

以下は、cf アプリケーションをすべてリストします。

```
bluemix list apps
```

以下は、コンテナーのインスタンスをすべてリストします。

```
bluemix list containers
```

以下は、アプリ、コンテナー、コンテナー・グループ、および VM グループをすべてリストします。

```
bluemix list
```


## bluemix scale
cf アプリケーションまたはコンテナー・グループを指定のインスタンス数、ディスク割り当て量、およびメモリー・サイズにスケールインまたはスケールアウトします。

**注:** コンテナー・グループのスケーリングで指定できるのはインスタンス数のみです。オプションを何も指定しない場合、このコマンドは、コンテナー・グループについては現行インスタンス数をリストします。cf アプリケーションについては、さらにディスク割り当て量とメモリー・サイズもリストします。

```
bluemix scale CF_APP_NAME|CONTAINER_GROUP_NAME [-i INSTANCE_COUNT] [-k DISK_QUOTA] [-m MEMORY_SIZE]
```

**前提条件**:  エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (必須):  スケーリング対象の cf アプリケーションまたはコンテナー・グループの名前。

-i *INSTANCE_COUNT*  (オプション):  スケーリング対象の cf アプリケーションまたはコンテナー・グループの新しいインスタンス数。このオプションは、スケーリング対象のコンテナー・グループに対する唯一有効なオプションです。

-k *DISK_QUOTA*  (オプション):  cf アプリケーションの新しいディスク割り当て量。コンテナー・グループのスケーリングには無効です。

-m *MEMORY_SIZE*  (オプション):  cf アプリケーションの新しいメモリー・サイズ。コンテナー・グループのスケーリングには無効です。

**例**:

以下は、「my-container-group」の現行インスタンス数を表示します。

```
bluemix scale my-container-group
```

以下は、「my-container-group」のインスタンス数を 2 にスケーリングします。

```
bluemix scale my-container-group -i 2
```

以下は、「my-java-app」について、インスタンス数を 3 に、ディスク割り当て量を 8G に、そしてメモリー・サイズを 1024M にスケーリングします。

```
bluemix scale my-java-app -i 3 -k 8G -m 1024M
```


## bluemix curl
Bluemix に対する未加工の HTTP 要求を実行します。「Content-Type」は、デフォルトでは「application/json」に設定されます。このコマンドは、要求を cf API エンドポイント (例えば https://api.ng.bluemix.net) ではなく、Bluemix コンソール・サーバー (例えば https://console.ng.bluemix.net) に送信します。

```
bluemix curl PATH [OPTIONS...]
```

**前提条件**:  エンドポイント、ログイン

**コマンド・オプション**:

*PATH*  (必須):  リソースの URL パス。例えば /rest/v2/apps。

*OPTIONS*  (オプション):  「bluemix curl」コマンドでサポートされているオプションは、「cf curl」コマンドのオプションと同じです。

**例**:

以下は、すべてのボイラープレート・テンプレートに関する情報を取得します。

```
bluemix curl /rest/templates
```


## bluemix iam orgs
このコマンドが持っている機能とオプションは「cf orgs」コマンドと同じです。


## bluemix iam org
このコマンドが持っている機能とオプションは「cf org」コマンドと同じです。


## bluemix iam org-create
このコマンドが持っている機能とオプションは「cf create-org」コマンドと同じです。


## bluemix iam org-rename
このコマンドが持っている機能とオプションは「cf rename-org」コマンドと同じです。


## bluemix iam org-delete
このコマンドが持っている機能とオプションは「cf delete-org」コマンドと同じです。


## bluemix iam spaces
このコマンドが持っている機能とオプションは「cf spaces」コマンドと同じです。


## bluemix iam space
このコマンドが持っている機能とオプションは「cf space」コマンドと同じです。


## bluemix iam space-create
このコマンドが持っている機能とオプションは「cf create-space」コマンドと同じです。


## bluemix iam space-rename
このコマンドが持っている機能とオプションは「cf rename-space」コマンドと同じです。


## bluemix iam space-delete
このコマンドが持っている機能とオプションは「cf delete-space」コマンドと同じです。


## bluemix iam user-create
このコマンドが持っている機能とオプションは「cf create-user」コマンドと同じです。


## bluemix iam user-delete
このコマンドが持っている機能とオプションは「cf delete-user」コマンドと同じです。


## bluemix iam org-users
このコマンドが持っている機能とオプションは「cf org-users」コマンドと同じです。


## bluemix iam org-role-set
このコマンドが持っている機能とオプションは「cf set-org-role」コマンドと同じです。


## bluemix iam org-role-unset
このコマンドが持っている機能とオプションは「cf unset-org-role」コマンドと同じです。


## bluemix iam space-users
このコマンドが持っている機能とオプションは「cf space-users」コマンドと同じです。


## bluemix iam space-role-set
このコマンドが持っている機能とオプションは「cf set-space-role」コマンドと同じです。


## bluemix iam space-role-unset
このコマンドが持っている機能とオプションは「cf unset-space-role」コマンドと同じです。


## bluemix catalog templates
Bluemix のボイラープレート・テンプレートを表示します。

```
bluemix catalog templates [-d]
```

**前提条件**:  エンドポイント、ログイン

**コマンド・オプション**:

-d  (オプション):  「-d」オプションを指定すると、各テンプレートの説明も表示されます。その他の場合は、各テンプレートの ID と名前のみ表示されます。


## bluemix catalog template-run
指定の URL と説明を使用した、指定のテンプレートに基づく cf アプリケーションを作成します。デフォルトでは、この新しいアプリは自動的に開始されます。

```
bluemix catalog template-run TEMPLATE_ID CF_APP_NAME [-u URL] [-d DESCRIPTION] [--no-start]
```

**前提条件**:  エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*TEMPLATE_ID*  (必須):  アプリケーションの作成時にそのアプリケーションの基盤とするテンプレート。すべてのテンプレートの ID を表示するには「bluemix templates」を使用します。

*CF_APP_NAME*  (必須):  作成する cf アプリケーションの名前。

-u *URL*  (オプション):  アプリケーションの経路。指定しない場合、経路はアプリ名とデフォルト・ドメインに基づき、Bluemix が自動的に設定します。

-d *DESCRIPTION*  (オプション): アプリケーションの説明。

--no-start  (オプション):  アプリケーションの作成後、そのアプリケーションの自動開始を行いません。指定しない場合、アプリケーションは作成後自動的に開始されます。

**例**:

以下は、「javaHelloWorld」テンプレートに基づいて「my-app」という cf アプリケーションを作成します。

```
bluemix catalog template-run javaHelloWorld my-app
```

以下は、「rubyHelloWorld」テンプレートに基づく「my-ruby-app」というアプリケーションを作成します。経路には「myrubyapp.ng.bluemix.net」が使用され、「My first ruby app on Bluemix.」という説明が付いています。:

```
bluemix catalog template-run rubyHelloWorld my-ruby-app -u myrubyapp.ng.bluemix.net -d "My first ruby app on Bluemix."
```

以下は、「pythonHelloWorld」テンプレートに基づく、自動開始を行わない「my-python-app」というアプリケーションを作成します。

```
bluemix catalog template-run pythonHelloWorld my-python-app --no-start
```


## bluemix network regions
Bluemix のすべての地域に関する情報を表示します。

```
bluemix network regions
```

**前提条件**:  エンドポイント


## bluemix network region-set
指定の地域に切り替えます。このコマンドは、可能なら自動的にその新しい地域にある同じ組織と同じスペースを新たなターゲットとし、それができない場合は、ユーザーが既にログインしていれば、そのユーザーに新しい組織とスペースを選択するよう要求します。API エンドポイントは、それに応じて変更されます。

```
bluemix network region-set REGION_NAME
```

**前提条件**:  エンドポイント

**コマンド・オプション**:

*REGION_NAME*  (必須):  切り替え先の地域の名前。「bluemix regions」コマンドを使用すると、地域名をすべて表示することができます。

**例**:

以下は、現行の地域を「eu-gb」に設定します。

```
bluemix network region-set eu-gb
```


## bluemix network routes
このコマンドが持っている機能とオプションは「cf routes」コマンドと同じです。


## bluemix network route-check
このコマンドが持っている機能とオプションは「cf check-route」コマンドと同じです。


## bluemix network route-map
指定のドメインとホスト名を持っている、既存の cf アプリケーションまたはコンテナー・グループへの経路をマップします。

```
bluemix network route-map CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**前提条件**:  エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (必須):  経路によってマップされる cf アプリケーションまたはコンテナー・グループの名前。

*DOMAIN*  (必須):  経路のドメイン。例えば、mybluemix.net or ng.bluemix.net。 

-n *HOST_NAME*  (オプション):  経路のホスト名。指定しない場合、ホスト名は、デフォルトではアプリ名またはコンテナー・グループ名に設定されます。

**例**:

以下は、指定のドメインを持った「my-app」への経路をマップします。

```
bluemix network route-map my-app mybluemix.net
```

以下は、指定のドメインとホスト名を持った「my-container-group」への経路をマップします。

```
bluemix network route-map my-container-group ng.bluemix.net -n abc
```


## bluemix network route-unmap
指定の経路を既存の cf アプリケーションまたはコンテナー・グループからマップ解除します。

```
bluemix network route-unmap CF_APP_NAME|CONTAINER_GROUP_NAME  DOMAIN  [-n HOST_NAME]
```

**前提条件**:  エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*CF_APP_NAME*|*CONTAINER_GROUP_NAME*  (必須):  cf アプリケーションまたはコンテナー・グループの名前。

*DOMAIN*  (必須):  経路のドメイン (例えば、mybluemix.net や ng.bluemix.net)。 

-n *HOST_NAME*  (オプション):  経路のホスト名。指定しない場合、ホスト名は、デフォルトではアプリ名またはコンテナー・グループ名に設定されます。

**例**:

以下は、「my-app」から「my-app.mybluemix.net」をマップ解除します。

```
bluemix network route-unmap my-app mybluemix.net
```

以下は、「my-container-group」から「abc.ng.bluexmix.net」をマップ解除します。

```
bluemix network route-unmap my-container-group ng.bluemix.net -n abc
```


## bluemix network route-create
このコマンドが持っている機能とオプションは「cf create-route」コマンドと同じです。


## bluemix network route-delete
このコマンドが持っている機能とオプションは「cf delete-route」コマンドと同じです。


## bluemix network orphaned-routes-delete
このコマンドが持っている機能とオプションは「cf delete-orphaned-routes」コマンドと同じです。


## bluemix network domains
このコマンドが持っている機能とオプションは「cf domains」コマンドと同じです。


## bluemix network domain-create
このコマンドが持っている機能とオプションは「cf create-domain」コマンドと同じです。


## bluemix network domain-delete
このコマンドが持っている機能とオプションは「cf delete-domain」コマンドと同じです。


## bluemix network shared-domain-create
このコマンドが持っている機能とオプションは「cf create-shared-domain」コマンドと同じです。


## bluemix network shared-domain-delete
このコマンドが持っている機能とオプションは「cf delete-shared-domain」コマンドと同じです。


## bluemix plugin repos
Bluemix CLI に登録されているプラグイン・リポジトリーをすべてリストします。

```
bluemix plugin repos
```

**前提条件**:  なし


## bluemix plugin repo-add
Bluemix CLI に新しいプラグイン・リポジトリーを追加します。

```
bluemix plugin repo-add REPO_NAME REPO_URL
```

**前提条件**:  なし

**コマンド・オプション**:

*REPO_NAME*  (必須):  追加するリポジトリーの名前。各リポジトリーには独自の名前を定義することができます。

*REPO_URL*  (必須):  追加するリポジトリーの URL。リポジトリー URL にはプロトコルを含めなければなりません (例えば、plugins.ng.bluemix.net ではなく、http://plugins.ng.bluemix.net とします)。http://plugins.ng.bluemix.net は、Bluemix CLI の公式プラグイン・リポジトリーです。

**例**:

以下は、Bluemix CLI の公式プラグイン・リポジトリーを「bluemix-repo」という名前で追加します。

```
bluemix plugin repo-add bluemix-repo http://plugins.ng.bluemix.net
```


## bluemix plugin repo-remove
Bluemix CLI からプラグイン・リポジトリーを削除します。

```
bluemix plugin repo-remove REPO_NAME
```

**前提条件**:  なし

**コマンド・オプション**:

*REPO_NAME*  (必須):  削除するリポジトリーの名前。

**例**:

以下は、Bluemix CLI から「bluemix-repo」リポジトリーを削除します。

```
bluemix plugin repo-remove bluemix-repo
```


## bluemix plugin repo-plugin-list
追加したすべてのリポジトリーまたは特定のリポジトリーで使用可能なプラグインをすべてリストします。

```
bluemix plugin repo-plugin-list [-r REPO_NAME]
```

**前提条件**:  なし

**コマンド・オプション**:

-r *REPO_NAME*  (オプション):  指定のリポジトリーに含まれているプラグインのみリストします。

**例**:

以下は、追加したすべてのリポジトリーに含まれているプラグインをすべてリストします。

```
bluemix plugin repo-plugin-list
```

以下は「bluemix-repo」リポジトリーに含まれているプラグインをすべてリストします。

```
bluemix plugin repo-plugin-list -r bluemix-repo
```


## bluemix plugin list
Bluemix CLI に含まれているインストール済みのプラグインをすべてリストします。

```
bluemix plugin list
```

**前提条件**:  なし


## bluemix plugin install
指定のパスまたはリポジトリーから Bluemix CLI にプラグインをインストールします。

```
bluemix plugin install PLUGIN_PATH|PLUGIN_NAME [-r REPO_NAME]
```

**前提条件**:  なし

**コマンド・オプション**:

*PLUGIN_PATH*|*PLUGIN_NAME*  (必須):  「-r *REPO_NAME*」を指定しない場合、プラグインは指定のローカル・パスまたはリモート URL からインストールされます。

-r *REPO_NAME*  (オプション):  プラグインのバイナリーが配置されているリポジトリーの名前。

**例**:

以下は、ローカル・ファイルからプラグインをインストールします。

```
bluemix plugin install /downloads/new_plugin
```

以下は、リモート URL からプラグインをインストールします。

```
bluemix plugin install http://plugins.ng.bluemix.net/downloads/new_plugin
```

以下は、「bluemix-repo」リポジトリーから「IBM-Containers」というプラグインをインストールします。

```
bluemix plugin install IBM-Containers -r bluemix-repo
```


## bluemix plugin uninstall
Bluemix CLI から指定のプラグインをアンインストールします。

```
bluemix plugin uninstall PLUGIN_NAME
```

**前提条件**:  なし

**コマンド・オプション**:

*PLUGIN_NAME*  (必須):  アンインストールするプラグインの名前。

**例**:

以下は、前にインストールした「IBM-Containers」というプラグインをアンインストールします。

```
bluemix plugin uninstall IBM-Containers
```
