---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry (cf) コマンド

*最終更新日: 2016 年 1 月 29 日*

Cloud Foundry (cf) コマンドを使用してアプリを管理できます。
{:shortdesc}

以下の情報は、アプリの管理に最も一般的に使用される cf コマンドをリストしています。すべての cf コマンドとそのヘルプ情報をリストするには、`cf help` を使用します。特定のコマンドの詳細なヘルプ情報を表示するには、`cf command_name -h` を使用します。

*注:* ネットワークに cf コマンドを実行するホストと Cloud Foundry API エンドポイント間の HTTP プロキシー・サーバーが含まれる場合は、`HTTP_PROXY` 環境変数を設定して、プロキシー・サーバーのホスト名または IP アドレスを指定する必要があります。詳しくは、[Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html) を参照してください。

## cf api

{{site.data.keyword.Bluemix_notm}} の API エンドポイントの URL を表示または指定します。```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>{{site.data.keyword.Bluemix_notm}} に接続するときに指定する必要のある Bluemix API エンドポイントの URL。通常、この URL は https://api.{DomainName} です。
現在使用している API エンドポイントの URL を表示したい場合、cf api コマンドにこのパラメーターを指定する必要はありません。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>SSL 検証プロセスを使用不可にします。このパラメーターを使用すると、セキュリティーの問題が起きる可能性があります。</dd>
<dt>*--unset*</dt>
<dd>すべての API エンドポイントの接続情報を削除します。</dd>
</dl>

## cf apps

現在のスペースにデプロイしたすべてのアプリケーションをリストします。各アプリケーションの状況も表示されます。

あるアプリのインスタンスが 1 つあるとすると、cf apps コマンドからの応答のインスタンス欄には、アプリが稼働している場合は 1/1、アプリがダウンしている場合は 0/1 が表示されます。アプリのインスタンスの状態が不明であることを示す ?/1 が表示される場合は、アプリの URL をブラウザーにコピーしてアプリが応答するかどうかをチェックできます。あるいは、`cf logs appname` コマンドを使用してログを追尾すれば、アプリがログ内容を生成しているかどうかが分かります。

## cf bind-service

既存のサービス・インスタンスをアプリケーションにバインドします。```
cf bind-service appname service_instance
```

例えば、現在の組織とスペースに `my_dataworks` という名前のサービス・インスタンスがある場合、
`cf bind-service my_app
my_dataworks` を使用してこのサービス・インスタンスをアプリケーションにバインドできます。

<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>service_instance</dt>
<dd>既存のサービス・インスタンスの名前。</dd>
</dl>

## cf create-service

サービス・インスタンスを作成します。```
cf create-service service_name service_plan service_instance
```
例えば、`cf create-service DataWorks free my_dataworks` を使用して、{{site.data.keyword.dataworks_short}} サービスのインスタンスを無料プランで作成できます。

<dl>
<dt>service_name</dt>
<dd>サービスの名前。</dd>
<dt>service_plan</dt>
<dd>サービス・プランの名前。</dd>
<dt>service_instance</dt>
<dd>作成する新規サービス・インスタンスに使用する名前。</dd>
</dl>

## cf create-space

スペースを作成します。
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>スペースの名前。</dd>
<dt>*-o*</dt>
<dd>その中にスペースを作成する組織の名前。</dd>
<dt>*-q*</dt>
<dd>新しく作成されるスペースに割り当てる割り当て量。指定されない場合、デフォルト割り当て量が自動的に割り当てられます。</dd>
</dl>

## cf delete

既存のアプリケーションを削除します。```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。<dd>
<dt>*-f*</dt>
<dd>確認を行わずに、アプリケーションを強制的に削除します。このパラメーターはオプションです。</dd>
<dt>*-r*</dt>
<dd>アプリケーションに関連付けられたすべてのドメイン・ネームを削除します。
このパラメーターはオプションです。</dd>
</dl>

## cf delete-space

スペースを削除します。
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>スペースの名前。</dd>
<dt>*-f*</dt>
<dd>確認を行わずに、スペースを強制的に削除します。このパラメーターはオプションです。</dd>
*注:* スペースの削除は、元に戻すことのできない操作です。
</dl>

## cf events

アプリケーションに関連するランタイム・イベントを表示します。```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
</dl>

## cf help

すべての cf コマンドのヘルプ情報を表示するか、または、command_name パラメーターが使用されている場合は特定の cf コマンドのヘルプ情報を表示します。
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>コマンドの名前。コマンドに固有のヘルプ情報が必要な場合は、このパラメーターを使用できます。</dd>
<dd>このパラメーターを指定しない場合は、すべての cf コマンドのヘルプ情報が表示されます。</dd>
</dl>


## cf login


{{site.data.keyword.Bluemix_notm}} にログインします。```
cf login```
cf login コマンドを実行するときには、以下のパラメーターの 1 つ以上を使用できます。
<dl>
<dt>*-a* https://api.{DomainName}
	 </dt>
<dd>{{site.data.keyword.Bluemix_notm}} の API エンドポイントの URL。このパラメーターはオプションです。</dd>
<dt>*-u*user_name</dt>
<dd>自分のユーザー名。このパラメーターはオプションです。</dd>
<dt>*-p*password</dt>
<dd>自分のパスワード。</dd>
<dd>*重要:* コマンド・ライン・インターフェースで *-p* パラメーターを使用してパスワードを指定すると、パスワードがコマンド・ライン履歴に記録される可能性があります。セキュリティー上の理由から、パスワードの指定には -p パラメーターを使用しないようにしてください。代わりに、コマンド・ライン・インターフェースでプロンプトが出された場合にパスワードを入力します。</dd>
<dt>*-o*organization_name</dt>
<dd>ログイン先の組織の名前。</dd>
<dt>*-s*space_name</dt>
<dd>ログイン先のスペースの名前。</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>SSL 検証プロセスを使用不可にします。このパラメーターを使用すると、セキュリティーの問題が起きる可能性があります。</dd>
</dl>

*注:* このコマンドの *-p* パラメーターでパスワードを指定すると、パスワードがシェル・コマンドのヒストリー・ファイルに記録される可能性があり、ローカル・オペレーティング・システムの他のユーザーに見られる可能性もあります。


## cf logs

アプリケーションの
STDOUT および STDERR ログ・ストリームを表示します。```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>*--recent*</dt>
<dd>最近のログを取得します。</dd>
</dl>

## cf marketplace

マーケットプレイスで提供されているすべてのサービスをリストします。このコマンドによってリストされるサービスは、{{site.data.keyword.Bluemix_notm}} カタログにも表示されます。
```
cf marketplace```

## cf push

新規アプリケーションを Bluemix にデプロイするか、または、Bluemix にある既存のアプリケーションを更新します。
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>*-b*buildpack_name</dt> <dd>ビルドパックの名前。buildpack_name には、カスタム・ビルドパックの名前または Git URL を指定できます。例えば、`my-buildpack` または `https://github.com/heroku/heroku-buildpack-play.git` とします。</dd>
<dt>*-c*start_command</dt> <dd>アプリケーションの開始コマンド。デフォルトの開始コマンドを使用するには、このオプションに値 null を指定します。例えば次のようにします。</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>このオプションを使用してスクリプト・ファイルを実行することもできます。以下に例を示します。```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f*manifest_path</dt> <dd>マニフェスト・ファイルへのパス。デフォルトのマニフェスト・ファイルは、アプリケーションのルート・ディレクトリーの下にある manifest.yml です。</dd>
<dt>*-i*instance_number</dt> <dd>インスタンスの番号。</dd>
<dt>*-k*disk_limit</dt> <dd>アプリケーションのディスクの制限。例えば、*256M*、*1024M*、または *1G* とします。</dd>
<dt>*-m*memory_limit</dt>
<dd>アプリケーションのメモリーの制限。例えば、*256M*、*1024M*、または *1G* とします。</dd>
<dt>*-n*host_name</dt>
<dd>アプリケーションのホスト名。例えば、*my-subdomain* とします。</dd>
<dt>*-p*app_path</dt> <dd>アプリケーション・ディレクトリーまたはアプリケーション・アーカイブ・ファイルへのパス。</dd>
<dt>*-t*timeout</dt> <dd>アプリケーションが開始するための最大時間 (秒単位)。他のサーバー・サイドのタイムアウトがこの値をオーバーライドする場合があります。</dd>
<dt>*-s* stackname</dt>
<dd>アプリケーションを実行するためのスタック。スタックは、オペレーション・システムを含む、事前ビルド済みのファイル・システムです。{{site.data.keyword.Bluemix_notm}} 内の使用可能なスタックを表示するには、`cf stacks` を使用します。</dd>
<dt>*--no-hostname*</dt> <dd>Bluemix システム・ドメインをこのアプリケーションにマップします。</dd>
<dt>*--no-manifest*</dt> <dd>デフォルトのマニフェスト・ファイルを無視します。</dd>
<dt>*--no-route*</dt> <dd>経路をこのアプリケーションにマップしません。</dd>
<dt>*--no-start*</dt> <dd>アプリケーションがデプロイされた後にアプリケーションを開始しません。</dd>
<dt>*--random-route*</dt> <dd>アプリケーションのランダムな経路を作成します。</dd>
</dl>

## cf scale

アプリケーションのインスタンス番号、ディスク・スペース制限、およびメモリー制限を表示または変更します。```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>*-i*instance_number</dt> <dd>インスタンスの番号。</dd>
<dt>*-k*disk_limit</dt> <dd>アプリケーションのディスクの制限。例えば、*256M*、*1024M*、または *1G* とします。</dd>
<dt>*-m*memory_limit</dt>
<dd>アプリケーションのメモリーの制限。例えば、*256M*、*1024M*、または *1G* とします。</dd>
<dt>*-f*</dt>
<dd>プロンプトを出さずに、アプリケーションを強制的に再始動します。</dd>
</dl>

## cf services

現在のスペースで使用可能なすべてのサービスをリストします。```
cf services```

## cf set-env

アプリケーションの環境変数を設定します。```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
<dt>var_name</dt>
<dd>環境変数の名前。</dd>
<dt>var_value</dt>
<dd>環境変数の値。</dd>
</dl>

## cf stacks

すべてのスタックがリストされます。スタックは、アプリを実行可能なオペレーティング・システムを含むビルド前のファイル・システムです。```
cf stacks```

## cf stop

アプリケーションを停止します。```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>アプリケーションの名前。</dd>
</dl>

## cf -v

cf コマンド・ライン・インターフェースのバージョンを表示します。```
cf -v
```

# 関連リンク
{: #rellinks}
## 一般 
{: #general}
* [クイック・リファレンス・カード - cf コマンド](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
