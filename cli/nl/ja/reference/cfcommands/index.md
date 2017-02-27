---



copyright:

  years: 2016, 2017

lastupdated: "2017-01-12"


---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}


# Cloud Foundry (cf) コマンド
{: #cf}

Cloud Foundry (cf) コマンド・ライン・インターフェース (CLI) は、アプリを管理するための一連のコマンドを提供します。以下の情報では、アプリを管理するために最もよく使用される cf コマンドをリストし、コマンドの名前、オプション、使用法、前提条件、説明、および例を示します。すべての cf コマンドと関連ヘルプ情報をリストするには、`cf help` を使用します。特定のコマンドの詳細なヘルプ情報を表示するには、`cf command_name -h` を使用します。
{: shortdesc}

**注**: ネットワークに cf コマンドを実行するホストと Cloud Foundry API エンドポイント間の HTTP プロキシー・サーバーが含まれる場合は、`HTTP_PROXY` 環境変数を設定して、プロキシー・サーバーのホスト名または IP アドレスを指定する必要があります。詳しくは、[Using the cf CLI with an HTTP Proxy Server ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html){: new_window} を参照してください。


## Cloud Foundry CLI コマンドの索引
{: #CLIname_commands_index}

以下の表の索引を使用して、使用頻度の高い Cloud Foundry コマンドを参照してください。

<table summary="アルファベット順の汎用 Cloud Foundry コマンド (コマンドの詳細情報を表示するリンクが含まれています)">
 <caption>表 1. 汎用 Cloud Foundry コマンド</caption>
 <thead>
 <th colspan="6">汎用 Cloud Foundry コマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[api](/docs/cli/reference/cfcommands/index.html#cf_api)</td>
 <td>[help](/docs/cli/reference/cfcommands/index.html#cf_help)</td>
 <td>[login](/docs/cli/reference/cfcommands/index.html#cf_login)</td>
 <td>[stacks](/docs/cli/reference/cfcommands/index.html#cf_stacks)</td>
 <td>[target](/docs/cli/reference/cfcommands/index.html#cf_target)</td>
 <td>[-v ](/docs/cli/reference/cfcommands/index.html#cf_v)</td>
 </tr>
   </tbody>
 </table>


<table summary="アプリ、スペース、およびサービスを管理するためのアルファベット順のコマンド。各コマンドには、コマンドの詳細を表示するリンクが含まれています。">
 <caption>表 2. アプリ、スペース、およびサービスを管理するためのコマンド</caption>
 <thead>
 <th colspan="5">アプリ、スペース、およびサービスを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[apps](/docs/cli/reference/cfcommands/index.html#cf_apps)</td>
 <td>[bind-service](/docs/cli/reference/cfcommands/index.html#cf_bind-service)</td>
 <td>[create-service](/docs/cli/reference/cfcommands/index.html#cf_create-service)</td>
 <td>[create-space](/docs/cli/reference/cfcommands/index.html#cf_create-space)</td>
 <td>[delete](/docs/cli/reference/cfcommands/index.html#cf_delete)</td>
  </tr>
 <tr>
 <td>[delete-space](/docs/cli/reference/cfcommands/index.html#cf_delete-space)</td>
 <td>[events](/docs/cli/reference/cfcommands/index.html#cf_events)</td>
 <td>[logs](/docs/cli/reference/cfcommands/index.html#cf_logs)</td>
 <td>[marketplace](/docs/cli/reference/cfcommands/index.html#cf_marketplace)</td>
 <td>[push](/docs/cli/reference/cfcommands/index.html#cf_push)</td>
  </tr>
 <tr>
 <td>[scale](/docs/cli/reference/cfcommands/index.html#cf_scale)</td>
 <td>[services](/docs/cli/reference/cfcommands/index.html#cf_services)
 <td>[set-env](/docs/cli/reference/cfcommands/index.html#cf_set-env)</td>
 <td>[ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh)</td>
 <td>[stop](/docs/cli/reference/cfcommands/index.html#cf_stop)</td>
 </tr>
 </tbody>
 </table>

## cf api
{: #cf_api}

このコマンドを使用して、{{site.data.keyword.Bluemix_notm}} の API エンドポイントの URL を表示または指定します。

```
cf api [BluemixServerURL] [--skip-ssl-validation] [--unset]
```

<strong>前提条件</strong>: なし。

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>BluemixServerURL (オプション)</dt>
   <dd>{{site.data.keyword.Bluemix_notm}} に接続するときに指定する必要のある Bluemix API エンドポイントの URL。通常、この URL は `https://api.{DomainName}` です。現在使用している API エンドポイントの URL を表示したい場合、cf api
コマンドにこのパラメーターを指定する必要はありません。</dd>
   <dt>* --skip-ssl-validation</dt>
   <dd>SSL 検証プロセスを使用不可にします。このパラメーターを使用すると、セキュリティーの問題が起きる可能性があります。</dd>
   <dt>* --unset</dt>
   <dd>すべての API エンドポイントの接続情報を削除します。</dd>
    </dl>

<strong>例</strong>:

現行 API エンドポイントを表示します。
```
cf api
```
{: codeblock}

api.ng.bluemix.net のすべての API エンドポイントへの接続を削除します。
```
cf api api.ng.bluemix.network --unset
```
{: codeblock}

api.ng.bluemix.network の SSL 検証プロセスを無効にします。
```
cf api api.ng.bluemix.network --skip-ssl-validation
```
{: codeblock}


## cf apps
{: #cf_apps}

現在のスペースにデプロイしたすべてのアプリケーションをリストします。各アプリケーションの状況も表示されます。

あるアプリのインスタンスが 1 つあるとすると、cf apps コマンドからの応答のインスタンス欄には、アプリが稼働している場合は 1/1、アプリがダウンしている場合は 0/1 が表示されます。アプリのインスタンスの状態が不明であることを示す ?/1 が表示される場合は、アプリの URL をブラウザーにコピーしてアプリが応答するかどうかをチェックできます。あるいは、`cf logs appname` コマンドを使用してログを追尾すれば、アプリがログ内容を生成しているかどうかが分かります。

```
cf apps
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`


## cf bind-service
{: #cf_bind-service}

既存のサービス・インスタンスをアプリケーションにバインドします。

```
cf bind-service appname service_instance
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>appname (必須)</dt>
   <dd>アプリケーションの名前。</dd>
   <dt>service_instance (必須)</dt>
   <dd>既存のサービス・インスタンスの名前。</dd>
    </dl>

<strong>例</strong>:

`my_dataworks` という名前のサービス・インスタンスを `my_app` という名前のアプリにバインドします。
```
cf bind-service my_app my_dataworks
```
{: codeblock}


## cf create-service
{: #cf_create-service}

サービス・インスタンスを作成します。

```
cf create-service service_name service_plan service_instance
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>service_name (必須)</dt>
   <dd>サービスの名前。</dd>
   <dt>service_plan (必須)</dt>
   <dd>サービス・プランの名前。</dd>
   <dt>service_instance (必須)</dt>
   <dd>作成する新規サービス・インスタンスに使用する名前。</dd>
    </dl>

<strong>例</strong>:

`free` プランの {{site.data.keyword.dataworks_short}} サービスのインスタンスを作成します。
```
cf create-service DataWorks free my_dataworks
```
{: codeblock}


## cf create-space
{: #cf_create-space}

スペースを作成します。


```
cf create-space space_name [-o] [-q]
```

<strong>前提条件</strong>: `cf api`、`cf login`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>space_name (必須)</dt>
   <dd>スペースの名前。</dd>
   <dt>*-o* (オプション)</dt>
   <dd>その中にスペースを作成する組織の名前。</dd>
   <dt>*-q* (オプション)</dt>
   <dd>新しく作成されるスペースに割り当てる割り当て量。指定されない場合、デフォルト割り当て量が自動的に割り当てられます。</dd>
    </dl>

<strong>例</strong>:

new_space という名前のスペースを作成します。
```
cf create-space new_space
```
{: codeblock}


## cf delete
{: #cf_delete}

既存のアプリケーションを削除します。

```
cf delete appname [-f] [-r]
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>appname (必須)</dt>
   <dd>アプリケーションの名前。</dd>
   <dt>*-f* (オプション)</dt>
   <dd>確認を行わずに、アプリケーションを強制的に削除します。</dd>
   <dt>*-r* (オプション)</dt>
   <dd>アプリケーションに関連付けられたすべてのドメイン・ネームを削除します。
</dd>
    </dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションを削除します (確認が必要)。
```
cf delete my_app
```
{: codeblock}

`my_app` という名前のアプリケーションを削除します (確認は不要)。
```
cf delete my_app -f
```
{: codeblock}

`my_app` という名前のアプリケーション、および `my_app` に関連付けられているすべてのドメイン・ネームを削除します。
```
cf delete my_app -r
```
{: codeblock}

`my_app` という名前のアプリケーション、および `my_app` に関連付けられているすべてのドメイン・ネームを削除します (確認は不要)。
```
cf delete my_app -f -r
```
{: codeblock}


## cf delete-space
{: #cf_delete-space}

スペースを削除します。


```
cf delete-space space_name [-f]
```

<strong>前提条件</strong>: `cf api`、`cf login`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>space_name (必須)</dt>
   <dd>スペースの名前。</dd>
   <dt>*-f* (オプション)</dt>
   <dd>確認を行わずに、スペースを強制的に削除します。</dd>
   *注:* スペースの削除は、元に戻すことのできない操作です。
</dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションを削除します (確認が必要)。
```
cf delete my_app
```
{: codeblock}

`my_app` という名前のアプリケーションを削除します (確認は不要)。
```
cf delete my_app -f
```
{: codeblock}

`my_app` という名前のアプリケーション、および `my_app` に関連付けられているすべてのドメイン・ネームを削除します。
```
cf delete my_app -r
```
{: codeblock}

`my_app` という名前のアプリケーション、および `my_app` に関連付けられているすべてのドメイン・ネームを削除します (確認は不要)。
```
cf delete my_app -f -r
```
{: codeblock}


## cf events
{: #cf_events}

アプリケーションに関連するランタイム・イベントを表示します。

```
cf events [appname]
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>appname</dt>
   <dd>アプリケーションの名前。</dd>
   </dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションのイベントを表示します。
```
cf events my_app
```
{: codeblock}


## cf help
{: #cf_help}

すべての cf コマンドのヘルプ情報または特定の cf コマンドのヘルプ情報を表示します。

```
cf help [command_name]
```

<strong>前提条件</strong>: なし。

<strong>コマンド・オプション</strong>:

   <dl>
   <dt>command_name (オプション)</dt>
   <dd>コマンドの名前。</dd>
    </dl>

<strong>例</strong>:

すべての cf コマンドのヘルプ情報を表示します。
```
cf help
```
{: codeblock}

events コマンドのヘルプ情報を表示します。
```
cf help events
```
{: codeblock}


## cf login
{: #cf_login}


{{site.data.keyword.Bluemix_notm}} にログインします。

**注:** [フェデレーテッド ID](/docs/admin/account.html#signup) でログインする場合は、シングル・サインオン (SSO) パラメーターを使用してログインする必要があります。

```
cf login [-a url] [-u user_name] [-p password] [-sso] [-o organization_name] [-s space_name] [--skip-ssl-validation]
```

<strong>前提条件</strong>: なし。

<strong>コマンド・オプション</strong>:

<dl>
<dt>*-a* https://api.{DomainName} (オプション)</dt>
<dd>{{site.data.keyword.Bluemix_notm}} の API エンドポイントの URL。</dd>
<dt>*-u* user_name (オプション)</dt>
<dd>自分のユーザー名。</dd>
<dt>*-p* password (オプション)</dt>
<dd>自分のパスワード。</dd>
<dd>*重要:* コマンド・ライン・インターフェースで *-p* パラメーターを使用してパスワードを指定すると、パスワードがコマンド・ライン履歴に記録される可能性があります。セキュリティー上の理由から、パスワードの指定には -p パラメーターを使用しないようにしてください。代わりに、コマンド・ライン・インターフェースでプロンプトが出された場合にパスワードを入力します。</dd>
<dt>*-sso*</dt>
<dd>フェデレーテッド ID でログインする場合は、シングル・サインオン・オプション (SSO) を使用する必要があります。IBMid でログインする場合は、その必要はありません。フェデレーテッド ID でサインインしようとしたときに SSO パラメーターを指定していない場合、SSO パラメーターを含めるように求めるプロンプトが出されます。SSO パラメーターを使用すると、ログイン時にワンタイム・パスコードの入力を求められます。</dd>
<dt>*-o*organization_name</dt>
<dd>ログイン先の組織の名前。</dd>
<dt>*-s*space_name</dt>
<dd>ログイン先のスペースの名前。</dd>
<dt>*--skip-ssl-validation* (オプション)</dt>
<dd>SSL 検証プロセスを使用不可にします。このパラメーターを使用すると、セキュリティーの問題が起きる可能性があります。</dd>
</dl>

*注:* このコマンドの *-p* パラメーターでパスワードを指定すると、パスワードがシェル・コマンドのヒストリー・ファイルに記録される可能性があり、ローカル・オペレーティング・システムの他のユーザーに見られる可能性もあります。

<strong>例</strong>:

{{site.data.keyword.Bluemix_notm}} にログインします。
```
cf login
```
{: codeblock}

定義されているエンドポイント `https://api.ng.bluemix.net` を使用して {{site.data.keyword.Bluemix_notm}} にログインします。
```
cf login -a https://api.ng.bluemix.net
```
{: codeblock}

定義されているエンドポイント `https://api.ng.bluemix.net` およびユーザー名 `user_name` を使用し、セキュリティーのためのパスワードを指定せずに、{{site.data.keyword.Bluemix_notm}} にログインします。
```
cf login -a https://api.ng.bluemix.net -u user_name
```
{: codeblock}

定義されているエンドポイント `https://api.ng.bluemix.net`、ユーザー名 `user_name`、組織名 `org_name`、およびスペース名 `space_name` を使用し、セキュリティーのためのパスワードを指定せずに、{{site.data.keyword.Bluemix_notm}} にログインします。
```
cf login -a https://api.ng.bluemix.net -u user_name -o org_name -s space_name
```
{: codeblock}


## cf logs
{: #cf_logs}

アプリケーションの
STDOUT および STDERR ログ・ストリームを表示します。

```
cf logs appname [--recent]
```
<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>*--recent* (オプション)</dt>
<dd>最近のログを取得します。</dd>
</dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションのログ・ストリームを表示します。
```
cf logs my_app
```
{: codeblock}

`my_app` という名前のアプリケーションの最近のログ・ストリームを表示します。
```
cf logs my_app --recent
```
{: codeblock}


## cf marketplace
{: #cf_marketplace}

マーケットプレイスで提供されているすべてのサービスをリストします。このコマンドによってリストされるサービスは、{{site.data.keyword.Bluemix_notm}} カタログにも表示されます。


```
cf marketplace
```
<strong>前提条件</strong>: `cf api`

<strong>コマンド・オプション</strong>: なし。

<strong>例</strong>:

マーケットプレイスのすべてのサービスをリストします。
```
cf marketplace
```
{: codeblock}


## cf push
{: #cf_push}

新規アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイするか、{{site.data.keyword.Bluemix_notm}} 内の既存のアプリケーションを更新します。

```
cf push appname [-b buildpack_name] [-c start_command] [-f manifest_path] [-i instance_number] [-k disk_limit] [-m memory_limit] [-n host_name] [-p app_path] [-s stack_name] [-t timeout_length] [--no-hostname] [--no-manifest] [--no-route] [--no-start] [--random-route]
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname (必須)</dt>
<dd>アプリケーションの名前。</dd>
<dt>*-b* buildpack_name (オプション)</dt>
<dd>ビルドパックの名前。buildpack_name には、カスタム・ビルドパックを、名前 (例: liberty-for-java) または Git URL (例: https://github.com/cloudfoundry/java-buildpack.git) で指定するか、または、ブランチまたはタグを伴う Git URL (例えば、v3.3.0 タグの場合は https://github.com/cloudfoundry/java-buildpack.git#v3.3.0) で指定できます。</dd>
<dt>*-c* start_command (オプション)</dt>
<dd>アプリケーションの開始コマンド。デフォルトの開始コマンドを使用するには、このオプションに値 null を指定します。</dd>
<dt>*-f* manifest_path (オプション)</dt>
<dd>マニフェスト・ファイルへのパス。デフォルトのマニフェスト・ファイルは、アプリケーションのルート・ディレクトリーの下にある manifest.yml です。</dd>
<dt>*-i* instance_number (オプション)</dt>
<dd>インスタンスの番号。</dd>
<dt>*-k* disk_limit (オプション)</dt>
<dd>アプリケーションのディスク制限。可能な値は、*256M*、*1024M*、または *1G* です。</dd>
<dt>*-m* memory_limit (オプション)</dt>
<dd>アプリケーションのメモリー制限。可能な値は、*256M*、*1024M*、または *1G* です。</dd>
<dt>*-n* host_name (オプション)</dt>
<dd>アプリケーションのホスト名。例えば、*my-subdomain* とします。</dd>
<dt>*-p* app_path (オプション)</dt>
<dd>アプリケーション・ディレクトリーまたはアプリケーション・アーカイブ・ファイルへのパス。</dd>
<dt>*-s* stack_name (オプション)</dt>
<dd>アプリケーションを実行するためのスタック。スタックは、オペレーション・システムを含む、事前ビルド済みのファイル・システムです。{{site.data.keyword.Bluemix_notm}} 内の使用可能なスタックを表示するには、`cf stacks` を使用します。</dd>
<dt>*-t* timeout (オプション)</dt>
<dd>アプリケーションが開始するための最大時間 (秒単位)。他のサーバー・サイドのタイムアウトがこの値をオーバーライドする場合があります。</dd>
<dt>*--no-hostname* (オプション)</dt>
<dd>{{site.data.keyword.Bluemix_notm}} システム・ドメインをこのアプリケーションにマップします。</dd>
<dt>*--no-manifest* (オプション)</dt>
<dd>デフォルトのマニフェスト・ファイルを無視します。</dd>
<dt>*--no-route* (オプション)</dt>
<dd>経路をこのアプリケーションにマップしません。</dd>
<dt>*--no-start* (オプション)</dt>
<dd>アプリケーションがデプロイされた後にアプリケーションを開始しません。</dd>
<dt>*--random-route* (オプション)</dt>
<dd>アプリケーションのランダムな経路を作成します。</dd>
</dl>

<strong>例</strong>:

デフォルトの開始コマンドで `my_app` という名前のアプリケーションを開始します。
```
cf push `my_app` -c null
```
{: codeblock}

`run.sh` という名前のスクリプト・ファイルを実行するオプションを指定して、`my_app` という名前のアプリケーションを開始します。
```
cf push `my_app` -c "bash ./<run.sh>"
```
{: codeblock}



## cf scale
{: #cf_scale}

アプリケーションのインスタンス番号、ディスク・スペース制限、およびメモリー制限を表示または変更します。

```
cf scale appname [-i instance_number] [-k disk_limit] [-m memory_limit] [-f]
```

<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname (必須)</dt>
<dd>アプリケーションの名前。</dd>
<dt>*-i* instance_number (オプション)</dt>
<dd>インスタンスの番号。</dd>
<dt>*-k* disk_limit (オプション)</dt>
<dd>アプリケーションのディスク制限。可能な値は、`256M`、`1024M`、または `1G` です。</dd>
<dt>*-m* memory_limit (オプション)</dt>
<dd>アプリケーションのメモリー制限。可能な値は、`256M`、`1024M`、または `1G` です。</dd>
<dt>*-f* (オプション)</dt>
<dd>プロンプトを出さずに、アプリケーションを強制的に再始動します。</dd>
</dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションのインスタンス数、ディスク・スペース制限、およびメモリー制限を表示します。
```
cf scale my_app
```
{: codeblock}

`my_app` という名前のアプリのインスタンス数を `1234` に、ディスク・スペース制限を `1G` に、メモリー制限を `1G` に変更します。
```
cf scale appname -i 1234 -k 1G -m 1G
```
{: codeblock}


## cf services
{: #cf_services}

現在のスペースで使用可能なすべてのサービスをリストします。

```
cf services
```
<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>: なし。

<strong>例</strong>:

現在のスペース内のすべてのサービスをリストします。
```
cf services
```
{: codeblock}


## cf set-env
{: #cf_set-env}

アプリケーションの環境変数を設定します。

```
cf set-env appname var_name var_value
```
<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname (必須)</dt>
<dd>アプリケーションの名前。</dd>
<dt>var_name (必須)</dt>
<dd>環境変数の名前。</dd>
<dt>var_value (必須)</dt>
<dd>環境変数の値。</dd>
</dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションに対して、値 `123` を指定して `variable_a` という名前の環境変数を設定します。
```
cf set-env my_app variable_a 123
```
{: codeblock}


## cf ssh
{: #cf_ssh}

アプリケーション・コンテナーに安全にアクセスします。`cf ssh` コマンドを使用して、特定のアプリケーション・コンテナー・インスタンスでの、対話式 SSH セッションのセットアップ、リモート・コマンドの実行、ファイルの転送、およびポート転送のセットアップを行うことができます。

```
cf ssh
```
<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

デフォルトでは、Diego アプリケーションには SSH アクセスが有効になります。`cf ssh-enabled` コマンドを使用して SSH アクセスが有効かどうかを検証することができ、アクセスが無効であった場合は `cf enable-ssh` コマンドを使用して有効にすることができます。 

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>-c</dt>
<dd>実行するリモート・コマンドを指定します。</dd>
<dt>-i</dt>
<dd>アプリケーションの特定インスタンスを対象にします。指定されないと、アプリケーションの最初のインスタンス (索引 0 のインスタンス) が使用されます。</dd>
<dt>-L</dt>
<dd>マシン上の出力ポートをアプリケーション VM 上の入力ポートにバインドするローカル・ポート転送を有効にします。</dd>
<dt>-N</dt>
<dd>リモート・コマンドを実行しません。</dd>
<dt>-t、-tt、または -T</dt>
<dd>端末回線出力を生成するのではなく、擬似 tty モードで SSH セッションを実行できるようにします。<dd>
</dl>

<strong>例</strong>:

`my_app` アプリケーションを実行しているコンテナー・インスタンスとの対話式 SSH セッションを開始します。
```
$ cf ssh my_app
```
{: codeblock}

`my_app` アプリケーション・コンテナー・インスタンス上で単一のコマンドを実行します。
```
$ cf ssh my_app -c "ls -l"
```

`my_app` アプリケーション・コンテナー・インスタンスから単一のファイルを転送します。
```
$ cf ssh my_app -c "/bin/cat logs/messages.log" > messages.log
```

ローカル・マシンの 7777 ポートから `my_app` アプリケーション・コンテナー・インスタンスの 8888 ポートへのポート転送をセットアップします。
```
$ cf ssh -N -T -L 7777:localhost:8888 my_app

```

## cf stacks
{: #cf_stacks}

すべてのスタックがリストされます。スタックは、アプリを実行できるオペレーティング・システムを含む、ビルド前のファイル・システムです。

```
cf stacks
```
<strong>前提条件</strong>: `cf api`、`cf login`

<strong>コマンド・オプション</strong>: なし。

<strong>例</strong>:

すべてのスタックをリストします。
```
cf stacks
```
{: codeblock}


## cf stop
{: #cf_stop}

アプリケーションを停止します。

```
cf stop appname
```
<strong>前提条件</strong>: `cf api`、`cf login`、`cf target`

<strong>コマンド・オプション</strong>:

<dl>
<dt>appname (必須)</dt>
<dd>アプリケーションの名前。</dd>
</dl>

<strong>例</strong>:

`my_app` という名前のアプリケーションを停止します。
```
cf stop my_app
```
{: codeblock}


## cf target
{: #cf_target}

ターゲットの組織またはスペースを設定または表示します。

```
cf target [-o org_name] [-s space_name]
```
<strong>前提条件</strong>: `cf api`、`cf login`

<strong>コマンド・オプション</strong>:

<dl>
<dt>-o *org_name* (オプション)</dt>
<dd>スペースがある組織の名前。</dd>
<dt>-s *space_name* (オプション)</dt>
<dd>スペースの名前。</dd>
</dl>

<strong>例</strong>:

「my_org」という名前の組織および「my_space」という名前のスペースにターゲットを設定します。
```
cf target -o my_org -s my_space
```
{: codeblock}


## cf -v
{: #cf_v}

cf コマンド・ライン・インターフェースのバージョンを表示します。

```
cf -v
```
<strong>前提条件</strong>: なし。<strong>コマンド・オプション</strong>: なし。

<strong>例</strong>:

cf コマンド・ライン・インターフェースのバージョンを表示します。
```
cf -v
```
{: codeblock}



# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [Cloud Foundry CLI のダウンロード ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}
* [クイック・リファレンス・カード - cf コマンド ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/cf_cli_refcard.html){: new_window}
