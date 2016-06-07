---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#アプリのデプロイ
{: #deployingapps}

*最終更新日: 2016 年 5 月 9 日*

{{site.data.keyword.Bluemix}} へのアプリケーションのデプロイは、コマンド・ライン・インターフェースや統合開発環境 (IDE) など、さまざまな方法で行うことができます。また、アプリケーション・マニフェストを使用してアプリケーションをデプロイすることも可能です。アプリケーション・マニフェストを使用することで、アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイする度に指定しなければならないデプロイメント詳細の数を減らします。
{:shortdesc}

##アプリケーション・デプロイメント
{: #appdeploy}

アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイする工程には、2 つの段階があります。アプリケーションをステージングする段階、およびアプリケーションを開始する段階です。

###アプリケーションのステージング

ステージングの段階では、Droplet Execution Agent (DEA) が cf コマンド・ライン・インターフェースまたは `manifest.yml` ファイルでユーザーが指定した情報を使用して、アプリケーションのステージング用に何を作成するかを決定します。DEA は、アプリケーションのステージングのために適切なビルドパックを選択します。このステージング・プロセスの結果が Droplet です。{{site.data.keyword.Bluemix_notm}} へのアプリケーションのデプロイについて詳しくは、[{{site.data.keyword.Bluemix_notm}} アーキテクチャー、{{site.data.keyword.Bluemix_notm}} の動作](../public/index.html#publicarch)を参照してください。

ステージングのプロセス中、DEA はビルドパックがアプリケーションと一致するかどうかをチェックします。例えば、.war ファイルに対する Liberty ランタイム、または .js ファイルに対する Node.js ランタイムなどです。DEA はその後、ビルドパックおよびアプリケーション・コードが含まれる独立したコンテナーを作成します。このコンテナーは Warden コンポーネントによって管理されます。詳しくは、「[How Applications Are Staged](http://docs.cloudfoundry.org/concepts/how-applications-are-staged.html){:new_window}」を参照してください。

###アプリケーションの開始

アプリケーションが開始されると、warden コンテナーのインスタンスが作成されます。**cf files** コマンドを使用すると、例えばログなど、Warden コンテナーのファイル・システムに保管されたファイルを表示することができます。アプリケーションの開始に失敗した場合、DEA はアプリケーションを停止し、Warden コンテナーのコンテンツはすべて削除されます。このため、アプリケーションが停止した場合やアプリケーションのステージング・プロセスが失敗した場合、ログ・ファイルを使用することができなくなります。

アプリケーションのログが使用できなくなって **cf     files** コマンドを使用してステージング・エラーの原因を確認することができない場合は、代わりに **cf logs** コマンドを使用できます。**cf logs** コマンドは Cloud Foundry ログ統合サービスを使用してアプリケーション・ログおよびシステム・ログの詳細を収集するので、このログ統合サービス内にバッファーされていた内容を確認することができます。このログ統合サービスの詳細については、[「Cloud Foundry へのログイン (Logging in Cloud Foundry)」](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}を参照してください。

**注:** バッファー・サイズには制限があります。アプリケーションが長時間実行されていて再始動されていない場合、ログ・バッファーがクリアされたために `cf logs appname --recent` を入力してもログが表示されない可能性があります。したがって、大規模なアプリケーションのステージング・エラーをデバッグするには、その cf コマンド・ライン・インターフェースとは別のコマンド・ラインで `cf logs appname` を入力してください。そうすれば、アプリケーションをデプロイしたときのログがトラッキングできます。

{{site.data.keyword.Bluemix_notm}} でアプリケーションをステージングする際に問題が発生している場合は、[「ステージング・エラーのデバッグ (Debugging staging errors)」](../debug/index.html#debugging-staging-errors)のステップに従って問題を解決することができます。

##cf コマンドを使用してのアプリケーションのデプロイ
{: #dep_apps}

アプリケーションをコマンド・ライン・インターフェースから {{site.data.keyword.Bluemix_notm}} にデプロイする場合、ご使用のアプリケーションの言語とフレームワークに基づいて、ビルドパックをランタイム環境として提供する必要があります。Delivery Pipeline サービスを使用して、{{site.data.keyword.Bluemix_notm}} にアプリケーションをデプロイすることもできます。

{{site.data.keyword.Bluemix_notm}} は、Java および Node.js をサポートする組み込みビルドパックを提供します。これらの言語およびフレームワークを使用する場合、コマンド・ライン・インターフェースを使用することで、アプリケーションのデプロイ時にビルドパックを指定する必要がなくなります。{{site.data.keyword.Bluemix_notm}} は Cloud Foundry にビルドされているため、コマンドはデフォルトでこれらのビルドパックに設定されます。

外部ビルドパックを使用する場合、アプリケーションをコマンド・プロンプトから {{site.data.keyword.Bluemix_notm}} にデプロイする際に **-b** オプションを使用して、ビルドパックの URL を指定する必要があります。

  * Liberty サーバー・パッケージを {{site.data.keyword.Bluemix_notm}} にデプロイするには、ソース・ディレクトリーから以下のコマンドを使用します。
  
  ```
  cf push
  ```
  
  Liberty ビルドパックの詳細については、[「Liberty for Java」](../runtimes/liberty/index.html)を参照してください。
  
  * Java Tomcat アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイするには、以下のコマンドを使用します。
  
  ```
  cf push appname -b https://github.com/cloudfoundry/java-buildpack.git -p app_path
  ```
  
  * WAR パッケージを {{site.data.keyword.Bluemix_notm}} にデプロイするには、以下のコマンドを使用します。
  
  ```
  cf push appname -p app.war
  ```
  もしくは、以下のコマンドを使用してアプリケーション・ファイルを含むディレクトリーを指定することも可能です。
  
  ```
  cf push appname -p "./app"
  ```
  
  * Node.js アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイするには、以下のコマンドを使用します。
  
  ```
  cf push appname -p app_path
  ```
  
アプリケーションが Node.js ビルドパックによって認識されるようにするには、`package.json` ファイルがご使用の Node.js アプリケーション内にある必要があります。`app.js` ファイルはアプリケーションのエントリー・スクリプトで、`package.json` ファイル内に指定できます。以下は単純な `package.json` ファイルの例です。

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                  "start": "node app.js"
},
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```
    
  `package.json` ファイルの詳細については、[package.json](https://www.npmjs.org/doc/files/package.json.html){:new_window} を参照してください。
  
  * PHP アプリケーション、Ruby アプリケーション、あるいは Python アプリケーションを {{site.data.keyword.Bluemix_notm}} にデプロイするには、そのアプリケーションのソースが含まれているディレクトリーから、以下のコマンドを使用してください。
  
  ```
  cf push appname 
```

###複数スペースへのアプリのデプロイ

アプリはデプロイされているスペースに固有です。{{site.data.keyword.Bluemix_notm}} 内のスペース間でのアプリの移動とコピーはいずれもできません。1 つのアプリを複数のスペースにデプロイするには、以下のステップに従って、使用するスペースごとにアプリをデプロイする必要があります。

  1. **-s** オプションを指定した **cf target** コマンドを使用して、アプリをデプロイするスペースに切り替えます。
  
  ```
  cf target -s <space_name>
  ```
  
  2. アプリケーション・ディレクトリーに移動し、**cf push** コマンドを使用してアプリをデプロイします。ここで、appname はドメイン内で固有でなければなりません。
  
  ```
  cf push appname 
```
  
##アプリケーション・マニフェスト
{: #appmanifest}

アプリケーション・マニフェストには、**cf push** コマンドに適用されるオプションが含まれています。アプリケーション・マニフェストを使用することで、{{site.data.keyword.Bluemix_notm}} にアプリケーションをプッシュする度に指定する必要のあるデプロイメント詳細の数を減らすことができます。

アプリケーション・マニフェストでは、作成するアプリケーション・インスタンスの数、アプリケーションに割り振るメモリー量とディスク割り当て量、アプリケーションのその他の環境変数などのオプションを指定できます。また、アプリケーション・マニフェストはアプリケーション・デプロイメントの自動化にも使用できます。マニフェスト・ファイルのデフォルト名は `manifest.yml` です。

###マニフェスト・ファイルでサポートされるオプション

以下の表では、アプリケーション・マニフェスト・ファイルで使用可能な、サポートされているオプションを示しています。`manifest.yml` 以外の異なるファイル名を使用することを選択する場合は、**-f** オプションを **cf push** コマンドと共に使用する必要があります。以下の例では、`appManifest.yml` がファイル名です。

```
cf push -f appManifest.yml
```

<p>  </p>


|options	|説明	|使用法または例|
|:----------|:--------------|:---------------|
|**ビルドパック (buildpack)**	|カスタム・ビルドパックの URL または名前。	|`buildpack:` *buildpack_URL*|
|**disk_quota**	|アプリケーションに割り振るディスク割り当て量。デフォルト値は 1 G です。	|`disk_quota: 500M`|
|**ドメイン (domain)**	|{{site.data.keyword.Bluemix_notm}} 内のアプリケーションのドメイン・ネーム。	|`domain:` ng.bluemix.net|
|**ホスト (host)**	|{{site.data.keyword.Bluemix_notm}} 内のアプリケーションのホスト名。この値は {{site.data.keyword.Bluemix_notm}} 環境で固有でなければなりません。	|`host:` *host_name*|
|**name**	|{{site.data.keyword.Bluemix_notm}} 内のアプリケーション名。この値は {{site.data.keyword.Bluemix_notm}} 環境で固有でなければなりません。	|`name:` *appname*|
|**path**	|アプリケーションのロケーション。この値は相対パスまたは絶対パスとすることができます。	|`path:` *path_to_application*|
|**command**	|アプリケーションのカスタム開始コマンド、またはスクリプト・ファイルの実行コマンド。	|`command:` *custom_command* `command:` *bash ./run.sh*|
|**memory**	|アプリケーションに割り振るメモリー量。デフォルト値は 1G です。	|`memory: 512M`|
|**instances**	|アプリケーション用に作成するインスタンスの数。	|`instances: 2`|
|**timeout**	|アプリケーションの開始に使用する最大時間 (秒)。デフォルト値は 60 秒です。	|`timeout: 80`|
|**no-route**	|アプリケーションがバックグラウンドで実行されているだけであれば、そのアプリケーションに経路が割り当てられないようにするブール値。デフォルト値は **false** です。	|`no-route: true`|
|**random-route**	|アプリケーションにランダムな経路を割り当てるブール値。デフォルト値は **false** です。	|`random-route: true`|
|**services**	|アプリケーションにバインドするサービス。	|`services: - mysql_maptest`|
|**env**	|アプリケーションのカスタム環境変数。|`env: DEV_ENV: production`|
*表 1. manifest.yml ファイルでサポートされるオプション*

###サンプル `manifest.yml` ファイル

以下の例は、{{site.data.keyword.Bluemix_notm}} 内の組み込みコミュニティー Node.js ビルドパックを使用する Node.js アプリケーションのマニフェスト・ファイルを示しています。

```
---
- name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

##環境変数
{: #app_env}

環境変数には、{{site.data.keyword.Bluemix_notm}} にデプロイされたアプリケーションの環境情報が含まれています。*Droplet Execution Agent (DEA)* およびビルドパックによって設定される環境変数に加えて、{{site.data.keyword.Bluemix_notm}} 上のアプリケーション用にアプリケーション固有の環境変数を設定することも可能です。

**cf env** コマンドを使用するか、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから、実行中の {{site.data.keyword.Bluemix_notm}} アプリケーションの以下の環境変数を表示できます。
	
  * アプリケーションに固有のユーザー定義の変数。ユーザー定義変数をアプリに追加する方法については、『[ユーザー定義環境変数の追加](#ud_env){:new_window}』を参照してください。
	 
  * サービス・インスタンスにアクセスするための接続情報を含む VCAP_SERVICES 変数。ご使用のアプリケーションが複数のサービスにバインドされている場合、VCAP_SERVICES 変数には各サービス・インスタンスの接続情報が含まれます。例えば次のようにします。
  
  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials"   :
  {"bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials"   :
  {"host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```
        
DEA およびビルドパックによって設定された環境変数にもアクセスできます。

DEA によって定義された変数を以下に示します。

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>デプロイ済みアプリケーションのルート・ディレクトリー。</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>アプリケーションの各インスタンスが使用できるメモリーの最大量。この値は、アプリケーションの <span class="ph filepath">manifest.yml</span> ファイル内で、またはアプリケーションをプッシュする際はコマンド・ラインで指定できます。</dd>
  <dt><strong>PORT</strong></dt>
  <dd>アプリケーションとの通信のための、DEA 上のポート。DEA はステージング時にポートをアプリケーションに割り振ります。</dd>
  <dt><strong>PWD</strong></dt>
  <dd>ビルドパックが実行中の現行作業ディレクトリー。</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>一時ファイルおよびステージング・ファイルが保管されているディレクトリー。</dd>
  <dt><strong>USER</strong></dt>
  <dd>DEA の実行に使用されるユーザー ID。</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>DEA ホストの IP アドレス。</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>デプロイ済みアプリケーションについての情報が含まれた JSON ストリング。この情報にはアプリケーション名、URI、メモリー制限、アプリケーションが現在の状態になった時点のタイム・スタンプなどが含まれます。以下に例を示します。
<pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainNameng.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>デプロイ済みアプリケーションにバインドされたサービスの情報が含まれた JSON ストリング。以下に例を示します。
<pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

ビルドパックによって定義される変数は、各ビルドパックによって異なります。互換性のある他のビルドパックについては、[Buildpacks](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window} を参照してください。

    

<ul>
    <li>Liberty ビルドパックによって定義された変数を以下に示します。
	
	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>アプリケーションを実行する Java SDK のロケーション。</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>アプリケーションの実行時に使用する Java SDK オプション。</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>DEA で Liberty プロファイルのサーバー・インスタンスを開始するための Java コマンド。</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>DEA で Liberty プロファイルのサーバー・インスタンスを開始する際の共有リソースとサーバー定義のロケーション。</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>実行中の Liberty プロファイルのサーバー・インスタンスのログ・ファイルや作業ディレクトリーなど、生成された出力のロケーション。</dd>
	  </dl>
</li>   
<li>Node.js ビルドパックによって定義された変数を以下に示します。
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Node.js ランタイム環境のディレクトリー。</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Node.js ランタイム環境がキャッシングに使用するディレクトリー。</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Node.js ランタイム環境によって使用されるシステム・パス。</dd>
	</dl>
</li>
</li>
</ul>	

以下のサンプル Node.js コードを使用して、VCAP_SERVICES 環境変数の値を取得できます。

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

各環境変数に関する詳細については、[「Cloud Foundry 環境変数 (Cloud Foundry Environment Variables)」](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}を参照してください。

## アプリケーション・デプロイメントのカスタマイズ
{: #customize_dep}

アプリケーションのデプロイメント・タスクをカスタマイズすることができます。例えば、アプリケーションの開始コマンドを指定したり、アプリケーションの開始環境を構成したりすることができます。
{:shortdesc}

### 開始コマンドの指定

アプリケーションの開始コマンドを指定するには、以下のいずれかの方法を使用できます。指定された開始コマンドは、ビルドパックが提供するデフォルト開始コマンドを上書きします。

**注:** ビルドパックの開始コマンドを優先させたい場合は、開始コマンドとして **null** を指定してください。

  * **cf push** コマンドを使用して -c パラメーターを指定します。例えば、Node.js アプリケーションをデプロイする場合、**node app.js** 開始コマンドを -c パラメーターに指定することができます。
  
  ```
  cf push appname -p app_path -c "node app.js"
  ```
  
  * `manifest.yml` ファイルで command パラメーターを使用します。例えば、Node.js アプリケーションをデプロイする場合、**node app.js** 開始コマンドをマニフェスト・ファイルで指定することができます。
  
  ```
  command: node app.js
```
  

### ユーザー定義環境変数の追加
{: #ud_env}

ユーザー定義環境変数はアプリケーションに固有です。ユーザー定義環境変数を実行中のアプリに追加する場合、以下のオプションがあります。

  * {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用します。以下のステップを実行します。
    1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、アプリのタイルをクリックします。アプリの詳細ページが表示されます。
	2. 左方のナビゲーション・ペインで、**「環境変数」**をクリックします。
	3. **「ユーザー定義」**をクリックし、次に**「追加」**をクリックします。
	4. 必須フィールドに入力し、次に**「保存」**をクリックします。
  * cf コマンド・ライン・インターフェースを使用します。`cf set-env` コマンドを使用してユーザー定義変数を追加します。以下に例を示します。
```
    cf set-env appname env_var_name env_var_value
    ```
	
  * `manifest.yml` ファイルを使用します。このファイル内に値の組を追加します。以下に例を示します。
```
	env:
      VAR1:value1
      VAR2:value2
    ```
	
ユーザー定義の環境変数を追加した後、以下のサンプル Node.js コードを使用して、定義した変数の値を取得できます。

```
var myEnv = process.env.env_var_name;
console.log("My user defined = " + myEnv);
```
	
### 開始環境の構成

アプリケーションの開始環境を構成するには、`/.profile.d` ディレクトリーにシェル・スクリプトを追加することができます。`/.profile.d` ディレクトリーは、アプリケーションのビルド・ディレクトリーの下にあります。`/.profile.d` ディレクトリー内のスクリプトは、アプリケーションの実行前に {{site.data.keyword.Bluemix_notm}} によって実行されます。例えば、以下のコンテンツを含む `node_env.sh` ファイルを `/.profile.d` ディレクトリーの下に置くことで、NODE_ENV 環境変数を **production** に設定することができます。

```
export NODE_ENV=production;
```

###ファイルおよびディレクトリーのアップロードの防止

cf コマンド・ライン・インターフェースを使用してアプリケーションをデプロイする際、{{site.data.keyword.Bluemix_notm}} が他の場所で入手できる特定のファイルおよびディレクトリーをスキップすることにより、アップロード時間を短縮することができます。そのようなファイルとディレクトリーが {{site.data.keyword.Bluemix_notm}} にアップロードされないようにするには、アプリケーションのルート・ディレクトリーに `.cfignore` ファイルを作成してください。

**注:** `.cfignore` ファイルは UTF-8 フォーマットになっていなければなりません。

`.cfignore` ファイルには、無視するファイルおよびディレクトリーの名前を 1 行に 1 個ずつ記載します。ワイルドカード文字としてアスタリスク (*) を使用できます。ディレクトリーを指定すると、そのディレクトリーに含まれているすべてのファイルおよびサブディレクトリーも無視されます。例えば、次の `.cfignore` ファイル内の内容は、すべての `.swp` ファイルと、`tmp/` ディレクトリーに含まれているすべてのファイルおよびサブディレクトリーを {{site.data.keyword.Bluemix_notm}} にアップロードしないことを示しています。

```
*.swp
tmp/
```

# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [アプリケーション・マニフェストを使用したデプロイ](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF マニフェスト生成プログラム](http://cfmanigen.mybluemix.net/){:new_window}
* [cf v6 入門](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [IBM Continuous Delivery Pipeline for Bluemix の概要](../services/DeliveryPipeline/index.html#getstartwithCD)
