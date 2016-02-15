{:shortdesc: .shortdesc}

# {{site.data.keyword.Bluemix_notm}} と対話するための bx コマンド
{: #bluemix_cli}

*最終更新日:* 2016 年 1 月 5 日

{{site.data.keyword.Bluemix}} コマンド・ライン・インターフェース (CLI) では、ユーザーが {{site.data.keyword.Bluemix_notm}} と対話できるように、名前空間別にグループ化したコマンドのセットが提供されています。一部の {{site.data.keyword.Bluemix_notm}} CLI コマンドは既存の cf コマンドのラッパーであり、bx コマンドと呼ばれます。それ以外は {{site.data.keyword.Bluemix_notm}} に固有のものです。以下の説明では、{{site.data.keyword.Bluemix_notm}} CLI によってサポートされるすべてのコマンドをリストし、名前、オプション、使用法、前提条件、説明、および例を示します。
{:shortdesc}
 
**注:** *前提条件*には、コマンドを使用する前に必要なアクションがリストされています。前提条件となるアクションのないコマンドでは、**なし**とリストされています。それ以外の場合、前提条件には以下のアクションのうちの 1 つ以上が含まれます。
<dl>
<dt>エンドポイント</dt>
<dd>このコマンドを使用する前に、<code>bluemix api</code> を介して API エンドポイントを設定する必要があります。</dd>
<dt>login</dt>
<dd>このコマンドを使用する前に、<code>bluemix login</code> コマンドを使用してログインする必要があります。</dd>
<dt>ターゲット</dt>
<dd>このコマンドを使用する前に、<code>bluemix target</code> コマンドを使用して組織およびスペースを設定する必要があります。</dd>
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

現行の組織を `MyOrg` に、スペースを `MySpace` に設定します。

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





## bluemix regions
{{site.data.keyword.Bluemix_notm}} のすべての地域の情報を表示します。

```
bluemix regions```

**前提条件**: エンドポイント


## bluemix region-set
指定された地域に切り替えます。このコマンドは、可能な場合、新しい地域の同じ組織およびスペースに自動的にターゲットを変更します。さもなければ、コマンドは、ユーザーが既にログインしている場合、新しい組織とスペースを選択するようユーザーにプロンプトを出します。API エンドポイントはそれに合わせて変更されます。

```
bluemix region-set REGION_NAME
```

**前提条件**: エンドポイント

**コマンド・オプション**:

*REGION_NAME* (required):  (必須): 切り替える先の地域の名前。`bluemix regions` コマンドを使用してすべての地域名を表示できます。

**例**:

現行地域を `eu-gb` に設定します。

```
bluemix region-set eu-gb
```



## bluemix config
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

一度に指定できるのは、`apps`、`containers`、`container-groups`、または `vm-groups` のいずれか 1 つのみです。これらのどれも指定されない場合、すべての cf アプリケーション、コンテナー、コンテナー・グループ、および VM グループがリストされます。

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
{{site.data.keyword.Bluemix_notm}} への未加工 HTTP 要求を実行します。*Content-Type* はデフォルトで *application/json* に設定されます。このコマンドは、cf API エンドポイント (例えば、https://api.ng.bluemix.net) ではなく、{{site.data.keyword.Bluemix_notm}} コンソール・サーバー (例えば、https://console.ng.bluemix.net) に要求を送信します。

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
このコマンドの機能とオプションは、組織が存在する地域も表示される点を除き、`cf orgs` コマンドと同じです。


## bluemix iam org
このコマンドの機能とオプションは、組織が存在する地域も表示される点を除き、`cf org` コマンドと同じです。


## bluemix iam org-create
このコマンドの機能とオプションは `cf create-org` コマンドと同じです。





## bluemix iam org-replicate
現在の地域から別の地域に組織を複製します。

```
bluemix iam org-replicate ORG_NAME REGION_NAME
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*ORG_NAME* (必須):  複製する、既存の組織の名前。

*REGION_NAME*  (必須):  複製された組織をホストする地域の名前。

**例**:

次のように、組織 `OE_Runtimes_Scaling` を地域 `eu-gb` に複製します。

```
bluemix iam org-replicate OE_Runtimes_Scaling eu-gb
```














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

-d (オプション): `-d` オプションが指定されている場合、各テンプレートの説明も表示されます。それ以外の場合、各テンプレートの ID および名前のみが表示されます。


## bluemix catalog template-run
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




## bluemix catalog template-register

{{site.data.keyword.Bluemix_notm}} に新しいボイラープレート・テンプレートを登録します。

```
bluemix catalog template-register TEMPLATE_ID TEMPLATE_URL
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*TEMPLATE_ID* (必須):  新しい登録済みテンプレートの ID。

*TEMPLATE_URL* (必須):  新しいテンプレートのメタデータをホストする URL。

**例**:

`javaHelloWorld` という名前でテンプレートを作成するには、以下のように指定します。

```
bluemix catalog template-register javaHelloWorld http://javaHelloWorld.ng.bluemix.net/info
```

## bluemix catalog template-deregister

既存のボイラープレート・テンプレートを登録解除します。

```
bluemix catalog template-deregister TEMPLATE_ID [-f]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*TEMPLATE_ID* (必須):  すべてのテンプレート ID を表示するには、`bluemix catalog templates`を使用します。

-f  (オプション):  確認なしで登録解除を強制します。

**例**:

確認なしでテンプレート `javaHelloWorld` を登録解除するには、以下のように指定します。

```
bluemix catalog template-deregister javaHelloWorld -f
```


## bluemix catalog template-registry
{{site.data.keyword.Bluemix_notm}} テンプレート・レジストリーを表示します。

```
bluemix catalog template-registry```

**前提条件**: エンドポイント









## bluemix catalog service-broker

指定したサービス・ブローカーの情報を表示します。

```
bluemix catalog service-broker SERVICE_BROKER_NAME
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*SERVICE_BROKER_NAME* (必須):  アクセスするサービス・ブローカーの名前。


## bluemix catalog service-broker-create
{: #bluemix_catalog_service_broker_create}
サービス・ブローカーを作成します。

```
bluemix catalog service-broker-create SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE [--no-billing]
```

**前提条件**:  エンドポイント、ログイン

**コマンド・オプション**:

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (必須):  作成する新規サービス・ブローカーを記述する JSON。JSON ファイル名を使用するか、JSON テキストを直接使用できます。

--no-billing (オプション):  このオプションが指定されている場合、このサービス・ブローカーに対する請求は使用不可になります。 

**例**:

JSON ファイルを使用してサービス・ブローカーを作成するには、以下のように指定します。

```
bluemix catalog service-broker-create ./broker.json
```

JSON テキストを使用し、請求なしで、新規サービス・ブローカーを作成するには、以下のように指定します。

```
bluemix catalog service-broker-create '{"name":"test_broker", ...}' --no-billing
```

以下の例は、すべての必須フィールドが指定された、サービス・ブローカーの JSON を示しています。

```
{
    "name": "my_broker",  // the name of service broker
    "broker_url": "http://my_broker.ng.bluemix.net"  // the URL that points to the metadata of service broker
    "auth_username": "username",
	"auth_password": "password",  // The user name and password to visit the service broker url. User name and password should be sent with HTTP basic authorization.
    "visibilities": [
        {"organization_name": "OE_Runtimes_Scaling"}
    ]
}
```


## bluemix catalog service-broker-update
既存のサービス・ブローカーを更新します。

```
bluemix catalog service-broker-update ORIGINAL_BROKER_NAME SERVICE_BROKER_JSON_TEXT|SERVICE_BROKER_JSON_FILE
```

**前提条件**:  エンドポイント、ログイン

**コマンド・オプション**:

*ORIGINAL_BROKER_NAME* (必須):  更新するサービス・ブローカーの名前。

*SERVICE_BROKER_JSON_TEXT*|*SERVICE_BROKER_JSON_FILE* (必須):  サービス・ブローカーを記述する、新しい JSON。JSON ファイル名を使用するか、JSON テキストを直接使用できます。

**例**:

既存のサービス・ブローカー `auto-scaling` を更新するには、以下のように指定します。

```
bluemix catalog service-broker-update auto-scaling ./auto-scaling.json
```

サービス・ブローカーの JSON フォーマットについて詳しくは、『[bluemix catalog service-broker-create](#bluemix_catalog_service_broker_create)』を参照してください。


## bluemix catalog service-broker-delete

指定したサービス・ブローカーを削除します。

```
bluemix catalog service-broker-delete SERVICE_BROKER_NAME [-f]
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*SERVICE_BROKER_NAME* (必須):  削除するサービス・ブローカーの名前。

-f  (オプション):  確認なしで削除を強制します。

**例**:

確認なしでサービス・ブローカー `auto-scaling` を削除するには、以下のように指定します。

```
bluemix catalog service-broker-delete auto-scaling -f
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

指定されたドメインで `my-app` に経路をマップします。

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

`my-app.mybluemix.net` を `my-app` からマップ解除するには、以下のように指定します。

```
bluemix network route-unmap my-app mybluemix.net
```

`abc.ng.bluexmix.net` を `my-container-group` からマップ解除するには、以下のように指定します。

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




## bluemix security cert

指定したホストの証明書情報をリストします。

```
bluemix security cert HOST_NAME
```

**前提条件**: エンドポイント、ログイン

**コマンド・オプション**:

*HOST_NAME* (必須):  証明書をホストするサーバーの名前。

**例**:

ホスト `ibmcxo-eventconnect.com` 上の証明書を表示するには、以下のように指定します。

```
bluemix security cert ibmcxo-eventconnect.com
```


## bluemix security cert-add

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
現在の組織内の、指定したドメインから証明書を削除します。

```
bluemix security cert-remove DOMAIN [-f]
```

**前提条件**: エンドポイント、ログイン、ターゲット

**コマンド・オプション**:

*DOMAIN* (必須):  証明書を削除するドメイン。

-f  (オプション):  確認なしで削除を強制します。








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

Bluemix CLI の公式プラグイン・リポジトリーを `bluemix-repo` として追加します。

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

{{site.data.keyword.Bluemix_notm}} CLI から `bluemix-repo` リポジトリーを削除します。

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

`bluemix-repo` リポジトリー内のすべてのプラグインをリストします。

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
